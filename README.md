# SQL теория:
`SQL (Structured Query Language)` - Язык структурированных запросов

`БД (База данных)` - Набор взаимосвязанных данных

`СУБД (Система управления базами данных)` - ПО для управления данными (отвечает за поддержку языка БД, механизмы хранения и извлечения данных)

`C.R.U.D.` - `CREATE` `READ` `UPDATE` `DELETE`

# Типы команд:
DDL (Data Definition Language) - `CREATE` `DROP` `ALTER` `TRUNCATE`

DQL (Data Query Language) - `SELECT`

DML (Data Manipulation Language) - `INSERT` `UPDATE` `DELETE` `CALL` `EXPLAIN CALL` `LOCK`

DCL(Data Control Language) - `GRANT` `REVOKE`

TCL (Transaction Control Language) - `COMMIT` `SAVEPOINT` `ROLLBACK` `SET TRANSACTION` `SET CONSTRAINT`


# SQL Синтаксис:

### Самый обычный запрос `SELECT`
```sql
SELECT * FROM Sample.Tab
WHERE id='id1';

Комментарий:
--SELECT --Выбрать
--* --Все колонки
--FROM --Откуда (из)
--Sample.Tab --Таблицы
--WHERE --Где
--id --наименование колонки
--'id1' --значение в колонке id (ставится в 'одинарные ковычки')

'Резюме - Выбрать всё из таблицы Sample, где id = id1'
```
---


### Запрос с выбором нескольких колонок `IN`

```sql
SELECT * FROM Sample.Tab
WHERE id IN ('id1','id2','id3');

Комментарий:
--IN --Даёт возможность перечисления нескольких колонок

'Резюме - Выбрать всё из таблицы Sample, где id = id1, id2, id3'
```
---


### Вложенный запрос `DISTINCT`

```sql
SELECT * FROM Sample.Tab
WHERE id IN (SELECT DISTINCT id FROM Sample.Tab WHERE name='Andrey');

Комментарий:
--DISTINCT --Уникальный

'Резюме - Выбрать всё из таблицы Sample, где все id имеют name = Andrey. (Используется обычно если бы в подзапросе была бы другая таблица)'
```
---


### Найти похожие значения `LIKE`

```sql
SELECT * FROM Sample.Tab
WHERE name LIKE 'Andrey%';

Комментарий:
--LIKE --Находит похожие значения

'Резюме - Выбрать всё из таблицы Sample, где name имеет схожесть, например Andrey Bogatyrev, Andrey Mikhailovich, Andrey SQL и т.п.'
```
---


### Исключить нулёвые значения `IS NOT`
```sql
SELECT * FROM Sample.Tab
WHERE name IS NOT NULL;

Комментарий:
--IS NOT --Не
--NULL --Значения равные нулю

'Резюме -- Выбрать всё из таблицы Sample, где name не равно нулю'
```
---


### Найти нулёвые значения `IS NULL`
```sql
SELECT * FROM Sample.Tab
WHERE name IS NULL;

Комментарий:
--IS --Равны
--NULL --Ноль

'Резюме -- Выбрать всё из таблицы Sample, где name равно нулю'
```
---


### Максимально выводимое количество строк `LIMIT`
```sql
SELECT * FROM Sample.Tab
LIMIT 10;

Комментарий:
--LIMIT --Максимум

'Резюме -- Выбрать всё из таблицы Sample, но только первых 10 записей'
```
---


### Считаем количество `COUNT`
```sql
SELECT COUNT(*) FROM Sample.Tab
WHERE id='id1';

Комментарий:
--COUNT --Подсчитывает количество строк

'Резюме -- Выбрать и посчитать всё количество строк из таблицы Sample, где id = id1'
```
---


### Считаем сумму `SUM`
```sql
SELECT SUM(name) FROM Sample.Tab
WHERE id='id1';

Комментарий:
--SUM --Считает сумму значений столбца

'Резюме -- Выбрать и посчитать сумму всех значений в колонке name из таблицы Sample, где id = id1'
```
---


### Находим минимальное значение `MIN`
```sql
SELECT MIN(name) FROM Sample.Tab
WHERE id='id1';

Комментарий:
--MIN --Минимальное значение

'Резюме -- Выбрать и найти минимальное значение в колонке name из таблицы Sample, где id = id1'
```
---


### Находим максимальное значение `MAX`
```sql
SELECT MAX(name) FROM Sample.Tab
WHERE id='id1';

Комментарий:
--MAX --Максимальное значение

'Резюме -- Выбрать и найти максимальное значение в колонке name из таблицы Sample, где id = id1'
```
---


### Находим максимальное значение `AVG` (AVERAGE)
```sql
SELECT AVG(name) FROM Sample.Tab
WHERE id='id1';

Комментарий:
--AVG --Среднее значение

'Резюме -- Выбрать и найти среднее значение в колонке name из таблицы Sample, где id = id1'
```
---


### Присваиваем псевдонимы и группируем данные `AS` `GROUP BY`
```sql
SELECT country, COUNT(id) AS Users FROM Sample.Tab
GROUP BY country;

Комментарий:
--AS --Назначить псевдоним (переименовать на выходе) (Alias)
--GROUP BY --Группировка данных (одинаковые значения будут объединены в одну группу)

'Резюме -- Выбрать колонки country и "COUNT(id) переименовывается в Users", и посчитать общее количество id из таблицы Sample, и группируем данные по столбцу country (причём все одинаковые значения будут объединены в одну группу)'
```
---


### Считаем только уникальные значения `COUNT(DISTINCT)`
```sql
SELECT COUNT(DISTINCT id) FROM Sample.Tab;

Комментарий:
--COUNT(DISTINCT column) --Посчитать только уникальные значения

'Резюме -- Выбрать и посчитать только уникальные значения по колонке id из таблицы Sample'
```
---


### Сортируем в порядке убывания `ORDER BY DESC`
```sql
SELECT country, SUM(money) FROM Sample.Tab
GROUP BY country
ORDER BY 2 DESC;

Комментарий:
--ORDER BY 2 DESC --Сортировать по значениям во втором столбце в порядке убывания

'Резюме -- Выбрать country и сумму money из таблицы Sample, группировать по столбцу country, и сортировать по значениям во втором столбце в порядке убывания'
```
---


### Сортируем в порядке возрастания `ORDER BY ASC`
```sql
SELECT country, SUM(money) FROM Sample.Tab
GROUP BY country
ORDER BY 2 ASC;

Комментарий:
--ORDER BY 2 ASC --Сортировать по значениям во втором столбце в порядке возрастания

'Резюме -- Выбрать country и сумму money из таблицы Sample, группировать по столбцу country, и сортировать по значениям во втором столбце в порядке возрастания'
```
---


### Выкидываем мусор (мелкие значения) `HAVING`
```sql
SELECT country, SUM(money) FROM Sample.Tab
GROUP BY country
HAVING SUM(money)>1000
ORDER BY 2 DESC;

Комментарий:
--HAVING --Оставить только значения равные условию

'Резюме -- Выбрать country и сумму money из таблицы Sample, группировать по столбцу country, оставить значения только которые больше 1000, и сортировать по значениям во втором столбце в порядке убывания'
```
---


### XXXXXXX `JOIN`
```sql
SELECT 








'Резюме -- 
```
---





'Резюме -- Выбрать всё из таблицы Sample, где id = id1, id2, id3






