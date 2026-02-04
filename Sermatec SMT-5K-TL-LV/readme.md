# Wechselrichter Hycube HY-5K-TL-LV

Das ist ein umgelabelter Sermatec SMT-5KT-LV, der auf der Rückseite des Cube mit Vorderseite nach innen und Kühlrippen nach außen montiert wurde. Dadurch kann man die Status-LEDs nicht sehen.

Hier sieht man den Wechselrichter ohne Batterien noch ganz gut:
![](https://github.com/xX-Overengineered-Xx/Hycube-PV-Research-Hub/blob/main/hycube%20e_Compact%20ohne%20Batterien.jpg)
Der WR kann etwa 5 kW, deshalb ist die Entladeleistung selbst bei den großen Batteriesätzen auf 4,8 kW begrenzt.

Der Wechselrichter baut ein eigenes WLAN mit dem Namen "ST000921…" mit kurzer Reichweite auf. Zum Auslesen einiger Daten kann man auf einem Mobiltelefon die Sermatec-App installieren und sich mit diesem WLAN verbinden (Passwort ist gsstes123456). Man muss aber ziemlich dicht daneben stehen.

Nach dem Start der App nicht anmelden, sondern ganz unten "lokal verwenden" (oder so). Die App zeigt auch Fehlermeldungen, falls es welche gibt. 
Die App erlaubt auch Cloud-Zugriff. Vielleicht gibt es hier die Möglichkeit, direkt über Sermatec irgendwie zu gehen und Zugriff auf den Wechselrichter von unterwegs zu erhalten...

Ob der WR von Sermatec für Hycube mit geänderter Firmware versehen wurde oder man intern die direkte Batterienutzung freischalten kann, ist aktuell nicht klar. Im ersten Fall wäre eine originale Firmware von Sermatec eine Lösung. Die hat bisher noch niemand gespendet.

Ersatz: Sermatec baut inzwischen keine Wechselrichter mehr für den Consumer-Bereich, deshalb hat Hycube bei den Tri.aktiv-Geräten auf IMEON gewechselt. Das wäre eine Option, falls ein Sermatec kaputt geht. Wichtig sollte sein, dass ein neuer WR auf der Kompatibilitätsliste von Pylontech steht, damit er die Batterien direkt ansprechen kann, falls der Hycube-Controller mal kaputt geht. Victron macht viel mit Pylontech. Falls man das System mit eigenem statt Hycube-Controller betreiben will/muss ist die Kompatibilität egal, weil der Controller zwischen WR und Batterie kommunizieren kann. Dann muss man aber alles selbst programmieren.

Siehe auch: https://github.com/sermatec-opensource
