## Zadanie 1

### 2
```sql
SELECT * FROM kreatura k
LEFT JOIN uczestnicy u ON k.idKreatury=u.id_uczestnika
LEFT JOIN wyprawa w ON w.id_wyprawy=u.id_wyprawy
WHERE u.id_uczestnika IS NULL;
```

### 3
```sql
SELECT w.nazwa, SUM(z.waga * z.ilosc) FROM wyprawa w
INNER JOIN kreatura k ON k.idKreatury=w.kierownik
INNER JOIN ekwipunek e ON e.idKreatury=k.idKreatury
INNER JOIN zasob z ON z.idZasobu=e.idZasobu
GROUP BY w.nazwa;

SELECT * FROM wyprawa w
INNER JOIN uczestnicy u on w.id_wyprawy=u.id_wyprawy
INNER JOIN kreatura k ON k.idKreatury=w.kierownik
INNER JOIN ekwipunek e ON e.idKreatury=k.idKreatury
INNER JOIN zasob z ON z.idZasobu=e.idZasobu; (nie dokonczone)

```

## Zadanie 2

### 2
```sql
SELECT ew.sektor, s.nazwa, ew.kolejnosc, w.data_rozpoczecia
FROM etapy_wyprawy ew
INNER JOIN sektor s ON ew.sektor=s.id_sektora
INNER JOIN wyprawa w ON w.id_wyprawy=ew.idWyprawy
INNER JOIN kreatura k ON k.idKreatur=w.kierownik
ORDER BY w.data_rozpoczecia ASC, ew.kolejnosc ASC;
```

### Zadanie 3

### 1

```sql
SELECT s.nazwa, IFNULL(COUNT(ew.sektor), 0)
FROM sektor s
LEFT JOIN etapy_wyprawy ew ON s.id_sektora=ew.sektor
GROUP BY s.nazwa;
```

### 2

```sql
SELECT k.nazwa, IF(COUNT(u.id_uczestnika), 'bral udzial w wyprawie', 'nie bral udzialu w wyprawie')
FROM uczestnicy u
RIGHT JOIN kreatura k ON k.idKreatury=u.id_uczestnika
GROUP BY k.nazwa;
```

##

```sql
SELECT k.nazwa, DATEDIFF(w.data_rozpoczecia, k.dataUr) as wiek_w_dniach 
FROM kreatura k
INNER JOIN uczestnicy u ON u.id_uczestnika=k.idKreatury 
INNER JOIN wyprawa w ON u.id_wyprawy=w.id_wyprawy 
INNER JOIN etapy_wyprawy ew ON ew.idWyprawy=w.id_wyprawy
WHERE ew.sektor=7
GROUP BY k.nazwa, k.idKreatury;
```
