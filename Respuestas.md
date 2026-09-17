## Pregunta 01 — Catálogo comercial activo

**Enunciado:** Obtén los productos que no están descatalogados y cuyo precio unitario esté entre 10 y 50 euros, ambos incluidos. Muestra el nombre del producto y su precio redondeado a dos decimales, ordenado de mayor a menor precio.

**Consulta:**

```sql
select 
	product_name as nombre,
	ROUND(unit_price::NUMERIC ,2) as precio
from products
where 
	discontinued = 0 and 
	unit_price between 10 and 50
order by
	unit_price desc;
```

**Resultado:**

![Resultado pregunta](./img/Ejercicio01.png)

**Comentario:** He usado `NUMERIC` ya que la columna unit_price esta declarado como un numero real y `ROUND()` necesita de un `Numeric` o un `Decimal` si no el código no funcionaría.

## Pregunta 02 — Concentración geográfica de la cartera

**Enunciado:** Cuenta cuántos clientes hay en cada país y muestra únicamente aquellos países con 5 o más clientes, ordenados de mayor a menor. Indica también cuántas ciudades distintas hay en cada uno de esos países.

**Consulta:**

```sql
select 	
	country as pais,
	COUNT(country) as numero_clientes,
	COUNT(DISTINCT city) as ciudades_distintas
from customers
group by 
	country
having 
	COUNT(country) >= 5
order by 
	numero_clientes desc;
```

**Resultado:**

![PONER FOTO EJ 02](./img/Ejercicio01.pn)

**Comentario:**  (HACER COMENTARIO)

## Pregunta 03 — Alerta de reposición

**Enunciado:** Localiza los productos activos cuyas unidades en stock sean inferiores o iguales a su nivel de reposición. Muestra el nombre, las unidades en stock, el nivel de reposición, las unidades ya pedidas al proveedor y una columna de texto que indique `CRÍTICO` cuando el stock sea 0 y `AVISO` en el resto de casos.

**Consulta:**

```sql
SELECT 
	product_name as nombre,
	units_in_stock as stock,
	reorder_level as nivel_de_reposicion,
	units_on_order as unidades_pedidas,
	CASE WHEN
		units_in_stock = 0 THEN 'CRITICO'
		ELSE 'AVISO'
	END AS categoria
FROM products 
WHERE 
	units_in_stock <= reorder_level;
```

**Resultado:**

![PONER FOTO EJ 03](./img/Ejercicio01.pn)

**Comentario:**  (HACER COMENTARIO)

## Pregunta 04 — Ficha completa de producto

**Enunciado:** Para los productos suministrados por empresas de Italia, Francia o España, muestra el nombre del producto, el nombre de la categoría, el nombre del proveedor, su país y su ciudad. Ordena por país y, dentro de cada país, por nombre de producto.

**Consulta:**

```sql
SELECT 
	p.product_name as nombre,
	c.category_name as categoria,
	s.company_name as nombre_empresa,
	s.country as pais_envio,
	s.city as ciudad_envio
FROM products as p
	inner join categories as c on p.category_id = c.category_id
	inner join suppliers as s on p.supplier_id = s.supplier_id
where
	s.country in ('Spain','Italy','France')
order by s.country,p.product_name;
```

**Resultado:**

![PONER FOTO EJ 04](./img/Ejercicio01.pn)

**Comentario:**  (HACER COMENTARIO)

## Pregunta 05 — Detalle valorizado de un pedido

**Enunciado:** Muestra, para ese pedido, el nombre del producto, el precio unitario aplicado, la cantidad, el descuento y el importe final de cada línea. Añade el nombre del cliente y la fecha del pedido.

**Consulta:**

```sql
SELECT
	c.contact_name,
	o.order_date,
	p.product_name,
	p.unit_price,
	od.quantity,
	od.discount,
	ROUND((p.unit_price::numeric) * od.quantity * (1 - od.discount::numeric), 2)
FROM ORDERS AS O
	INNER JOIN ORDER_DETAILS AS OD ON OD.ORDER_ID = O.ORDER_ID
	INNER JOIN PRODUCTS AS P ON OD.PRODUCT_ID = P.PRODUCT_ID
	INNER join customers as c on c.customer_id = o.customer_id 
WHERE
	o.ORDER_ID = 10248;
```

**Resultado:**

![PONER FOTO EJ 05](./img/Ejercicio01.pn)

**Comentario:**  (HACER COMENTARIO)

## Pregunta 06 — Ranking de categorías por facturación

**Enunciado:** Calcula la facturación total de cada categoría durante toda la historia de la compañía. Muestra el nombre de la categoría, el número de líneas de pedido que ha generado, el número de productos distintos vendidos y la facturación total. Incluye únicamente las categorías que superen los 100.000 euros de facturación, ordenadas de mayor a menor.

**Consulta:**

```sql

```

**Resultado:**

![PONER FOTO EJ 06](./img/Ejercicio01.pn)

**Comentario:**  (HACER COMENTARIO)
