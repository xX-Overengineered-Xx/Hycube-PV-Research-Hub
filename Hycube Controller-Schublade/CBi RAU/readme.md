## Ersatz für CBi-Schalter

Die Fernbetätigungseinheit (RAU) ist seitlich an einen Leistungsschalter angeflanscht. Sie ermöglicht das ferngesteuerte Trennen und Schliessen des Plus-Kabels zwischen Wechselrichter und Batterie. 

<img src="https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/blob/main/Hycube%20Controller-Schublade/CBi%20RAU/CBi%20Seite.JPG" width="40%">
<img src="https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/blob/main/Hycube%20Controller-Schublade/CBi%20RAU/CBi%20vorn.JPG" width="40%">
<img src="https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/blob/main/Hycube%20Controller-Schublade/CBi%20RAU/CBi%20oben.JPG" width="40%">

Eingebaut ist der Schalter ganz links in der 'Schublade'.

<img src="https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/blob/main/Hycube%20Controller-Schublade/CBi%20RAU/CBi%20eingebaut.jpg" width="40%">

Für dieses Bauteil gibt es aktuell keine Einkaufsquelle und keinen Ersatz von einem anderen Hersteller.
So richtig klar ist mir aber nicht, warum man die Leitung zur Batterie noch extra trennen muss. Ich vermute, Hycube hat das Teil eingebaut, "weil des das konnte" und um wirklich alle möglichen anderen Batterien verbaut zu können.  

### Überhaupt nötig?
Pylontech schreibt "Zum Schutz des Systems sollte zwischen der Batteriebank und dem Wechselrichter ein Leitungsschutzschalter zwischengeschaltet werden." (Handuch US2000C v1.4, Seite 35). Die Gefahr geht von der Batterie aus, die bei Kurzschluss sehr höhe Ströme erzeugen kann (einige tausend Ampere). Wenn am Wechselrichter ein Kurzschluss auftritt und die interne Absicherung der Batterie (400 A) versagt, könnten die Kabel zum Wechselrichter schmelzen oder abreißen und Schäden verursachen. Es wird also ein Sicherungselement benötig, der bei zu hohen Strömen die Plusleitung zwischen Batterien und WR trennt.

### Sicherungsautomat oder Sicherung?
Die Schaltfunktion (u.a. im Touchscreen des Hycube-Controllers) entfällt auf jeden Fall, da es kein vergleichbares fernbedienbares Gerät am Markt gibt. Man kann als Ersatz einen Sicherungsautomaten einbauen oder eine Sicherung. 
Ein Sicherungsautomat würde gut auf die DIN-Hutschiene darunter passen, aber hat immer Schraubanschlüsse. Man müsste die vorhandenen Kabelschuhe abtrennen und Aderendhülsen (25 mm²) aufpressen.
Der "Offgridtec MEGA-Fuse Sicherung Halter" von Victron hat den Vorteil, dass er Schraubanschlüsse hat, die genau zu den vorhandenen M8-Kabelschuhen passen. Er hat auch ein geschlossenes Gehäuse. Bei den dazu gehörigen MEGA-Sicherungen benötigt man die 58 V-Variante.
Möglich wäre auch ein NH-Sicherungs-Lasttrenner 80 V DC, 1-polig schaltbar für Aufbaumontage ab 110 €. Falls er räumlich reinpasst.

### Bemessung der Sicherung
Die Bemessung der Absicherung kann man aus dem Entladestrom der Batterien berechnen. Dieser ist bei Hycube durch das CBi begrenzt, das bei allen Batteriezahlen gleich ist. 

Die Entladeleistung beträgt laut Hycube-Datenblatt bei ein bis vier Batterien 1200 W pro Batterie. (48 V DC. 1 Batterie: 25 A, zwei 50 A, drei 75 A, vier 100 A). Das ist auch der Dauer-Entladestrom der Pylontechs. Bei fünf und sechs Batterien ist die Entladeleistung von Hycube auf 4800 W (100 A) begrenzt, aber es gibt eine maximale Entladeleistung je nach Temperatur von 6000 W (125 A). Die Begrenzung kommt auch vom Wechselrichter, der Sermatec-WR kann dauerhaft 5000 W (AC!) und kurzzeitig 120% Überlast (6000 W AC) für 5 Minuten..
125 A ist der Nennstrom des CBi RAU. Überlastauslösung bei 156 A, das ist genau 125%.

Bei Sicherungen und Sicherungsautomaten ist immer der Nennstrom (Betriebsstrom) angegeben. Für ein bis vier Batterien könnte man einen niedrigeren Wert als die 125 A des CBi benutzen. Die Auslegung für Batterien ist aber recht unkritisch, weil der Kurzschlussstrom so extrem hoch ist.
