# Batteriespeicher
Der Batteriespeicher besteht aus zwei bis sechs Pylontech US2000C Akku-Packs 48 V mit je 2,4 kWh parallel. 
Die Pylontechs gibt es schon lange (erste Versionen seit 2016) und sie sind gut dokumentiert. Bei Markteinführung 2016 hießen die Modelle US200B oder US2000 Plus. Der Name wurde 2019 zu US2000 geändert. Etwa 2022 wurde die aktuelle Serie US2000C eingeführt, die bessere Kommunikation, Softstart und einen Anschlusskontakt zum Fernstart bietet. Die Bezeichnung "US2000" oder "US2000C" steht vorn groß drauf.

Die Batterieeinheiten werden übereinander in den Schrank geschoben und vorn mit vier Schrauben befestigt. Die Masterbatterie, meist die unterste, steuert die übrigen. Sie ist mit den ankommenden Batteriekabeln und dem Datenkabel mit dem WR verbunden. Bei Mischbestückung sollte sie die aus der neueste Modellreihe sein. 
In den Hycube-Würfel passen theoretisch 7 Batterien.

## Pylontech-Akkus auslesen mit Konsolen-Kabel und BatteryView
Zum Auslesen von Daten und zum Aktualisieren der Firmware benötigt man ein "Konsolenkabel", das die Batterien mit einem Laptop verbindet. Die Batterie US2000C hat einen RJ45-Anschluss, das ist ein normaler EtherCAT-Stecker. Alte US2000 haben einen RJ11-Anschluss. 
Man findet im Internet noch Anleitungen für den Eigenbau eines solchen Kabels mit DB9-Stecker auf der anderen Seite. Auch die Anleitung von EFFEKTA.com zeigt solche Kabel. Nur ist der "Serielle Port" D-Sub-Anschluss an aktuellen Laptops schon lange nicht mehr vorhanden. Also bräuchte man zusätzlich noch einen Adapter von DB9 auf USB. Das geht einfacher:
Ich verwende direkt ein Adapterkabel von RJ45-Stecker auf USB. Wichtig ist, dass das Kabel für das RS232-Protokoll ist und einen CH340-Chip hat. Ein Kabel mit FT32R-Chip von FTDI hat bei mir nicht funktioniert und ich vermute, ein Prolific PL2303GT funktioniert auch nicht. (Das modernere RS485-Protokoll wird an einem anderen Port für die Kommunikation der Batterien mit dem WR genutzt.)
Die Kabel sind oft hellblau und kosten zwischen 8 und 13 €. Ein Meter ist zu kurz, wenn der Laptop auf dem Cube stehen soll. 

"Kabel zum Auslesen der Pylontech Akkus selber bauen oder kaufen? Hier ein kostengünstiger Vorschlag!" (https://www.youtube.com/watch?v=tSIuWZ_N07c)

Das Programm BatteryView wurde wohl 2014 etwas 'schmutzig' programmiert, deshalb muss jeder Benutzer ein paar Kopfstände machen:
1. Treiberchip im Kabel nur CH340
2. Windows COM-Port-Treiber nur Version 3.7
3. Windows muss auf 'Sprache und Region', 'Regionales Format' auf 'Englisch (Vereintes Königreich) oder Englisch (Vereinigte Staaten)' stehen, damit Komma und Dezimalpunkt richtig übertragen werden. Sonst gibt es die Fehlermeldung "EOF in Header".

In Windows den Geräte-Manger öffnen nach "Anschlüsse (COM & LPT)" suchen. Wenn das neue Gerät dort mit einem Warnzeichen (oder unter "andere") auftaucht, muss man noch einen passenden Treiber installieren. COM-Port-Treiber unter Windows werden wohl für immer eine Baustelle bleiben. 

BatteryView (letzte vorhandene Version 3.0.36). https://www.photovoltaikforum.com/thread/201866-wo-finde-ich-die-pylontech-software-battery-view/?postID=4343567#post4343567

Gleich noch ein Hinweis: Es wird allgemein empfohlen, das UpdateTool (vorhandene Version v1.0.10_3) zum aktualisieren der Firmware zu benutzen, nicht BatteryView. 
Während der Chipkrise wurden in US2000C andere Chips verbaut (erkennbar an E3 oder C3 in der Mitte der Seriennummer), die eine andere Firmware benötigen. Es wird deshalb empfohlen, die unentpackte ZIP-Datei zum Flashen zu benutzen. Das Tool sucht sich die richtige Datei darin selbst. Aktuelle [Firmware](https://www.effekta.com/download/firmwareupdate-fuer-us2000c-3000c/) und das Programm zum Aufspielen gibt es auf der Seite von EFFEKTA.com. 

Siehe auch: https://github.com/Frankkkkk/python-pylontech

