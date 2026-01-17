Hier sammeln wir technische Daten zu PV-Wechselrichter-Batteriesystemen der insolventen Firma Hycube. Hilfe zur Selbsthilfe.
Dateien sind aus dem Internet zusammengesucht und wurden so umbenannt, dass man versteht, was drin ist.

Oben rechts unter 'Code' kann man mit 'Download ZIP' alles auf einmal runterladen.

Falls jemand sein Copyright verletzt sieht, sagt bitte einfach Bescheid, dann reden wir drüber.


Ich fange mit dem "e.Compact neo" an, weil ich solch ein System besitze.

Die Hycube-"Waschmaschine" eCompact neo besteht aus drei Teilen:

# 1. Wechselrichter Hycube HY-5K-TL-LV
Siehe [Unterverzeichnis](https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/tree/main/Sermatec%20SMT-5K-TL-LV).

# 2. Batteriespeicher Pylontech UC2000C
Siehe [Unterverzeichnis](https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/tree/main/Pylontech%20US2000C).

# 3. Hycube Controller-Schublade
Siehe [Unterverzeichnis](https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/tree/main/Hycube%20Controller-Schublade).

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
