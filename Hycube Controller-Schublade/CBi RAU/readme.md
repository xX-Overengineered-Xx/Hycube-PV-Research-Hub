## Ersatz für CBi-Schalter

Die Fernbetätigungseinheit (RAU) ist seitlich an einen Leistungsschalter angeflanscht. Sie ermöglicht das ferngesteuerte Trennen und Schliessen des Plus-Kabels zwischen Wechselrichter und Batterie. 

<img src="https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/blob/main/Hycube%20Controller-Schublade/CBi%20RAU/CBi%20Seite.JPG" width="40%">
<img src="https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/blob/main/Hycube%20Controller-Schublade/CBi%20RAU/CBi%20vorn.JPG" width="40%">
<img src="https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/blob/main/Hycube%20Controller-Schublade/CBi%20RAU/CBi%20oben.JPG" width="40%">

Eingebaut ist der Schalter ganz links in der 'Schublade'.

<img src="https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/blob/main/Hycube%20Controller-Schublade/CBi%20RAU/CBi%20eingebaut.jpg" width="40%">

CBi International hat auf Anfrage mitgeteilt, dass sie nicht an Privatleute liefern, sondern nur an Großhändler oder die Industrie. Ihr Großhändler für Europa ist [emcomp.se](https://www.emcomp.se/products/cbi-circuit-breakers/cbi-front-mounted-rear-connected-mcbs-cbes/rau-remote-controlled-mcb-05-300a-for-ac-and-dc-applications/). Man könnte versuchen, dort eine Sammelbestellung zu organisieren, aber - siehe nächster Abschnitt. 

### Überhaupt nötig?
So richtig verstehe ich noch nicht, warum man die Leitung zur Batterie noch extra trennen muss. Ich vermute, Hycube hat das Teil eingebaut, "weil es das konnte" und um wirklich alle möglichen anderen Batterien verbaut zu können.  

Pylontech schreibt "Zum Schutz des Systems sollte zwischen der Batteriebank und dem Wechselrichter ein Leitungsschutzschalter zwischengeschaltet werden." (Handbuch US2000C v1.4, Seite 35). Die Gefahr geht von der Batterie aus, die bei Kurzschluss sehr hohe Ströme erzeugen kann (einige tausend Ampere). Wenn am Wechselrichter ein Kurzschluss auftritt und die interne Absicherung der Batterie (400 A) versagt, könnten die Kabel zum Wechselrichter schmelzen oder abreißen und Schäden verursachen. Es wird also ein Sicherungselement benötigt, das bei zu hohen Strömen die Plusleitung zwischen Batterien und WR trennt.

### Sicherungsautomat oder Sicherung?
Die Ein- und Abschaltfunktion (u.a. im Touchscreen des Hycube-Controllers) entfällt auf jeden Fall, da es keinen vergleichbaren fernbedienbaren Leistungsschalter am Markt gibt. Man kann als Ersatz einen normalen Leistungsschalter einbauen oder eine Sicherung. 
Ein geeigneter Leistungsschalter wäre z.B. ein Heschen HSM1PV-125 (ab 27 €). 
Der "Offgridtec MEGA-Fuse Sicherung Halter" hat den Vorteil, dass er Schraubanschlüsse hat, die genau zu den vorhandenen M8-Kabelschuhen passen. Er hat auch ein geschlossenes Gehäuse. Bei den dazu gehörigen MEGA-Sicherungen benötigt man die 58 V-Variante.

<img src="https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/blob/main/Hycube%20Controller-Schublade/CBi%20RAU/MEGA-Sicherungshalter.jpg" width="30%">

### Bemessung der Sicherung
Die Bemessung der Absicherung kann man aus dem Entladestrom der Batterien berechnen. Dieser ist bei Hycube durch das CBi begrenzt, das bei allen Batteriezahlen gleich ist. 

Die Entladeleistung beträgt laut Hycube-Datenblatt bei ein bis vier Batterien 1200 W pro Batterie. (48 V DC. 1 Batterie: 25 A, zwei 50 A, drei 75 A, vier 100 A). Das ist auch der Dauer-Entladestrom der Pylontechs. Bei fünf und sechs Batterien ist die Entladeleistung von Hycube auf 4800 W (100 A) begrenzt, aber es gibt eine maximale Entladeleistung je nach Temperatur von 6000 W (125 A). Die Begrenzung kommt auch vom Wechselrichter, der Sermatec-WR kann dauerhaft 5000 W (AC!) und kurzzeitig 120% Überlast (6000 W AC) für 5 Minuten..
125 A ist der Nennstrom des CBi RAU. Überlastauslösung bei 156 A, das ist genau 125%.

Bei Sicherungen und Sicherungsautomaten ist immer der Nennstrom (Betriebsstrom) angegeben. Für ein bis vier Batterien könnte man einen niedrigeren Wert als die 125 A des CBi benutzen. Die Auslegung für Batterien ist aber recht unkritisch, weil der Kurzschlussstrom so extrem hoch ist.
