# Домашнее задание к занятию «Репликация и масштабирование. Часть 1»

---

### Задание 1
Выполните конфигурацию master-slave репликации, примером можно пользоваться из лекции.

*Приложите скриншоты конфигурации, выполнения работы: состояния и режимы работы серверов.*
###Решение 1

![1](https://github.com/znak72/hw-12-6/blob/main/001.png)
---

### Задание 2

Разработайте план для выполнения горизонтального и вертикального шаринга базы данных. База данных состоит из трёх таблиц: 

- пользователи, 
- книги, 
- магазины (столбцы произвольно). 

Опишите принципы построения системы и их разграничение или разбивку между базами данных.

*Пришлите блоксхему, где и что будет располагаться. Опишите, в каких режимах будут работать сервера.* 

###Решение 2

База данных состоит из трех таблиц:

пользователи,
книги,
магазины.

# Вертикальный шардинг

Каждая таблица находится на отдельном сервере. 


![Вертикальное шардирование ](https://github.com/znak72/hw-12-6/blob/main/200164189-4bde1720-e2bd-40de-9d1a-3943297397db.png)





# Горизонтальный шардинг
таблица Books разделена на 2 сервера по названию книги от A-N и от O-Z

таблица Users разделена по тоже разделена на 2 сервера по принципу аутонтификации и данных users

таблица Stores была перенесена полностью в отдельный сервер без изменений 


![Снимок экрана от 2022-11-06 01-49-39](https://github.com/znak72/hw-12-6/blob/main/200164193-2e558350-6133-4a6a-87c4-4e302dc43479.png)

