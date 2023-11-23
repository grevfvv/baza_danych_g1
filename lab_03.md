```sql
CREATE TABLE postac (
id INT PRIMARY KEY AUTO_INCREMENT,
nazwa VARCHAR(40),
rodzaj enum("wiking", "ptak", "kobieta"),
data_ur DATE,
wiek int unsigned);
```

```sql
INSERT INTO postac VALUES(default, 'Bjorn', 'wiking', '1700-11-09', 323);
```

```sql
UPDATE postac SET nazwa='Tesciowa' WHERE nazwa='Tesciowo';
```

```sql
CREATE TABLE walizka (
    id INT PRIMARY KEY AUTO_INCREMENT,
    pojemnosc INT UNSIGNED,
    kolor enum('rozowy', 'czerwony', 'teczowy', 'zolty'),
    id_wlasciciela int,
    FOREIGN KEY (id_wlasciciela) REFERENCES postac(id) ON DELETE CASCADE);
```

```sql
ALTER TABLE walizka ALTER kolor SET default 'rozowy';
```

```sql
SHOW CREATE TABLE tb
```

```sql
DESC tb
```

```sql
INSERT into walizka(pojemnosc, id_wlasciciela) VALUES(50, 3);
```

```sql
CREATE TABLE izba(
    adres_budynku VARCHAR(100),
    nazwa_izby VARCHAR(100),
    metraz int unsigned,
    wlasciciel int,
    PRIMARY KEY(adres_budynku, nazwa_izby),
    FOREIGN KEY(wlasciciel) REFERENCES postac(id) ON DELETE SET NULL);
```

```sql
CREATE TABLE `przetwory` (
    `id` int PRIMARY KEY AUTO_INCREMENT,
    `rok_produkcji` int DEFAULT,
    `id_wykonawcy` int DEFAULT,
    `zawartosc` varchar(40) DEFAULT,
    `dodatek` varchar(40) DEFAULT ('papryczka chilli'),
    `id_konsumenta` int DEFAULT,
    FOREIGN KEY(id_wykonawcy) REFERENCES postac(id),
    FOREIGN KEY(id_konsumenta) REFERENCES postac(id)
)
```

```sql
CREATE TABLE statek(
	nazwa_statku VARCHAR(40) PRIMARY KEY,
	rodzaj_statku enum('wioslowy', 'zaglowy', 'wojskowy'),
	data_wodowania SMALLINT,
	max_ladownosc INT UNSIGNED
)
```

```sql
ALTER TABLE postac ADD COLUMN funckja VARCHAR(40);
```

```sql
UPDATE postac SET funckja='kapitan' WHERE nazwa='Bjorn'
```

```sql
ALTER TABLE postac ADD COLUMN statek VARCHAR(40);
ALTER TABLE postac ADD FOREIGN KEY (statek) REFERENCES statek(nazwa_statku);
```

```sql
UPDATE postac SET statek='statek wojskowy' WHERE rodzaj="wiking" OR nazwa="Drozd";
```

```sql
DELETE FROM izba WHERE nazwa_izby="spizarnia";
```

```sql
DROP TABLE izba;
```

# lab 5
```sql
DELETE FROM postac WHERE nazwa != 'Bjorn' AND rodzaj='wiking' ORDER BY wiek DESC LIMIT 2;
```

### 1.b
```sql
ALTER TABLE walizka DROP FOREIGN KEY walizka_ibfk_1;
ALTER TABLE przetwory DROP FOREIGN KEY przetwory_ibfk_1;
ALTER TABLE przetwory DROP FOREIGN KEY przetwory_ibfk_2;

#usuniece auto_increment
ALTER TABLE postac MODIFY id INT;
 
ALTER TABLE postac drop PRIMARY KEY;
SHOW CREATE TABLE postac;
```

### zad 2
```sql
ALTER TABLE postac ADD COLUMN pesel CHAR(11) first;
UPDATE postac SET pesel='756753178' + id;
ALTER TABLE postac ADD PRIMARY KEY(pesel);
``

```sql
ALTER TABLE postac MODIFY rodzaj enum('wiking','ptak','kobieta','syrenka');
```

```sql
INSERT INTO postac VALUES ('1241512125', 'Gretruda Nieszczera', 'syrenka', '1690-11-6', 19, NULL, NULL, NULL);
```

```sql
SELECT nazwa FROM postac WHERE nazwa REGEXP '\a';
```

```sql
UPDATE statek SET max_ladownosc=max_ladownosc * 0.7 WHERE YEAR(data_wodowania) BETWEEN 1901 AND 2000;
```

```sql
ALTER TABLE postac ADD CHECK (wiek <= 1000);
```

```sql
CREATE TABLE marynarz LIKE postac;
```

```sql
INSERT INTO marynarz SELECT * FROM postac WHERE statek IS NOT NULL;
```

```sql
ALTER TABLE marynarz ADD FOREIGN KEY (statek) REFERENCES statek(nazwa_statku);
```

```sql
ALTER TABLE postac MODIFY rodzaj enum('wiking','ptak','kobieta','syrenka', 'waz');
```

```sql
INSERT INTO postac VALUES('1255125120', 'Loko', 'waz', '1120-01-01', 900, NULL, NULL, NULL);
```

### zad 5
```sql
UPDATE postac SET id_statku=NULL;
UPDATE marynarz SET id_statku=NULL;
UPDATE postac SET statek=NULL;
UPDATE marynarz SET statek=NULL;
```

```sql
DELETE FROM postac WHERE rodzaj='wiking' AND nazwa != 'Bjorn' LIMIT 1; 
```

```sql
DELETE FROM statek;
```

```sql
CREATE TABLE zwierz(
id INT PRIMARY KEY AUTO_INCREMENT,
nazwa VARCHAR(40),
wiek TINYINT UNSIGNED
)
```

```sql
INSERT INTO zwierz (nazwa, wiek) SELECT nazwa, wiek FROM postac WHERE rodzaj IN('ptak', 'waz');
```
