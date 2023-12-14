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

### Zadanie 2

