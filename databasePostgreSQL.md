# Лабораторная работа №1

1. С помощью комманды \dt
2. С помощью комманды help
3. Сначала стоит нам создать саму базу данных, в этом нам поможет комманда ```CREATE DATABASE```. <br>
Теперь приступим к созданию бд: <br>
```CREATE DATABASE passenger_air_tranportation;``` <br> 
Потом подключаемся к БД: <br>
```\c passenger_air_tranportation``` <br>
Теперь у нас есть база данных, но у нас нет таблиц airports. Чтобы создать ее, нам потребуется комманда ```CREATE TABLE```. Создадим  с некоторые параметрами: <br>
```
passenger_air_tranportation=# CREATE TABLE airport(
passenger_air_tranportation(# id SERIAL PRIMARY KEY,
passenger_air_tranportation(# Name VARCHAR(100),
passenger_air_tranportation(# Year DATE
passenger_air_tranportation(# );
```
Теперь можно отобразить таблицу через комманду ```SELECT * FROM airport```. <br>
4. Создать : ```CREATE TABLE``` <br>
5. Сгруппировать : ```GROUP BY``` <br>
6. Отсортировать : ```ORDER BY``` <br> 
7. Обновить : ```UPDATE``` <br>
8. Посчитать кол-во : ```COUNT``` <br>
9. Подключиться к базе данных demo с именем пользователя postgres: ```psql -d demo -U postgres``` <br>
10.  Таблица pilots
```
passenger_air_tranportation-# CREATE TABLE pilots (
passenger_air_tranportation(# first_name TEXT NOT NULL,
passenger_air_tranportation(# name TEXT NOT NULL,
passenger_air_tranportation(# last_name TEXT NOT NULL);
```
11.
```
passenger_air_tranportation=# ALTER TABLE pilots
passenger_air_tranportation-# ADD years_old INTEGER NOT NULL;
```
12.
```
passenger_air_tranportation=# INSERT INTO pilots (first_name, name, last_name, years_old)
passenger_air_tranportation-# VALUES ('Melnikov','Stepan','Ivanovich',52),
passenger_air_tranportation-# ('Okrugin','Nikita','Anatolyevich',22),
passenger_air_tranportation-# ('Ribkin','Kirill','jojobavich',61);
INSERT 0 3
passenger_air_tranportation=# SELECT * FROM pilots;
 first_name |  name  |  last_name   | years_old
------------+--------+--------------+-----------
 Ivanov     | Ivan   | Borisovich   |        29
 Melnikov   | Stepan | Ivanovich    |        52
 Okrugin    | Nikita | Anatolyevich |        22
 Ribkin     | Kirill | jojobavich   |        61
```
13.
```
passenger_air_tranportation=# ALTER TABLE pilots
passenger_air_tranportation-# RENAME TO pilots_hobbies;
ALTER TABLE
passenger_air_tranportation=# SELECT * FROM pilots_hobbies;
 first_name |  name  |  last_name   | years_old
------------+--------+--------------+-----------
 Ivanov     | Ivan   | Borisovich   |        29
 Melnikov   | Stepan | Ivanovich    |        52
 Okrugin    | Nikita | Anatolyevich |        22
 Ribkin     | Kirill | jojobavich   |        61
```
14
```
passenger_air_tranportation=# ALTER TABLE pilots_hobbies
passenger_air_tranportation-# ADD COLUMN hobbies jsonb NULL;
ALTER TABLE
passenger_air_tranportation=# SELECT * FROM pilots_hobbies;
 first_name |  name  |  last_name   | years_old | hobbies
------------+--------+--------------+-----------+---------
 Ivanov     | Ivan   | Borisovich   |        29 |
 Melnikov   | Stepan | Ivanovich    |        52 |
 Okrugin    | Nikita | Anatolyevich |        22 |
 Ribkin     | Kirill | jojobavich   |        61 |
(4 строки)
```
15.
```
passenger_air_tranportation=# UPDATE pilots_hobbies
passenger_air_tranportation-# SET hobbies = '{"sport": ["Swimming","running"], "Games": ["MOBA","Strategy"]}';
UPDATE 4
passenger_air_tranportation=# SELECT * FROM pilots_hobbies;
 first_name |  name  |  last_name   | years_old |                              hobbies
------------+--------+--------------+-----------+-------------------------------------------------------------------
 Ivanov     | Ivan   | Borisovich   |        29 | {"Games": ["MOBA", "Strategy"], "sport": ["Swimming", "running"]}
 Melnikov   | Stepan | Ivanovich    |        52 | {"Games": ["MOBA", "Strategy"], "sport": ["Swimming", "running"]}
 Okrugin    | Nikita | Anatolyevich |        22 | {"Games": ["MOBA", "Strategy"], "sport": ["Swimming", "running"]}
 Ribkin     | Kirill | jojobavich   |        61 | {"Games": ["MOBA", "Strategy"], "sport": ["Swimming", "running"]}
(4 строки)
```
16. В общих чертах я мог сделать это ограничение, но я не хотел себя удалять себя родимого, поэтому я поставил ограничение в 21

```
passenger_air_tranportation=# ALTER TABLE pilots_hobbies
passenger_air_tranportation-# ADD CHECK (years_old > 21);
ALTER TABLE
```

17.Сначала надо найти название ограничения:
```
passenger_air_tranportation=# SELECT constraint_name, constraint_type
passenger_air_tranportation-# FROM information_schema.table_constraints
passenger_air_tranportation-# WHERE table_name = 'pilots_hobbies';
        constraint_name         | constraint_type
--------------------------------+-----------------
 pilots_hobbies_years_old_check | CHECK
 2200_16412_1_not_null          | CHECK
 2200_16412_2_not_null          | CHECK
 2200_16412_3_not_null          | CHECK
 2200_16412_4_not_null          | CHECK
(5 строк)
```
потом его удаляем:
```
passenger_air_tranportation=# ALTER TABLE pilots_hobbies
passenger_air_tranportation-# DROP CONSTRAINT pilots_hobbies_years_old_check;
ALTER TABLE
```
18.
```

passenger_air_tranportation=# DROP TABLE pilots_hobbies;
DROP TABLE

```