Im Controller steckt eine Micro SD-Karte mit zwei Linux-Partitionen (1. Booot, 2. Programme und Daten).

Historische Daten:
- Die historischen Daten liegen als gepackte SQLite-Datenbank auf der zweiten Partition vor (*.gz)
- Pfade:
    root/database_hycube-xxxx_YYYYMMDD-HHMM_KDB.sql3db.gz   (xxxx=Anlagennummer; HHMM ist meistens 2359=23:59Uhr)
    root/hycube-xxxx/YYYY/  (xxxx=Anlagennummer; YYYY=Jahr)
    
- pro Jahr kommen ca. 120MByte an Daten zusammen (bei der Standard 16GB-Karte reicht das für über 100Jahre)

