CUE: FUNDAMENTOS DE BASES DE DATOS RELACIONALES
FINAL DRILLING: ARRIENDO DE DVDS
Marcelo Aceituno | Python 0079

--DESARROLLO DEL EJERCICIO:->

--Construye las siguientes consultas:

--Aquellas usadas para insertar, modificar y eliminar un Customer, Staff y Actor.

--Customer
--Insertar un nuevo cliente:
INSERT INTO customer (customer_id, store_id, first_name, last_name, email, address_id, activebool, create_date, last_update)
VALUES (800,800, 'Zacarias', 'Flores del Campo', 'zaca@example.com', 5, true, NOW(), NOW());

--Modificar un cliente existente:
UPDATE customer
SET first_name = 'Jane', last_name = 'Smith', email = 'janesmith@example.com'
WHERE customer_id = 800;

--Eliminar un cliente:
DELETE FROM customer
WHERE customer_id = 800;


--Staff
--Insertar un nuevo empleado:
INSERT INTO staff (first_name, last_name, address_id, email, store_id, active, username, password)
VALUES ('Elvis', 'Cocho', 10, 'elvis.cocho@example.com', 1, true, 'elvisc', 'mypassword');

--Modificar un empleado existente:
UPDATE staff
SET first_name = 'Elvis', last_name = 'Williams', email = 'elvis.williams@example.com'
WHERE staff_id = 10;

--Eliminar un empleado:
DELETE FROM staff
WHERE staff_id = 10;


--Actor
--Insertar un nuevo actor:
INSERT INTO actor (first_name, last_name)
VALUES ('Jonh', 'Cena');

--Modificar un actor existente:
UPDATE actor
SET first_name = 'Otro', last_name = 'Nombre'
WHERE actor_id = 10;

--Eliminar un actor:
DELETE FROM actor
WHERE actor_id = 200;


------------------
--Listar todas las “rental” con los datos del “customer” dado un año y mes.
SELECT 
	cu.first_name AS FirstName, 
	cu.last_name AS LastName, 
	cu.email AS email, 
	re.rental_id AS Rental_ID,
	re.inventory_id AS Inventory_ID,
	re.rental_date AS Rental_Date
FROM customer cu
JOIN rental re
ON cu.customer_id = re.customer_id
WHERE EXTRACT(MONTH FROM re.rental_date) = 10 AND EXTRACT(YEAR FROM re.rental_date) = 2006;
------


--Listar Número, Fecha (payment_date) y Total (amount) de todas las “payment”.
SELECT payment_id AS Número, payment_date AS Fecha, amount AS Total
FROM payment;


--Listar todas las “film” del año 2006 que contengan un (rental_rate) mayor a 4.0.
SELECT title, release_year, rental_rate
FROM film
WHERE release_year = 2006 AND rental_rate > 4.0;



------------------------------------------
DICCIONARIO DE DATOS->

1. Tabla: actor
Columnas:
	actor_id: INT, no nulo
	first_name: VARCHAR(45), no nulo
	last_name: VARCHAR(45), no nulo
	last_update: TIMESTAMP, no nulo

2. Tabla: address
Columnas:
	address_id: INT, no nulo
	address: VARCHAR(50), no nulo
	address2: VARCHAR(50), nulo
	district: VARCHAR(20), no nulo
	city_id: SMALLINT, no nulo
	postal_code: VARCHAR(10), nulo
	phone: VARCHAR(20), no nulo
	last_update: TIMESTAMP, no nulo

3. Tabla: category
Columnas:
	category_id: TINYINT, no nulo
	name: VARCHAR(25), no nulo
	last_update: TIMESTAMP, no nulo

4. Tabla: city
Columnas:
	city_id: INT, no nulo
	city: VARCHAR(50), no nulo
	country_id: SMALLINT, no nulo
last_update: TIMESTAMP, no nulo

5. Tabla: country
Columnas:
	country_id: INT, no nulo
	country: VARCHAR(50), no nulo
	last_update: TIMESTAMP, no nulo

6. Tabla: customer
Columnas:
	customer_id: INT, no nulo
	store_id: TINYINT, no nulo
	first_name: VARCHAR(45), no nulo
	last_name: VARCHAR(45), no nulo
	email: VARCHAR(50), nulo
	address_id: SMALLINT, no nulo
	active: TINYINT(1), no nulo
	create_date: DATE, no nulo
	last_update: TIMESTAMP, nulo

7. Tabla: film
Columnas:
	film_id: INT, no nulo
	title: VARCHAR(255), no nulo
	description: TEXT, nulo
	release_year: YEAR, nulo
	language_id: TINYINT, no nulo
	original_language_id: TINYINT, nulo
	rental_duration: TINYINT, no nulo
	rental_rate: DECIMAL(4,2), no nulo
	length: SMALLINT, nulo
	replacement_cost: DECIMAL(5,2), no nulo
	rating: ENUM('G','PG','PG-13','R','NC-17'), nulo
	special_features: 
	SET('Trailers','Commentaries','Deleted Scenes',
	'Behind the 	Scenes'), nulo
	last_update: TIMESTAMP, no nulo

8. Tabla: film_actor
Columnas:
	actor_id: INT, no nulo
	film_id: SMALLINT, no nulo
	last_update: TIMESTAMP, no nulo

9. Tabla: film_category
Columnas:
	film_id: SMALLINT, no nulo
	category_id: TINYINT, no nulo
	last_update: TIMESTAMP, no nulo

10. Tabla: inventory
Columnas:
	inventory_id: INT, no nulo
	film_id: SMALLINT, no nulo
	store_id: TINYINT, no nulo
	last_update: TIMESTAMP, no nulo

11. Tabla: language
Columnas:
	language_id: TINYINT, no nulo
	name: CHAR(20), no nulo
	last_update: TIMESTAMP, no nulo

12. Tabla: payment
Columnas:
	payment_id: INT, no nulo
	customer_id: SMALLINT, no nulo
	staff_id: TINYINT, no nulo
	rental_id: INT, nulo
	amount: DECIMAL(5,2), no nulo
	payment_date: DATETIME, no nulo
	last_update: TIMESTAMP, nulo

13. Tabla: rental
Columnas:
	rental_id: INT, no nulo
	rental_date: DATETIME, no nulo
	inventory_id: INT, no nulo
	customer_id: SMALLINT, no nulo
	return_date: DATETIME, nulo
	staff_id: TINYINT, no nulo
last_update: TIMESTAMP, no nulo

14. Tabla: staff
Columnas:
	staff_id: TINYINT, no nulo
	first_name: VARCHAR(45), no nulo
	last_name: VARCHAR(45), no nulo
	address_id: SMALLINT, no nulo
	email: VARCHAR(50), nulo
	store_id: TINYINT, no nulo
	active: TINYINT(1), no nulo
	username: VARCHAR(16), no nulo
	password: VARCHAR(40), nulo
	last_update: TIMESTAMP, no nulo
	picture: BLOB, nulo

15. Tabla: store
Columnas:
	store_id: TINYINT, no nulo
	manager_staff_id: TINYINT, no nulo
	address_id: SMALLINT, no nulo
	last_update: TIMESTAMP, no nulo
------------------------------------------------









