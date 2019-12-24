# SQL
Code SQL Basic

-- select columns from customers --
SELECT 
	FirstName,
	LastName
 FROM customers;

-- QUIZ -- select all columns from invoices -- 
SELECT *
FROM invoices;

 -- select albumid, name, Milliseconds , Bytes from tracks --
SELECT 
	albumid, 
	name, 
	milliseconds,
	bytes 
 FROM tracks;

-- select albumid, name, Milliseconds(เปลี่ยนเป็นนาที โดยหาร 60000.0 และตั้งชื่อ cloumn เป็น mins) , Bytes (เปลี่ยนเป็นmb โดยหาร (1024.0*1024.0)  และตั้งชื่อ cloumn เป็น mb) from tracks --
SELECT
	AlbumId,
	name,
	Milliseconds/60000.0 AS mins,  
	Bytes/(1024.0*1024.0) AS mb 
FROM tracks;

-- select 5 first rows from customews -- 
SELECT*
FROM customers LIMIT 5;

-- cal 5*83 and Name column is result --
SELECT
	(5*83) AS result ;

-- select all customers โดยที่ Country = 'Norway'--
SELECT * 
FROM customers
WHERE Country = 'Norway';

---- select all customers โดยที่ Country = 'Norway' OR 'Belgium'--
SELECT * 
FROM customers
WHERE Country = 'Norway' 
	OR Country = 'Belgium';

-- select all customers โดยที่ Country not 'USA'--
SELECT * 
FROM customers
WHERE Country <> 'USA';

-- select CustomerId,InvoiceDate, total from invoices โดยที่ total>20 -- 
SELECT 
	CustomerId,
	InvoiceDate,
	total
FROM invoices
WHERE total>20;

-- select CustomerId,InvoiceDate, total from invoices โดยที่ total 15 AND 20 --
SELECT 
	CustomerId,
	InvoiceDate,
	total
FROM invoices
WHERE total BETWEEN 15 AND 20;

SELECT 
	CustomerId,
	InvoiceDate,
	total
FROM invoices
WHERE total >=15 AND total <= 20;

-- QUIZ -- select all customers โดยที่ Country='USA' OR 'Brazil' OR 'France' --
SELECT * FROM customers
WHERE Country='USA' OR 'Brazil' OR 'France';

SELECT * FROM customers
WHERE Country IN ('USA' ,'Brazil' , 'France');

-- select all customers โดยที่ company is NULL --
SELECT * FROM customers
WHERE Company IS NULL;

-- select all customers โดยที่ company is NOT NULL -- (NOT=TRUE change to FLUSE) --
SELECT * FROM customers
WHERE Company IS NOT NULL;

------ DATA CLEANING -------
-- select FirstName,LastName,Company from customers โดยที่ Company IS  NULL -- 
SELECT 
	FirstName,
	LastName,
	Company
FROM customers
WHERE Company IS  NULL;

 ---- select FirstName,LastName,Company from customers  โดยที่ Company IS  NULL จะกำหนดเป็น 'End customers' of Name is Company -- 
SELECT 
	FirstName,
	LastName,
	coalesce(Company, 'End customers') AS Company
FROM customers
WHERE Company IS  NULL;

-- select firstname from customers เรียง Z-A --
SELECT 
	FirstName
FROM customers
ORDER BY FirstName DESC;

-- select firstname ,country from customers เรียง country A-Z ก่อน --
SELECT 
	FirstName,
	Country
FROM customers
ORDER BY Country, FirstName;

SELECT 
	FirstName,
	Country
FROM customers
ORDER BY 2,1;
 
 -- select firstname ,country from customers เรียง country แบบ Z-A ก่อน --
SELECT 
	FirstName,
	Country
FROM customers
ORDER BY 2 DESC,1 ;

------ QUIZ-----
-- select  FirstName, Email from customers โดยที่ email LIKE 'L%'--
SELECT 
	FirstName,
	Email
FROM customers
WHERE email LIKE 'L%';

-- select  FirstName, Email from customers โดยที่ email LIKE ‘@gmail.com’--
SELECT 
	FirstName,
 	Email
FROM customers
WHERE email LIKE ‘@gmail.com’;

-- select จำนวน rows country(ไม่นับที่ซ้ำ) from customers --
SELECT count(DISTINCT Country)
FROM customers;

-- select count rows country(ไม่นับที่ซ้ำ) and count all rows country from customers  --
SELECT 
	count(DISTINCT Country),
	count(*)
FROM customers;

-- select count rows customerId(ไม่นับที่ซ้ำ) and count all rows customerId from customers  --
SELECT 
	count(DISTINCT CustomerId),
	count(*)
FROM customers;

-- select Aggregate Functions from invoices --
SELECT 
	AVG(total),
	SUM(total),
	MAX(total),
	MIN(total),
	COUNT(total)
FROM invoices;
-- select Aggregate Functions from invoices ตั้งชื่อ --
SELECT 
	AVG(total) AS mean_invoice,
	SUM(total) AS sum_invoice,
	MAX(total) AS  max_invoice,
	MIN(total) AS min_invoice,
	COUNT(total) AS count_invoice
FROM invoices;

SELECT 
	AVG(total) mean_invoice,
	SUM(total) sum_invoice,
	MAX(total) max_invoice,
	MIN(total) min_invoice,
	COUNT(total) count_invoice
FROM invoices;

-- ปรับค่า ROUND(AVG(total),2) เป็นทศนิยม 2 ตำแหน่ง -- 
SELECT 
	round(AVG(total),2) mean_invoice,
	SUM(total) sum_invoice,
	MAX(total) max_invoice,
	MIN(total) min_invoice,
	COUNT(total) count_invoice
FROM invoices;

-- ปรับค่า UPPER ตัวพิมพ์ใหญ่ and LOWER ตัวพิมพ์เล็ก --
SELECT 
	FirstName,
	upper(FirstName),
	lower(FirstName)
FROM customers;

-- ปรับค่า UPPER ตัวพิมพ์ใหญ่ Country ='USA' --
SELECT*
FROM customers
WHERE upper(Country) ='USA';

-- select firstname ,ROMDOM(FirstName) from customers --
SELECT 
	FirstName,
	random()
FROM customers;

-- select firstname ,ROMDOM(FirstName) ตั้งชื่อเป็น id from customers 5 first rows --
SELECT 
	FirstName,
	random() AS id
FROM customers
ORDER BY id
LIMIT 5;

-- select Country from customers GROUP BY country (นับจำนวนกลุ่ม)--
SELECT 
	Country,COUNT(*) AS n
FROM customers
GROUP BY Country;

-- select Country, State, GROUP BY Country,State --
SELECT 
	Country, 
	State,  COUNT(*) AS n
FROM customers
GROUP BY Country,State;

SELECT 
	Country, 
	State,  COUNT(*) AS n
FROM customers
GROUP BY 1,2;

-- HAVING n >=3 same as WHERE(อยู่หลัง GROUP BY เสมอ ทำการ GROUP BY ก่อน ถึง HAVING) --
SELECT 
	Country, 
	State,  COUNT(*) AS n
FROM customers
GROUP BY 1,2
HAVING n >=3;

-- HAVING n >=3 AND Country<>'USA' -- 
SELECT 
	Country, 
	State,  COUNT(*) AS n
FROM customers
GROUP BY 1,2
HAVING n >=3 AND Country<>'USA';

-- ทำการไม่เอา USA ก่อน แล้ว GROUR BY and HAVING n >=3 --
SELECT 
	Country, 
	State,  COUNT(*) AS n
FROM customers
WHERE Country <> 'USA'
GROUP BY 1,2
HAVING n >=3 ;
 
-- ทำการไม่เอา USA ก่อน แล้ว GROUR BY and HAVING n >=3 ใน n เรียงมาก-น้อย --
SELECT 
	Country, 
	State,  COUNT(*) AS n
FROM customers
WHERE Country <> 'USA'
GROUP BY 1,2
HAVING n >=3 
ORDER BY n DESC;

------ INNER JOIN ------ ตารางมา JOIN กัน -------
-- select A of ArtistId and name JOIN กับ B of Title -- 
SELECT 
	A.ArtistId,
	A.name,
	B.Title
FROM artists AS A
JOIN albums AS B
	ON A.ArtistId = B.ArtistId;

-- select A of ArtistId and name JOIN กับ B of Title โดยที่ ArtistID = 99 -- 
SELECT 
	A.ArtistId,
	A.name,
	B.Title
FROM artists AS A
JOIN albums AS B
	ON A.ArtistId = B.ArtistId
	WHERE A.ArtistId = 99;

 -- select A of ArtistId and name JOIN กับ B of Title JOIN กับ C of name โดยที่ ArtistID = 99 -- JOIN ที่ หัวข้อ and ON ที่ PK=FK --
SELECT 
	A.ArtistId,
	A.name AS ARTIST_NAME,
	B.Title,
	C.name AS TRACK_NAME
FROM artists AS A
JOIN albums AS B
	ON A.ArtistId = B.ArtistId
JOIN tracks AS C
	ON B.AlbumId = C.AlbumId
WHERE A.ArtistId =99;

SELECT 
	A.EmployeeId,
	B.City
FROM employees AS A
JOIN customers AS B
	ON A.EmployeeId = B.SupportRepId;

SELECT 
	A.ArtistId,
	A.name AS ARTIST_NAME,
	B.Title,
	C.name AS TRACK_NAME
FROM artists AS A
JOIN albums AS B
	ON A.ArtistId = B.ArtistId
	AND A.ArtistId = 99
JOIN tracks AS C
	ON B.AlbumId = C.AlbumId;

-สร้าง CASE name is segment ใหม่ ใน total from invoices ตามเงื่อนไข --
SELECT total,
CASE
	WHEN total >= 20 THEN 'Hight'
	WHEN total >=10 THEN 'Medium'
	ELSE 'Low'
END AS segment
FROM invoices
ORDER BY 2;

-- เงื่อนไขซ้อนเงื่อนไข ดึงข้อมูลที่มีค่า MAX ของ bytes from tracks --
SELECT* FROM tracks
WHERE Bytes=(
	SELECT max(Bytes) FROM tracks) ;

-- ดึงข้อมูลของ FirstName,LastName,Address from customers โดยที่ Country='USA' --
SELECT
	FirstName,
	LastName,
	Address
FROM (
	SELECT * FROM customers
	WHERE Country='USA' );

-----กด save as view USA_customers----
-- ลบ USA_customers --
DROP VIEW USA_customers;
