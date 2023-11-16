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
