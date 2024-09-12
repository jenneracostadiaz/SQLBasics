Para un negocio de carwash, podemos tener dos tablas principales: `clientes` y `servicios`. Estas tablas estarán relacionadas para llevar un control de los clientes y los servicios que solicitan.

### Creación de las tablas:

```sql
-- Tabla de clientes
CREATE TABLE clientes (
    id_cliente INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50),
    apellido VARCHAR(50),
    telefono VARCHAR(15),
    email VARCHAR(50)
);

-- Tabla de servicios
CREATE TABLE servicios (
    id_servicio INT PRIMARY KEY AUTO_INCREMENT,
    tipo VARCHAR(30), -- Tipos de servicio: Lavado Completo, Lavado Exterior, etc.
    precio DECIMAL(6, 2),
    fecha DATE,
    id_cliente INT,
    FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente)
);
```

### Agregar 15 filas a cada tabla:

#### Insertar clientes:

```sql
INSERT INTO clientes (nombre, apellido, telefono, email)
VALUES
('Carlos', 'Ramos', '999999999', 'carlos@gmail.com'),
('María', 'Gonzales', '988888888', 'maria@gmail.com'),
('Juan', 'Pérez', '977777777', 'juan@gmail.com'),
('Ana', 'Salazar', '966666666', 'ana@gmail.com'),
('Luis', 'Torres', '955555555', 'luis@gmail.com');
```

#### Insertar servicios:

```sql
INSERT INTO servicios (tipo, precio, fecha, id_cliente)
VALUES
('Lavado Completo', 25.00, '2024-09-01', 1),
('Lavado Exterior', 15.00, '2024-09-02', 2),
('Lavado Completo', 25.00, '2024-09-03', 3),
('Pulido y Cera', 40.00, '2024-09-04', 4),
('Lavado Exterior', 15.00, '2024-09-05', 5),
('Lavado Completo', 25.00, '2024-09-06', 3),
('Pulido y Cera', 40.00, '2024-09-07', 2),
('Lavado Completo', 25.00, '2024-09-08', 1),
('Lavado Exterior', 15.00, '2024-09-09', 4),
('Pulido y Cera', 40.00, '2024-09-10', 3),
('Lavado Completo', 25.00, '2024-09-11', 4),
('Lavado Exterior', 15.00, '2024-09-12', 5),
('Pulido y Cera', 40.00, '2024-09-13', 2),
('Lavado Completo', 25.00, '2024-09-14', 3),
('Lavado Exterior', 15.00, '2024-09-15', 1);
```

### Consultas SQL:

#### 1. Consulta básica: Obtener todos los servicios realizados
```sql
SELECT id_servicio, tipo, precio FROM servicios;
SELECT DISTINCT tipo, precio FROM servicios; -- Si no queremos que se repitan los datos
```

#### 2. Consulta con `JOIN`: Mostrar los clientes junto a los tipos de servicio que solicitaron
```sql
SELECT clientes.nombre, clientes.apellido, servicios.tipo, servicios.fecha
FROM clientes
JOIN servicios ON clientes.id_cliente = servicios.id_cliente;
```

#### 3. Consulta con filtro y función de agregación: Mostrar el total gastado por cada cliente
```sql
SELECT clientes.nombre, clientes.apellido, SUM(servicios.precio) AS total_gastado
FROM clientes
JOIN servicios ON clientes.id_cliente = servicios.id_cliente
GROUP BY clientes.id_cliente;
```

#### 4. Consulta avanzada: Mostrar los tipos de servicio con la cantidad de veces que se realizaron, ordenados por la frecuencia
```sql
SELECT servicios.tipo, COUNT(servicios.id_servicio) AS cantidad
FROM servicios
GROUP BY servicios.tipo
ORDER BY cantidad DESC;
```

#### 5. Consulta con subconsulta: Mostrar los clientes que han realizado el servicio "Pulido y Cera" más de una vez
```sql
SELECT nombre, apellido
FROM clientes
WHERE id_cliente IN (
    SELECT id_cliente
    FROM servicios
    WHERE tipo = 'Pulido y Cera'
    GROUP BY id_cliente
    HAVING COUNT(id_servicio) > 1
);
```

#### 6. 

Estas consultas permiten obtener información desde lo más básico hasta análisis más avanzados sobre los servicios solicitados y el comportamiento de los clientes. ¡Avísame si necesitas más detalles o ejemplos!