---
title: WeckerMk2 - Wie geht es weiter?
date: 2026-04-11
draft: false
---
### Grundidee

Nun da der erste Prototyp abgeschlossen wurde, widme ich mich der Entwicklung der zweiten Iteration meines Wecker-Projektes. Dabei möchte ich einerseits mein Skill-Set bezüglich der Programmierung erweitern, meine Arbeit mit verschiedenen Bauteilen und ihren Libraries fortsetzen, und einige weitere Funktionen im Vergleich zum ersten Prototypen hinzufügen.

Der Mk1 war fähig, die einfachste Alarm-Funktion zu erfüllen. Nun sollen folgende weitere Funktionen hinzukommen:

- Sommer- und Winterzeit sollen unterschieden und beachtet werden
- Neben einem Weckton soll der Gebetsruf abgespielt werden
- die richtigen Gebetszeiten sollen entweder berechnet, oder abgefragt werden
- das Wetter/ die momentane Temperatur soll angezeigt werden

Da der Funktionsumfang sehr zugenommen hat, werden weitere Bauteile benötigt. Um die Funktionen zu realisieren verwende ich folgende Bauteile:

- ESP32 als "Steuerungseinheit"
- MAX98357A I2S Verstärker-Board für das Abspielen von Audio-Dateien
- 3 W/4 Ohm Lautsprecher (Mono)
- SD-Kartenmodul auf Basis des SPI-Protokolls
- 1,3" OLED-Display mit I2C-Protokoll

Die Bauteile wurden auf Basis meines momentanen Wissenstandes über die Fähigkeiten des ESP32 ausgewählt. Der ESP müsste die verwendeten Protokolle "verstehen" können, somit müssten die Komponenten miteinander Kompatibel sein. Aber das wird sich am Ende dieser Iteration herausstellen.

### Wie soll der Wecker funktionieren?

Im Grunde genommen bleibt das Prinzip dasselbe: es wird eine Weckzeit eingestellt, und diese wird immer mit der momentanen Uhrzeit vergleichen. Zusätzlich werden die Gebetszeiten verglichen werden müssen. Stimmen Weck-/Gebetszeit und momentane Uhrzeit überein, wird die jeweilige Audiodatei von der Micro-SD-Karte gelesen und abgespielt.

Die Uhrzeit soll nun anstelle eines RTC-Moduls durch das Network Time Protocol (NTP), also "über das Internet", bereitgestellt. Dadurch wird im selben Zug das Problem mit der Sommerzeit gelöst, da diese durch das NTP mit einstellen der Zeitzone kompensiert wird. 

Wie bereits erwähnt, liest der ESP mittels SPI-Protokoll dann die jeweilige Audiodatei ein, wandelt diese in ein I2S-Signal für den Verstärker um, der dieses dann für einen Lautsprecher aufbereitet. Angezeigt sollen die Uhrzeit, die Außentemperatur, und eventuell die Uhrzeit des nächsten Gebetes. Dies ist abhängig davon, wie gut ich mit dem geringen Patz des 1,3" Displays zurecht komme.

### Mini-Projekte

Da ich in meinem Artikel ["Wecker Mk1 Zwischenbericht"](https://munilab.dev/posts/zweiter_artikel/) erwähnt habe, dass ich ein Problem mit den C-Strings hatte, da ich mir die Dokumentation zur RTC-Library nicht genau durchgelesen habe, möchte ich solchen Problemen vorbeugen. 

Erneut fragte ich die KI meines Vertrauens, ob sie mir nicht einige Mini-Projekte geben könnte, mit denen ich mich zunächst mit jeder Komponente für sich auseinander setze. Dadurch möchte ich Fehler bereits im Vorhinein eliminieren, und mir die Suche nach diesen erleichtern. Ich werde nicht verwirrt, welches Bauteil nun einen Fehler verursacht, da ich immer nur eines gleichzeitig verwende. Zudem kenne ich dann eventuelle Fehlerbilder bereits, und kann diese genauer einordnen. 

Das eigentliche Programm soll das Ziel haben, meine gewünschten Funktionen umzusetzen, und nicht das Versuchslabor für meine Bauteile darstellen.

Erst vergewissern, dass alle Komponente funktionieren, und ich sie verstehe, dann können diese zusammengesetzt werden.

Ich habe dennoch bereits daran gearbeitet, einen Schaltplan zu erstellen, in dem direkt alle Bauteile mit dem ESP verbunden werden. Ich möchte mir den ständigen Verdrahtungsaufwand sparen, indem alles sofort vorverdrahtet wird. So kann ich dennoch alle Bauteile allein testen, da ich dann einfach nur ein neues Programm aufspielen muss, was die Signale der anderen Bauteile ignoriert.

### Zielsetzung

Meine Ziele für den kommenden Monat sollen sein:

- Schaltplan erstellen, Dokumentationen zu den Komponenten lesen
- Testprojekte erfolgreich beenden
- erste Tests mit dem Breadboard durchführen

Anschließend geht es dann damit weiter, den Wecker voll funktionsfähig zu machen und in ein konkretes Produkt zu bringen.

