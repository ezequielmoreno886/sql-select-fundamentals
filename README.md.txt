SQL Select Fundamentals

Objetivo

Este ejercicio tiene como finalidad practicar consultas básicas SQL utilizando la instrucción SELECT, la selección específica de columnas y el uso de alias para generar resultados más comprensibles para usuarios del negocio.

¿Por qué es mala práctica usar SELECT * en producción?
Aunque SELECT * resulta útil durante la exploración inicial de una tabla o en pruebas rápidas, en entornos productivos suele considerarse una mala práctica por varias razones.

1. Rendimiento
Cuando se utiliza SELECT *, la base de datos recupera todas las columnas de la tabla, incluso aquellas que no son necesarias para el análisis o reporte.

Por ejemplo:

SELECT *
FROM sales;

Si el informe únicamente requiere identificar al cliente y el importe de la venta, sería más eficiente consultar:

SQL

SELECT customer_id, total_amount
FROM sales;

De esta manera se reduce la cantidad de datos transferidos, se consume menos memoria y se mejora el tiempo de respuesta de la consulta.

2. Mantenibilidad

Una consulta con SELECT * depende totalmente de la estructura actual de la tabla.

Si en el futuro se agrega una nueva columna a la tabla sales, el resultado de la consulta cambiará automáticamente sin necesidad de modificar el código. Esto puede afectar reportes, aplicaciones o procesos automatizados que esperan recibir una cantidad determinada de columnas.

Por el contrario, especificar explícitamente las columnas hace que las consultas sean más estables y fáciles de mantener.

3. Seguridad y exposición de datos

Al utilizar SELECT * existe el riesgo de exponer información que no debería mostrarse a ciertos usuarios.

Por ejemplo, si una tabla incorpora posteriormente campos sensibles como:

customer_phone
customer_address
credit_card_number

una consulta con SELECT * devolvería automáticamente esa información.

Seleccionar únicamente las columnas necesarias ayuda a proteger los datos y aplicar el principio de mínimo acceso.

¿Por qué son importantes los alias para un stakeholder no técnico?

Los nombres de las columnas suelen estar diseñados para desarrolladores o administradores de bases de datos. Sin embargo, las personas de áreas como Finanzas, Ventas o Marketing necesitan reportes con nombres fáciles de interpretar.

Por ejemplo, una columna llamada:
total_amount

puede resultar poco intuitiva para algunos usuarios de negocio.

Mediante el uso de alias se puede presentar la misma información de forma más clara:

SELECT total_amount AS monto_total
FROM sales;

El resultado aparecerá con el encabezado:

monto_total
2400.00
140.00
450.00

Ahora cualquier persona del departamento financiero puede comprender inmediatamente que se trata del importe total de cada venta.

Beneficios de utilizar alias

Mejoran la comprensión de los reportes.
Reducen la necesidad de conocimientos técnicos.
Facilitan la comunicación entre áreas técnicas y de negocio.
Permiten adaptar los nombres de las columnas al idioma de los usuarios finales.
Hacen más legibles los resultados de consultas complejas.

Ejemplo práctico

SELECT
    order_date,
    product_name,
    quantity
FROM sales;

Consulta utilizando alias:

SELECT
    order_date AS fecha_pedido,
    product_name AS nombre_producto,
    quantity AS cantidad_unidades
FROM sales;

Resultado esperado:
fecha_pedido	nombre_producto	cantidad_unidades
2024-01-05	Laptop Pro 15	2
2024-01-08	Mouse Inalámbrico	5

Los alias convierten nombres técnicos en etiquetas comprensibles para cualquier stakeholder, mejorando la interpretación y el valor de los datos.