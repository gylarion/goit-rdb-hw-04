create database LibraryManagement;
use LibraryManagement;
create table authors(
	author_id INT auto_increment primary key,
    author_name varchar(255)
);
create table genres(
	genre_id int auto_increment primary key,
    genre_name varchar(255)
);
CREATE TABLE books(
	book_id int auto_increment primary key,
    title varchar(255),
    publication_year year,
    author_id int,
    genre_id int,
    foreign key (author_id) references authors(author_id),
    foreign key (genre_id) references genres(genre_id)
);
create table users(
	user_id int auto_increment primary key,
    username varchar(255),
    email varchar(255)
);
create table borrowed_books (
	borrow_id int auto_increment primary key,
    book_id int,
    user_id int,
    borrow_date date,
    return_date date,
    foreign key (book_id) references books(book_id),
    foreign key (user_id) references users(user_id)
);
INSERT INTO authors (author_name) VALUES 
('George Orwell'),
('J.K. Rowling');

INSERT INTO genres (genre_name) VALUES 
('Dystopian'),
('Fantasy');

INSERT INTO books (title, publication_year, author_id, genre_id) VALUES 
('1984', 1949, 1, 1),
('Harry Potter', 1997, 2, 2);

INSERT INTO users (username, email) VALUES 
('user1', 'user1@gmail.com'),
('user2', 'user2@gmail.com');

INSERT INTO borrowed_books (book_id, user_id, borrow_date, return_date) VALUES 
(1, 1, '2024-01-01', '2024-01-10'),
(2, 2, '2024-02-01', '2024-02-15');

use hw3;

SELECT * 
FROM order_details
INNER JOIN orders ON order_details.order_id = orders.id
INNER JOIN customers ON orders.customer_id = customers.id
INNER JOIN employees ON orders.employee_id = employees.employee_id
INNER JOIN shippers ON orders.shipper_id = shippers.id
INNER JOIN products ON order_details.product_id = products.id
INNER JOIN categories ON products.category_id = categories.id
INNER JOIN suppliers ON products.supplier_id = suppliers.id;

SELECT COUNT(*) as total_rows
FROM order_details
INNER JOIN orders ON order_details.order_id = orders.id
INNER JOIN customers ON orders.customer_id = customers.id
INNER JOIN employees ON orders.employee_id = employees.employee_id
INNER JOIN shippers ON orders.shipper_id = shippers.id
INNER JOIN products ON order_details.product_id = products.id
INNER JOIN categories ON products.category_id = categories.id
INNER JOIN suppliers ON products.supplier_id = suppliers.id;

SELECT COUNT(*) as total_rows
FROM order_details
LEFT JOIN orders ON order_details.order_id = orders.id
LEFT JOIN customers ON orders.customer_id = customers.id
LEFT JOIN employees ON orders.employee_id = employees.employee_id
LEFT JOIN shippers ON orders.shipper_id = shippers.id
LEFT JOIN products ON order_details.product_id = products.id
LEFT JOIN categories ON products.category_id = categories.id
LEFT JOIN suppliers ON products.supplier_id = suppliers.id;

SELECT COUNT(*) as total_rows
FROM order_details
RIGHT JOIN orders ON order_details.order_id = orders.id
RIGHT JOIN customers ON orders.customer_id = customers.id
RIGHT JOIN employees ON orders.employee_id = employees.employee_id
RIGHT JOIN shippers ON orders.shipper_id = shippers.id
RIGHT JOIN products ON order_details.product_id = products.id
RIGHT JOIN categories ON products.category_id = categories.id
RIGHT JOIN suppliers ON products.supplier_id = suppliers.id;

SELECT 
    categories.name AS category_name,
    COUNT(*) AS row_count,
    AVG(order_details.quantity) AS avg_quantity
FROM order_details
INNER JOIN orders ON order_details.order_id = orders.id
INNER JOIN customers ON orders.customer_id = customers.id
INNER JOIN employees ON orders.employee_id = employees.employee_id
INNER JOIN shippers ON orders.shipper_id = shippers.id
INNER JOIN products ON order_details.product_id = products.id
INNER JOIN categories ON products.category_id = categories.id
INNER JOIN suppliers ON products.supplier_id = suppliers.id
WHERE employees.employee_id > 3 AND employees.employee_id <= 10
GROUP BY categories.name
HAVING AVG(order_details.quantity) > 21
ORDER BY row_count DESC
LIMIT 4 OFFSET 1;