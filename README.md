# Домашнее задание к занятию "`Базы данных`" - `Островский Евгений`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Легенда
Заказчик передал вам файл в формате Excel, в котором сформирован отчёт.

На основе этого отчёта нужно выполнить следующие задания.

### Задание 1
Опишите не менее семи таблиц, из которых состоит база данных:

- какие данные хранятся в этих таблицах;
- какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.
Приведите решение к следующему виду:

Сотрудники (

- идентификатор, первичный ключ, serial,
- фамилия varchar(50),
- ...
- идентификатор структурного подразделения, внешний ключ, integer).

### Решение:

**Сотрудники** (
- идентификатор, первичный ключ, serial,
- фамилия varchar(50),
- имя varchar(50),
- отчество varchar(50),
- дата найма date,
- идентификатор филиала, внешний ключ, integer,
- идентификатор структурного подразделения, внешний ключ, integer)

**Филиал** (
- идентификатор, первичный ключ, serial,
- Субьект varchar(100),
- Город varchar(50),
- Улица varchar(50),
- Дом varchar(10))

**Должность** (
- идентификатор, первичный ключ, serial,
- Должность varchar(50),
- Описание varchar(50),
- идентификатор проекта, внешний ключ, integer)

**Структурное подразделение** (
- идентификатор, первичный ключ, serial,
- Подразделение varchar(50),
- Описание varchar(50),
- идентификатор должности, внешний ключ, integer)

**Подразделения** (
- идентификатор, первичный ключ, serial,
- Тип подразделения varchar(50),
- идентификатор структурного подразделения, внешний ключ, integer)

**Проект** (
- идентификатор, первичный ключ, serial,
- Проект varchar(100),
- идентификатор сотрудника, внешний ключ, integer)

**Оклад** (
- идентификатор сотрудника, внешний ключ, integer,
- идентификатор должности, внешний ключ, integer,
- оклад float)

---
## Дополнительные задания (со звездочкой*)

Эти задания дополнительные (не обязательные к выполнению) и никак не повлияют на получение вами зачета по этому домашнему заданию. Вы можете их выполнить, если хотите глубже и/или шире разобраться в материале.

### Задание 2

Перечислите, какие, на ваш взгляд, в этой денормализованной таблице встречаются функциональные зависимости и какие правила вывода нужно применить, чтобы нормализовать данные.

**Решение**
Возмем степени функциональной зависимости:
 - частичная зависимость - когда таблица содержит составной ключи - в нашем случае можно вывести - оклад из должности и сотрудника, проект из сотрудника и структурного подразделения
- транзитивная зависимость - это связь двух через третьего - в нашем  случае -  Сотрудник  -> Тип подразделения -> Структурное подразделение
- многозначная зависимость - когда одному значению соответствует несколько значений - например - Тип подразделения - Структурное подразделение, Должность - Сотрудник.

Возможно применить следующие правила:
- удаление транзитивных зависимостей
- декомпозиция функциональных зависимостей
- удаление избыточнах зависимостей
