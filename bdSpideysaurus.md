**Ejemplo de base de datos NoSQL (MongoDB) para una tienda de juguetes de dinosaurios**

## 📌 Base de Datos:

`TiendaDinosaurios`

Dentro de esta base de datos se pueden crear las siguientes **colecciones**:

---

# 🦖 Colección: Productos

### Documento Ejemplo:

```json
{
  "_id": 1,
  "nombre": "T-Rex Gigante",
  "categoria": "Figura de acción",
  "material": "Plástico",
  "precio": 499.99,
  "stock": 15,
  "edad_recomendada": 5,
  "marca": "DinoToy",
  "activo": true
}
```

### Atributos y Tipo de Datos:

| Atributo         | Tipo de Dato |
| ---------------- | ------------ |
| _id              | Entero       |
| nombre           | String       |
| categoria        | String       |
| material         | String       |
| precio           | Decimal      |
| stock            | Entero       |
| edad_recomendada | Entero       |
| marca            | String       |
| activo           | Boolean      |

---

# 🦕 Colección: Clientes

### Documento Ejemplo:

```json
{
  "_id": 101,
  "nombre": "Carlos Ramírez",
  "correo": "carlos@gmail.com",
  "telefono": "6561234567",
  "direccion": "Av. Principal #45",
  "fecha_registro": "2026-04-27"
}
```

### Atributos y Tipo de Datos:

| Atributo       | Tipo de Dato |
| -------------- | ------------ |
| _id            | Entero       |
| nombre         | String       |
| correo         | String       |
| telefono       | String       |
| direccion      | String       |
| fecha_registro | Date         |

---

# 🦴 Colección: Ventas

### Documento Ejemplo:

```json
{
  "_id": 5001,
  "id_cliente": 101,
  "id_producto": 1,
  "cantidad": 2,
  "total": 999.98,
  "fecha_venta": "2026-04-27",
  "metodo_pago": "Tarjeta"
}
```

### Atributos y Tipo de Datos:

| Atributo    | Tipo de Dato |
| ----------- | ------------ |
| _id         | Entero       |
| id_cliente  | Entero       |
| id_producto | Entero       |
| cantidad    | Entero       |
| total       | Decimal      |
| fecha_venta | Date         |
| metodo_pago | String       |

---

# 🦖 Colección: Proveedores

### Documento Ejemplo:

```json
{
  "_id": 301,
  "nombre_empresa": "Jurassic Toys SA",
  "contacto": "Luis Pérez",
  "telefono": "6569876543",
  "correo": "ventas@jurassictoys.com"
}
```

### Atributos y Tipo de Datos:

| Atributo       | Tipo de Dato |
| -------------- | ------------ |
| _id            | Entero       |
| nombre_empresa | String       |
| contacto       | String       |
| telefono       | String       |
| correo         | String       |

---

# 📌 Resumen de Colecciones

* Productos
* Clientes
* Ventas
* Proveedores

---

# 💡 Si quieres, también puedo darte este ejemplo **en formato SQL (MySQL)** o **para Firebase / MongoDB Compass**, que se ve más profesional para tarea escolar.
