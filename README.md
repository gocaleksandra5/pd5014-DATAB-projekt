# Projekt końcowy – Relacyjne bazy danych

## Wyniki zapytań SQL

### Zapytanie 4 II

**Testy, w których uczestniczyło więcej niż 30 pacjentów**

```sql
SELECT 
    t.test_type,
    COUNT(DISTINCT pt.patient_id) AS num_patients
FROM tests t
JOIN patient_test pt ON t.test_id = pt.test_id
GROUP BY t.test_type
HAVING COUNT (DISTINCT pt.patient_id) > 30;
```

**Wynik:**

| test_type | num_patients |
| --------- | ------------ |
| NGS-panel | 38           |
| SNP Array | 39           |

---




### Zapytanie 4 III

**Średnia liczba wariantów dla każdego typu testu**

```sql
SELECT 
    sub.test_type,
    AVG(sub.variant_count) AS avg_variants
FROM (
    SELECT 
        t.test_id,
        t.test_type,
        COUNT(r.result_id) AS variant_count
    FROM tests t
    LEFT JOIN results r ON t.test_id = r.test_id
    GROUP BY t.test_id, t.test_type
) sub
GROUP BY sub.test_type;
```

**Wynik**

| test_type    | avg_variants |
| ------------ | ------------ |
| SNP Array    | 3,0000       |
| NGS-panel    | 3,5833       |
| WES          | 3,4286       |
| WGS          | 3,4828       |

---
