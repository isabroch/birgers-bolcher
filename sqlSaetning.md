# Øvelse 2

### 2.1	Udskriv alle informationer om alle bolcher.
```sql
SELECT *
FROM `bolche_old`
```

### 2.2	Find og udskriv navnene på alle de røde bolcher.
```sql
SELECT `name`
FROM `bolche_old`
WHERE `color` = 'Rød'
```

### 2.3	Find og udskriv navnene på alle de røde og de blå bolcher, i samme SQL udtræk.
```sql
SELECT `name`
FROM `bolche_old`
WHERE `color` IN ('Rød','Blå')
```

### 2.4	Find og udskriv navnene på alle bolcher, der ikke er røde, sorteret alfabetisk.
```sql
SELECT `name`
FROM `bolche_old`
WHERE `color` != 'Rød'
ORDER BY `name`
```

### 2.5	Find og udskriv navnene på alle bolcher som starter med et “B”.
```sql
SELECT `name`
FROM `bolche_old`
WHERE `name` LIKE 'B%'
```

### 2.6	Find og udskriv navene på alle bolcher, hvor der i navnet findes mindst ét “e”.
```sql
SELECT `name`
FROM `bolche_old`
WHERE `name` LIKE '%e%'
```

### 2.7	Find og udskriv navn og vægt på alle bolcher der vejer mindre end 10 gram, sorter stigende efter vægt.
```sql
SELECT `name`, `weight`
FROM `bolche_old`
WHERE `weight` < 10
ORDER BY `weight`
```

### 2.8	Find og udskriv navne på alle bolcher, der vejer mellem 10 og 12 gram (begge tal inklusiv), sorteret alfabetisk og derefter vægt.
```sql
SELECT `name`
FROM `bolche_old`
WHERE `weight` BETWEEN 10 AND 12
ORDER BY `name`, `weight`
```

### 2.9	Find og udskriv de tre største (tungeste) bolcher.
```sql
SELECT *
FROM `bolche_old`
ORDER BY `weight` DESC
LIMIT 3
```

### 2.10 Udskriv alle informationer om et tilfældigt bolche, udvalgt af systemet (sql).
```sql
SELECT *
FROM `bolche_old`
ORDER BY RAND()
LIMIT 1
```


# Øvelse 4

### 4.1	Udskriv alle informationer om alle bolcher.
```sql
SELECT
    `id`,
    `name`,
    `weight`,
    `price`,
    bolche_color.color_value AS color,
    bolche_taste_type.taste_type_value AS taste_type,
    bolche_taste_strength.taste_strength_value AS taste_strength,
    bolche_taste_sourness.taste_sourness_value AS taste_sourness
FROM
    `bolche`
JOIN bolche_color ON bolche.FK_color_id = bolche_color.color_id
JOIN bolche_taste_sourness ON bolche.FK_taste_sourness_id = bolche_taste_sourness.taste_sourness_id
JOIN bolche_taste_strength ON bolche.FK_taste_strength_id = bolche_taste_strength.taste_strength_id
JOIN bolche_taste_type ON bolche.FK_taste_type_id = bolche_taste_type.taste_type_id
```

### 4.2	Find og udskriv navnene på alle de røde bolcher.
```sql
SELECT NAME
FROM
    `bolche`
JOIN bolche_color ON bolche.FK_color_id = bolche_color.color_id
WHERE
    color_value = 'Rød'
```

### 4.3	Find og udskriv navnene på alle de røde og de blå bolcher, i samme SQL udtræk.
```sql
SELECT NAME
FROM
    `bolche`
JOIN bolche_color ON bolche.FK_color_id = bolche_color.color_id
WHERE
    color_value IN ('Rød','Blå')
```

### 4.4	Find og udskriv navnene på alle bolcher, der ikke er røde, sorteret alfabetisk.
```sql
SELECT NAME
FROM
    `bolche`
JOIN bolche_color ON bolche.FK_color_id = bolche_color.color_id
WHERE
    color_value != 'Rød'
ORDER BY `name`
```

### 4.5	Find og udskriv navnene på alle bolcher som starter med et “B”.
```sql
SELECT `name`
FROM `bolche`
WHERE `name` LIKE 'B%'
```

### 4.6	Find og udskriv navene på alle bolcher, hvor der i navnet findes mindst ét “e”.
```sql
SELECT `name`
FROM `bolche`
WHERE `name` LIKE '%e%'
```

### 4.7	Find og udskriv navn og vægt på alle bolcher der vejer mindre end 10 gram, sorter stigende efter vægt.
```sql
SELECT `name`, `weight`
FROM `bolche`
WHERE `weight` < 10
ORDER BY `weight`
```

### 4.8	Find og udskriv navne på alle bolcher, der vejer mellem 10 og 13 gram (begge tal inklusiv), sorteret alfabetisk og derefter vægt.
```sql
SELECT `name`
FROM `bolche`
WHERE `weight` BETWEEN 10 AND 13
ORDER BY `name`, `weight`
```

### 4.9	Find og udskriv de tre største (tungeste) bolcher.
```sql
SELECT
    `id`,
    `name`,
    `weight`,
    `price`,
    bolche_color.color_value AS color,
    bolche_taste_type.taste_type_value AS taste_type,
    bolche_taste_strength.taste_strength_value AS taste_strength,
    bolche_taste_sourness.taste_sourness_value AS taste_sourness
FROM
    `bolche`
JOIN bolche_color ON bolche.FK_color_id = bolche_color.color_id
JOIN bolche_taste_sourness ON bolche.FK_taste_sourness_id = bolche_taste_sourness.taste_sourness_id
JOIN bolche_taste_strength ON bolche.FK_taste_strength_id = bolche_taste_strength.taste_strength_id
JOIN bolche_taste_type ON bolche.FK_taste_type_id = bolche_taste_type.taste_type_id
ORDER BY `weight` DESC
LIMIT 3
```

### 4.10 Udskriv alle informationer om et tilfældigt bolche, udvalgt af systemet (sql).
```sql
SELECT
    `id`,
    `name`,
    `weight`,
    `price`,
    bolche_color.color_value AS color,
    bolche_taste_type.taste_type_value AS taste_type,
    bolche_taste_strength.taste_strength_value AS taste_strength,
    bolche_taste_sourness.taste_sourness_value AS taste_sourness
FROM
    `bolche`
JOIN bolche_color ON bolche.FK_color_id = bolche_color.color_id
JOIN bolche_taste_sourness ON bolche.FK_taste_sourness_id = bolche_taste_sourness.taste_sourness_id
JOIN bolche_taste_strength ON bolche.FK_taste_strength_id = bolche_taste_strength.taste_strength_id
JOIN bolche_taste_type ON bolche.FK_taste_type_id = bolche_taste_type.taste_type_id
ORDER BY RAND()
LIMIT 1
```


# Øvelse 5
### 5.1	Udskriv en prisliste med bolchenavn og kilopris henholdsvis med og uden moms
```sql
SELECT
    `name`,
    `weight` AS `weight (g)`,
    ROUND(price / 100, 2) AS `production price (kr)`,
    ROUND(price * 3.5 / 100, 2) AS `net price (kr)`,
    ROUND(
        price * 3.5 / weight * 1000 / 100,
        2
    ) AS `net price/kg u. moms (kr)`,
    ROUND(
        price * 3.5 / weight * 1000 / 100 * 1.25,
        2
    ) AS `net price/kg m. moms (kr)`
FROM
    `bolche`
```

# Øvelse 6
### 6.2	Løs opgave 2.4 ved brug af NOT IN
```sql
SELECT `name`
FROM `bolche_old`
WHERE `color` NOT IN ('Rød')
ORDER BY `name`
```

### 6.3	Udskriv hvor mange bolscher der vejer under 15 g.
```sql
SELECT COUNT(*) AS `Bolche under 15g` FROM bolche WHERE weight < 15
```

### 6.4	Udskriv hvor mange forskellige bolcher der er i tabellen
```sql
SELECT COUNT(*) AS `Unique Products` FROM bolche
```

### 6.5	Udskriv gennemsnitsprisen per bolche
```sql
SELECT ROUND(SUM(price) / COUNT(*)) as `Average Price` FROM bolche
```

### 6.6	Udskriv navn og pris på det dyreste og billigste bolche
```sql
SELECT
(SELECT CONCAT(`name`, ": ", price, " kr") FROM bolche ORDER BY price ASC LIMIT 1) AS `Cheapest`,
(SELECT CONCAT(`name`, ": ", price, " kr") FROM bolche ORDER BY price DESC LIMIT 1) AS `Most Expensive`
```

or

```sql
(SELECT name, price FROM `bolche` ORDER BY price ASC LIMIT 1)
UNION
(SELECT name, price FROM `bolche` ORDER BY price DESC LIMIT 1)
```