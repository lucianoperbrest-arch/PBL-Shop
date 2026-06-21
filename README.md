# PBL Shop - Donde la Magia Se Hace Real
## Actividad Formativa N.° 2: Diseñando un e-Commerce con Inteligencia Artificial
### Cátedra: Algoritmos y Estructuras de Datos | ISI - UTN FRRE

# Nombre del e-Commerce: PBL Shop
# Descripcion: 
PBL Shop es una plataforma de e-commerce temática diseñada para fans de los mundos de fantasía, videojuegos, magia y ficción especulativa. Su propuesta de valor va mucho más allá de una tienda convencional: cada interacción está construida como si el usuario fuera un personaje que ingresa a un universo paralelo para adquirir artefactos, hechizos y reliquias.
La aplicación fusiona la experiencia de compra en línea con la estética y la narrativa de los géneros de ficción más amados. En lugar de categorías genéricas, el usuario navega por "zonas del mapa" (Reinos, Mazmorras, Naves Estelares, Academias de Magia). Cada producto tiene su propio lore: una remera no es una remera, es "la túnica del Errante del Norte, tejida con fibras de éter".
El público objetivo son jóvenes adultos de 16 a 35 años, fanáticos de franquicias como D&D, The Witcher, Final Fantasy, Harry Potter, Tolkien, anime y sci-fi clásico, que buscan consumir productos con identidad y no solo mercancía genérica.
Lo que distingue a PBL Shop no es el inventario, sino la experiencia. El sistema de gremios y niveles transforma la fidelización en un juego de rol real: cuanto más compras, más sube tu rango dentro de la comunidad.

# Diseño de los Registros

# 🛒 Diccionario de Datos: Tabla `productos` (PBL Shop)

Este repositorio contiene la especificación y el diseño lógico del **Registro Principal de Productos de PBL Shop**. El modelo está preparado para soportar características avanzadas de e-commerce clásico combinadas con elementos narrativos y gamificados de fantasía (*Lore*).

## 📊 Vista General de la Tabla

La tabla `productos` está conformada por un total de **18 campos**, distribuidos en **5 tipos de datos** principales: `Entero`, `Real`, `Cadena`, `Booleano`, `Fecha` y `Lista` (arreglo).

| Métrica | Detalle |
| :--- | :--- |
| **Nombre de la Tabla** | `productos` |
| **Número Total de Campos** | 18 |
| **Clave Primaria (PK)** | `producto_id` |
| **Tipos de Datos Soportados** | Entero, Real, Cadena, Booleano, Fecha, Lista |

---

## 📐 Esquema Detallado de Campos

A continuación se detallan las secciones lógicas que componen la entidad de productos.

### 🔑 Identificación
Campos críticos para el control, indexación y unicidad del inventario.

*   **`producto_id`** `[Entero]` `[PK]`: Identificador único autoincremental de cada producto en el sistema.
*   **`sku`** `[Cadena]`: Código alfanumérico único de referencia interna (*Stock Keeping Unit*).  
    *Ejemplo:* `PBL-RPG-0042`

### 📝 Descripción del Producto
Contenido textual enfocado en la conversión comercial y la inmersión del usuario en el universo fantástico.

*   **`nombre`** `[Cadena]`: Nombre comercial del producto.  
    *Ejemplo:* `"Espada del Cazador Eterno"`
*   **`nombre_lore`** `[Cadena]`: Nombre narrativo o fantástico del producto dentro del universo de PBL Shop.
*   **`descripcion_corta`** `[Cadena]`: Resumen breve del producto (máx. 150 caracteres) optimizado para tarjetas de catálogo.
*   **`descripcion_lore`** `[Cadena]`: Descripción extensa y narrativa del producto redactada en tono fantástico/épico (sin límite de caracteres).

### 🏷️ Clasificación
Estructura taxonómica para potenciar los módulos de búsqueda, navegación y recomendaciones del sitio.

*   **`categoria`** `[Cadena]`: Categoría principal a la que pertenece el ítem.  
    *Ejemplos:* `"Figuras"`, `"Ropa"`, `"Videojuegos"`, `"Libros"`.
*   **`universo_tematico`** `[Cadena]`: Zona temática o facción de PBL Shop correspondiente.  
    *Ejemplos:* `"Reino Élfico"`, `"Nave Estelar"`, `"Academia Arcana"`.
*   **`etiquetas`** `[Lista (Cadenas)]`: Arreglo de palabras clave dinámicas para optimizar búsquedas y filtros internos.  
    *Ejemplo:* `["RPG", "magia", "coleccionable"]`

### 💰 Precio e Inventario
Datos numéricos de precisión financiera y control logístico en tiempo real.

*   **`precio`** `[Real]`: Precio de venta al público en la moneda local (soporta decimales).  
    *Ejemplo:* `2499.99`
*   **`precio_descuento`** `[Real]`: Precio especial temporal aplicable durante promociones o eventos mágicos de la tienda. Retorna `null` si no hay rebajas activas.
*   **`stock`** `[Entero]`: Cantidad actual de unidades disponibles en el inventario. Un valor de `0` inhabilita la compra directa indicando producto agotado.

### 🖼️ Multimedia
Referencias a recursos estáticos almacenados en servidores de medios o CDNs.

*   **`imagen_principal`** `[Cadena]`: URL absoluta o relativa de la imagen destacada del producto.
*   **`imagenes_extra`** `[Lista (Cadenas)]`: Arreglo de URLs con imágenes adicionales destinado a la galería detallada (soporta hasta 6 fotografías adicionales).

### ⭐ Valoración y Estado
Metadatos de negocio y rendimiento social del artículo dentro de la plataforma.

*   **`puntuacion_media`** `[Real]`: Promedio de calificaciones otorgadas por los clientes en una escala de `1.0` a `5.0`.
*   **`activo`** `[Booleano]`: Flag lógico que determina si el producto está visible y apto para ser comprado en el catálogo público (`true`/`false`).
*   **`es_destacado`** `[Booleano]`: Bandera que marca si el ítem debe ser posicionado en la página de inicio o en banners promocionales de relevancia.

### 🕒 Auditoría
Campos de control temporal para la trazabilidad de los datos.

*   **`fecha_alta`** `[Fecha]`: Fecha y hora exactas en las que el registro fue ingresado por primera vez en la base de datos (Estructurado bajo el estándar **ISO 8601**).

---

## 📌 Glosario de Convenciones y Leyenda

*   **`PK`**: *Primary Key* (Clave Primaria). Identificador único irrepetible de la tupla.
*   **`Lista`**: Estructura de datos tipo arreglo que agrupa múltiples valores homogéneos (en este diseño, colecciones de cadenas de texto).
*   **`Real`**: Tipo de dato numérico de punto flotante ideal para representar valores monetarios precisos o promedios con decimales.

# Identificacion y explicacion de la clave

# 🛒 Sistema de Gestión de Catálogo y Base de Datos - PBL Shop

Este repositorio contiene la especificación técnica, el diseño lógico y las reglas de integridad de datos para el **Registro Principal de Productos de PBL Shop**. El modelo combina la robustez de un e-commerce clásico con elementos narrativos y mecánicas gamificadas de fantasía (*Lore*).

---

## 📊 Vista General de la Tabla `productos`

La tabla principal `productos` está conformada por un total de **18 campos**, distribuidos de manera balanceada en **5 tipos de datos** nativos del motor relacional.

### 📈 Métricas de la Estructura
* **Nombre de la Entidad:** `productos`
* **Campos Totales:** 18
* **Clave Primaria (PK):** `producto_id`
* **Tipos de Datos Utilizados:** Entero (`INT`), Real (`DECIMAL`/`FLOAT`), Cadena (`VARCHAR`), Booleano (`BOOLEAN`), Fecha (`DATETIME`/`TIMESTAMP`) y Lista (Arreglos/JSON).

### 🏷️ Tipos de Datos Soportados
* **Entero:** Identificadores y cantidades logísticas.
* **Real:** Valores monetarios y métricas de rendimiento.
* **Cadena:** Textos planos, URLs y bloques descriptivos.
* **Booleano:** Flags de control y estados lógicos.
* **Fecha:** Marcas de tiempo bajo el estándar **ISO 8601**.
* **Lista:** Colecciones u objetos homogéneos (representados mediante tipos `JSON` o tablas asociativas).

---

## 📐 Diccionario de Datos Detallado

A continuación se presenta la segmentación por capas lógicas de todos los campos estructurados.

### 🔑 Capa A: Identificación
Campos de indexación crítica, control único y rastreo de inventario.
* **`producto_id`** `[Entero]` `[PK]`: Identificador único autoincremental de cada producto en el sistema.
* **`sku`** `[Cadena]`: Código alfanumérico único de referencia interna (*Stock Keeping Unit*).  
  *Ejemplo de formato:* `PBL-RPG-0042`

### 📝 Capa B: Descripción e Inmersión (*Lore*)
Bloques de texto optimizados para conversión en interfaz de usuario y narrativa fantástica.
* **`nombre`** `[Cadena]`: Nombre comercial visible en el catálogo de cara al cliente.  
  *Ejemplo:* `"Espada del Cazador Eterno"`
* **`nombre_lore`** `[Cadena]`: Nombre narrativo, místico o histórico del ítem dentro del lore de la tienda.
* **`descripcion_corta`** `[Cadena]`: Resumen comercial conciso (máximo 150 caracteres) para tarjetas de catálogo y previsualizaciones rápidas.
* **`descripcion_lore`** `[Cadena]`: Relato extenso e inmersivo en tono épico/fantástico del producto, sin límite de extensión.

### 🏷️ Capa C: Clasificación y Taxonomía
Campos dinámicos orientados a los módulos de búsqueda, filtrado avanzado y motores de recomendación.
* **`categoria`** `[Cadena]`: Clasificación macro del producto.  
  *Valores válidos:* `"Figuras"`, `"Ropa"`, `"Videojuegos"`, `"Libros"`, etc.
* **`universo_tematico`** `[Cadena]`: Región, zona o facción de la tienda a la que pertenece el artículo.  
  *Valores válidos:* `"Reino Élfico"`, `"Nave Estelar"`, `"Academia Arcana"`, etc.
* **`etiquetas`** `[Lista (Cadenas)]`: Arreglo de palabras clave para búsquedas internas.  
  *Ejemplo:* `["RPG", "magia", "coleccionable"]`

### 💰 Capa D: Finanzas y Logística
Datos de precisión numérica y control de inventario en tiempo real.
* **`precio`** `[Real]`: Precio estándar de venta al público en la moneda local. Soporta el ingreso de posiciones decimales.  
  *Ejemplo:* `2499.99`
* **`precio_descuento`** `[Real]`: Precio rebajado aplicado durante eventos especiales o campañas flash. Almacena un valor nulo (`null`) si el ítem no tiene un descuento activo.
* **`stock`** `[Entero]`: Cantidad de unidades físicas disponibles en bodega. El valor `0` inhabilita automáticamente la adición al carrito de compras (Agotado).

### 🖼️ Capa E: Recursos Multimedia
Rutas y referencias a los servidores estáticos de imágenes o CDNs.
* **`imagen_principal`** `[Cadena]`: URL absoluta de la fotografía principal del artículo.
* **`imagenes_extra`** `[Lista (Cadenas)]`: Arreglo o colección de URLs que componen la galería extendida del producto (soporta un límite técnico recomendado de hasta 6 imágenes secundarias).

### ⭐ Capa F: Estado y Rendimiento del Negocio
Métricas lógicas y relacionales de cara a la plataforma web.
* **`puntuacion_media`** `[Real]`: Calificación promedio asignada por la comunidad de compradores (en un rango exacto de `1.0` a `5.0`).
* **`activo`** `[Booleano]`: Estado de visibilidad en producción (`true` para mostrar en la tienda, `false` para ocultar o descontinuar).
* **`es_destacado`** `[Booleano]`: Flag para empujar el producto directamente a la página de inicio o banners promocionales de alta relevancia.

### 🕒 Capa G: Auditoría interna
* **`fecha_alta`** `[Fecha]`: Estampa de tiempo exacta (Fecha y hora) del momento en que se insertó el registro inicial en el sistema.

---

## 🔑 3. Arquitectura de Clave Primaria

El corazón relacional de esta tabla reside en la correcta elección de su clave única. Tras un exhaustivo análisis técnico, se implementó una **clave primaria subrogada** basada en el campo `producto_id`.

### ⚙️ Propiedades Físicas de `producto_id`
* **Tipo nativo:** `INT` (Entero sin signo).
* **Estrategia de asignación:** `AUTO_INCREMENT` nativo del motor de base de datos.
* **Restricción de nulidad:** `NOT NULL` estricto.
* **Comportamiento:** Secuencial, controlado y aislado de la lógica de negocio.

---

## ⚖️ Matriz de Descarte de Candidatas (¿Por qué no otros campos?)

Antes de dictaminar a `producto_id` como la ganadora, se evaluaron otros atributos del modelo, siendo descartados bajo rigurosos criterios arquitectónicos:

1. **`sku` (Candidata Parcial - Descartada):** Aunque actualmente su diseño garantiza valores únicos, los SKUs **no son 100% inmutables**. Si la empresa reestructura el etiquetado logístico o cambia de sistema de almacenes, el código se vería forzado a mutar, rompiendo relaciones históricas.
2. **`nombre` (Descartada):** No garantiza unicidad. Dos productos idénticos pero de diferentes lotes, o dos variantes sutiles, podrían colisionar. El lenguaje comercial tiende a ser repetitivo.
3. **`nombre_lore` (Descartada):** Al ser bloques de texto descriptivos, largos y de naturaleza de fantasía, son completamente ineficientes para la indexación y la creación de un árbol B+ de base de datos.
4. **`precio` (Descartada):** Es un valor volátil que muta constantemente debido a la inflación, promociones o devaluación. Cientos de productos pueden compartir el mismo costo simultáneamente.
5. **`fecha_alta` (Descartada):** No es segura. En un entorno de producción masivo o mediante cargas por API (`bulk inserts`), dos o más registros de productos pueden crearse exactamente en el mismo milisegundo de tiempo.

---

## 🛠️ Reglas Técnicas y Problemas Evitados

La arquitectura elegida para la base de datos de PBL Shop cumple estrictamente con las **reglas de oro de un diseño relacional sano**, previniendo de manera nativa los siguientes problemas operativos:

* **Evita Duplicados Accidentales:** Si se utilizara el `nombre` comercial, el lanzamiento de una *"Espada del Héroe (Edición Estándar)"* y una *"Espada del Héroe (Edición Deluxe)"* generaría un error de colisión de llaves si los nombres se simplificaran por error tipográfico.
* **Mitiga Claves Huérfanas por Reestructuración:** Si el `sku` fuese la PK y se actualizara su patrón de codificación, todas las órdenes de compra pasadas, las reseñas de los clientes y los artículos guardados en listas de deseos perderían su correspondencia relacional de inmediato.
* **Garantiza la Integridad Referencial:** Al enlazar tablas foráneas (`pedidos`, `favoritos`, `reviews`) mediante un `producto_id` numérico e inmutable, el sistema se mantiene blindado ante modificaciones estéticas o de costos comerciales.
* **Maximiza la Eficiencia en Búsquedas:** Indexar un entero de 4 bytes es exponencialmente más veloz en memoria RAM y disco duro que procesar cadenas de texto complejas como `nombre_lore`.
* **Anula el Error Humano en Carga:** Al delegar la creación del ID al mecanismo `AUTO_INCREMENT`, ningún operador o script de migración manual puede introducir un identificador erróneo o romper la secuencia del índice.

---

## 📌 Glosario de Convenciones técnico-logísticas

* **`PK` (Primary Key):** Atributo que identifica de manera unívoca a un registro dentro de una base de datos.
* **`FK` (Foreign Key):** Campo en una tabla que apunta directamente a la Clave Primaria de otra tabla para entablar una relación fuerte.
* **`ISO 8601`:** Estándar internacional para la representación de fechas y horas (`YYYY-MM-DDTHH:MM:SSZ`), utilizado aquí en `fecha_alta`.
* **`Inmutabilidad`:** Propiedad de un dato que garantiza que una vez guardado en el storage físico, no sufrirá variaciones a lo largo del ciclo de vida del software.

# PROMPTS UTILIZADOS

### Prompt 1: Generar la idea general 
Diseña una aplicación de e-Commerce llamada "PBL Shop", inspirada en mundos de fantasía, videojuegos, magia y ficción. Haz una descripción general de la aplicacion.

### Prompt 2: Diseñar el registro principal 
Para la aplicación, crea un registro principal que almacene la información de los productos. Indica: Nombre de cada campo. Tipo de dato de cada campo (entero, real, cadena, booleano, fecha, etc.). Breve descripción de cada campo. Presenta la información en forma de tabla.

### Prompt 3: Definir la clave 
Define una clave única para el registro de productos. Explica por qué esa clave es la mejor opción para identificar cada producto de forma única dentro del sistema y qué problemas evita.

### Prompt 4: Diseñar la interfaz 
Debe incluir: Diseño oscuro en tonos negro y violeta. Barra de navegación con logo, buscador y carrito. Banner principal con un castillo fantástico. Categorías de productos. Catálogo de productos. Carrito de compras funcional. Cada producto debe tener su propia ilustración relacionada con su descripción. Productos de ejemplo: Espada Élfica, Libro de Hechizos, Varita Mágica, Figura de Dragón, Casco Legendario, Figura de Guerrero. Las imágenes deben tener estilo de fantasía épico y con calidad profesional.

### Prompt 5: Generación del código 
Te adjunto un zip con las imagenes creadas. Ahora genera el código completo de la aplicación utilizando HTML y las imágenes para los productos. Requisitos: Diseño similar a una tienda online moderna de fantasía. Tema oscuro con colores negro y violeta. Barra de navegación con logo, buscador y carrito. Banner principal. Categorías de productos. Catálogo de productos mostrando las imágenes generadas. Carrito de compras funcional.

# ENLACE DE LA PAGINA
https://lucianoperbrest-arch.github.io/PBL-Shop/

# ENLACE DEL VIDEO TUTORIAL
https://drive.google.com/drive/folders/1uHS9-OnZJw1O3yIl-_X1VBlcdrrscHWz?usp=sharing

# Reflexion
La incorporación de la Inteligencia Artificial en esta actividad formativa resultó de gran utilidad para vincular los conceptos teóricos de la materia con un caso práctico y creativo. Durante el proceso la herramienta me permitió estructurar de manera lógica el registro principal, facilitando la asignación correcta de los tipos de datos y la correcta eleccion de variables según las necesidades del e-commerce. Asimismo, el intercambio de ideas con la IA fue fundamental para profundizar en el concepto de clave de registro; inicialmente había considerado utilizar el nombre del producto, pero el análisis me demostró que esto generaría duplicaciones y errores en la base de datos. En conclusión, la IA funcionó como un soporte que optimizó los tiempos y mejoró mi comprensión sobre el tema.
