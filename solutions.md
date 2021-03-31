                            
                                                Practice joins



PROBLEM 1 
SELECT * FROM invoice i JOIN invoice_line il ON il.invoice_id = i.invoice_id WHERE il.unit_price > 0.99

PROBLEM 2
SELECT i.invoice_date, c.first_name, c.last_name, i.total FROM invoice i JOIN customer c ON i.customer_id = c.customer_id

PROBLEM 3
SELECT c.first_name, c.last_name, e.first_name, e.last_name FROM customer c JOIN employee e ON c.support_rep_id = e.employee_id

PROBLEM 4
SELECT al.title, ar.name FROM album al JOIN artist ar ON al.artist_id = ar.artist_id

PROBLEM 5
SELECT pt.track_id FROM playlist_track pt JOIN playlist p ON p.playlist_id = pt.playlist_id WHERE p.name = 'Music'

PROBLEM 6
SELECT t.name FROM track t JOIN playlist_track pt ON pt.track_id = t.track_id WHERE pt.playlist_id = 5

PROBLEM 7
SELECT t.name, p.name FROM track t JOIN playlist_track pt ON t.track_id = pt.track_id JOIN playlist p ON pt.playlist_id = p.playlist_id

PROBLEM 8 
SELECT t.name, a.title FROM track t JOIN album a ON t.album_id = a.album_id JOIN genre g ON g.genre_id = t.genre_id WHERE g.name = 'Alternative & Punk'

-------------------------------------------------------------------------------------------------------------
                                              Practice nested queries



PROBLEM 1
SELECT * FROM invoice WHERE invoice_id IN ( SELECT invoice_id FROM invoice_line WHERE unit_price > 0.99 );

PROBLEM 2
SELECT * FROM playlist_track WHERE playlist_id IN ( SELECT playlist_id FROM playlist WHERE name = 'Music' );

PROBLEM 3
SELECT name FROM track WHERE track_id IN ( SELECT track_id FROM playlist_track WHERE playlist_id = 5 );

PROBLEM 4
SELECT * FROM track WHERE genre_id IN ( SELECT genre_id FROM genre WHERE name = 'Comedy' );

PROBLEM 5
SELECT * FROM track WHERE album_id IN ( SELECT album_id FROM album WHERE title = 'Fireball' );

PROBLEM 6
SELECT * FROM track WHERE album_id IN ( SELECT album_id FROM album WHERE artist_id IN ( SELECT artist_id FROM artist WHERE name = 'Queen') ); 

------------------------------------------------------------------------------------------------------------------
                                              Practice updating Rows



PROBLEM 1
UPDATE customer SET fax = null WHERE fax IS NOT null;

PROBLEM 2 
UPDATE customer SET company = 'Self' WHERE company IS null;

PROBLEM 3
UPDATE customer SET last_name = 'Thompson' WHERE first_name = 'Julia' AND last_name = 'Barnett';

PROBLEM 4
UPDATE customer SET support_rep_id = 4 WHERE email = 'luisrojas@yahoo.cl';

PROBLEM 5
UPDATE track SET composer = 'The darkness around us' WHERE genre_id = ( SELECT genre_id FROM genre WHERE name = 'Metal' ) AND composer IS null;

--------------------------------------------------------------------------------------------------------------------
                                                    GROUP BY


PROBLEM 1
SELECT COUNT(*), g.name FROM track t JOIN genre g ON t.genre_id = g.genre_id GROUP BY g.name;

PROBLEM 2
SELECT COUNT(*), g.name FROM track t JOIN genre g ON g.genre_id = t.genre_id WHERE g.name = 'Pop' OR g.name = 'Rock' GROUP BY g.name;

PROBLEM 3
SELECT ar.name, COUNT(*) FROM album al JOIN artist ar ON ar.artist_id = al.artist_id GROUP BY ar.name;


----------------------------------------------------------------------------------------------------------------------
                                                    Use Distinct



PROBLEM 1
SELECT DISTINCT composer FROM track;

PROBLEM 2
SELECT DISTINCT billing_postal_code FROM invoice;

PROBLEM 3
SELECT DISTINCT company FROM customer;


--------------------------------------------------------------------------------------------------------------------------
                                                DELETE ROWS


PREP WORK

CREATE TABLE practice_delete ( name TEXT, type TEXT, value INTEGER );
INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'bronze', 50);
INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'bronze', 50);
INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'bronze', 50);
INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'silver', 100);
INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'silver', 100);
INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'gold', 150);
INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'gold', 150);
INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'gold', 150);
INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'gold', 150);

SELECT * FROM practice_delete;


PROBLEM 1
DELETE FROM practice_delete WHERE type = 'bronze';

PROBLEM 2
DELETE FROM practice_delete WHERE type = 'silver';

PROBLEM 3
DELETE FROM practice_delete WHERE value = 150;


------------------------------------------------------------------------------------------------------------------------------
                                            eCommerce



PORBLEM 1
CREATE TABLE e_commerce (
  	e_commerce SERIAL PRIMARY KEY,
    users VARCHAR(250),
    email VARCHAR(250)
);

CREATE TABLE products (
  product_id SERIAL PRIMARY KEY, 
  name VARCHAR(250),
  price INT
  );

CREATE TABLE orders (
  order_ID SERIAL PRIMARY KEY,
  order_number INT,
  order_price INT
  );


PROBLEM 2
e_commerce values 
INSERT INTO e_commerce (users, email) VALUES ('Hammy234_', 'insertEmailHere@notreal.com');

INSERT INTO e_commerce (users, email) VALUES ('PhadedTorch', 'insertEmailHere@notreal.com');

INSERT INTO e_commerce (users, email) VALUES ('QuarthPow', 'insertEmailHere@notreal.com');


products values 
INSERT INTO products (name, price) VALUES ('PS4', 250);

INSERT INTO products (name, price) VALUES ('Gaming labtop', 1400);

INSERT INTO products (name, price) VALUES ('XBox One', 250);


orders values
INSERT INTO orders (order_number, order_price) VALUES (1, 1400);

INSERT INTO orders (order_number, order_price) VALUES (2, 250);

INSERT INTO orders (order_number, order_price) VALUES (3, 250);



PROBLEM 3
SELECT * FROM products

SELECT * FROM orders

SELECT DISTINCT orders.order_price FROM orders

ALTER TABLE orders
ADD product_id INT;


PROBLEM 4
ALTER TABLE orders DROP FOREIGN KEY (product_id) REFERENCES products(product_id)

ALTER TABLE orders ADD FOREIGN KEY (product_id) REFERENCES products(product_id)

PROBLEM 5
Updates Orders with Product Ids
 update orders
 set product_id = products.product_id
 from products 
 where products.product_id = orders.order_id

