---
title: "Mein Einstieg ins Homelabing"
date: 2026-03-15
---

Seit längerem hat sich bei mir der Wunsch geäußert, unabhängiger in der digitalen Welt zu werden. Dazu gehört allem voran das Zurückgewinnen der Kontrolle über die eigenen Daten und das Durchbrechen Inkompatibilität verschiedender Plattformen wie Linux und Apple. Im Zuge dessen hab ich mich sehr mit NAS (Network Attached Storage), Heimservern und Netzwerken beschäftigt. Und ziemlich schnell den Entschluss gefasst: "Das brauche ich auch". Somit fing ich an, extrem viele Artikel zu dem Thema zu lesen und etliche Videos anzuschauen. So hatte ich sofort ein großen Input an Möglichkeiten, gängigen Methoden und Zugang zu einem umfassenden Grundverständnis von Heimnetzwerken. Ziemlich hilfreich waren verschiedene Youtube-Kanäle wir Ardens, Switch and Click und Hardware Haven, die mit ihrer Dartsellung eigener Projekte und Erfahrungen bereits auf einige Schwierigkeiten hinwiesen.

## Was möchte ich mit dem Server machen?

Schnell stellte sich die Frage, wie ich den mein eigenes Heimnetzwerk aufbauen möchte. Zu Beginn dachte ich an einen Raspberry Pi, der mittels einer alten HDD, die ich noch übrig hatte, betrieben werden und als einfaches NAS dienen soll. Ziemlich schnell aber hat sich die Liste meiner gewünschten FUnktionen erweitert, und ich hatte Angst, ein einfacher Raspberyy Pi könnte eventuell schnell an seine Grenzen kommen, was die Hardware-Auslastung betrifft. Ich wollte auf jeden Fall meinen iCloud-Dienst voll ersetzen können, und die meist verwendete FUnktion war eben iCloud-Photos. Somit stand neben dem NAS auch eine Foto-Galerie auf der Liste, und ein Passwort-Manager, da dieser der sensibelste Dienst von allen ist und daher auf jeden Fall selbst gehostet werden soll. Außerdem wollte ich einen VPN-Zugriff einrichten, um von überall an meine Daten zu kommen. 

Somit stand fest, was ich haben wollte, und ich konnte mich damit beschäftigen, wie ich das ganze umsetze. Ich entschied mich, anstelle eines Raspberrys einen alten Office-Rechner, den ich im Internet für einen guten Preis erworben habe, zu verwenden, einfach um mehr Möglichkeiten beim Upgrade und Austausch der Hardware zu haben. Somit hatte ich außerdem ein sauberes System, mit Platz für Erweiterungen und Speichermedien.

### Die Hardware

Zu den Specs: Es handelt sich um einen Esprimo Rechner mit einem Intel i5 der 6. Generation, einer 256 GB SSD Boot-Drive mit Windows 11 und 8 GB RAM. Ich habe gleich eine zussätzliche 512 GB SSD M2 mittels PCIe-Adapter eingebaut, um genug Platz für die später laufende Software zu haben. Anschließend baute ich noch zwei 4 TB NAS-HDDs ein, die den Speicherplatz für meine Daten zur Verfügung stellen sollten. Damit bin ich langfristig gut gewappnet, und das System ist modular so aufgebaut, das (zumindest erhoffe ich mir das) ein späterer Upgrade auf leistungsstärere Komponenten ein einfach Austausch sein wird, ohne meine ganzen Daten verschieben zu müssen oder ähnliches.

Das Betriebssystem habe ich gegen die Server Version von Ubuntu Linux 24.04 LTS ausgetauscht, weil ich ein großer Fan von Open-Source bin, und ich mir eine höhere  Effizienz durch die fehlende GUI (Graphic User Interface) erhofft habe. Außerdem wollte ich mich dadurch zwingen, meinen Terminal-Workflow zu verbessern. Die Programme bzw. die von den Programmen verwendeten Daten wollte ich auf der M2-SSD speichern, sodass ich genug Platz habe und das System ungesorgt wachsen kann. Rückblickend betrachtet ist das Setup vielleicht etwas unnötig, aber ich fand die 256 GB definitv zu klein, und hatte mir ehrlich gesagt nicht vorstellen können, was ich sonst mit der kleinen Festplatte hätte tun sollen.

### Die Software

Da nun das fertige Gerät vor mir stand, musste ich mir Gedanken dazu machen, wie ich den alten Office-Rechner nun zu einem echten Server mache. Die Ziele standen fest, nun sollte es darum gehen, wie diese Ziele erreicht werden konnten. Dabei war mir wie immer wichtig, dass es sich um Open-Source-Software handelt, und ich so wenig wie möglich abhängig auf Dienste von anderen Unternehmen bin. 

Da ich mich, wie bereits erwähnt, für Ubuntu Server entschieden habe, fielen NAS-Betriebssysteme wie TrueNAS oder OpenMediaVault für mich raus, da ich das Gefühl hatte, ich werde mir damit mehr Probleme einkaufen als mir lieb ist. Definitiv haben diese OS ihre Daseins-Berechtigung, jedoch wollte ich ein leichtes, effizientes System, wo ich nicht auf die Funktionalitäten des Betriebssystems beschränkt bin. Ich kann mir auf Ubuntu Server alle Dienste so zusammenbauen, wie es mir passt. 

Die Idee war, jeden Dienst in einem Docker-Container zu starten, um diese einigermaßen voneinander zu trennen und den Zugriff jedes Dienstes auf das nötigste zu beschränken. Durch die Isolation in Containern hatte ich die Möglichkeit, die Dienste einfach zu verwalten, zu bearbeiten, und einfach hoch und runterzufahren. Außerdem macht das aufsetzen eines Dienstes mit Docker Compose es sehr einfach, da bereits viele Entwickler fertige DOcker Compose Dateien zu ihren Diensten veröffentlicht haben. 

Welche Dienste ich nun hosten wollte, machte ich eben an diesen 2 Kriterien fest: Open-Source und die einfache Implementierung mit Hilfe von Docker.

Für den NAS empfahl sich auf den ersten Blick Nextcloud, ein bekanntes Tool mit einer umfangreichen Funktionspalette, die theoretisch mein gesamtes iCloud-Problem lösen konnte. Ich habe jedoch beim einrichten gemerkt, dass Nextcloud etwas zu viel für mich ist. Die Benutzeroberfläche war darauf ausgelegt, ein zusammenhängendes Erlebnis mit allen Diensten zu schaffen, für meinen Anwendungsfall, einzig und allein den Datei Explorer nutzen zu wollen, hat sich das etwas verschwendet angefühlt. Somit habe ich Nextcloud schnell verworfen, und mich für einfache Datei-Freigabe mit Hilfe von Samba entschieden. Es ist leichtgewichtig, ist schnell zu konfigurieren und bietet einfache Kompatibilität über mehrer Plattformen hinweg.

Für meine Foto-Galerie hat sich Immich als perfekte Alternative erwiesen. Es bietet eine iCloud ähnliche Erfahrung mit Standort- und Personenerkennung, einer Galeriefunktion und ebenfalls Plattform übergriefender Kompatibilität, zudem man auch über den Brwoser auf seine Bilder und Videos zugreifen kann. Das war eine leichte Entscheidung.

Zu guter Letzt, der Passwort-Manager. Dies war auch eine leichte Entscheidung, denn mit Vaultwarden hat man eine open-source Implementation für Bitwarden, einem Manager, der ebenfalls auf vielen Plattformen verfügbar ist.

Damit ist meine erste Palette an Diensten fertig, und ich konnte mich daran machen, diese umzusetzen.

### Samba

In der Theorie ist das Umsetzen von Samba gar nicht so schwer: man installiert Samba, konfiguriert die smb.conf-Datei, startet den Samba-Daemon und fertig ist dein lokales NAS. Leider gehört dazu aber auch, dass man weiss, was man konfigurieren muss, und wie man das zu tun hat.

Bei Samba bspw. habe ich zunächst gar nicht verstanden, was es zu konfigurieren gibt, da die Dokumentation von Samba zum Thema "Standalone Server" recht marger ausfällt. Somit musste ich mich auf alternative Quellen stützen. Das größte Problem, was ich dabei lösen musste, war nicht, wo ich meine Daten speichern möchte, sondern, wie ich von einem anderengerät darauf zugreifen kann. Nämlich gab es Schwierigkeiten mit den Benutzerrechten, und ich musste einen kurzen Exkurs in die Rechte und Benutzer von Linux machen. ALs das aber gelöst war, hatte ich eine Freigabe für meine gesamten Dateien, über alle Plattformen hinweg, zumindest fast. Ich könnte mich ganz einfach über die Datei-Explorer meiner Geräte auf dem Server einloggen, und hatte Zugriff auf die Dateien. Außer bei Apple. Dort durfte ich nur sehen, was auf dem Server war, aber nichts ändern. Somit hatte mein Benutzer nur Leserechte. Als ich aber einen alternativen Dateiexplorer nutzte, war das Problem behoben, somit schien es sich um ein Apple-spezifisches Problem zu handeln. Stattdessen nutze ich nun einfach den alternativen Explorer.

Alles in allem war Samba aber die richtige Wahl. Ich hatte relativ schnell einen funktionsfähigen NAS aus dem Office-Rechner gemacht, kann von allen meinen Geräten auf diesen zugreifen und muss nun nur noch die VPN für Remote Zugriff einrichten.

### Immich

Immich stellte sich als schnelle und einfache Installation heraus. Mit einer kurzen Anpassung der Compose-File, die sehr gut beschrieben auf der Homepage von Immich zu finden ist, hatte man eine lokal erreichbare Galerie, die sofort die Bilder von iCLoud übernommen hat. Es war eine sehr angenehme Erfahrung, Immich zu nutzen.

### Vaultwarden

Mit Vaultwarden kamen einige Probleme auf mich zu. Eigentlich habe ich mich gegen das exponieren meiner Dienste ins Internet entschieden. Ich habe es auch geschafft, Vaultwarden im lokalen Netzwerk zum Laufen zu bringen. Jedoch konnte ich aufgrund fehlender HTTPS-Verschlüsselung nicht auf den Dienst zugreifen. Da mein technisches Know-How nicht ausreicht, dafür einen Umweg zu finden, entschied ich mich für das Umsetzen von Vaultwarden mittels Reverse Proxy über Nginx. Im selben Zug entschied ich mich, Immich ebenso über Reverse Proxy zu öffnen, sodass der Remote Zugriff deutlich schneller von statten gehen kann. 

Da aber auch Vaultwarden eine meiner Meinung nach sehr ausbaufähige Dokumentation hat, musste ich mich wieder alternativen Quellen bedienen. Zwar gab es für die Docker Compose File und Nginx Konfiguration fertige Dateien, ich musste mich dennoch erst in das Thema Nginx und Reverse Proxy einlesen. Denn das war in dem Fall die größte Schwierigkeit, Nginx zu konfigurieren. Ich habe es nicht geschafft, eine HTTPS-Zertifizierung für meine Domains zu generieren.

Obwohl ich die Ports auf meinen Server umgeleitet und die Domains bei meinem Provider eingetragen habe, konnte ich keine Verbindung zu meinem Server herstellen, und habe nicht verstanden, woran es lag, da ich alles nach Anleitung umgesetzt habe. Irgendwann fiel mir jedoch auf, dass ich den DNS-Server von dem Default DNS meines Domain Providers auf die DNS-Server von Netlify geändert habe, da ich meinen Blog über Netlify hoste. Somit habe ich die DOmains auf dem Netlify-DNS eingetragen, und das Problem wurde gelöst.

So hatte ich dann endlich nach ewiger Fehlersuche sowohl Immich und Vaultwarden immer erreichbar. Jetzt geht es nur darum, die Daten zu übertragen, und Freude an dem privaten, eigenen Server zu haben.

## Fazit

Auch bei diesem Projekt hatte ich viel neues Wissen sammeln können. Funktion von DNS, Ports, Proxys und sogar die einfache Benutzerverwatung von Linux. Die Wartezeit auf meine Wecker PCBs habe ich mit dem aufsetzen des Servers super und produktiv umsetzen können. Und mit Hilfe des Internets ging die Einrichtung sogar schneller als gedacht. Da der Server nun steht, möchte ich mich auch etwas mit dem Hardening befassen, um den Angriff auf den Server zu erschweren, dazu aber mehr in Zukunft.
