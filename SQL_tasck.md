**Краткая информация о базе данных "Компьютерная фирма":**
****
Схема БД состоит из четырех таблиц:
**Product**   ***(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)***
Таблица **Product** представляет производителя **(maker)**, номер модели **(model)** и тип (**'PC'** - ПК, **'Laptop'** - ПК-блокнот или **'Printer'** - принтер). Предполагается, что номера моделей в таблице **Product** уникальны для всех производителей и типов продуктов. В таблице **PC** для каждого ПК, однозначно определяемого уникальным кодом – **code**, указаны модель –** model** (внешний ключ к таблице **Product**), скорость - **speed** (процессора в мегагерцах), объем памяти - **ram** (в мегабайтах), размер диска - **hd** (в гигабайтах), скорость считывающего устройства - **cd** (например, '4x') и цена - **price**. Таблица **Laptop** аналогична таблице **РС** за исключением того, что вместо скорости **CD **содержит размер экрана -**screen** (в дюймах). В таблице **Printer** для каждой модели принтера указывается, является ли он цветным - **color** ('y', если цветной), тип принтера - **type** (лазерный – 'Laser', струйный – 'Jet' или матричный – 'Matrix') и цена - **price**.
****
********
**Задание: 1**

Для каждого производителя, выпускающего ПК-блокноты c объёмом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.

**ответ:**

SELECT DISTINCT product.maker,laptop.speed

 FROM product JOIN laptop
 
ON product.model= laptop.model

 WHERE hd >= '10'


----------
**Задание: 2**

Найдите производителей принтеров. Вывести: maker

**ответ:**

SELECT DISTINCT maker

FROM Product

WHERE type = 'Printer';


----------

**Задание: 3**

Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 

**ответ:**

SELECT model, ram, screen

FROM Laptop

WHERE price>1000;
 

----------
**Задание: 4**

Найдите все записи таблицы Printer для цветных принтеров

**ответ:**

SELECT*FROM Printer

WHERE color='y';


----------
**Задание: 5**

Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.

**ответ:**

SELECT model, speed, hd

FROM PC

WHERE (cd = '12x' OR cd = '24x') AND price < 600;


----------
**Задание: 6**

Найдите номера моделей и цены всех имеющихся в продаже продуктов (любого типа) производителя B (латинская буква).

**ответ:**

SELECT DISTINCT product.model, Pc.price

FROM Product JOIN pc On product.model = pc.model 

WHERE maker ='B' 

UNION 

SELECT DISTINCT product.model, laptop.price

FROM Product JOIN Laptop On product.model = laptop.model 

WHERE maker ='B' 

UNION 

SELECT DISTINCT product.model, printer.price

FROM Product JOIN printer On product.model = printer.model 

WHERE maker ='B';

----------
**Задание: 7**

Найдите производителя, выпускающего ПК, но не ПК-блокноты.

**ответ:**

SELECT DISTINCT maker

FROM Product

WHERE type = 'pc'

EXCEPT

SELECT DISTINCT product.maker

FROM Product

WHERE type = 'laptop';

----------



