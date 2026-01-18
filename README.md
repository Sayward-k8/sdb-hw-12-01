# Домашнее задание к занятию «Базы данных» 

# Задание 1
Опишите не менее семи таблиц, из которых состоит база данных:

какие данные хранятся в этих таблицах;
какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.
Приведите решение к следующему виду:

Сотрудники (

идентификатор, первичный ключ, serial,
фамилия varchar(50),
...
идентификатор структурного подразделения, внешний ключ, integer).

# Решение 1

  1. Филиалы
<details>

```sql
Филиалы (
    id_филиала PRIMARY KEY serial,
    Адрес филиала VARCHAR(255)
    ); 
```

</details>

  2. Тип подразделения
<details>
  
```sql
Тип подразделения(
    id_типа_подразделения PRIMARY KEY serial,
    название типа подразделения VARCHAR(50) NOT NULL UNIQUE
    );
```
</details>

  3. Структурные подразделения
<details>
  
```sql
Структурные_подразделения (
    id_структурного подразделения PRIMARY KEY serial,
    название подразделения VARCHAR(255) NOT NULL,
    id_типа_подразделения INT NOT NULL,
    foreign key(id_типа_подразделения) REFERENCES Типы_подразделений(id),
    id_филиала INT NOT NULL,
    foreign key(id_филиала) REFERENCES Филиалы(id)
    );
```
</details>

  4. Должности
<details>
  
```sql
Должности (
    id_должность PRIMARY KEY serial,
    название должности VARCHAR(150) NOT NULL UNIQUE,
    оклад numeric(10,2) CHECK (оклад > 0)
    );
```
</details>

  5. Сотрудники
<details>
  
```sql
Сотрудники (
    id_сотрудника PRIMARY KEY serial,
    ФИО VARCHAR(50) NOT NULL,
    Оклад NUMERIC(10,2) CHECK (оклад > 0)
    id_должность INT NOT NULL,
    foreign key (id_должность) REFERENCES Должности(id),
    Дата найма DATE NOT NULL,
    id_структурного подразделения INT NOT NULL,
    foreign key (id_структурного подразделения) REFERENCES Структурные_подразделения(id)
    );
```
</details>


  6. Проекты
<details>
  
```sql
Проекты (
    id_проекта PRIMARY KEY serial,
    название проекта varchar(255) NOT NULL UNIQUE
    );
```
</details>

  7. Назначения на проекты
<details>
   
```sql 
Назначения на проекты(
    id_проекта INT,
    id_сотрудника INT,
    PRIMARY KEY(id_проекта, id_сотрудника),
    FOREIGN KEY (id_проекта) REFERENCES Проекты(id),
    FOREIGN KEY (id_сотрудника) REFERENCES Сотрудники(id)
    )
```
</details>

# Задание 2*
Перечислите, какие, на ваш взгляд, в этой денормализованной таблице встречаются функциональные зависимости и какие правила вывода нужно применить, чтобы нормализовать данные.

