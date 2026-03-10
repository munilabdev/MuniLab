---
title: "Erster Platinenversuch Mk1"
date: 2026-03-10
---
## Der Weg zur ersten Platine

### Rückblick
Das Ziel für diesen Monat ist es gewesen, eine Leiterplatine für den Wecker Mk1 zu designen und produzieren zu lassen. Dafür sollte die auf dem Breadboard geplante Verschaltung in einem CAD-Programm umgesetzt werden. 

### Planung
Ich entschied mich für KiCAD als Software für das Platinendesign, da es ein sehr umfangreiches Tool ist, und dazu auch noch Open-Source, also sehr zugänglich für den Hobbygebrauch und sehr gut dokumentiert ist.

Da ich noch keine Erfahrung mit CAD-Software hatte, entschloss ich mich, anstattdirekt mehrere Youtube-Tutorials anzschauen, erstmal die von KiCAD herausgegebenen Start-Guides als Grundlage zu nehmen. Es stellte sich heraus, dass die Dokumentation von KiCAD äußerst angenehm zu lesen und verstehen ist. Daher nahm ich diese als Leitfaden für die gesamte Planung und Umsetzung dieses Projektschritts an.

Doch bevor ich mich an die digitale Umsetzung machen konnte, skizzierte ich die Verschaltung per Hand und erstellte eine kleine Klemmentabelle, in der alle benötigten Verbindungen aufgelistet sind. Das sollte meine Gedankenstütze werden.

### Umsetzung in KiCAD
Auf Grundlage dieser Skizze erstellte ich dann mit Hilfe der KiCAD-Doku meinen Schaltplan. Im Prinzip bestand diese Aufgabe nur aus dem Setzen und Verbinden von Bauteilen. Nach kurzer Recherche konnten auch die richtigen Footprints für die Bauteile gesetzt werden, bis hierhin also alles kein Problem.

Als es dann zu dem eigentlichen Design der Platine geht, sah ich bereits einige Probleme. Da ich ja eine Art Shield für den Arduino erstellen wollte, hatte ich die Sorge, der Shiel selbst würde nicht genau auf dem Arduino passen. Ich wusste nicht, wie ich die genauen Maße ins Programm kriege. Und in Anbetracht der langen Wartezeit und Kosten der PCB-Fertigung, war Trial-and-Error keine Möglichkeit, Mess- und Designfehler auszubessern.

Da aber ebenso der Arduino Open-Source ist, und damit auch seine Zubehörteile, konnte ich mir einfach von der Homepage eine PCB-Datei eines Shields runterladen und in das Projekt importieren. Diese konnte ich dann einfach an meine Bedürfnisse anpassen. 

Somit war das Design relativ schnell fertig, und ich konnte die Platine in Auftrag geben. Jedoch bin ich nicht zu 100% zufrieden mit dem Desing. Ich habe eine unkluge Aufteilung gewählt, und die Platine ist in Anbetracht der relativ geringen Komplexität der Schaltung überproportional groß geworden. Zudem gab es relativ viele Kreuzungen der Pfade, die ich mit Vias umgehen konnte. 

Aber, ich glaube wenn die Platine funktioniert, kann ich es dennoch als Erfolg abschreiben. Da es sich immer noch um meinen ersten Versuch handelt, bin ich damit zufrieden, alle Bauteile auf einer Platine untegebrachr zu haben und einen funktionierenden Wecker zu haben. Somit nehme ich mir aber jetzt schon vor, bei dem Mk2 mehr darauf zu achten, Verzweigungen zu vermeiden und die Platine so kompakt wie möglich zu designen.

### Was jetzt?
Da die Platinen lange brauchen werden, bis Sie bei mir ankommen, werde ich mich in der Zwischenzeit etwas mit meinem Server und FreeCAD beschäftigen, dazu aber mehr in den anderen Posts.
