# Batteriespeicher
Der Batteriespeicher besteht aus zwei bis sechs Pylontech US2000C Akku-Packs 48 V mit je 2,4 kWh parallel. 
Die Pylontechs gibt es schon lange (erste Versionen seit 2016) und sie sind gut dokumentiert. Bei Markteinführung 2016 hießen die Modelle US200B oder US2000 Plus. Der Name wurde 2019 zu US2000 geändert. Etwa 2022 wurde die aktuelle Serie US2000C eingeführt, die bessere Kommunikation, Softstart und einen Anschlusskontakt zum Fernstart bietet. Die Bezeichnung "US2000" oder "US2000C" steht vorn groß drauf.

Die Batterieeinheiten werden übereinander in den Schrank geschoben und vorn mit vier Schrauben befestigt. Die Masterbatterie, meist die unterste, steuert die übrigen. Sie ist mit den ankommenden Batteriekabeln und dem Datenkabel mit dem WR verbunden. Bei Mischbestückung sollte sie die aus der neueste Modellreihe sein. 
In den Hycube-Würfel passen theoretisch 7 Batterien.

## 1. Pylontech-Batterien auslesen mit Konsolen-Kabel und BatteryView
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

## 2. Pylontech-Batterien Firmware updaten mit UpdateTool
Zusätzlich sollte man jetzt einmal die neueste Firmware aufspielen. Pylontech veröffentlich keine Beschreibungen, was in der Firmware geändert wurde, aber man kann davon ausgehen, dass sie in der Zwischenzeit Fehler bei den neuen Chips (2021) korrigiert haben. Es wird allgemein empfohlen, das UpdateTool (vorhandene Version v1.0.10_3) zum aktualisieren der Firmware zu benutzen, nicht BatteryView. 
Während der Chipkrise wurden in US2000C andere Chips verbaut (erkennbar an E3 oder C3 in der Mitte der Seriennummer), die eine andere Firmware benötigen. Es wird deshalb empfohlen, die unentpackte ZIP-Datei zum Flashen zu benutzen. Das Tool sucht sich die richtige Datei darin selbst. Aktuelle [Firmware](https://www.effekta.com/download/firmwareupdate-fuer-us2000c-3000c/) und das Programm zum Aufspielen gibt es auf der Seite von EFFEKTA.com. 

## 3. Pylontech-Batterie aufladen mit Labornetzteil
Wenn der Hycube-Controller aus ist, kann man dem Wechselrichter nicht den Befehl geben, die Batterien aus dem Netz zu laden. Man sollte dann erstmal herausfinden, warum der Controller nicht funktioniert und ob etwas kaputt ist.

Pylontech schreibt in der Bedienungsanleitung: "2) Bei längerer Lagerung der Batterie muss diese alle sechs Monate aufgeladen werden und es muss sichergestellt sein, dass der Ladungszustand nicht weniger als 90% beträgt. 3) Nach vollständiger Entladung muss die Batterie innerhalb von 12 Stunden wieder aufgeladen werden."

Für alle Anleitungen gilt: Wenn ihr komplette Elektro-Muggel seid, fragt jemanden, der sich wirklich damit auskennt und lasst den das machen. Also zum Beispiel einen Elektriker, nicht ChatGPT.

Die einzige mir bekannte Methode ist, die Pylontech-Batterien einzeln von extern laden, zum Beispiel mit einem DC-Labornetzteil 60 Volt (mindestens 5 Ampere). Kostet bei Amazon ab 65 €. Wie es geht, wird in diesem Video beschrieben: https://www.youtube.com/watch?v=4K3RAzwkvss

Alle Batterien trennen (Kabel abziehen), eine Batterie an Plus und Minus des Netzteils anschließen, 52 V bei 5 A einstellen und lange warten. Der Strom fällt immer weiter, bis die Batterie fast voll ist. Bei 52 V sind die Batterien nicht 100% voll (die offizielle Ladespannung beträgt 53,5 V), aber es ist sicher und reicht, dass die Zellen wieder ausbalanciert werden (min. 92% SoC). Den Vorgang für jede Batterie wiederholen und hinterher alle Batterien miteinander verbinden und sich gemeinsam ausbalancieren lassen. Wird nochmal lange dauern, aber dann sind alle wieder fit.
Man kann das noch perfektionieren, indem man beispielsweise die Ladespannung in kleinen Schritten von 0,2 V bis zum Höchstwert von 53 V erhöht, immer wenn der Ladestrom unter 1 A fällt. Ich bin nicht sicher, ob das den Aufwand lohnt, auch weil man hinterher immer auch die Batterien sich untereinander balancen lassen muss, aber es gibt Leute, die schwören darauf. 

Ich würde keine Batterie anfassen, ohne sie vorher per Konsolenkabel und BatteryView auf Fehler zu untersuchen. Siehe oben. Hinterher kann man hoffentlich sehen, dass die 15 Zellspannungen in einer Batterie ziemlich gleich sind (Unterschied unter 1%).

Balancing bei voller Ladung ist übrigens von Pylontech vorgeschrieben, wenn man neue Batterien zu alten hinzufügen will. Dabei kann man das Laden aber im Gerät machen.
Ich würde das auch immer machen, wenn die Batterien lange halbleer ausgeschaltet gestanden haben.

## 4. Das Problem mit dem "Aufblähen"

_Ich bin kein Batterieexperte. Hier steht, was ich mir aus vielen Threads, Videos und Kommentaren zusammen gereimt habe. Falls hier ein echter Experte vorbeischaut, würde ich mich über Feedback freuen._
 
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

## 5. Hardware
Wer einmal risikofrei in die Pylontech-Batterien hineinsehen will, wie das BMS aussieht, dem sei das [YouTube-Video von José Faria](https://www.youtube.com/watch?v=BYKeGvza1OM) empfohlen.
