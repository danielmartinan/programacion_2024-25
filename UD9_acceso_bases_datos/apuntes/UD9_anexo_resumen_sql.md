# Anexo: Resumen de sintaxis SQL

A continuación, se presenta un resumen de las principales instrucciones SQL utilizadas para **crear, consultar, modificar y eliminar datos** en una base de datos. Es importante conocer estos comandos, ya que serán ejecutados mediante JDBC desde Java.

## Creación de base de datos y selección

```sql
CREATE DATABASE nombre_basedatos;
USE nombre_basedatos;
```

## Creación de tablas

```sql
CREATE TABLE productos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    precio DECIMAL(8,2),
    stock INT DEFAULT 0
);
```

Otras características frecuentes:

- `PRIMARY KEY` → Clave primaria.
- `AUTO_INCREMENT` → Aumenta automáticamente el valor del campo (MySQL).
- `NOT NULL` → Campo obligatorio.
- `DEFAULT` → Valor por defecto.

## Inserción de datos

```sql
INSERT INTO productos (nombre, precio, stock)
VALUES ('Ratón inalámbrico', 19.95, 25);
```

Puedes insertar varias filas a la vez:

```sql
INSERT INTO productos (nombre, precio, stock)
VALUES 
('Teclado', 29.99, 15),
('Pantalla', 199.99, 5);
```

## Consultas (`SELECT`)

**Obtener todos los datos:**

```sql
SELECT * FROM productos;
```

**Campos concretos:**

```sql
SELECT nombre, precio FROM productos;
```

**Con condiciones:**

```sql
SELECT * FROM productos WHERE stock > 0;
```

**Ordenación:**

```sql
SELECT * FROM productos ORDER BY precio DESC;
```

**Limitar resultados:**

```sql
SELECT * FROM productos LIMIT 5;
```

**Sentencias con combinación de tablas:**

```sql
SELECT p.nombre, c.nombre AS categoria
FROM productos p
JOIN categorias c ON p.categoria_id = c.id;
```

**Agrupación de datos:**

```sql
SELECT categoria_id, COUNT(*) AS total_productos
FROM productos
GROUP BY categoria_id;
```

**Filtrar grupos:**

```sql
SELECT categoria_id, COUNT(*) AS total_productos
FROM productos
GROUP BY categoria_id
HAVING total_productos > 5;
```

**Subconsultas:**

```sql
SELECT nombre, precio
FROM productos
WHERE precio > (SELECT AVG(precio) FROM productos);
```

## Modificación de registros

**Actualizar un campo:**

```sql
UPDATE productos 
SET stock = 10 
WHERE id = 1;
```

Es importante usar `WHERE` para **evitar actualizar todos los registros**.

## Eliminación de datos

**Eliminar una fila:**

```sql
DELETE FROM productos WHERE id = 3;
```

**Eliminar todos los datos:**

```sql
DELETE FROM productos;
```

## Eliminación de tabla o base de datos

```sql
DROP TABLE productos;
DROP DATABASE nombre_basedatos;
```
