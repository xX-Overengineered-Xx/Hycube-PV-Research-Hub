# Batteriespeicher
Der Batteriespeicher besteht aus zwei bis sechs Pylontech US2000C Akku-Packs 48 V mit je 2,4 kWh parallel. 
Die Pylontechs gibt es schon lange (erste Versionen seit 2016) und sie sind gut dokumentiert. Bei Markteinführung 2016 hießen die Modelle US200B oder US2000 Plus. Der Name wurde 2019 zu US2000 geändert. Etwa 2022 wurde die aktuelle Serie US2000C eingeführt, die bessere Kommunikation, Softstart und einen Anschlusskontakt zum Fernstart bietet. Die Bezeichnung "US2000" oder "US2000C" steht vorn groß drauf.
Bei Videos und Anleitungen darauf achten, dass die nicht für UC3000 oder UC5000 sind. Diese größeren Modelle sind neuer und etwas anders.

Die Batterien werden einfach übereinander in den Schrank geschoben und vorn mit vier Schrauben befestigt. Jede Batterie hat zwei verbundene Pluspole (rot) und zwei verbundene Minuspole (schwarz). Die erste Batterie wird an ein rotes und ein schwarzes Kabel vom Wechselrichter angeschlossen. Dann kommen die kurzen Kabel jeweils zur nächsten Batterie. Es sind alle Pluspole und alle Minuspole miteinander verbunden, die Batterien also parallel geschaltet. Deshalb haben alle die gleiche Spannung von nominell 48 Volt.
Bei der Datenverkabelung läuft es so ähnlich. Eine Batterie ist die Masterbatterie, sie steuert die übrigen. Sie ist mit einem Datenkabel im unteren mittleren Anschluss "B/RS485" mit dem WR verbunden. Bei Mischbestückung sollte sie die aus der neueste Modellreihe sein. Dann kommen die kurzen schwarzen Datenkabel, jeweils vom "Linkport 1" zum "Linkport 0" der nächsten Batterie.  

![Foto 4x Pylontech](https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/blob/main/Pylontech%20US2000C/4x%20Pylontech.jpg)

## 1. Was tun, wenn die Batterie pfeift?
Achtung: Da ist ersthaft etwas falsch. Wer hier einfach ein paarmal den Reset-Knopf drückt, riskiert mindestens seine Batterien.

Pylontech schreibt: "Summer weisen auf einen fehlerhaften Zustand mit hohem Risiko hin.

a) Polarität der Batteriekabel (Powerkabel vertauscht)

Lösung: Schalten Sie alle Batterien und Wechselrichter aus. Leistungsschalter abklemmen. Überprüfen Sie die Kabelverbindung und ziehen Sie alle Stromkabel ab. Überprüfen Sie, ob der Stromanschluss beschädigt ist oder nicht. Schalten Sie dann das einzelne Modul ein, ohne dass ein Kabel angeschlossen ist. Wenn kein Alarm vorliegt, handelte es sich um eine falsche Verbindung der Kabel. Schalten Sie das Modul aus und wenden Sie sich an Ihren Händler.

b) Interner Hardwarfehler.

Lösung: Schalten Sie alle Batterien und Wechselrichter aus. Leistungsschalter abklemmen. Überprüfen Sie die Kabelverbindung und ziehen Sie alle Stromkabel ab. Überprüfen Sie, ob der Stromanschluss beschädigt ist oder nicht. Schalten Sie dann das einzelne Modul ein, ohne dass ein Kabel angeschlossen ist. Wenn immer noch ein Summer ertönt. Dann liegt ein Interner Fehler vor. Schalten Sie das Modul aus und wenden Sie sich an Ihren Händler."

## 2. Pylontech-Batterien auslesen mit Konsolen-Kabel und BatteryView
Man kann die Spannungen aller Zellen und die Ladezustände (SoC) der einzelnen Batterien auch im Webinterface hycube.local unter Einstellungen, Anlagenkontrolle, Batterien auslesen. Oder am Controller unter Systemeinstellung, Service, Status, Batterie.

Zum Auslesen weiterer Daten und zum Aktualisieren der Firmware benötigt man ein "Konsolenkabel", das die Batterien mit einem Laptop verbindet. Die Batterie US2000C hat einen RJ45-Anschluss, das ist ein normaler EtherCAT-Stecker. Alte US2000 haben einen RJ11-Anschluss. 
Man findet im Internet noch Anleitungen für den Eigenbau eines solchen Kabels mit DB9-Stecker auf der anderen Seite. Auch die Anleitung von EFFEKTA.com zeigt solche Kabel. Nur ist der "Serielle Port" D-Sub-Anschluss an aktuellen Laptops schon lange nicht mehr vorhanden. Also bräuchte man zusätzlich noch einen Adapter von DB9 auf USB. Das geht einfacher:
Ich verwende direkt ein Adapterkabel von RJ45-Stecker auf USB. Wichtig ist, dass das Kabel für das RS232-Protokoll ist und einen CH340-Chip hat. Ein Kabel mit FT32R-Chip von FTDI hat bei mir nicht funktioniert und ich vermute, ein Prolific PL2303GT funktioniert auch nicht. (Das modernere RS485-Protokoll wird an einem anderen Port für die Kommunikation der Batterien mit dem WR genutzt.)
Die Kabel sind oft hellblau und kosten zwischen 8 und 13 €. Ein Meter ist zu kurz, wenn der Laptop auf dem Cube stehen soll. 

Das Video "[Kabel zum Auslesen der Pylontech Akkus selber bauen oder kaufen? Hier ein kostengünstiger Vorschlag!](https://www.youtube.com/watch?v=tSIuWZ_N07c)" von *Solar-einfach-gemacht* zeigt beispielhaft ein Kabel und wie man den richtigen Treiber unter Windows installiert.

Das Programm BatteryView wurde wohl 2014 etwas 'schmutzig' programmiert, deshalb muss jeder Benutzer ein paar Kopfstände machen:
1. Treiberchip im Kabel nur CH340. FT-Chips funktionieren nicht immer.
2. Windows COM-Port-Treiber nur Version 3.7
3. Windows muss auf 'Sprache und Region', 'Regionales Format' auf 'Englisch (Vereintes Königreich) oder Englisch (Vereinigte Staaten)' stehen, damit Komma und Dezimalpunkt richtig übertragen werden. Sonst gibt es die Fehlermeldung "EOF in Header".

In Windows den Geräte-Manger öffnen nach "Anschlüsse (COM & LPT)" suchen. Wenn das neue Gerät dort mit einem Warnzeichen (oder unter "andere") auftaucht, muss man noch einen passenden Treiber installieren. COM-Port-Treiber unter Windows werden wohl für immer eine Baustelle bleiben. 

Beim Verbindungsaufbau muss die Checkbox "United" ausgewählt sein und bei "Units" die Anzahl der Module eingetragen werden, dann kann man alle Batterien gleichzeitig auslesen.

BatteryView (letzte vorhandene Version 3.0.36). https://www.photovoltaikforum.com/thread/201866-wo-finde-ich-die-pylontech-software-battery-view/?postID=4343567#post4343567

## 3. Pylontech-Batterien Firmware updaten mit UpdateTool
Zusätzlich sollte man jetzt einmal die neueste Firmware aufspielen. Pylontech veröffentlich keine Beschreibungen, was in der Firmware geändert wurde, aber man kann davon ausgehen, dass sie in der Zwischenzeit Fehler bei den neuen Chips (2021) korrigiert haben. Es wird allgemein empfohlen, das UpdateTool (vorhandene Version v1.0.10_3) zum aktualisieren der Firmware zu benutzen, nicht BatteryView. 
Während der Chipkrise wurden in US2000C andere Chips verbaut (erkennbar an E3 oder C3 in der Mitte der Seriennummer), die eine andere Firmware benötigen. Es wird deshalb empfohlen, die unentpackte ZIP-Datei zum Flashen zu benutzen. Das Tool sucht sich die richtige Datei darin selbst. Aktuelle [Firmware](https://www.effekta.com/download/firmwareupdate-fuer-us2000c-3000c/) und das Programm zum Aufspielen gibt es auf der Seite von EFFEKTA.com. 

## 4. Pylontech-Batterie aufladen mit Labornetzteil
Wenn der Hycube-Controller aus ist, kann man dem Wechselrichter nicht den Befehl geben, die Batterien aus dem Netz zu laden. Man sollte dann erstmal herausfinden, warum der Controller nicht funktioniert und ob etwas kaputt ist.

Pylontech schreibt in der Bedienungsanleitung: "2) Bei längerer Lagerung der Batterie muss diese alle sechs Monate aufgeladen werden und es muss sichergestellt sein, dass der Ladungszustand nicht weniger als 90% beträgt. 3) Nach vollständiger Entladung muss die Batterie innerhalb von 12 Stunden wieder aufgeladen werden."

Für alle Anleitungen gilt: Wenn ihr komplette Elektro-Muggel seid, fragt jemanden, der sich wirklich damit auskennt und lasst den das machen. Also zum Beispiel einen Elektriker, nicht ChatGPT.

Die einzige mir bekannte Methode ist, die Pylontech-Batterien einzeln von extern laden, zum Beispiel mit einem DC-Labornetzteil 60 Volt (mindestens 5 Ampere). Kostet bei Amazon ab 65 €. Wie es geht, wird in diesem Video beschrieben: https://www.youtube.com/watch?v=4K3RAzwkvss

Zur höchsten Ladespannung: "Im Akkudoktor-Forum ist man sich längst 'darüber einig', dass das Laden über 3,45 V pro Zelle nicht nötig ist, um einen Lifepo Akku voll zu laden" [Link](https://akkudoktor.net/t/lifepo4-grundlagen-ladespannung-und-balancierung/31693/13). Das wären bei 15 Zellen 51,75 V.

Alle Batterien trennen (Kabel abziehen), eine Batterie an Plus und Minus des Netzteils anschließen, 52 V bei 5 A einstellen und lange warten. Der Strom fällt immer weiter, bis die Batterie fast voll ist. Bei 52 V sind die Batterien nicht 100% voll (die offizielle Ladespannung beträgt 53,5 V), aber es ist sicher und reicht, dass die Zellen wieder ausbalanciert werden (min. 92% SoC). Den Vorgang für jede Batterie wiederholen und hinterher alle Batterien miteinander verbinden und sich gemeinsam ausbalancieren lassen. Wird nochmal lange dauern, aber dann sind alle wieder fit.
Man kann das noch perfektionieren, indem man beispielsweise die Ladespannung in kleinen Schritten von 0,2 V bis zum Höchstwert von 53 V erhöht, immer wenn der Ladestrom unter 1 A fällt. Ich bin nicht sicher, ob das den Aufwand lohnt, auch weil man hinterher immer auch die Batterien sich untereinander balancen lassen muss, aber es gibt Leute, die schwören darauf. 

Ich würde keine Batterie anfassen, ohne sie vorher per Konsolenkabel und BatteryView auf Fehler zu untersuchen. Siehe oben. Hinterher kann man hoffentlich sehen, dass die 15 Zellspannungen in einer Batterie ziemlich gleich sind (Unterschied unter 1%).

Balancing bei voller Ladung ist übrigens von Pylontech vorgeschrieben, wenn man neue Batterien zu alten hinzufügen will. Dabei kann man das Laden aber im Gerät machen.
Ich würde das auch immer machen, wenn die Batterien lange halbleer ausgeschaltet gestanden haben.

## 5. Das Problem mit dem "Aufblähen"

_Ich bin kein Batterieexperte. Aber ich habe kürzlich mit einem gesprochen, und die Sache scheint für den Normalbenutzer etwas weniger dramatisch zu sein. Zwischen März 2022 und September 2023 gab es wohl bei Pylontech Produktionsschargen, bei denen einzelne Zellen (von 15) schlecht waren. Die sind alle nach spätestens 3 Monaten mit hunderten Fehlermeldungen gestorben. Damit hat sich mein Plan wie unten beschrieben, fast erledigt. Die betroffenen Geräte sind inzwischen verstorben und der Rest hat die übliche Zuverlässigkeit._
 
Pylontech-Batterien haben intern ein passives Battery Management System (BMS). Das gleichmäßige Laden aller 15 Zellen pro Batterie wird dadurch geregelt, dass einzelne Zellen per zuschaltbarem Widerstand ausgebremst werden. Sobald die erste Zelle trotz Widerstand mehr als 3,6 V erreicht (Ladeschlußspannung), schaltet das BMS ab und die Batterie geht in den Overvoltage (OV) Modus = Ruhezustand. Kein Balancing mehr möglich, obwohl andere Zellen vielleicht erst bei 3,4 V sind.
Die häufig verwendeten 53,2 V Ladespannung sind bei 15 Zellen in Reihe je 3,55 V. Das ist recht hoch und dicht an 3,6 V und so kann es passieren, dass die Batterie häufig mit OV-Modus abschaltet. So können die Ladungen der Zellen innerhalb einer Batterie bei längerem Gebrauch immer weiter auseinander driften. Das kann zu schweren Schäden führen, wenn einige Zellen immer wieder mit zu hoher Spannung geladen werden. Die Zellen können Gasblasen bilden und sich schließlich aufblähen. Das ist möglich, weil es Pouch-Zellen ohne druckfeste Hülle sind. 

Victron versucht das Problem zu vermeiden, indem sie die Ladespannung des Wechselrichters auf 52,4 V begrenzen. Dadurch verringert man deutlich das Risiko, dass die Batterie mit OV abschaltet und das Balancing ausfällt. Der Nachteil ist eine geringfügige Verringerung der Kapazität der Batterie, aber nur bei höchster Ladung.
Das funktioniert allerdings nur, wenn der Wechselrichter seine Begrenzung auch einhält und nicht durch die per Bussystem gegebenen Grenzwerte des BMS überstimmt wird. Im BMS der Pylontech-Batterien stehen seit Jahren die gleichen höheren Werte.

Laut Christoph Weidner (deyeguru, Kommentar [hier](https://www.youtube.com/watch?v=xAQWjpebymQ)) hatten die von ihm ausgewerteten aufgeblähten Akkus von Beginn an mit HV und OV Fehlern zu kämpfen. HV-Fehler (High Voltage) können alle möglichen Fehler sein, unter anderem fehlerhafte Kommunikation zwischen BMS und Wechselrichter aber auch dass Über- oder Unterspannungsschutz ausgelöst wurden. Wenn man die Fehlermeldungen im Betrieb auswerten könnte, hätte man eine gute Vorwarnung.

Das BMS kann die Zellen auch im Stillstand untereinander ausgleichen, aber nur wenn sich die Zellen im flachen Bereich der Ladekurve, also im recht hohen Ladezustand (SoC, State of Charge) größer als 92% befinden. Außerdem kann der Regler nur 100 mA (?) pro Zelle übertragen, also dauert das ewig. Wenn die Batterien also nicht längere Zeit über 92% SoC stehen, kann das Balancing schlecht sein.

Eine gute Lösung wäre, die vom BMS gemessene maximale und minimale Zellspannung zu beobachten und bei mehr als 1% Unterschied (das sind nur 30 mV, die laut Pylontech okay sind) den Benutzer zu warnen. Oder gleich ein Balancing zu erzwingen. Das geht am Einfachsten, indem man alle Batterien (ggf. aus dem Netz) voll lädt und so lange stehen lässt, bis die Zellspannungen angeglichen sind. Das kann, wie gesagt, recht lange dauern. Das Ende des Selbst-Balancing erkennt man am Stromverbrauch, am Blinkmuster der LEDs und daran, dass sich die Zellspannungen angeglichen haben.

Wie bekommt man also Pylontech-Batterien kaputt?
- Hohe Ladeschlussspannung, so dass die Batterie jeden Ladevorgang mit OV-Fehler beendet und das Balancing nicht beendet.
- Einen Wechselrichter benutzen, der Überspannungswarnungen und unterschiedliche Zellspannungen ignoriert. 
- Batterien nie voll geladen länger stehen lassen, um Self-Balancing zu verhindern.

## 6. Hardware
Wer einmal risikofrei in die Pylontech-Batterien hineinsehen will, wie das BMS aussieht, dem sei das [YouTube-Video von José Faria](https://www.youtube.com/watch?v=BYKeGvza1OM) empfohlen.
Er zeigt einen Fall, dass die Batterie keinen Fehler und keine Auffälligkeiten meldet, aber keine Spannung liefert. Die letzte Schutzstufe ganz links sind selbst rückstellende Sicherungen, die auch durch eine interne Heizung ausgelöst werden können. Die waren alle durchgebrannt und werden von ihm ersetzt.
