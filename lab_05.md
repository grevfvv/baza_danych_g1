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
