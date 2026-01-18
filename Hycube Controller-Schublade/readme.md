# Hycube Controller-Schublade
Dies ist der interessanteste Teil, denn die anderen Komponenten sind recht gut dokumentiert, wenn man ihren Namen kennt.

Der zentrale Controller ist ein [Chipsee EPC-A8-50-C](https://chipsee.com/product/epca8050c/) Minicomputer ("Controller") mit farbigem 5 Zoll-Display mit Touchscreen. Das ist die flache Kunststoffkiste hinter dem Touchscreen rechts. Darauf läuft ein Embedded-Linux-Betriebssystem auf einem ARM Cortex-A8. 
Links auf der Oberseite ist ein Slot für eine microSD-Karte. Auf der Karte ist das Betriebssystem und alle bisherigen Verlaufsdaten, tagesgenau in SQL-Dateien. Über Ethernet-Kabel stellt der Controller auch den Webserver für die Hycube.local-Oberfläche im lokalen LAN-Netzwerk (in jedem Webbrowser).

Weitere Komponenten
Hinten ganz links zwei Verteilerblöcke Contaclip 27202.0 für Plus und Minus 48 V.

Links davor fernbedienbarer Leistungsschalter (Remote Actuator Unit = RAU) von CBi D-5AAMX2VASK125KXA-XXXXXBDVAX3-X Re-order no: D5AKXA0001. 

Hinten links DC/DC-Wandler Traco Power TCL 060-124 DC (18-75 V auf 24 V), 
davor USB-Hub 1 auf 4,
davon Finder Installationsschütz 22.32.0.230.4440
In der Mitte ein USB-Relaisboard von Denkovi.

Rechts vorn Stromstoßschalter Finder 20.21.9.024.4000. Dies ist ein bistabiles Relais, das die Spannungsversorgung für den Controller ein- oder ausschalten kann. Betätigt von Versorgungsspannung 48 V von Batterien oder vom weißen Taster vorn rechts.
