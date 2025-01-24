Задание 5!!
Вывести покупателей с количеством осуществленных покупок

SELECT 
    c.first_name AS Имя,
    c.last_name AS Фамилия,
    COUNT(o.id) AS Количество_покупок
FROM 
    Customers c
JOIN 
    Orders o ON c.id = o.customer_id
GROUP BY 
    c.id, c.first_name, c.last_name;

Общую стоимость товаров для каждого покупателя и отсортировать результат по убыванию
SELECT 
    c.first_name AS Имя,
    c.last_name AS Фамилия,
    SUM(p.price * oi.quantity) AS Общая_стоимость
FROM 
    Customers c
JOIN 
    Orders o ON c.id = o.customer_id
JOIN 
    Order_Items oi ON o.id = oi.order_id
JOIN 
    Products p ON oi.product_id = p.id
GROUP BY 
    c.id, c.first_name, c.last_name
ORDER BY 
    Общая_стоимость DESC;

Получить покупателей, купивших только один товар
SELECT 
    c.first_name AS Имя,
    c.last_name AS Фамилия
FROM 
    Customers c
JOIN 
    Orders o ON c.id = o.customer_id
JOIN 
    Order_Items oi ON o.id = oi.order_id
GROUP BY 
    c.id, c.first_name, c.last_name
HAVING 
    COUNT(DISTINCT oi.product_id) = 1;
