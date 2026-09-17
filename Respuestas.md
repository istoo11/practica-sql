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

![Resultado pregunta](./img/ejercicio01.png)

**Comentario:** He usado `NUMERIC` ya que la columna unit_price esta declarado como un numero real y `ROUND()` necesita de un `Numeric` o un `Decimal` si no el código no funcionaría.
