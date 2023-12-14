## Zadanie 1

### 1
```sql
SELECT AVG(waga), as srednia_waga
FROM kreatura
WHERE rodzaj='wiking';
```

### 2
```sql
SELECT AVG(waga) AS srednia_waga, rodzaj, COUNT(rodzaj) as ilosc
FROM kreatura
GROUP BY rodzaj;
```

### 3
```sql
SELECT AVG(YEAR(dataUr)) as sredni_wiek, rodzaj
FROM kreatur
GROUP BY rodzaj;
```

## Zadanie 2

### 1
```sql
SELECT SUM(waga*ilosc) as suma_wag, rodzaj
FROM zasob
GROUP BY rodzaj;
```

### 2
```sql
SELECT nazwa, AVG(waga*ilosc) as srednia_waga
FROM zasob
WHERE ilosc >= 4
GROUP BY nazwa HAVING srednia_waga > 10;
```

### 3
```sql
SELECT rodzaj, COUNT(DISTINCT(nazwa)) as nazwy
FROM zasob
GROUP BY rodzaj HAVING min(ilosc) > 1;
```

## Zadanie 3

### 1

```sql
SELECT k.nazwa, SUM(e.ilosc) as niesione_rzeczy
FROM kreatura k, ekwipunek e
WHERE k.idKreatury=e.idKreatury
GROUP BY k.nazwa;
```

### 2
```sql
SELECT k.nazwa, z.nazwa FROM kreatura k
JOIN ekwipunek e ON k.idKreatury=e.idKreatury
JOIN zasob z ON e.idZasobu=z.idZasobu;
```

### 3
```sql
SELECT * FROM kreatura k
LEFT JOIN ekwipunek e ON k.idKreatury=e.idKreatury
WHERE e.idKreatury IS NULL;

```

## Zadanie 4

### 1
```sql
SELECT k.dataUr, k.nazwa, z.nazwa FROM kreatura k
INNER JOIN ekwipunek e on k.idKreatury=e.idKreatury
INNER JOIN zasob z on e.idZasobu=z.idZasobu
WHERE YEAR(k.dataUr) BETWEEN 1670 AND 1679
AND k.rodzaj = 'wiking';
```

### 2
```sql
SELECT * FROM kreatura k
INNER JOIN ekwipunek e on k.idKreatury=e.idKreatury
INNER JOIN zasob z on e.idZasobu=z.idZasobu
WHERE z.rodzaj='jedzenie'
ORDER BY k.dataUr DESC
LIMIT 5;
```

### 3
```sql
SELECT CONCAT(k1.nazwa, ' - ', k2.nazwa) as kreatury
FROM kreatura k1
INNER JOIN kreatura k2 ON
k1.idKreatury-k2.idKreatury=5;
```

## Zadanie 5

### 1

```sql
SELECT k.rodzaj, AVG(e.ilosc * z.waga) FROM kreatura k
INNER JOIN ekwipunek e on k.idKreatury=e.idKreatury
INNERJ OIN zasob z on e.idZasobu=z.idZasobu
WHERE k.rodzaj NOT IN('malpka', 'waz') 
AND e.ilosc < 30;
```

### 2

```sql
SELECT n.najstarsza, n.najmlodszka FROM
(
SELECT rodzaj, min(dataUr) najstarsza, max(dataUr) najmlodszka
FROM kreatura
GROUP BY rodzaj
) n, kretaura k;
WHERE n.najstarsza=k.dataUr
OR n.najmlodszka=k.dataUr;
```
