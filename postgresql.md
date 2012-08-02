# Memo PostgreSQL

## lister les bases de données
```
psql -l
\l
```

Changer de base dans psql
```
\connect autre-base
```

## Commandes psql de base

```
\l = liste des bases
\d = liste des tables
\q = quitter
\h = aide
SELECT version(); = version PostgreSQL
SELECT current_date; = date actuelle
\i fichier.sql = lit les instructions du fichier fichier.sql
\d table = décrit une table (comme DESCRIBE avec MySQL)
```

## Manipulation des tables
```
CREATE TABLE ma_table (col1 type, [...], coln type);
DROP TABLE ma_table;

CREATE TABLE weather (
    city            varchar(80),
    temp_lo         int,           -- low temperature
    temp_hi         int,           -- high temperature
    prcp            real,          -- precipitation
    date            date
);

Rq : deux tirets -- introduisent des commentaires...
```

Pour effacer toutes les données d'une table :

```
DELETE FROM weather;
```

## INSERT

```
INSERT INTO weather VALUES ('San Francisco', 46, 50, 0.25, '1994-11-27');
INSERT INTO weather (city, temp_lo, temp_hi, prcp, date)
    VALUES ('San Francisco', 43, 57, 0.0, '1994-11-29');
COPY weather FROM '/home/user/weather.txt';
```

## SELECT
```
SELECT * FROM weather;
SELECT city, (temp_hi+temp_lo)/2 AS temp_avg, date FROM weather;
SELECT * FROM weatherWHERE city = 'San Francisco' AND prcp > 0.0;
SELECT DISTINCT city FROM weather ORDER BY city;
```

Avec des jointures :

```
SELECT * FROM weather, cities WHERE city = name;
SELECT weather.city, weather.temp_lo, cities.location 
FROM weather, cities WHERE cities.name = weather.city;
SELECT * FROM weather INNER JOIN cities ON (weather.city = cities.name);
SELECT * FROM weather LEFT OUTER JOIN cities ON 
(weather.city = cities.name);
SELECT * FROM weather w, cities c WHERE w.city = c.name;
```

Avec des fonctions (Aggregate Functions) :

```
SELECT max(temp_lo) FROM weather;
```

Attention, les "Aggregate Functions" ne peuvent être utilsées dans la clause WHERE
Ainsi la requête suivante est fausse :

```
SELECT city FROM weather WHERE temp_lo = max(temp_lo);
```

On devra donc faire :

```
SELECT city FROM weather WHERE temp_lo = (SELECT max(temp_lo) FROM weather);
```

## UPDATE
```
UPDATE weather SET temp_hi = temp_hi - 2, temp_lo = temp_lo - 2 WHERE date > '1994-11-28';
```

## DELETE
```
DELETE FROM weather WHERE city = 'Hayward';
```

## SAUVEGARDES

```
$ pg_dump NOM_BASE > NOM_FICHIER
$ pg_dumpall > NOM_FICHIER
```

Pour restaurer une base de données :

```
$ createdb newbase
psql newbase < NOM_FICHIER
```
