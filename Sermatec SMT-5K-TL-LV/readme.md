# Wechselrichter Hycube HY-5K-TL-LV

Das ist ein umgelabelter Sermatec SMT-5KT-LV, der auf der Rückseite des Cube mit Vorderseite nach innen und Kühlrippen nach außen montiert wurde. Dadurch kann man die Status-LEDs nicht sehen.

Hier sieht man den weißen Wechselrichter noch ganz gut, bevor die Batterien eingebaut werden:
<img src="https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/blob/main/hycube%20e_Compact%20ohne%20Batterien.jpg" width="60%">

Der WR kann etwa 5 kW, deshalb ist die Entladeleistung selbst bei den großen Batteriesätzen auf 4,8 kW begrenzt. Die Einspeiseleistung ist wegen der Schieflastgrenze auf 4600 VA begrenzt, ebenso wie für den zusätzlichen WR an der Wand. Das bedeutet, dass die ungewöhnliche "1+1-phasige" Anlage von Hycube nie mehr als 9,2 kW einspeisen kann (Leistungsfaktor 1,0), egal wie viele PV-Panels man hat.

Der Wechselrichter baut ein eigenes WLAN mit dem Namen "ST000921…" mit kurzer Reichweite auf. Zum Auslesen einiger Daten kann man auf einem Mobiltelefon die Sermatec-App installieren und sich mit diesem WLAN verbinden (Passwort ist gsstes123456). Man muss aber ziemlich dicht daneben stehen. Wer mehr Reichweite braucht, schliesst an den Antennenanschluss (SMA) eine WLAN-Antenne an. Gegen Sicherheitsbedenken hilft eine abschirmende Verschlusskappe aus Metall.

Nach dem Start der App nicht anmelden, sondern ganz unten "lokal verwenden" (oder so). Die App zeigt auch Fehlermeldungen, falls es welche gibt. 
Die App erlaubt auch Cloud-Zugriff. Vielleicht gibt es hier die Möglichkeit, direkt über Sermatec zu gehen und Zugriff auf den Wechselrichter von unterwegs zu erhalten...

Ob der WR von Sermatec für Hycube mit geänderter Firmware versehen wurde oder man intern die direkte Batterienutzung freischalten kann, ist aktuell nicht klar. Im ersten Fall wäre eine originale Firmware von Sermatec eine Lösung. Die hat bisher noch niemand gespendet.

Ersatz: Sermatec baut inzwischen keine Wechselrichter mehr für den Consumer-Bereich, deshalb hat Hycube bei den Tri.aktiv-Geräten auf IMEON gewechselt. Allerdings sind solch kleine (5 kW) Hybridwechselrichter vergleichsweise teuer. Man sollte überlegen, ob man nicht einen so großen WR beschafft, dass er alle PV-Panels bedienen kann. Damit entfällt der zweite externe WR und im Winter steht die gesamte PV-Leistung der Batterie zur Verfügung.
Wichtig sollte sein, dass ein neuer WR auf der Kompatibilitätsliste von Pylontech steht, damit er die Batterien direkt ansprechen kann. Falls man das System mit eigenem statt Hycube-Controller betreiben will/muss ist die Kompatibilität egal, weil der Controller zwischen WR und Batterie kommunizieren kann.

Falls jemand mal reinsehen möchte: [Innenansicht](https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/tree/main/Sermatec%20SMT-5K-TL-LV/Innenansicht)

Siehe auch: https://github.com/sermatec-opensource
