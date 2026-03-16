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
<img width="1098" height="966" alt="Captura de pantalla 2026-03-15 a la(s) 18 52 59" src="https://github.com/user-attachments/assets/7782387f-1b37-4ff1-b197-2308cd680aed" />

Página web 
<img width="1066" height="991" alt="Captura de pantalla 2026-03-16 a la(s) 11 27 13" src="https://github.com/user-attachments/assets/28a2677d-c6a0-4cea-8e84-d672280a2e3c" />

# Códigos Finales
```
components/ product_card.py
import flet as ft


class ProductCard(ft.Container):

    def __init__(self, nombre, descripcion, precio, imagen, fav_action, cart_action):
        super().__init__()

        self.nombre = nombre
        self.fav_action = fav_action
        self.cart_action = cart_action

        self.favorito = False
        self.en_carrito = False

        # Botón favorito
        self.btn_fav = ft.IconButton(
            icon=ft.Icons.FAVORITE_BORDER,
            icon_color="grey",
            on_click=self.toggle_favorito
        )

        # Botón carrito
        self.btn_carrito = ft.IconButton(
            icon=ft.Icons.SHOPPING_CART_OUTLINED,
            on_click=self.toggle_carrito
        )

        self.col = 3
        self.width = 250
        self.padding = 10
        self.border_radius = 15
        self.bgcolor = "#ffffff"

        self.shadow = ft.BoxShadow(
            blur_radius=15,
            color=ft.Colors.GREY_400,
            offset=ft.Offset(3, 3)
        )

        self.content = ft.Column(
            controls=[

                ft.Image(
                    src=f"/{imagen}",
                    width=200,
                    height=150,
                ),

                ft.Text(
                    nombre,
                    weight="bold",
                    size=16
                ),

                ft.Text(
                    descripcion,
                    size=12,
                    color=ft.Colors.GREY
                ),

                ft.Text(
                    f"${precio}",
                    size=18,
                    weight="bold",
                    color=ft.Colors.GREEN
                ),

                ft.Row(
                    alignment="spaceBetween",
                    controls=[
                        self.btn_fav,
                        self.btn_carrito
                    ]
                )
            ]
        )

    # FAVORITOS
    def toggle_favorito(self, e):

        self.favorito = not self.favorito

        if self.favorito:
            self.btn_fav.icon = ft.Icons.FAVORITE
            self.btn_fav.icon_color = "red"
        else:
            self.btn_fav.icon = ft.Icons.FAVORITE_BORDER
            self.btn_fav.icon_color = "grey"

        self.fav_action(self.nombre, self.favorito)

        self.update()

    # CARRITO
    def toggle_carrito(self, e):

        self.en_carrito = not self.en_carrito

        if self.en_carrito:
            self.btn_carrito.icon = ft.Icons.SHOPPING_CART
        else:
            self.btn_carrito.icon = ft.Icons.SHOPPING_CART_OUTLINED

        self.cart_action(self.nombre, self.en_carrito)

        self.update()
```
```
data.py
productos = [
    {
        "id": 1,
        "nombre": "Laptop Gamer",
        "descripcion": "Laptop con procesador i7 y 16GB RAM",
        "precio": 25000,
        "imagen": "laptop.png"
    },
    {
        "id": 2,
        "nombre": "Smartphone",
        "descripcion": "Pantalla AMOLED de 6.5 pulgadas",
        "precio": 12000,
        "imagen": "phone.png"
    },
    {
        "id": 3,
        "nombre": "Tablet",
        "descripcion": "Tablet ligera ideal para estudio",
        "precio": 8000,
        "imagen": "tablet.png"
    },
    {
        "id": 4,
        "nombre": "Audífonos",
        "descripcion": "Audífonos inalámbricos",
        "precio": 3500,
        "imagen": "headphones.png"
    },
    {
        "id": 5,
        "nombre": "Mouse Gamer",
        "descripcion": "Mouse RGB de alta precisión",
        "precio": 900,
        "imagen": "mouse.png"
    }
]
```
```
assets/imagenes.pnj
```
```
main.py
import flet as ft
from data import productos
from components.product_card import ProductCard


def main(page: ft.Page):

    page.title = "Tecnologia y Más"
    page.bgcolor = "#f5f5f5"

    favoritos = []
    carrito = []

    contador_fav = ft.Text("0 ", weight="bold")
    contador_carrito = ft.Text("0 ", weight="bold")

    # SnackBar (notificación)
    snack = ft.SnackBar(content=ft.Text(""))
    page.overlay.append(snack)

    def mostrar_mensaje(texto):
        snack.content.value = texto
        snack.open = True
        page.update()

    # FAVORITOS
    def actualizar_favorito(nombre, estado):

        if estado:
            if nombre not in favoritos:
                favoritos.append(nombre)
                mostrar_mensaje(f"{nombre} agregado a favoritos ")
        else:
            if nombre in favoritos:
                favoritos.remove(nombre)
                mostrar_mensaje(f"{nombre} eliminado de favoritos")

        contador_fav.value = f"{len(favoritos)} "
        page.update()

    # CARRITO
    def actualizar_carrito(nombre, estado):

        if estado:
            if nombre not in carrito:
                carrito.append(nombre)
                mostrar_mensaje(f"{nombre} agregado al carrito ")
        else:
            if nombre in carrito:
                carrito.remove(nombre)
                mostrar_mensaje(f"{nombre} eliminado del carrito")

        contador_carrito.value = f"{len(carrito)} "
        page.update()

    # VER FAVORITOS
    def ver_favoritos(e):

        lista = ft.Column()

        for p in favoritos:
            lista.controls.append(
                ft.ListTile(
                    title=ft.Text(p),
                    leading=ft.Icon(ft.Icons.FAVORITE, color="red")
                )
            )

        page.dialog = ft.AlertDialog(
            title=ft.Text("Favoritos"),
            content=lista
        )

        page.dialog.open = True
        page.update()

    # VER CARRITO
    def ver_carrito(e):

        lista = ft.Column()

        for p in carrito:
            lista.controls.append(
                ft.ListTile(
                    title=ft.Text(p),
                    leading=ft.Icon(ft.Icons.SHOPPING_CART)
                )
            )

        page.dialog = ft.AlertDialog(
            title=ft.Text("Carrito"),
            content=lista
        )

        page.dialog.open = True
        page.update()

    tarjetas = []

    for producto in productos:

        card = ProductCard(
            producto["nombre"],
            producto["descripcion"],
            producto["precio"],
            producto["imagen"],
            actualizar_favorito,
            actualizar_carrito
        )

        tarjetas.append(card)

    page.add(

        ft.Container(
            expand=True,

            content=ft.Column(

                controls=[

                    ft.Row(
                        alignment="spaceBetween",
                        controls=[

                            ft.Text(
                                "Tecnologia y Más",
                                size=30,
                                weight="bold"
                            ),

                            ft.Row(
                                controls=[

                                    ft.ElevatedButton(
                                        "Favoritos",
                                        on_click=ver_favoritos
                                    ),

                                    contador_fav,

                                    ft.ElevatedButton(
                                        "Carrito",
                                        on_click=ver_carrito
                                    ),

                                    contador_carrito

                                ]
                            )

                        ]
                    ),

                    ft.ResponsiveRow(
                        controls=tarjetas,
                        spacing=20,
                        run_spacing=20
                    )

                ],

                scroll="auto"

            )

        )

    )


ft.run(main, assets_dir="assets")
```
