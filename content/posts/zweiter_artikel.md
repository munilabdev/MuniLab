---
title: "Wecker Mk1 Zwischenbericht"
date: 2026-02-14
---
## Grundidee und Umsetzung

Zuletzt habe ich mir 3 Ziele definiert, die ich für diesen Moant erreichen möchte. Kurz zur Wiederholung, waren es das Anzeigen der Uhrzeit, Einstellen der Weckzeit, und das Abspielen eines Wecktons bei Übereinstimmung der vorherigen.

Um das umzusetzen, wollte ich mich eines neuen Konzeptes bedienen, welches in der Hocschule kennenlernte: dem Zustandsautomaten. Im Grunde genommen wollte ich jede dieser drei Funktionen als eigenen Zustand definieren, um dann mit Hilfe der Tasteneingabe zwischen diesen zu wechseln und die Funktionen auszuführen.

Dabei wollte ich zunächst einmal die Zustände für sich alleinstehend definieren, und wie sich diese Zustände verhalten sollen. Beispielhaft hätte man das wie folgt lösen können: realtime für die Uhrzeit, wakeuptime für die Weckzeit und alarm für den Weckton. 

Nachdem ich jeden Zustand an und für sich entwickelt und erprobt habe, konnte ich mir darüber Gedanken machen, WIE ich zwischen den Zuständen wechsle.

Dazu möchte ich nochmal kurz meine Grundvorstellung anreißen: Mit dem Taster Set soll der Bediener durch die Menüs geführt werden, und mit Reset sollen Eingaben bestätigt werden. Ebenso soll der Alarmton mittels Reset-Taste ausgeschaltet werden.

Die meiste Interaktion zwischen Mensch und Wecker/Mikrocontroller geschieht beim Einstellen der Weckzeit. Um diese der Komplexität wegen relativ gering zu halten, beschränkte ich mich auf das Einstellen der Stunde, der Minute und noch der Einstellung, ob ein Alarm überhaupt losgehen soll oder nicht.

## Stolpersteine

Prinzipiell war ich mit meiner grundlegenen Planung zufrieden und wollte mich an die Implementierung von dem Code machen. Dabei sind mehrere Probleme aufgetreten:

### Problem 1: Uhrzeit

Die Uhrzeit wurde beim Boot vom Arduino angezeigt, aber nur die momentan Uhrzeit. Trotz sich wiederholenden Abfrage wurde die Zeit auf dem Display nicht aktualisiert, erst beim Betätigen der Reset-Taste am Mikrocontroller selbst.

Gelöst wurde dies nach langer Recherche zur Funktionsweise des RTC-Moduls. Ich verwendete einen DS3231 zusammen mit der fertigen RTClib Bibliothek. Diese verlangte einen C-String im Format "hh:mm:ss", welcher noch abhängig der geforderten Information angepasst werden konnte. Da dieser C-String jedoch bei dem Abfragen mit der momentanen Uhrzeit überschrieben wurde, ist das gefporderte Format verloren gegangen, und der String wurde nicht mit der aktuellen Uhrzeit beschrieben.

Dies konnte ich durch einen weiteren C-String lösen, der als Format-Vorlage diente. Diesen kopierte ich vor jeder Zeitabfrage in den Zeit-String, sodass immer die richtige Formatierung vorlag. Dadurch konnte immer die aktuelle Uhrzeit angezeigt werden.

### Problem 2: Flankenerkennung

Wenn man eine Tastenabfrage durchführt, fragt man im Prinzip den Spannungspegel am EIngangspin ab. Aufgrund der schnellen Wiederholung der if-Abfragen im Arduino (void loop) und der im Vergleich sehr langen Betätigung des Tasters durch den Bediener, kann es dazu kommen, dass dieselbe if-Abfrage mehrmals durchgeführt wird, oder eine Tasterbetätigung fehlinterpretiert wird und daher zu einem Überspringen von Menüs oder anderen unerwünschten Reaktionen führt.

Daher musste eine Flankensteuerung her. Da der Arduino dies aber nativ nicht unterstützt, beziehungsweise es keine direkte Flankenabfrage wie in VHDL gibt, musste ich mir diese selber bauen.

Im Prnzip müsse dafür zwei Abfragen geschehen: eine, die den Zustand des Tasters abfragt, um eine FUnktion hervorzurufen, und eine, die den Zustand kurzzeitig speichert. 

Zunächst habe ich dafür eine Zustandsabgfrage des Tasters vor die if-Abfrage der Funktion gelegt, und dann abgefragt, ob sich diese zwei Zustände des Tasters unterscheiden. Dies hat aber nicht funktioniert, da ich dann bei der Bedienung immer den Zeitpunkt ZWISCHEN diesen zwei Abfragen (Taster vorher und Taster jetzt) erwischen musste. Keine gelungene Umsetzung.

Da die Grundidee aber eigentlich richtig war, musste ich einfach den Zeitpunkt der vorherigen Tasterabfrage verändern. Anstatt den Zustand vor der eigentlichen FUnktion abzufragen, fragte ich den Zustand der Taster am Ende von void loop ab. Dadurch erreichte ich, dass der Mikrocontroller dann im neuen Durchlauf von einem noch immer gedrückten Taster ausgeht, und dann die Funktion verweigert. Dadurch, dass der Arduino aber sehr schnell über den Code iterriert, fällt diese kleine Verzögerung nicht auf und es wird der Anschein einer direkten Reaktion erweckt, ohne dabei unpräzise zu wirken.

Somit war Problem zwei auch gelöst.

### Problem 3: Änderung der Alarmzeit

Funktion 2 des Weckers stellte eine Herausforderung für sich da. Wie kann ich mit nur einem Taster die Stunden und Minuten einstellen? Klar ist, Set soll durch die Menüs klicken. Was ist also, wenn ich in dem Zustand "wakeuptime" einen weiteren Zustandsautomaten baue, der zwischen Stunden, Minuten und Alarmmodus wechselt? 

Prinzipiell wäre das möglich, aber ich habe mich dafür entschieden, diese Unterzustände als eigene Zustände in dem Automaten zu definieren, in etwa wie "sethour", "setminute" und "setmode".

Dies verhinderte, dass der Code zu verschachtelt wird, und man kann die Iterationskette von Set einfach unterbrechen und weitere Zustände hinzufügen. Somit ist der Code leicht zu erweitern und bleibt übersichtlich.

Um den Modus einzustellen, konnte ich einfach eine doppelte if-Abfrage implementieren, die den momentanen Modus bei Tasterinput abfragt und einfach in den Gegenteiligen ändert.

Für die Uhrzeit selbst implementierte ich einfach einen Zähler, der bei Input von Reset um 1 inkrementiert und dann, für Stunden bei 24, für Minuten bei 60 umschlägt.

### Problem 4: Alarmton

Auch die dritte Funktion war nicht auf Anhieb ein Erfolg. Ich wollte unbedingt eine Melodie umsetzen, jedoch war der Buzzer zu träge, und schwang in den Pausen nach, was den Ton verschmierte und nur wie ein langer, penetranter Piepton klang, was vermutlich der mangelhaften Verarbeitung des Bauteils zu schulden ist.

Jedoch ließ sich das durch eine kleine Transistorschaltung und dem Anpassen des Tastverhältnisses ändern. Anstatt Pause und Ansteuerung gleich groß zu lassen (T= 50%), verkürzte ich die Ansteuerung des Buzzers, sodass diese gar nicht erst so sehr ins Schwingen geriet. Mit einem Tastverhältnis von ca. 1,4% konnte ich eine klare, nicht allzu nervige Melodie umsetzen.

Die Zustandsänderung war zum Schluss relativ einfach. Mit der funktionierenden Flankenerkennung konnte ich bei jeder Änderung den Zustand wechseln, und in festgelegter Reihenfolge durch die Menüs klicken.

## Fazit

Das Entwickeln des Prototypen zeigte mir: es läuft nicht immer alles auf Anhieb. Das ist denke ich die wichtigste Lektion bei diesem Schritt. Aber noch wichtiger: selbst wenn es nicht läuft, ist es nicht das Ende des Projekts. Ich bin durch die Fehler, die ich beim Entwickeln gemacht habe, an meine Frustgrenze gestoßen, und musste lernen, Ursachen von Fehlfunktionen ausfindig zu machen und dafür Lösungen zu finden. Und ich denke, dass ich dabei erfolgreich war. Da alle Ziele, die ich mir letzten Monat gesetzt habe, erfüllt sind, möchte ich auf die weiteren Schritte auch eingehen.

Da nun die Grundfunktion de sWeckers abgebildet ist, kann man sich der weiteren Umsetzung widmen. Softwareseitig ist somit alles abgeschlossen, und um die Schaltung selbst nun in ein Gehäuse zu bekommen, muss die Verdrahtung kompakt und elegant gelöst werden. 

Zunächst dachte ich an Verbindung der Komponenten durch Stecker und Leitungen, im Prinzip wie aneinander geklebte Jumper-Wires mit Male- und Female-Connectors. Da die Leitungen aber unnötig Platz einnehmen und das Zusammenbauen des Gehäuses unnötig verkomplizieren, dachte ich an die Entwicklung einer PCB, die ich fertgen lassen könnte.

Diese Umsetzung war mir aus Projekten durch verschiedene Youtube-Videos bekannt, und es erwies sich als eine sehr elegante Lösung, alles kompakt miteinander zu verbinden.

Dementsprechend wird die Zielsetzung für den kommenden Monat beinhalten, eben diese PCB zu entwickeln und fertigen zu lassen. Dazu gehört, einen Schaltplan zu erstellen und auf Basis darauf die Platine fertigen zu lassen. Umgesetzt werden soll das mit KiCad, einem Open-Source-Tool für Elektrotechnik.

Im Anschluss soll das Gehäuse gefertigt werden. Ob es bis nächsten Monat einen fertigen Druck geben wird, ist nicht genau zu sagen. Abhängig mache ich das von meiner Geschwindigkeit mit dem PCB-Design und der Fertigung eben dieser. Daher zählt erstmal: PCB fertig, alles andere ist Bonus.

