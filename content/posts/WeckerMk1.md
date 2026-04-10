---
title: WeckerMk1 fertiggestellt - Aufbau der Platine und Gehäusedesign
date: 2026-04-10
---
Einige Wochen, nachdem ich die Platinen in Fertigung gegeben habe, kamen diese auch bei mir Zuhause an, und ich konnte diese genauer unter die Lupe nehmen. Es war schön zu sehen, wie etwas, was man zuvor aus seinen groben Ideen in einem Programm zusammengeführt hat, plötzlich in den eigenen Händen liegt. Die Vorfreude und die Aufregung waren riesengroß. Also hab ich mich so schnell es ging an den Lötkolben gesetzt und angefangen, die Platine fertigzustellen.

## Der Zusammenbau

### Löten und die Bauteilanordnung

Als ich mich ans Einlöten der Widerstände, Pinleisten, Kondensatoren etc. machte, merkte ich sofort eine Sache: Ich habe keine Ahnung, an welche Stelle welcher Widerstand kommt, oder welcher Kondensator. Bei der kleinen Platine und dieser einfachen Schaltung waren das insgesamt vielleicht 5 oder 6 Bauteile, bei denen es wichtig war, zu wissen, welche Größe nun dahin gehört. Nichtsdestotrotz war dies ärgerlich, und ich hätte mir das mit einer einfachen Beschriftung auf der Platine deutlich erleichtern können. Auf jeden Fall eine Lektion, die ich mir für spätere Projekte merken werde.

Da die Zahl der Bauteile recht überschaubar war, war das Löten recht schnell abgeschlossen, und ich konnte die Module und den Arduino aufstecken. Da bemerkte ich auch, dass die Pinleisten für den Arduino etwas Versatz haben, und ich diesen etwas auf die Pins zurecht drücken musste. Entweder war das Modell nicht ganz sauber, welches ich runtergeladen habe, oder ich habe versehentlich beim Design etwas verschoben. So ärgerlich dies auch war, der Prototyp war (noch) nicht zum scheitern verurteilt.

Zudem bemerkte ich aber auch, dass meine Bauteilanordnung nicht ganz optimal war. Zum einen drückte die USB-Buchse des Arduino von unten auf den Anschlusspin eines Widerstands. Dies sorgte nicht nur ebenfalls für ein erschwertes Aufstecken des Arduino, sondern auch später für einen Kurzschluss, der die Ansteuerung für den Buzzer auf Masse zog. Daher gab dieser keinen Ton von sich. Lösen ließ das Problem entweder durch Herausziehen des Arduinos um ca 1 mm oder durch Überkleben der Kontaktfläche mit Isolierband. 

Zum anderen berührten sich das LCD-Display und ein Kondensator. Auch war damit keine vernünftige Verbindung des LCD-Displays möglich, und ich musste es etwas am Kondensator vorbeidrücken. 

Das sind Dinge, über die ich mir ehrlicherweise beim Design der Platine keine Gedanken gemacht habe, und die sich sofort gerächt haben. Glücklicherweise stand einem Test dennoch nichts im Wege.

### Die Funktionsprüfung

Nachdem der Zusammenbau abgeschlossen war, wollte ich die Konstruktion testen. Also schloss ich das Kabel an, in der Erwartung, da das Programm noch geladen sein sollte, sofort die Wecker UI aufleuchten sollte. Doch es passierte nichts. Und ich hatte auch bereits eine Vermutung, warum.

Ich habe in KiCAD alle Masse-Anschlüsse durch ein Massepanel verbinden wollen. Das bedeutet, die untere, leitfähige Schicht der Platine soll durchgängig verbunden sein, und dann auf das Potential gelegt werden. So erreicht man einerseits eine schnelle Verbindung aller Bauteile, aber auch kapazitive und induktive Vorteile für die Schaltung (in diesem Fall eher irrelevant, da die Schaltung keine hochfrequenten Signale überträgt o.ä.). Das war aber genau der Schritt, der für mich am wenigsten nachvollziehbar war, da ich nicht genau verifizieren konnte, ob die Verbindungen erfolgreich hergestellt wurden oder nicht.

Mit Hilfe eines Multimeters habe ich die Verbindung überprüft, und sie war leider nicht vorhanden. Um nicht gleich eine neue Platine bestellen zu müssen, habe ich die Kontaktflächen auf der Platine aufgekratzt und provisorisch die Verbindungen aufgelötet. Nochmals mit einem Multimeter die Verbindungen geprüft, und anschließen konnte ich den Test durchführen.

Es hat ziemlich genauso funktioniert, wie ich es mir erhofft habe. Ein zufriedenstellendes Ergebnis.

## Design des Gehäuses

Wie im letzten Artikel zum WeckerMk1 erwähnt, wollte ich die Wartezeit mit dem Gehäusedesign überbrücken. Neben der Servereinrichtung habe ich mich auch damit beschäftigt, Ideen für ein Gehäuse zu finden.

Auch hier stellte mir meine schlechte Anordnung der Bauteile Steine in den Weg. Das Breakout-Board, auf dem das LCD-Panel montiert ist, ragte etwas über die Taster hinaus. Somit waren die Taster etwas verdeckt, und von oben nicht ganz frei zugänglich. Dadurch erschwerte sich natürlich die Betätigung durch ein Gehäuse, da ich mir eine Konstruktion überlegen musste, "um die Ecke" zu drücken.

Da es sich aber immer noch "nur" um einen Prototypen handelte, und das Erlernen neuer Fähigkeiten und der Umgang mit neuen Tools hier im Vordergrund standen, entschied ich mich für ein Gehäuse mit offener Front. Ich finde, das eine sichtbare Platine recht gut aussieht, und ich für meinen ersten 3D-Druck einen einfachen Rahmen gut hinkriegen sollte. Im Prinzip sollte die Platine samt angeschlossener Module seitlich in den Rahmen geschoben und mit einem Deckel verschlossen werden.

Um mich aber mit der Software FreeCAD vertraut zu machen, fragte ich die KI meines Vertrauens nach 3-4 einfachen Testprojekten, die ich designen sollte, um ein Gefühl für die Software zu bekommen.

Nachdem ich diese Aufgaben erfolgreich absolviert habe, machte ich mich an das Gehäuse. Ich möchte nicht genau auf die einzelnen Schritte eingehen, aber dennoch grob den Ablauf zusammenfassen:

1. Zunächst wurde das Seitenprofil des Rahmens skizziert, und anschließend auf die erforderliche Länge extrudiert
2. Anschließend wurde das Profil auf einer Seite verschlossen, und Aussparungen für die Arduino Anschlüsse (USB und Spannung) ausgeschnitten
3. Auf die andere Seite des Profils wurde ein einfacher Decken eingezeichnet und ebenfalls auf die erforderliche Dicke extrudiert

Ein hilfsbereiter Arbeitskollege hatte sich dazu bereit erklärt, mir das Modell auszudrucken, da ich noch nicht im Besitz eines eigenen 3D-Druckers bin. Ein erster Test hat gezeigt, dass die Abmessungen noch nicht 100% gepasst haben, insgesamt war der Rahmen zu eng, sodass die Platine zu fest drin , und es war leider nicht genug Platz für den Arduino. Also korrigierte ich das 3D-Modell, und gab es erneut meinem Arbeitskollegen.

Als das neue Gehäuse dann fertig gedruckt war, musste ich feststellen, dass auch hier einige Punkte anzumerken waren, wie die (bewusst) großzügig gewählten Toleranzen für die Ausschnitte der Arduino-Anschlüsse für USB und Spannung. Dafür hat aber der Wecker ins Gehäuse gepasst, und damit konnte der erste Prototyp als vollendet betrachtet werden.

## Fazit

Wie bereits erwähnt, es gibt viele Punkte, die nicht so gut gelaufen sind. Dazu gehören unter anderem:
- Verständnis von C++-Code
- Umgang mit IDEs
- Bauteilauslegung auf Platinen
- Verständnis von der Funktionsweise meiner verwendeten Bauteile
- Funktionsumfang auf das mindeste beschränkt (z.B. keine Lösung für Sommer- und Winterzeit)
- Abmessung und Umsetzung von Objekten in Modellierungssoftware

Das ist aber nicht verkehrt, denn darum geht es ja bei der Entwicklung von Prototypen: Erprobung der eigenen Idee und die Feststellung von Fehlern und Schwächen. Hinzu kam, dass ich ebenso die Priorität auf das Erlernen von neuen Fähigkeiten gesetzt habe. Es war mein erstes Mal, dass ich CAD-Programme wie KiCAD und FreeCAD benutzte. Auch war es überhaupt das erste Mal, dass ich versucht habe, eine Idee von der Pike aus zu realisieren. 

Das dabei ein funktionierender Wecker entstanden ist, der prinzipiell seine Aufgabe zuverlässig übernehmen würde, erfüllt mich mit stolz und voller Vorfreude auf die nächste Iteration meiner Idee. 

Dementsprechend wird bald der Artikel zum WeckerMk2 folgen, in der ich genauer auf meine nächsten Ziele eingehen werde.

