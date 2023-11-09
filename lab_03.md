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
