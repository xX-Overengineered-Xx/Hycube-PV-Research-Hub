Hier sammeln wir technische Daten zu PV-Wechselrichter-Batteriesystemen der insolventen Firma Hycube. Hilfe zur Selbsthilfe.
Dateien sind aus dem Internet zusammengesucht und wurden so umbenannt, dass man versteht, was drin ist.

Oben rechts unter 'Code' kann man mit 'Download ZIP' alles auf einmal runterladen.

Falls jemand sein Copyright verletzt sieht, sagt bitte einfach Bescheid, dann reden wir drüber.

Für alle Anleitungen gilt: Wenn ihr komplette Elektro-Muggel seid, fragt jemanden, der sich wirklich damit auskennt und lasst den das machen. Also zum Beispiel einen Elektriker, nicht ChatGPT.

Ich fange mit dem "e.Compact neo" an, weil ich solch ein System besitze.
![](https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/blob/main/hycube%20e_Compact.jpg)

# Zusammenfassung, ganz wichtig
Eine "Hycube-Anlage e.Compact neo" ist aus zugekauften Komponenten zusammengestellt. Alle Komponenten, außer dem eingebauten Wechselrichter, sind einzeln frei nachkaufbar. Sogar der Minicomputer des Controllers. Hycube-Controller und Wechselrichter bilden zusammen die "Hycube-Anlage".

<ins><b>Falls der Wechselrichter kaputtgeht, ist es sofort kein Hycube-System mehr.</b></ins> Der Hycube-Controller arbeitet nicht mit anderen Wechselrichtern, kann also weg. Mit dem Wechselrichter eines anderen Herstellers kauft man praktischerweise auch einen passenden Controller von diesem Hersteller.

Das Problem ist also nicht "Wir müssen ein Hycube-System reparieren, Hycube gibt es nicht mehr und wir haben keine Ahnung", sondern "Wir kaufen einen neuen Wechselrichter und schließen unsere Batterien und PV-Panels an". Das hört sich auch für einen örtlichen Installateur deutlich netter an.

Der reine Materialpreis für einen vergleichbaren 'einfachen' Hydrid-Wechselrichter (5,x kWp, einphasig 230 V, LV-Batterieanschluss, möglichst von der Pylontech-Kompatibilitätsliste) liegt "so um die 1000 €".
Man kann auch die Chance nutzen, mit einem besseren Wechselrichter aufzurüsten. Drei Phasen, unterbrechungfreier Ersatzstrom, alle PV-Panels an die Batterie angeschlossen...

Falls die Anlage läuft: Hycube-PV-Systeme funktionieren auch ohne Internetserver von Hycube weiter. Bisher ist noch keine Funktion bekannt, die über die lokale Weboberfläche hycube.local nicht einstellbar ist. Außer natürlich der dynamische Stromtarif HYMAX, die aber wohl noch gar nicht vollständig gestartet war.

# Mein System läuft, was sollte ich jetzt tun?
- Backup der SD-Karte im Controller machen. Auf die SD-Karte werden regelmäßig alle Erzeugungs- und Verbrauchsdaten geschrieben. SD-Karten überleben eine begrenzte Anzahl Schreibvorgänge, danach geht sie kaputt. Ohne Hycube kann der Inhalt der SD-Karte nicht wieder hergestellt werden. Der Controller funktioniert nicht mehr, weil er kein Betriebssystem hat (das läßt sich wohl lösen) aber die historischen Erzeugung- und Verbrauchsdaten sind weg. Die SD-Karte ist eine echte Archillesferse des Systems. Manchmal ist eine defekte Karte noch lesbar, nur nicht beschreibbar (um die Daten zu schützen), aber darauf sollte man sich nicht verlassen. Ich empfehle den Einsatz einer neueren High Endurance-Karte, die deutlich länger hält.
- Bei Bedarf: Fehlerspeicher der Pylontech-Batterien auslesen und Firmware aktualisieren. Bei gefundenen Fehlern die Ladespannung im Wechselrichter auf 52 V heruntersetzen.
- Bei Bedarf: Regelmäßig (mindestens alle 6 Monate) alle Zellspannungen der Pylontech-Batterien überprüfen und sie ggf. manuell balancieren. (Batterien voll laden und zum Selbstausgleich lange stehen lassen, bis die LEDS nicht mehr blinken.)
- Schon mal überlegen, wie man vorgehen möchte, wenn der Wechselrichter irgendwann ausfällt. Also welchen Wechselrichter man kaufen möchte, um danach Hycube-frei zu sein. Ein Plan und sein Preis wirken entspannend.
- Ansonsten: "Alle Anlagendaten bleiben im lokalen Speichersystem erhalten (auf der SD-Karte). Die Funktion Ihrer Anlage ist durch das Abschalten des Servers nicht beeinträchtigt. Lokaler Zugriff bleibt dauerhaft und kostenfrei möglich." Zugriff über einen Browser im Heimnetzwerk: http://hycube.local (klappt selten nicht, notfalls über die IP-Adresse der Anlage, zu finden im Router). Für den Zugriff aus dem Internet muss man z.B. einen VPN-Zugang einrichten.

## Anleitung: Backup der SD-Karte machen
Unter Windows mit dem Programm Win32 Disk Imager. SD-Karte ins Kartenlesegerät stecken, den Laufwerksbuchstaben der Karte als Quelle wählen, Dateiname für Ziel auf der Festplatte eingeben. Die erzeugte Image-Datei ist eine 1:1-Kopie der 16 GB großen SD-Karte, hat also auch jede Menge Leerraum. Man kann sie auf etwa 660 MB komprimieren, um Speicherplatz zu sparen.

Unter MacOS ist die Sache etwas komplizierter. Siehe [hier](https://www.photovoltaikforum.com/thread/254137-hycube-insolvenz-umr%C3%BCstung-auf-open-source-manager/?postID=4659622#post4659622). Ich vermute, dass es es Programme gibt, die das Auslesen wie unter Windows ohne Kommandozeile erledigen.

Wenn (nicht *falls*) der Originalkarte etwas passiert, kann man das Image auf jede beliebige SD-Karte aufspielen und den Controller weiter betreiben. Die Erzeugungsdaten seit dem letzten Backup sind allerdings weg.
***

Die Hycube-"Waschmaschine" eCompact neo besteht aus drei Teilen:

# 1. Wechselrichter Hycube HY-5K-TL-LV
Siehe [Unterverzeichnis](https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/tree/main/Sermatec%20SMT-5K-TL-LV).

# 2. Batteriespeicher Pylontech UC2000C
Siehe [Unterverzeichnis](https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/tree/main/Pylontech%20US2000C).

# 3. Hycube Controller-Schublade
Siehe [Unterverzeichnis](https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/tree/main/Hycube%20Controller-Schublade).

# 4. Zweiter Wechselrichter ohne Batterieanschluss
Der Sermatec-WR hat nur Anschlüsse für zwei PV-Strings, deshalb werden alle weiteren Strings über einen zweiten, externen WR bedient, der aber nicht mit den Batterien verbunden ist. Das ist oft ein FoxESS T*-G3, wobei * für die Leistung in kW steht.
Falls der interne oder der externe WR kaputt geht, sollte man überlegen, ob man nicht einen großen Hybridwechselrichter für die gesamte PV-Anlage beschafft, so dass man die gesamt PV-Leistung in die Batterie laden kann. 

# Wallbox nachrüsten
Siehe [Unterverzeichnis](https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/tree/main/Wallbox%20(Heidelberg)).

Die Wallbox "Hycube Energy Control" ist eine umgelabelte von Heidelberg. Eine originale 11 kW Wallbox vom Typ "Heidelberg energy control" lässt sich mittels eines RS485-auf-USB-Adapters (oft falsch "Dongle" genannt) mit dem HyCube Controller verbinden. Somit lässt sich die Wallbox dann auch smart steuern, sowohl am Display als auch im Web Interface über hycube.local.

# Schaltbare Steckdosen nachrüsten
Es wurde das EnOcean-System verwendet. Siehe Posting [hier](https://www.photovoltaikforum.com/thread/254137-hycube-insolvenz-umr%C3%BCstung-auf-open-source-manager/?postID=4648154#post4648154). Den USB-Sender nicht direkt in den USB-Hub in der Schublade stecken, sonst ist die Reichweite wegen der Abschirmung der Box zu gering. USB-Verängerungskabel nach ausserhalb der Box verwenden.
Das EnOcean-System finde ich persönlich zu hochpreisig und die Steuerungmöglichkeiten der Steckdose im Hycube-Controller (wenn..dann) sind recht einfach. Ich würde es nur verwenden, wenn ich absolut kein Interesse an einer eigenen, Hycube-unabhängigen Haussteuerung (z.B. mit Home Assistant) hätte.

# Notstrom
Hycubes e.Compact hat hinten eine Schuko-Steckdose, mit der man ein Gerät mit einphasig 230 V Notstrom versorgen kann. Bei längerem Stromausfall könnte man dort zum Beispiel die kleine Heizungspumpe anschließen, die Heizungswasser zu den Heizkörpern pumpt, damit im Winter die Heizungsrohre nicht einfrieren.

# Ersatzstrom
Ersatzstrom für das ganze Haus ist etwas aufwändiger. Es wurde ein automatische Lastumschalter Typ "Socomec ATyS p M" im Sicherungskasten verbaut. Der Lastumschalter trennt bei Stromausfall alle drei Phasen des Hausnetzes vom Stromnetz, so dass der Wechselrichter das Hausnetz aus den Batterien versorgen kann, ohne im Stromnetz jemanden zu gefährden. Das Umschalten ist ziemlich laut und die Spannungsversorgung wird für ein paar Sekunden unterbrochen. Da der Wechselrichter nur einphasig AC ausgeben kann, steht während des Netzausfalls kein Drehstrom zur Verfügung.

# Hycube-Besonderheiten, Fehler
Soweit ich es verstehe, ist die Einschaltreihenfolge so, dass zuerst der WR gestartet wird, dann die Batterien, dann der Controller. Das kann bis zu 2 Minuten dauern.
Leider scheint es so zu sein, dass ein Fehler am WR oder einer Batterie dazu führt, dass der Controller nicht mehr hochfährt, da er aus den 48 V DC-Kabeln zwischen Wechselrichter und Batterie versorgt wird. Das kann ein Hardwarefehler sein, den der WR feststellt oder der Tiefentladeschutz der Batterien. In dem Fall muss man die Fehler dieses Gerätes zuerst beheben, damit der Controller wieder läuft. Zu Testzwecken kann man das Traco-'Netzteil' auch mit 18 bis 75 V DC fremdversorgen, um den Controller unabhängig vom System zu starten. Falls das nicht klappt könnte das Traco defekt sein, dann die Ausgangsseite mit 24 V DC fremdversorgen. 
Danach weiter mit Sermatec-App und Konsolenkabel. 

# Einfachste Fehlersuche
Zuerst die externe Sicherung in einem Sicherungsschrank kontrollieren.

Wenn der Controller nicht startet, ist entweder der Controller selbst kaputt (selten) oder die Spannungsversorgung aus der 48 Volt DC-Verbindung zwischen Batterien und Wechselrichter funktioniert nicht. Oft gehen die Batterien nach dem Selbsttest auf Störung und ihre roten ALM-LEDs (Alarm) leuchten. Die Frage ist dann "Sind es die Batterien oder der Wechselrichter?".

Um das heraus zu bekommen, schaltet man zuerst die gesamte Anlage nach Hycube-Bedienungsanleitung aus. Dann zieht man die beiden langen Batteriekabel ab, die zum Wechselrichter führen (Knopf am Stecker drücken, siehe Pylontech-Bedienungsanleitung). Nun sind die Batterien noch untereinander verbunden, aber nicht mehr mit dem Wechselrichter. Wenn man die Batterien jetzt nacheinander mit ihren Ein-/Aus-Kippschaltern einschaltet und dann an der Masterbatterie (die sonst die Kabel zum WR hat) für mindestens 0,5 Sekunden den roten SW-Knopf drückt, werden alle Batterien geweckt, machen einen Selbsttest und zeigen hoffentlich keinen Fehler mehr.
Glückwunsch, die teuren Batterien sind okay, es ist wahrscheinlich der Wechselrichter.

Ein Fachmann könnte jetzt im abgeschalteten Zustand eine Durchgangsprüfung zwischen den freien Enden der beiden abgezogenen Batteriekabeln machen. Wenn man dort Null Ohm misst, ist wahrscheinlich der Wechselrichter kaputt. Der nächste Schritt wäre jetzt, über die App des Wechselrichters eine Fehlermeldung zu bekommen, zum Beispiel "Bus Insulation Resistance Fault".

Falls trotzdem noch Batterien Fehler melden, liest man sie einzeln oder zusammen per Konsolenkabel und BatteryView aus. 

Wenn der Wechselrichter und die Batterien einzeln ohne Fehlermeldung starten, der Controller aber nach mehreren Minuten (und Drücken des weissen Startknopfes) nicht, könnte es sein, dass der DC/DC-Wandler ("Netzteil") von Traco für die Hilfskomponenten in der Schublade defekt ist. Ein Fachmann könnte entweder 18-75 V DC am Eingang oder 24 V DC am Ausgang anschliessen, um zu sehen, ob der Controller startet. Der Controller nimmt dann direkt wieder Kontakt mit dem Internetserver auf.

# Home Assistant
Da der Hycube-Controller im Hausnetz eine Weboberfläche bereitstellt (hycube.local) kann man über einen RESTful-Sensor eine json-Abfrage aller angezeigten Werte starten ([Link](https://community.simon42.com/t/daten-aus-http-abfrage-auswerten/60653)). Einstellen kann man damit aber nichts.

Für den Sermatec-WR gibt eine standalone-Integration ([Link](https://github.com/sermatec-opensource/homeassistant-sermatec-inverter)) für Home Assistant, allerdings muss man den WR dann per LAN-Kabel verbinden. Der Ethernet-Stecker ist aber mit dem Hycube-Controller verbunden.

Die App EVCC (Electric Vehicle Charge Controller)([Link](https://docs.evcc.io/en/docs/Home), [GitHub](https://github.com/evcc-io/evcc)) unterstützt seit Ende 2025 auch den Sermatec. EVCC kann das Ladeverhalten des WR an Wallboxen oder Batterien steuern. Es gibt auch eine inoffizielle Home Assistant Integration ([Link](https://docs.evcc.io/docs/integrations/home-assistant))([GitHub](https://github.com/marq24/ha-evcc))([Erklärung, warum gut](https://smarterkram.de/8590/warum-evcc-in-kombination-mit-home-assistant-richtig-spass-macht/))([Tipps](https://github.com/evcc-io/evcc/discussions/19628)).
