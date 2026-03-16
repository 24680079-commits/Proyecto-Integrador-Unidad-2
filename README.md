# Proyecto-Integrador-Unidad-2
#  Catálogo de Productos Reutilizable con Flet

# Proyecto Integrador - Unidad 2

Materia: Tópicos Avanzados de Programación

Este proyecto consiste en el desarrollo de una aplicación utilizando **Python y Flet** para mostrar un catálogo de productos tecnológicos mediante un componente reutilizable.

---

#  Objetivo

Diseñar y crear componentes visuales reutilizables para construir una interfaz gráfica profesional aplicando:

* Programación orientada a objetos
* Herencia
* Modularización
* Gestión de recursos

---

#  Arquitectura del Proyecto

El proyecto está dividido en tres partes principales:

### 1️ Modelo de Datos

El archivo `data.py` contiene una lista de diccionarios que representan los productos del catálogo.

Cada producto contiene:

* id
* nombre
* descripción
* precio
* imagen

Ejemplo:

```python
productos = [
{
"id":1,
"nombre":"Laptop Gamer",
"descripcion":"Laptop con procesador i7",
"precio":25000,
"imagen":"laptop.png"
}
]
```

---

### 2️ Componente Reutilizable

Se creó una clase llamada:

```
ProductCard
```

ubicada en:

```
components/product_card.py
```

Esta clase **hereda de `ft.Container`** para crear un componente visual reutilizable.

El componente incluye:

* Imagen del producto
* Nombre del producto
* Descripción
* Precio destacado
* Botón de favorito
* Botón de agregar al carrito

Esto permite reutilizar el mismo componente para cualquier producto.
---
# Explicación de herencia
La clase ProductCard fue creada como un componente personalizado que hereda de ft.Container del framework Flet.

Esta herencia permite aprovechar todas las propiedades visuales del contenedor, como padding, bordes, sombras y layout, mientras se agregan controles internos como imágenes, texto y botones.

Gracias a este diseño, el componente puede reutilizarse múltiples veces para mostrar diferentes productos sin duplicar código.

Gestión de recursos (Assets)

En el proyecto se creó la carpeta:

assets/

Aquí se almacenan las imágenes.

Flet se configura así:
```
ft.run(main, assets_dir="assets")
```
Esto permite cargar imágenes con:
```
/laptop.png
```
El diseño del componente ProductCard fue pensado para ser reutilizable y desacoplado del origen de datos.
Esto permite que en futuras unidades los productos puedan cargarse desde una API o base de datos sin modificar el diseño visual del componente.

---
# Diagrama de clases

             +--------------------+
             |   ProductCard      |
             |--------------------|
             | nombre             |
             | descripcion        |
             | precio             |
             | imagen             |
             | favorito           |
             | en_carrito         |
             |--------------------|
             | toggle_favorito()  |
             | toggle_carrito()   |
             +---------▲----------+
                       |
                       |
                hereda de
                       |
              +----------------+
              |   ft.Container |
              +----------------+

                       ↑
                       |
                usado por
                       |
                +-------------+
                |   main.py   |
                +-------------+
---

### 3️ Interfaz Principal

El archivo `main.py` es el encargado de:

* Cargar los datos
* Crear instancias del componente `ProductCard`
* Organizar los productos en una cuadrícula adaptable usando `ResponsiveRow`.

---

#  Tecnologías utilizadas

* Python
* Flet
* Programación Orientada a Objetos
* Componentes reutilizables

---

#  Gestión de Recursos (Assets)

Las imágenes de los productos se almacenan dentro de la carpeta:

```
/assets
```

Flet permite cargar estos recursos utilizando:

```python
ft.run(main, assets_dir="assets")
```

Esto hace que todas las imágenes dentro de esa carpeta puedan ser utilizadas en la aplicación.

---

#  Modularidad del Código

El proyecto fue diseñado de forma modular:

| Archivo         | Función                 |
| --------------- | ----------------------- |
| main.py         | Interfaz principal      |
| data.py         | Modelo de datos         |
| product_card.py | Componente reutilizable |

Esto permite que en el futuro los datos puedan venir de:

* una API
* una base de datos
* un archivo externo

sin modificar el diseño de la interfaz.

---

#  Evidencia de funcionamiento

La aplicación muestra un catálogo de productos con:

* tarjetas reutilizables
* imágenes
* botones de acción
* diseño adaptable

---

#  Ejecución del proyecto

Instalar dependencias:

```
pip install flet
```

Ejecutar aplicación:

```
python main.py
```

---

#  Autor

Proyecto desarrollado por:

**Noel Castillo Villanueva**

Para la materia de **Tópicos Avanzados de Programación**

# Evidencia
