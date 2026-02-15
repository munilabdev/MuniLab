---
title: "Der erste Anlauf in Richtung Langzeitprojekt: Der Wecker Mk1"
date: 2026-01-11
---
Wie bereits erwähnt, arbeite ich auf einen Wecker mit einigen Zusatzfunktionen hin. Nachdem ich die Basics in mehreren kleineren Projekten angerissen und umgesetzt habe, ist die Zeit gekommen, den ersten Prototypen zumindest einmal grob umzusetzen. Ziel dieses Zwischenprojektes soll es sein, meine Kenntnisse mit I2C-Protokollen auszuweiten, in diesem Fall an einem RTC-Modul, und die abgefragtem Daten nicht nur auf einem Display darzustellen, sondern auch mit von einem Benutzer festgelegten Daten abzugleichen. 

Konkret für das Projekt bedeutet das, der Nutzer stellt eine Uhrzeit ein, zu der der Alarm losgehen soll, über eine Zwei-Tastensteuerung ein, und der Arduino gleicht diese eingestellte Uhrzeit mit der Uhrzeit vom RTC-Modul ab. Stimmen die zwei Daten überein, so geht ein Alarm los, der von einem Passiven Buzzer abgegeben wird. 

Um nochmal kurz zusammenzufassen, das sind die Bauteile, welche in diesem Projekt verwendet werden:

- Arduino UNO
- RTC-Modul DS3132
- LCD-Display
- passiver Buzzer
- 2x Taster

Dieses Projekt habe ich auch zum Anlass genommen, von der ArduinoIDE zur PlatformIO IDE zu wechseln, um meinen Workflow früher an die Funktionsweise klassischer IDEs anzupassen. Da der Einstieg zunächst einmal überwältigend sein kann, habe ich ein Tutorial vom YouTube-Kanal [DroneBot Workshop](https://www.youtube.com/watch?v=JmvMvIphMnY) zur Hilfe herangezogen. Somit konnte ich mich bereits vor dem Schreiben erster Codezeilen mit der neuen Entwicklungsumgebung vertraut machen.

Um dieses Projekt Softwareseitig umzusetzen, möchte ich mich einer Zustandssteuerung bedienen. Diese Zustandssteuerung soll durch Definition der Zustände, wie bspw. SET-ALARM, SHOW-TIME und ALARM und der Eingabe von Eingangssignalen durch zwei Taster umgesetzt werden.

Nachdem ich eine grobe Struktur festgelegt habe, machte ich mich an eine Umsetzung in Pseudocode, die ich relativ schnell in der IDE umgesetzt und auf den Arduinogeladen habe. Für die Prototyp-Test habe ich alles mit dem Breaderboard verbunden und die ersten Tests gemacht. Relativ schnell scheiterte es aber daran, dass die Zeit nicht synchronisiert wurde. Die Uhrzet, die beim Boot des Arduino ausgewertet wird, freezt auf dem Bildschirm. Nach einiger Recherche hab ich festgestellt, dass der C-String, in dem die Zeit gespeichert wird, IMMER neu in das vom RTC verstandene Format zurückformatiert werden muss, da er bei jedem Synchronisieren zurückgesetzt wird. Daher konnte die Uhrzeit nicht aktualisiert werden.

Nachdem ich also diese Problem lösen konnte, konnte ich mich der Erprobung der weiteren Funktionen widment. Darunter fielen die Flankenerkennung für diue Bedienung durch den Benutzer, das Auslösen des Wecktons und der Weckton selbst. Das wurde relativ schnell gelöst, die Flankensteuerung habe ich durch zwei Abfragen der Zustände am Eingangspin des Mikrocontrollers gelöst, wobei sich die Zustände eben unterscheiden müssen (erst HIGH, dann LOW). Die Wecktonproblematik löste ich durch eine kleine Transistorschaltung und eine kurzzeitige Anteuerung des Piezo-Summers und längere Pausen (Verhältnis 1:150 von Ansteuerung zu Pause), da die Piezo-Summer relativ minderwertig sind und daher lange Nachschwingen, was zu einem "Schmieren" des Wecktons geführt hat.

Somit sind die Grundfunktionen des ersten Prototypen erprobt worden, und ich kann nun die Entwicklung der Anschlussplatine starten, und im Anschluss das Design des Gehäuses. In diesem Sinne will ich diesen Teil abschließen, und mit der Entwicklung der Platine in KiCad geht es nächsten Monat weiter.
