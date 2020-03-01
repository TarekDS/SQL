
--People Who Cooperated At Least Three Times

select performer1_id, performer2_id from ADir
where performer1_id = performer2_id
group by performer1_id, performer2_id
having count(*) > = 3

--Ads Performance

1148. Article Views I
select distinct(author_id) as id from views where author_id = viewer_id 
order by author_id asc

--Average Selling Price

select UnitsSold.Product_id, round(sum(prices.Price * UnitsSold.Units)/sum(UnitsSold.Units),2) as Average_Price from UnitsSold left join Prices on UnitsSold.Product_id = Prices.product_id
where UnitsSold.purchase_date between Prices.Start_date and Prices.end_date
group by UnitsSold.product_id

--Big Countries
select name, population, area from World where area > 3000000 or population > 25000000

--Biggest Single Number
select max(num) as num from (
select num from my_numbers
group by num
having count(num) = 1) as t

--Classes More Than 5 Students
select class from Courses 
group by class
having count(class) >= 5

--Consecutive Available Seats
select distinct(a.seat_id) from cinema a join cinema b on a.seat_id = b.seat_id+1
or a.seat_id = b.seat_id-1
where a.free = 'true' and b.free = 'true'

--Customer Placing the Largest Number of Orders
select top 1 customer_number from (
select customer_number, count(customer_number) as c from orders
group by customer_number) a
order by c desc

--Customers Who Never Order
select customers.Name as customers from Customers left join Orders on Customers.id = Orders.customerid
where orders.customerid is null

--Employee Bonus
select Employee.Name, Bonus.bonus from Employee left outer join Bonus on employee.empid = Bonus.empid 
where bonus.bonus < 1000 or bonus is null

--Employees Earning More Than Their Managers
select e.name as Employee from employee e join employee on employee.id = e.managerid

--Find Customer Referee
select name from customer where referee_id <> 2 or referee_id is null

--Find the Team Size
select employee.employee_id, t.team_size from (
select team_id, count(team_id) as team_size from Employee 
group by team_id) t right join Employee
on t.team_id = Employee.team_id

--Consecutive Numbers

select num as ConsecutiveNums from (
select *, lag (logs.num) over (order by id) as previous,
lead (logs.num) over (order by id) as next
from logs) l
where num = previous and previous = next

--Customers Who Bought All Products
select customer_id from Customer 
group by customer_id
having count(distinct(product_key)) = (select distinct(count(product_key)) from product)


--Highest Salary:
select dname as Department, a.name as Employee, Salary from 
(select e.id, e.name, e.salary, e.departmentid, d.name as dname, dense_rank() over (partition by e.departmentid order by salary  desc) salaryrank from employee e join department d on e.departmentid = d.id)a
where salaryrank = 1;

Select Department.Name as Department, Employee.Name as Employee, Employee.Salary as salary from Employee left join Department on Employee.departmentid = Department.id
where
(Employee.salary, Employee.departmentid) in (
select max(salary), Departmentid from Employee
group by DepartmentId)

--Product Sales Analysis
select a.Product_id, f_year as first_year, quantity, price from
(select distinct(min(year) over (partition by product_id)) as f_year, Product_id from Sales) a
left join
Sales s
on s.Product_id = a.Product_id
and s.year = a.f_year

--Rank Scores
select Score, DENSE_RANK () OVER (ORDER BY Score DESC
 ) rank from scores

--Department Top Three Salaries
select d.name as Department, a.Name as Employee, a.salary
from (
select dense_rank() over (partition by Departmentid order by Salary Desc) as S_rank, Departmentid, Name, salary from Employee) a
join Department d
on a.Departmentid = d.id
where a.S_rank <= 3

select count(*) from transactions t right join visits v
on t.transaction_date = v.visit_date
and t.user_id = v.user_id
where transaction_date is null

--Last Person to Fit in the Elevator
select top 1 person_name from (
select person_name, sum(weight) over (order by turn asc) as CW from queue
) a 
where CW <= 1000
order by CW Desc

--unknown problem

select top 1 users.name as results from (
select user_id, count(movie_id) as c from Movie_rating
group by user_id) a join Users
on a.user_id = Users.user_id
order by c Desc;


--Market Analysis
WITH   cte
AS (
select si, case when si is not null then 'yes' else 'no' end as '2nd_item_fav_brand' from (
select u.favorite_brand as fb, i.item_brand as ib, o.seller_id as si , dense_rank() over (partition by seller_id order by order_date) as o_rank from Orders o left join items i
on o.item_id = i.item_id
left join Users u 
on u.user_id = o.seller_id) a
where fb = ib
and o_rank = 2
), cte2 as 

(SELECT 1 AS si, 'no' as '2nd_item_fav_brand'
        UNION ALL
        SELECT si + 1, 'no'
        FROM   cte2
        WHERE  si < 4 
       )
SELECT cte2.si as seller_id, case when cte.[2nd_item_fav_brand] is null then  cte2.[2nd_item_fav_brand]
when cte2.[2nd_item_fav_brand] is not null then cte.[2nd_item_fav_brand] end as [2nd_item_fav_brand]
FROM   cte2
left join
 cte on cte.si = cte2.si
