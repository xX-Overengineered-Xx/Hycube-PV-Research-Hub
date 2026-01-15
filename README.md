Hier sammeln wir technische Daten zu PV-Wechselrichter-Batteriesystemen der insolventen Firma Hycube. Hilfe zur Selbsthilfe.
Dateien sind aus dem Internet zusammengesucht und wurden so umbenannt, dass man versteht, was drin ist.
Oben rechts unter 'Code' kann man mit 'Download as ZIP' alles auf einmal runterladen.
Fall jemand sein Copyright verletzt sieht, sagt bitte einfach Bescheid, dann reden wir drüber.


Ich fange mit dem "e.Compact neo" an, weil ich solch ein System besitze.

Die Hycube-"Waschmaschine" eCompact neo besteht aus drei Teilen:
# 1. Wechselrichter Hycube HY-5K-TL-LV
Das ist ein umgelabelter Sermatec SMT-5KT-LV, der auf der Rückseite des Cube mit Vorderseite nach innen und Kühlrippen nach außen montiert wurde. Dadurch kann man die Status-LEDs nicht sehen.
Der WR kann etwa 5 kW, deshalb ist die Entladeleistung selbst bei den großen Batteriesätzen auf 4,8 kW begrenzt.

Der Wechselrichter baut ein eigenes WLAN mit dem Namen "ST000921…" mit kurzer Reichweite auf. Zum Auslesen einiger Daten kann man auf einem Mobiltelefon die Sermatec-App installieren und sich mit diesem WLAN verbinden (Passwort ist gsstes123456). Man muss aber ziemlich dicht daneben stehen.

Nach dem Start der App nicht anmelden, sondern ganz unten "lokal verwenden" (oder so). Die App zeigt auch Fehlermeldungen, falls es welche gibt. 
Die App erlaubt auch Cloud-Zugriff. Vielleicht gibt es hier die Möglichkeit, direkt über Sermatec irgendwie zu gehen und Zugriff auf den Wechselrichter von unterwegs zu erhalten...

Ob der WR von Sermatec für Hycube mit geänderter Firmware versehen wurde oder man intern die direkte Batterienutzung freischalten kann, ist aktuell nicht klar. Im ersten Fall wäre eine originale Firmware von Sermatec eine Lösung. Die hat bisher noch niemand gespendet.

Ersatz: Sermatec baut inzwischen keine Wechselrichter mehr für den Consumer-Bereich, deshalb hat Hycube bei den Tri.aktiv-Geräten auf IMEON gewechselt. Das wäre eine Option, falls ein Sermatec kaputt geht. Wichtig sollte sein, dass ein neuer WR auf der Kompatibilitätsliste von Pylontech steht, damit er die Batterien direkt ansprechen kann, falls der Hycube-Controller mal kaputt geht. Victron macht viel mit Pylontech. Falls man das System mit eigenem statt Hycube-Controller betreiben will/muss ist die Kompatibilität egal, weil der Controller zwischen WR und Batterie kommunizieren kann. Dann muss man aber alles selbst programmieren.

https://github.com/sermatec-opensource

# 2. Batteriespeicher
Der Batteriespeicher besteht aus zwei bis sechs Pylontech US2000C Akku-Packs 48 V mit je 2,4 kWh parallel. 
Die Pylontechs gibt es schon lange (erste Versionen seit 2016) und sie sind gut dokumentiert. Bei Markteinführung 2016 hießen die Modelle US200B oder US2000 Plus. Der Name wurde 2019 zu US2000 geändert. Etwa 2022 wurde die aktuelle Serie US2000C eingeführt, die bessere Kommunikation, Softstart und einen Anschlusskontakt zum Fernstart bietet. Die Bezeichnung "US2000" oder "US2000C" steht vorn groß drauf.

Die Batterieeinheiten werden übereinander in den Schrank geschoben und vorn mit vier Schrauben befestigt. Die Masterbatterie, meist die unterste, steuert die übrigen. Sie ist mit den ankommenden Batteriekabeln und dem Datenkabel mit dem WR verbunden. Bei Mischbestückung sollte sie die aus der neueste Modellreihe sein. 
In den Hycube-Würfel passen theoretisch 7 Batterien.

## 2.1 Pylontech-Akkus auslesen mit Konsolen-Kabel und BatteryView
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

BatteryView (letzte vorhandene Version 3.0.36). 
Aktuelle [Firmware](https://www.effekta.com/download/firmwareupdate-fuer-us2000c-3000c/) und Programme zum Aufspielen gibt es auf der Seite von EFFEKTA.com. 

Gleich noch ein Hinweis: Es wird allgemein empfohlen, das UpdateTool (vorhandene Version v1.0.10_3) zum aktualisieren der Firmware zu benutzen, nicht BatteryView. 
Während der Chipkrise wurden in US2000C andere Chips verbaut (erkennbar an E3 oder C3 in der Mitte der Seriennummer), die eine andere Firmware benötigen. Es wird deshalb empfohlen, die unentpackte ZIP-Datei zum Flashen zu benutzen. Das Tool sucht sich die richtige Datei darin selbst.


https://github.com/Frankkkkk/python-pylontech

# 3. Hycube Controller-Schublade
Dies ist der interessanteste Teil, denn die anderen Komponenten sind recht gut dokumentiert, wenn man ihren Namen kennt.

Der zentrale Controller ist ein Chipsee-Minicomputer ("Controller") mit farbigem 5 Zoll-Display mit Touchscreen. Das ist die flache Kunststoffkiste hinter dem Touchscreen rechts. Vermutlich läuft darauf ein minimales Android-Betriebssystem auf einem ARM Cortex-A8. Links auf der Oberseite ist ein Slot für eine microSD-Karte. Auf der Karte ist das Betriebssystem und alle bisherigen Verlaufsdaten, tagesgenau in SQL-Dateien. Über Ethernet-Kabel stellt der Controller auch den Webserver für die Hycube.local-Oberfläche im lokalen LAN-Netzwerk (in jedem Webbrowser).

Weitere Komponenten
Hinten ganz links zwei Verteilerblöcke Contaclip 27202.0 für Plus und Minus 48 V.

Links davor fernbedienbarer Leistungsschalter (Remote Actuator Unit = RAU) von CBi D-5AAMX2VASK125KXA-XXXXXBDVAX3-X Re-order no: D5AKXA0001. 

Hinten links Netzteil Traco Power TCL 060-124 DC (18-75 V auf 24 V), 
davor USB-Hub 1 auf 4,
davon Finder Installationsschütz 22.32.0.230.4440
In der Mitte ein USB-Relaisboard von Denkovi.

Rechts vorn Stromstoßschalter Finder 20.21.9.024.4000. Dies ist ein bistabiles Relais, das die Spannungsversorgung für den Controller ein- oder ausschalten kann. Betätigt von Versorgungsspannung 48 V von Batterien oder vom weißen Taster vorn rechts.

# 4. Zweiter Wechselrichter ohne Batterieanschluss
Der Sermatec-WR hat nur Anschlüsse für zwei PV-Strings, deshalb werden alle weiteren Strings über einen zweiten, externen WR bedient, der aber nicht mit den Batterien verbunden ist. Das ist oft ein FoxESS T*-G3, wobei * für die Leistung in kW steht. 

# Wallbox nachrüsten
Die Wallbox "Hycube Energy Control" ist eine umgelabelte von Heidelberg. Eine originale 11 kW Wallbox vom Typ "Heidelberg energy control" lässt sich mittels eines RS485-auf-USB-Adapters (oft falsch "Dongle" genannt) mit dem HyCube Controller verbinden. Somit lässt sich die Wallbox dann auch smart steuern, sowohl am Display als auch im Web Interface über hycube.local.

# Notstrom
Hycubes e.Compact hat hinten eine Schuko-Steckdose, mit der man ein Gerät mit einphasig 230 V Notstrom versorgen kann. Bei längerem Stromausfall könnte man dort zum Beispiel die kleine Heizungspumpe anschließen, die Heizungswasser zu den Heizkörpern pumpt, damit im Winter die Heizungsrohre nicht einfrieren.

# Ersatzstrom (dreiphasig)
Dreiphasiger Ersatzstrom für das ganze Haus ist etwas aufwändiger. Es wurde ein automatische Lastumschalter Typ "Socomec ATyS p M" im Sicherungskasten verbaut. Der Lastumschalter trennt bei Stromausfall das Hausnetz vom Stromnetz, so dass der Wechselrichter das Hausnetz aus den Batterien versorgen kann, ohne im Stromnetz jemanden zu gefährden. Das Umschalten ist ziemlich laut und die Spannungsversorgung wird für ein paar Sekunden unterbrochen.
# Hycube-Besonderheiten, Fehler
Soweit ich es verstehe, ist die Einschaltreihenfolge so, dass zuerst der WR gestartet wird, dann die Batterien, dann der Controller. Das kann bis zu 2 Minuten dauern.
Leider scheint es so zu sein, dass ein Fehler am WR oder einer Batterie dazu führt, dass der Controller nicht mehr hochfährt, da er aus den 48 V DC-Kabeln zwischen Wechselrichter und Batterie versorgt wird. Das kann ein Hardwarefehler sein, den der WR feststellt oder der Tiefentladeschutz der Batterien. In diesem Fall muss man die Fehler dieses Gerätes zuerst beheben, damit irgendwann der Controller wieder läuft. Zu Testzwecken kann man das Traco-Netzteil auch Fremdversorgen, um den Controller unabhängig vom System zu starten.
Stichwort Sermatec-App, Konsolenkabel. 

# Home Assistant
Da der Hycube-Controller eine Weboberfläche bereitstellt (hycube.local) kann man über eine RESTful-Sensor eine json-Abfrage aller angezeigten Werte starten ([Link](https://community.simon42.com/t/daten-aus-http-abfrage-auswerten/60653)). Einstellen kann man damit aber nichts.

Für den Sermatec-WR gibt eine standalone-Integration ([Link](https://github.com/sermatec-opensource/homeassistant-sermatec-inverter)) für Home Assistant, allerdings muss man diesen dann per LAN-Kabel verbinden. Der Ethernet-Stecker ist aber mit dem Hycube-Controller verbunden.

Die App EVCC (Electric Vehicle Charge Controller)([Link](https://docs.evcc.io/en/docs/Home), [GitHub](https://github.com/evcc-io/evcc)) unterstützt seit Ende 2025 auch den Sermatec. EVCC kann das Ladeverhalten des WR an Wallboxen oder Batterien steuern. Es gibt auch eine inoffizielle Home Assistant Integration ([Link](https://docs.evcc.io/docs/integrations/home-assistant))([GitHub](https://github.com/marq24/ha-evcc))([Erklärung, warum gut](https://smarterkram.de/8590/warum-evcc-in-kombination-mit-home-assistant-richtig-spass-macht/))([Tipps](https://github.com/evcc-io/evcc/discussions/19628)).
