# SQL — продвинутый уровень

### GROUP BY
-----------------------------------------
#### Q1. Что произойдет, если при использовании GROUP BY указаны колонки, но не указаны агрегирующие функции?
- [x] `запрос вернет уникальные значения по колонкам, которые прописаны и в GROUP BY, и в SELECT`
  
#### Q2. Что произойдет, если при использовании GROUP BY применить агрегирующую функцию MAX к колонке, содержащей строковые значения?
  

- [x] `Для каждого уникального значения в GROUP BY вернется последняя строка по алфавиту`
  

#### Q3. Есть две таблицы из одной колонки, в них содержатся NULL-значения. В левой таблице — пять значений NULL, в правой — семь. Сколько строк вернется с NULL при выполнении различных типов соединений?
  

- [x] `INNER — 0, LEFT — 5, RIGHT — 7, FULL — 12`


#### Q4. Какой будет результат, если значение в колонке таблицы подходит под несколько условий в CASE?
  

- [x] `вернется значение THEN первого условия.`
  

#### Q5. В этом SQL-запросе допущено несколько ошибок (в данных при этом ошибок нет). Выберите вариант со всеми перечисленными ошибками.
  

- [x] `один из подзапросов в WHERE возвращает две колонки; для двух подзапросов нет алиаса; JOIN происходит по полю, которого нет в подзапросе`
  

#### Q6. У вас есть уже существующее материальное представление test_view. Вы хотите добавить в него новый столбец num_purchases. Как сделать это синтаксически верно?
  

- [x] `delete materialized view test_view; create or replace materialized_view test_view as select user_id, min(dt) as first_payed, sum(price) as revenue, count(*) as num_purchases group by user_id`
  

#### Q7. Укажите запрос, который выберет все фильмы, связанные со словами bad, good, angry. В названиях фильмов могут содержаться эти слова в разном виде, например в разных регистрах (Badboys) или в измененной форме (goodspeed).
  

- [x] `select movie_name from movies where lower(movie_name) like '%bad%' or lower(movie_name) like '%angry%' or lower(movie_name) like '%good%'`
  

#### Q8. Выберите вариант, где для каждого запроса указана ошибка, из-за которой запрос либо не сработает, либо вернет неверные значения.
  

- [x] `regexp_replace возвращает некорректное значение для CAST`
  

#### Q9. Какой будет результат, если в запросе неправильно рассчитаны показатели?
  

- [x] `скользящая сумма заказов, разница во времени между заказами, ранг пользователя по сумме заказов`
  

#### Q10. Выберите синтаксически корректный запрос.
  

- [x] `alter table public.table_1 modify (user_id int, salary float, department_id int)`
  

#### Q11. Какой из следующих индексов будет наиболее оптимальным для ускорения запросов, фильтрующих данные по user_id и сортирующих их по created_at?
  

- [x] `create index payments_user_id_created_at_idx on payments using btree (user_id, created_at);`
  

#### Q12. Определите список разрешений, на который можно выдать или отозвать права с помощью операторов GRANT, REVOKE.
  

- [x] `CREATE, TRUNCATE, DELETE, TRIGGER`
  

#### Q13. Выберите верное утверждение относительно операторов EXISTS и ANY в SQL.
  

- [x] `EXISTS проверяет, содержит ли подзапрос хотя бы одну строку, и возвращает TRUE, если строка есть.`
  

#### Q14. Выберите верное утверждение относительно операторов INTERSECT, EXCEPT, UNION и т.д.
  

- [x] `Смена порядка запросов для EXCEPT поменяет выводимые данные.`
  

#### Q15. Выберите операторы, относящиеся только к DDL.
  

- [x] `DROP, ALTER, CREATE, RENAME`
  

#### Q16. Почему следующий запрос может вернуть неверный ранг пользователя в пределах месяца?
rank() over (partition by date_trunc('month', order_date) order by sum(amount) over (partition by user_id)).
  

- [x] `Он использует оконную функцию внутри другой оконной функции.`
  

#### Q17. Вам нужно обновить поле status в таблице orders на ‘cancelled' для всех заказов старше 2020 года. Какой запрос использовать?
  

- [x] `update orders set status = 'cancelled' where year(order_date) < 2020.`
  

#### Q18. Какой запрос позволяет создать обычное представление с фильтрацией по сумме?
  

- [x] `create view revenue_summary as select user_id, sum(price) as total from payments group by user_id having sum(price) > 10000`
  

#### Q19. Что вернёт следующий запрос, если в таблице нет ни одной строки?
SELECT SUM(amount), COUNT(*) FROM transactions
  

- [x] `NULL И О`
  

#### Q20. Почему этот запрос может дать неожиданные результаты?
SELECT category, COUNT (price) FROM products GROUP BY category;
  

- [x] `COUNT(price) не учитывает NULL, и результат может быть занижен`
  

#### Q21. Получите список имен и фамилий сотрудников, которые работают в отделе маркетинга, из таблицы Employees.
  

- [x] `SELECT first_name, last_name FROM Employees WHERE department = 'Marketing';`
  

#### Q22. Добавьте новый столбец email с типом данных VARCHAR(255) в существующую таблицу.
  

- [x] `ALTER TABLE Clients ADD email VARCHAR(255);`
  

#### Q23. Каким будет результат выполнения следующего кода для таблицы Cars, если car_id - первичный ключ?
  

- [x] `Отобразится ошибка`
  

#### Q24. Вы хотите найти заработную плату отделов, у которых общая заработная плата не превышает 700 000 рублей, в таблице Salaries. Какая ошибка допущена в запросе?
SELECT department_id, SUM(salary) AS total_salary FROM Salaries
HAVING total_salary <= 700000 GROUP BY department_id;
  

- [x] `HAVING total_salary <= 700000 стоит перед GROUP BY, а не после него`
- [x] `total_salary <= 700000 вместо SUM(salary) <= 700000`
  

#### Q25. Найдите данные, относящиеся только к левой таблице Orders, в таблицах Orders и Clients, учитывая, что общий столбец между ними — client_id.
  

- [x] `SELECT Orders.order_id FROM Orders LEFT JOIN Clients ON Clients.client_id = Orders.client_id WHERE Clients.client_id IS NULL;`
  

#### Q26. Найдите имена сотрудников, зарплата которых ниже медианной зарплаты всех сотрудников в таблице Employees.
  

- [x] `SELECT first_name, last_name FROM Employees WHERE salary < (SELECT MEDIAN(salary) FROM employees);`
  

#### Q27. Вам нужно создать представление с именем PeopleView с данными из двух таблиц Respondents и Info, в котором будут содержаться возраст, телефоны и адреса респондентов. Какая ошибка допущена в запросе?
CREATE VIEW PeopleView
AS SELECT age, phone_number, address
FROM Respondents, Info
WHERE Respondents.respondent_id=Info.respondent_id;
  

- [x] `Нужно указывать, из каких таблиц взяты данные, т.е. Respondents.age, Respondents.phone_number, Info.address`
  

#### Q28. Вы создали некластеризованный индекс в таблице Products для столбца category, который содержит его записи и адреса соответствующей строки (в основной таблице), в которой находится запись столбца. Какой шаг из перечисленных ниже не совершается при запуске следующего запроса?
CREATE INDEX product_category_index
ON Products (category);
SELECT product_name, category, price
FROM Products
WHERE category= 'electronics';
  

- [x] `Сохранение выбранных значений в дополнительной таблице`
  

#### Q29. Вы создали таблицу:
CREATE TABLE yourtable(x int NOT NULL,
y int NOT NULL,
CONSTRAINT pk_yourtable PRIMARY KEY(x, y));
Выберите, какая команда должна быть первой в процедуре, работающей с ошибками и транзакциями.
 

- [x] `SET XACT ABORT, NOCOUNT ON`
  

#### Q30. У вас есть таблица Orders с миллионом строк и проиндексированным столбцом order_date, который был создан с использованием следующего запроса:
CREATE INDEX order_index ON Orders(order_date);
Каким образом вы будете оптимизировать производительность запроса, который извлекает информацию о последнем заказе для клиента из таблицы?
  

- [x] `Использую подзапрос, чтобы получить последний order_date для клиента, а затем объединю результаты с таблицей Orders, чтобы получить полную информацию о заказе`
  

#### Q31. Напишите SQL-запрос, который выберет все записи из таблицы Customers, у которых имя (name) начинается на букву "A" или "M", и возраст (age) больше 25 лет. Отсортируйте список в порядке убывания возраста.
  

- [x] `SELECT * FROM Customers WHERE (name LIKE 'A%' OR name LIKE 'M%') AND age > 25 ORDER BY age DESC`
  

#### Q32. Вы даете разрешение или запрет на выполнение определенных операций над объектами базы данных компании. Какие операторы вы используете в данном процессе?
  

- [x] `GRANT, REVOKE`
 

#### Q33. Какую задачу может решать данный код?
SELECT product_name,
CASE WHEN (price > 100) THEN 'expensive'
ELSE 'cheap'
END AS product_cost
FROM cd.database;  


- [x] `Получение данных о дорогих и дешевых товарах, где дорогими считаются товары дороже 100 рублей. При этом отобразится таблица с названием товаров в одном столбике и указанием дорогой он или дешевый в другом.`
  

#### Q34. Вам нужен отсортированный в алфавитном порядке список из 10 неповторяющихся имён в таблице group_A. С помощью какого кода может быть решена данная задача?
  

- [x] `SELECT DISTINCT surname FROM group_A ORDER BY surname LIMIT 10;`
  

#### Q35. У вас есть две таблицы: workers и salary. Первая таблица содержит уникальный id сотрудника, его фамилию (surname) и должность (position). Во второй таблице указано: id должности, сама должность и соответствующая ей зарплата.

Вам нужно узнать, сколько зарабатывает каждый сотрудник. Какой вариант кода сможет решить данную задачу?

  
- [x] `SELECT * FROM workers w JOIN salary s ON w.position = s.position;`
  

