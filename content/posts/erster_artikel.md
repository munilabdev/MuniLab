---
title: "Übersicht über ersten Projekte"
date: 2026-01-06
draft: false
---

## Was will ich umsetzen und bis wann?

Die ersten Projekte sollen werden:
	- Wecker mit Adhan und Wetterstation -> zuletzt AI/Assisstantintegration
	- Server mit Selfhosting (Cloud-Speicher, Fotoverwaltung, VPN und Passkey-Manager)

Um nicht an zu vielen Projekten gleichzeitig zu arbeiten, ist die Zahl erstmal auf zwei Projekte beschränkt, um nicht den Fokus aus den Augen zu verlieren.

Stichtag für den endgültigen Wecker ist September 2026, während der Server bis Mai zumindest im eigenen Heimnetz lauffähig sein soll. Der Zugriff ausserhalb des Heimnetzes kann später ergänzt werden (Sicherheit der Daten > Schnelle Funktionalität des Servers).

Dennoch möchte ich zunächst einen ersten Weckerprototyp fertigstellen, um doch ein "schnelles" Erfolgserlebnis zu haben und auszuloten, welche Schwierigkeiten in Zukunft folgen könnten.

### Wecker Mk1

Der erste Prototyp soll um einen Arduino mit RTC-Modul herum gebaut werden. Das RTC-Modul dient der Erfassung der Uhrzeit. 

Als Ausgabe-Plattform soll ein 16x2 LCD-Display fungieren, während Bediener-Eingaben durch zwei Taster registriert werden sollen (Set und Reset). 

Der Weckton soll mit Hilfe eines Buzzers realisiert werden, um die Komplexität gering zu halten und nicht unnötig Platz im Gehäuse mit zusätzlichen Bauteilen, wie dem Audio-Modul, zu verschwenden. 

Zuletzt kommt ein 3D gedrucktes Gehäuse, wo alles seinen Platz finden wird. 

Im folgenden sollen die weiteren Wecker-Prototypen immer weiterentwickelt werden, sodass Stück für Stück mehr Funktionen des endgültigen Weckers hinzugefügt werden. Dies möchte ich im folgenden definieren:

	- Mk2 soll anstelle eines Arduino UNO durch einen ESP32 betrieben werden. Vorteil sind eine WLAN-Anbindung für Wetter und Adhan APIs und eine kompaktere Bauform. 
	- als Ausgabemedium soll ein größeres, höher auflösendes OLED-Display verwendet werden, um mehr Platz für die dargestellten Informationen zu haben.
	- Und für die Audioausgabe wird aufgrund des Adhans ein Lautsprecher benötigt. 

Somit wäre die Definition des Weckers Mk2 abgeschlossen. Im letzten Schritt würde die AI-Integration folgen, da der ESP32 dafür aber nicht leistungsstark genug ist, muss dafür eine andere Lösung gefunden werden. Ganz grundlegend ist aber das Projekt abgeschlossen, und es würden technische Optimierungen und optische Verbesserungen folgen.


### Server

Der Server soll zunächst durch einen Raspberry Pi 4b als NAS (Network Attached Storage) umgesetzt werden. Anschließend sollen die anderen Funktionen schrittweise dazukommen. Zu genaueren Spezifikationen kommen wir nach Abschluss des Weckers Mk1.


### Zielsetzung für den kommenden Monat

Ziel sollte sein, eine funktionierende Grundfunktion eines Weckers nachzubilden. Dazu gehören:
	- Anzeige von Uhrzeit
	- Einstellen einer Weckzeit
	- Abspielen eines Alarmtons bei Erreichen der Weckzeit

Die reine Funktionalität steht im Vordergrund. Daher wird eine Grundschaltung auf einem Breadboard erstellt, und diese Funktionen nacheinander umgesetzt.
