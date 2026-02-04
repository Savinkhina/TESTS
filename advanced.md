# SQL — продвинутый уровень

### SQL
-----------------------------------------
#### Какой будет результат, если значение в колонке таблицы подходит под несколько условий в CASE?
- вернется значение THEN последнего условия
- [x] `вернется значение THEN первого условия
- вернется значение THEN первого условия
- вернется NULL

#### Укажите запрос, который выберет все фильмы, связанные со словами bad, good, angry. В названиях фильмов могут содержаться эти слова в разном виде, например в разных регистрах (Badboys) или в измененной форме (goodspeed).
- select movie_name from movies where lower (movie_name) like 'bad' or lower(movie_name) like
- select movie_name from movies where movie_name like '%bad%' or movie_name like '%angry%' or
- select movie_name from movies where movie_name like '%Good' or movie_name like '%Bad' or mo
- [x] `select movie_name from movies where lower(movie_name) like '%bad%' or lower(movie_name) like '%angry%' or lower(movie_name) like '%good%'`
- select movie_name from movies where movie_name in ('bad', 'angry', 'good')

#### Выберите верное утверждение относительно операторов EXISTS и ANY в SQL.
- [x] `EXISTS проверяет, содержит ли подзапрос хотя бы одну строку, и возвращает TRUE, если строка есть.`

#### Выберите верное утверждение относительно операторов INTERSECT, EXCEPT, UNION и т.д.
- [x] `Смена порядка запросов для EXCEPT поменяет выводимые данные.`

#### Что вернёт следующий запрос, если в таблице нет ни одной строки?
- SELECT SUM(amount), COUNT(*) FROM transactions
- Некорректный результат
- Ошибку
- О и 0
- NULL и NULL
- [x] `NULL И О`

#### Что означает, если МАХ (updated_at) возвращает NULL ?
- МАХ() не применим к датам
- Поле не имеет индекса
- [x] `Все значения в updated_at - NULL`
- Ошибка сравнения
- Значения updated_at отрицательные

#### Получите список имен и фамилий сотрудников, которые работают в отделе маркетинга, из таблицы Employees.
- [x] `SELECT first_name, last_name FROM Employees WHERE department = 'Marketing';`

#### Каким будет результат выполнения следующего кода для таблицы Cars, если car_id - первичный ключ?
- [x] `Отобразится ошибка`

#### Вы хотите найти заработную плату отделов, у которых общая заработная плата не превышает 700 000 рублей, в таблице Salaries. Какая ошибка допущена в запросе?
SELECT department_id, SUM(salary) AS total_salary FROM Salaries
HAVING total_salary <= 700000 GROUP BY department_id;
- [x] `HAVING total_salary <= 700000 стоит перед GROUP BY, а не после него`
- [x] `total_salary <= 700000 вместо SUM(salary) <= 700000`

#### Найдите имена сотрудников, зарплата которых ниже медианной зарплаты всех сотрудников в таблице Employees.
- [x] `SELECT first_name, last_name FROM Employees WHERE salary < (SELECT MEDIAN(salary) FROM employees);`

#### Напишите SQL-запрос, который выберет все записи из таблицы Customers, у которых имя (name) начинается на букву "A" или "M", и возраст (age) больше 25 лет. Отсортируйте список в порядке убывания возраста.
- [x] `SELECT * FROM Customers WHERE (name LIKE 'A%' OR name LIKE 'M%') AND age > 25 ORDER BY age DESC`

#### Какую задачу может решать данный код?
SELECT product_name,
CASE WHEN (price > 100) THEN 'expensive'
ELSE 'cheap'
END AS product_cost
FROM cd.database;  
- [x] `Получение данных о дорогих и дешевых товарах, где дорогими считаются товары дороже 100 рублей. При этом отобразится таблица с названием товаров в одном столбике и указанием дорогой он или дешевый в другом.`

#### Вам нужен отсортированный в алфавитном порядке список из 10 неповторяющихся имён в таблице group_A. С помощью какого кода может быть решена данная задача?
- [x] `SELECT DISTINCT surname FROM group_A ORDER BY surname LIMIT 10;`

### JOIN
-----------------------------------------
#### В каком случае LEFT JOIN может вернуть меньше строк, чем таблица слева?
- Если соединяем по ключу, которого нет в правой таблице
- Если используем USING вместо ON
- Если таблицы имеют разное количество колонок
- Если SELECT не используется
- [x] `При наличии WHERE -условия, отфильтровывающего строки из результата`

#### Есть две таблицы из одной колонки, в них содержатся NULL-значения. В левой таблице — пять значений NULL, в правой — семь. Сколько строк вернется с NULL при выполнении различных типов соединений?
- [x] `INNER — 0, LEFT — 5, RIGHT — 7, FULL — 12`

#### Найдите данные, относящиеся только к левой таблице Orders, в таблицах Orders и Clients, учитывая, что общий столбец между ними — client_id.
- [x] `SELECT Orders.order_id FROM Orders LEFT JOIN Clients ON Clients.client_id = Orders.client_id WHERE Clients.client_id IS NULL;`

#### У вас есть две таблицы: workers и salary. Первая таблица содержит уникальный id сотрудника, его фамилию (surname) и должность (position). Во второй таблице указано: id должности, сама должность и соответствующая ей зарплата. Вам нужно узнать, сколько зарабатывает каждый сотрудник. Какой вариант кода сможет решить данную задачу?
- [x] `SELECT * FROM workers w JOIN salary s ON w.position = s.position;`

#### Зачем используют подзапрос в SELECT (вместо JOIN )?
- Для объединения нескольких таблиц
- [ ] `Для фильтрации строк до группировки`
- [x] `Для изоляции агрегатной логики по каждой строке`
- Для ускорения выполнения запроса
- Для упрощения GROUP BY
      
### GROUP BY
-----------------------------------------
#### Что произойдет, если при использовании GROUP BY указаны колонки, но не указаны агрегирующие функции?
- [x] `запрос вернет уникальные значения по колонкам, которые прописаны и в GROUP BY, и в SELECT`
  
#### Что произойдет, если при использовании GROUP BY применить агрегирующую функцию MAX к колонке, содержащей строковые значения?
- [x] `Для каждого уникального значения в GROUP BY вернется последняя строка по алфавиту`

### UNION
-----------------------------------------
#### Что делает UNION ALL по сравнению с UNION ?
Выполняет объединение без удаления дубликатов
Фильтрует строки по ключу
Использует индекс для объединения
Объединяет только числовые колонки
Автоматически сортирует результат
- [x] `Выполняет объединение без удаления дубликатов`

### BAG SQL
-----------------------------------------
#### В этом SQL-запросе допущено несколько ошибок (в данных при этом ошибок нет). Выберите вариант со всеми перечисленными ошибками.
- [x] `один из подзапросов в WHERE возвращает две колонки; для двух подзапросов нет алиаса; JOIN происходит по полю, которого нет в подзапросе`

#### Выберите вариант, где для каждого запроса указана ошибка, из-за которой запрос либо не сработает, либо вернет неверные значения.
- [x] `regexp_replace возвращает некорректное значение для CAST`

#### Какой будет результат, если в запросе неправильно рассчитаны показатели?
- [x] `скользящая сумма заказов, разница во времени между заказами, ранг пользователя по сумме заказов`

#### Выберите синтаксически корректный запрос.
- [x] `alter table public.table_1 modify (user_id int, salary float, department_id int)`

#### Почему этот запрос может дать неожиданные результаты?
SELECT category, COUNT (price) FROM products GROUP BY category;
GROUP BY не работает с текстовыми колонками
COUNT(price) не учитывает NULL, и результат может быть занижен
COUNT нельзя применять к строкам
category не включён в SELECT
Запрос вернёт NULL
- [x] `COUNT(price) не учитывает NULL, и результат может быть занижен`

#### Почему этот запрос вызовет ошибку?
SELECT department, COUNT(*), salary
FROM employees
GROUP BY department;
salary не включён в GROUP BY и не агрегирован
department нельзя использовать в GROUP BY
Нельзя группировать по строковым полям
COUNT не может сочетаться с GROUP BY
SELECT должен содержать только агрегатные функции
- [x] `salary не включён в GROUP BY и не агрегирован`

### WINDOW
-----------------------------------------
#### Что делает конструкция row_number() over (partition by user_id order by order_date) ?
Нумерует заказы внутри пользователя по дате
Отфильтровывает первые строки
Создаёт ранг по сумме
Назначает уникальный номер для каждого пользователя
Считает количество заказов
- [x] `Нумерует заказы внутри пользователя по дате`

#### Почему следующий запрос может вернуть неверный ранг пользователя в пределах месяца? 
rank() over (partition by date_trunc('month', order_date) order by sum(amount) over (partition by user_id))
Он группирует по user_id, а не по месяцу
date_trunc нельзя использовать в partition by
Он использует оконную функцию внутри другой оконной функции
Он возвращает одинаковый ранг для всех
rank() требует group by
- [x] `Он использует оконную функцию внутри другой оконной функции`

### INDEX
-----------------------------------------
#### Какой из следующих индексов будет наиболее оптимальным для ускорения запросов, фильтрующих данные по user_id и сортирующих их по created_at?
create index payments_user_id_hash_idx on payments using hash (user_id);
create index payments_user_id_idx on payments using btree (user_id);
create index payments_user_id_created_at_idx on payments using btree (user_id, created_at);
create index payments_gin_idx on payments using gin (to_tsvector('english', user_id::text));
create index payments_brin_idx on payments using brin (created_at);
- [x] `create index payments_user_id_created_at_idx on payments using btree (user_id, created_at);`

#### Вы создали некластеризованный индекс в таблице Products для столбца category, который содержит его записи и адреса соответствующей строки (в основной таблице), в которой находится запись столбца. Какой шаг из перечисленных ниже не совершается при запуске следующего запроса?
CREATE INDEX product_category_index
ON Products (category);
SELECT product_name, category, price
FROM Products
WHERE category= 'electronics';
- [x] `Сохранение выбранных значений в дополнительной таблице`

### VIEW
-----------------------------------------
#### У вас есть уже существующее материальное представление test_view. Вы хотите добавить в него новый столбец num_purchases. Как сделать это синтаксически верно?
- [x] `delete materialized view test_view; create or replace materialized_view test_view as select user_id, min(dt) as first_payed, sum(price) as revenue, count(*) as num_purchases group by user_id`

#### У вас есть таблица Orders с миллионом строк и проиндексированным столбцом order_date, который был создан с использованием следующего запроса:
CREATE INDEX order_index ON Orders(order_date);
Каким образом вы будете оптимизировать производительность запроса, который извлекает информацию о последнем заказе для клиента из таблицы?
- [x] `Использую подзапрос, чтобы получить последний order_date для клиента, а затем объединю результаты с таблицей Orders, чтобы получить полную информацию о заказе`

#### Вам нужно создать представление с именем PeopleView с данными из двух таблиц Respondents и Info, в котором будут содержаться возраст, телефоны и адреса респондентов. Какая ошибка допущена в запросе?
CREATE VIEW PeopleView
AS SELECT age, phone_number, address
FROM Respondents, Info
WHERE Respondents.respondent_id=Info.respondent_id;
- [x] `Нужно указывать, из каких таблиц взяты данные, т.е. Respondents.age, Respondents.phone_number, Info.address`

#### Какой запрос позволяет создать обычное представление с фильтрацией по сумме?
create materialized view revenue_summary as select user_id, sum(price) as total from payments group by user_id
create or replace table as select user_id, sum(price) from payments
create view revenue_summary as select user_id, sum(price) as total from payments group by user_id having sum(price) > 10000
create view revenue_summary from payments group by user_id
select into revenue_summary from payments group by user_id
- [x] `create view revenue_summary as select user_id, sum(price) as total from payments group by user_id having sum(price) > 10000`

#### Как обновить материальное представление, чтобы оно учитывало только данные за последние 3 месяца?
Использовать ALTER MATERIALIZED VIEW с добавлением условия
Выполнить REFRESH MATERIALIZED VIEW с фильтром
Обновить материализованное представление через UPDATE
Применить WHERE dt > now() к уже существующему представлению
Удалить представление и создать его заново с фильтром
WHERE dt > current_date - interval '3 months'
- [x] `Выполнить REFRESH MATERIALIZED VIEW с фильтром`

### DML
-----------------------------------------
#### Определите список разрешений, на который можно выдать или отозвать права с помощью операторов GRANT, REVOKE.
- [x] `CREATE, TRUNCATE, DELETE, TRIGGER`

#### Выберите операторы, относящиеся только к DDL.
- [x] `DROP, ALTER, CREATE, RENAME`

#### Добавьте новый столбец email с типом данных VARCHAR(255) в существующую таблицу.
- [x] `ALTER TABLE Clients ADD email VARCHAR(255);`

#### Вы хотите удалить колонку temp_flag из таблицы sessions. Какой SQL-запрос это реализует?
alter sessions remove column temp_flag
alter table sessions drop column temp_flag
delete temp_flag from sessions
drop column temp_flag from sessions
remove column temp_flag in sessions
- [x] `alter table sessions drop column temp_flag`

#### Вы создали таблицу:
CREATE TABLE yourtable(x int NOT NULL,
y int NOT NULL,
CONSTRAINT pk_yourtable PRIMARY KEY(x, y));
Выберите, какая команда должна быть первой в процедуре, работающей с ошибками и транзакциями.
- [x] `SET XACT ABORT, NOCOUNT ON`

#### Какой из операторов создаёт таблицу в SQL?
insert into users values (...)
rename users to users_backup
alter users create table
select into table users
create table users (...)
- [x] `create table users (...)`

#### Вам нужно обновить поле status в таблице orders на ‘cancelled' для всех заказов старше 2020 года. Какой запрос использовать?
update orders set status = 'cancelled' where order_date < '2020-01-01'
update orders set status = 'cancelled' and order_date < '2020'
alter orders set status = 'cancelled' where order_date < 2020
update orders set status = 'cancelled' where order_date like '201%'
update orders set status = 'cancelled' where year(order_date) < 2020
- [x] `update orders set status = 'cancelled' where year(order_date) < 2020.`

#### Вы даете разрешение или запрет на выполнение определенных операций над объектами базы данных компании. Какие операторы вы используете в данном процессе?
- [x] `GRANT, REVOKE`

#### Есть таблица с информацией о транзакциях: В данных есть особенность: в поле amount могут находиться целые и дробные данные с указанием валюты, например 1.43 EUR, 250, 37.18, 893 RUB. Также есть SQL-запрос, который написан аналитиком и рассчитывает сумму одобренных транзакций по месяцам 2023 года.
select
sum(cast(regexp_replace(amount, '[^0-9.]', ', 'g') as numeric)) as total_approved_amount
from transactions
where
status = 'approved'
and date_trunc('YEAR', transaction_date::date) = '2023'
group by month
order by month

Выберите вариант, где для каждого запроса указана ошибка, из-за которой запрос либо не сработает, либо вернет неверные значения:
date_trunc не работает с датами в формате YYYY, a regexp_replace удаляет только буквы, но нелишние символы
regexp_replace возвращает некорректное значение для САЅТ, а date_trunc('YEAR', transaction_date::date) = '2023' записано с ошибкой
to_char(transaction_date, 'YYYY-MM') не поддерживает преобразование дат, а sum(...) не суммирует значения типа numeric
cast(regexp_replace(...)) as numeric нельзя применять в агрегатных функциях, a date_trunc('YEAR', transaction_date::date)='2023' не фильтрует по году
regexp_replace искажает числовые значения, а group by month некорректно сгруппирует данные
- [x] `regexp_replace возвращает некорректное значение для САЅТ, а date_trunc('YEAR', transaction_date::date) = '2023' записано с ошибкой`

