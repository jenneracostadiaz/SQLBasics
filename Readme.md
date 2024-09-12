
# SQL Básico: Fundamentos y Comandos Principales

## 1. Introducción a SQL
SQL (Structured Query Language) es un lenguaje estándar para la gestión y manipulación de bases de datos relacionales. A continuación, se presentan los comandos básicos que debes conocer para comenzar a trabajar con bases de datos.

## 2. Creación de Tablas

### **CREATE TABLE**
Este comando se utiliza para crear una nueva tabla dentro de una base de datos. Especifica los nombres de las columnas y sus tipos de datos.

```sql
CREATE TABLE nombre_de_tabla (
    columna1 tipo_dato,
    columna2 tipo_dato,
    columna3 tipo_dato,
    PRIMARY KEY (columna1)
);
```

**Ejemplo:**
```sql
CREATE TABLE productos (
    id_producto INT PRIMARY KEY,
    nombre VARCHAR(50),
    precio DECIMAL(10, 2),
    stock INT
);
```



## 3. Insertar Datos

### **INSERT INTO**
Este comando se utiliza para agregar nuevos registros a una tabla. Debes especificar los valores en el mismo orden que aparecen las columnas.

```sql
INSERT INTO nombre_de_tabla (columna1, columna2, columna3) 
VALUES (valor1, valor2, valor3);
```

**Ejemplo:**
```sql
INSERT INTO productos (id_producto, nombre, precio, stock) 
VALUES (1, 'Laptop', 1200.00, 15);
```



## 4. Seleccionar Datos

### **SELECT**
Este es el comando más básico para recuperar datos de una o más tablas. Puedes especificar las columnas que deseas obtener.

```sql
SELECT columna1, columna2 
FROM nombre_de_tabla;
```

**Ejemplo:**
```sql
SELECT nombre, precio 
FROM productos;
```



## 5. Filtrado de Datos

### **WHERE**
El comando `WHERE` se utiliza para filtrar registros que cumplen una condición específica.

```sql
SELECT columna1, columna2 
FROM nombre_de_tabla 
WHERE condición;
```

**Ejemplo:**
```sql
SELECT nombre, precio 
FROM productos 
WHERE precio > 500;
```



## 6. Actualización de Datos

### **UPDATE**
Este comando se utiliza para modificar los valores de uno o más registros existentes en una tabla.

```sql
UPDATE nombre_de_tabla
SET columna1 = nuevo_valor
WHERE condición;
```

**Ejemplo:**
```sql
UPDATE productos
SET stock = 10
WHERE id_producto = 1;
```



## 7. Eliminar Datos

### **DELETE**
El comando `DELETE` se utiliza para eliminar uno o más registros de una tabla.

```sql
DELETE FROM nombre_de_tabla 
WHERE condición;
```

**Ejemplo:**
```sql
DELETE FROM productos 
WHERE id_producto = 10;
```



## 8. Relaciones Entre Tablas

### **INNER JOIN**
El comando `INNER JOIN` se utiliza para combinar registros de dos o más tablas basadas en una condición.

```sql
SELECT columnas
FROM tabla1
INNER JOIN tabla2
ON tabla1.columna_común = tabla2.columna_común;
```

**Ejemplo:**
```sql
SELECT p.nombre, v.cantidad
FROM productos p
INNER JOIN ventas v ON p.id_producto = v.id_producto;
```



## 9. Agregación de Datos

### **SUM, COUNT, AVG**
SQL permite realizar operaciones de agregación para obtener resultados como sumas, promedios o contar registros.

```sql
SELECT SUM(columna), COUNT(columna), AVG(columna)
FROM nombre_de_tabla;
```

**Ejemplo:**
```sql
SELECT SUM(cantidad) AS total_vendido
FROM ventas;
```



## 10. Agrupamiento de Datos

### **GROUP BY**
El comando `GROUP BY` se utiliza para agrupar filas que tienen valores en común en columnas específicas.

```sql
SELECT columna, COUNT(*)
FROM nombre_de_tabla
GROUP BY columna;
```

**Ejemplo:**
```sql
SELECT nombre, SUM(cantidad) AS total_vendido
FROM productos
INNER JOIN ventas ON productos.id_producto = ventas.id_producto
GROUP BY nombre;
```



## 11. Condicionales en Consultas

### **HAVING**
Se utiliza junto con `GROUP BY` para filtrar los grupos según una condición.

```sql
SELECT columna, COUNT(*)
FROM nombre_de_tabla
GROUP BY columna
HAVING condición;
```

**Ejemplo:**
```sql
SELECT nombre, COUNT(id_venta) AS veces_vendido
FROM productos p
INNER JOIN ventas v ON p.id_producto = v.id_producto
GROUP BY nombre
HAVING COUNT(id_venta) > 2;
```



## 12. Ordenar Resultados

### **ORDER BY**
El comando `ORDER BY` se utiliza para ordenar los resultados según una o más columnas, en orden ascendente o descendente.

```sql
SELECT columna1, columna2 
FROM nombre_de_tabla 
ORDER BY columna1 ASC | DESC;
```

**Ejemplo:**
```sql
SELECT nombre, precio 
FROM productos
ORDER BY precio DESC;
```



## 13. Eliminar Tablas

### **DROP TABLE**
El comando `DROP TABLE` se utiliza para eliminar una tabla y sus datos.

```sql
DROP TABLE nombre_de_tabla;
```

**Ejemplo:**
```sql
DROP TABLE ventas;
```

## 14. Actualizar la Estructura de la Tabla

### **ALTER TABLE**
Este comando permite agregar, modificar o eliminar columnas de una tabla existente.

- Agregar una columna:
```sql
ALTER TABLE nombre_de_tabla
ADD nueva_columna tipo_dato;
```

- Eliminar una columna:
```sql
ALTER TABLE nombre_de_tabla
DROP COLUMN nombre_columna;
```

## Conclusión
Estos son los comandos básicos que necesitas para trabajar con SQL en cualquier sistema de bases de datos relacional. Recuerda practicar creando tus propios ejemplos y utilizando estos comandos para fortalecer tu entendimiento de SQL.
