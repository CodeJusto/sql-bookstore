1. SELECT isbn FROM editions AS e INNER JOIN publishers AS p ON (e.publisher_id=p.id) WHERE p.name = 'Random House';

2. SELECT isbn, title FROM editions AS e INNER JOIN publishers AS p ON (e.publisher_id=p.id) INNER JOIN books AS b ON (b.id = e.book_id) WHERE p.name = 'Random House';

3. SELECT e.isbn, title, stock, cost AS "Retail Price" FROM editions AS e INNER JOIN publishers AS p ON (e.publisher_id=p.id) INNER JOIN books AS b ON (b.id = e.book_id) INNER JOIN stock AS s ON (s.isbn = e.isbn) WHERE p.name = 'Random House';

4. SELECT e.isbn, title, stock, cost AS "Retail Price" FROM editions AS e INNER JOIN publishers AS p ON (e.publisher_id=p.id) INNER JOIN books AS b ON (b.id = e.book_id) INNER JOIN stock AS s ON (s.isbn = e.isbn) WHERE p.name = 'Random House' AND s.stock !=0;

5. SELECT e.isbn, title, stock, cost AS "Retail Price", 
  CASE WHEN e.type = 'h' THEN 'hardcover' 
    WHEN e.type = 'p' THEN 'paperback' 
  END AS Type 
  FROM editions AS e 
  INNER JOIN publishers AS p ON (e.publisher_id=p.id) 
  INNER JOIN books AS b ON (b.id = e.book_id) 
  INNER JOIN stock AS s ON (s.isbn = e.isbn) 
  WHERE p.name = 'Random House' AND s.stock != 0;

6. SELECT title, publication FROM books AS b LEFT OUTER JOIN editions AS e ON b.id=e.book_id;

7. SELECT sum(stock) FROM stock;

8. SELECT ROUND(AVG(cost),2) AS "Average Cost", ROUND(AVG(retail),2) AS "Average Retail", ROUND(AVG(retail - cost),2) AS "Average Profit" FROM stock;

9. SELECT e.book_id, stock AS "Total Stock" FROM stock AS s INNER JOIN editions AS e ON (s.isbn=e.isbn) ORDER BY "Total Stock" DESC LIMIT 1;

10. SELECT a.id, CONCAT(first_name, ' ', last_name) AS "Full Name", COUNT(b.id) AS "Number of Books" FROM authors AS a INNER JOIN books AS b  ON (b.author_id = a.id) GROUP BY a.id;