# Apuntes de Clase - Unidad I: Introducción a la Graficación por Computadora

---

## 1.1 Historia y Evolución de la Graficación por Computadora

La **graficación por computadora** es la disciplina que estudia la creación, manipulación y representación de imágenes mediante sistemas computacionales.


La historia de la graficación por computadora es la evolución de cómo las máquinas pasaron de imprimir números en papel a generar mundos visuales interactivos. Este desarrollo ha sido impulsado por la convergencia de avances en hardware, algoritmos matemáticos y la demanda de industrias como la defensa, el entretenimiento y el diseño.

**Década de 1950 - Los Primeros Pasos**

Los inicios se dieron en entornos militares y de investigación. El Proyecto Whirlwind (MIT) y el sistema de defensa SAGE fueron pioneros al utilizar pantallas de tubo de rayos catódicos (CRT) y el lápiz óptico para la interacción en tiempo real, sentando las bases de la interacción hombre-máquina.

**Década de 1960 - La Fundación del Campo**

El hito más importante fue Sketchpad (1963), desarrollado por Ivan Sutherland en el MIT. Este programa permitía dibujar y manipular figuras geométricas en una pantalla con un lápiz óptico, estableciendo las bases de los modernos programas de Diseño Asistido por Computadora (CAD) y los gráficos vectoriales . El término "Computer Graphics" fue acuñado poco después por William Fetter en Boeing .

**Década de 1970 - La Búsqueda del Realismo**

La Universidad de Utah se convirtió en el epicentro de la innovación. Allí se desarrollaron técnicas fundamentales para el modelado 3D, como los modelos de iluminación Gouraud y Phong (sombreado), el mapeo de texturas por Ed Catmull y el algoritmo del Z-buffer para gestionar la profundidad . En 1974 se celebró la primera conferencia de la ACM SIGGRAPH, que se consolidó como el foro mundial más importante de gráficos por computadora .

**Década de 1980 - Democratización y Estándares**

Con la llegada del ordenador personal, los gráficos llegaron a las masas. Estándares como CGA y VGA en las PC de IBM permitieron los primeros gráficos en color. Apple popularizó la Interfaz Gráfica de Usuario (GUI) con la Macintosh en 1984, haciendo las computadoras más accesibles mediante iconos y ventanas .

**Década de 1990 - Fotorrealismo y las GPU**

El cine y los videojuegos impulsaron el realismo. Toy Story (1995) fue el primer largometraje completamente animado por computadora, y Parque Jurásico (1993) demostró el poder de los efectos especiales digitales. Para manejar la creciente complejidad de los gráficos 3D en tiempo real, surgió la Unidad de Procesamiento Gráfico (GPU) , un hardware especializado que liberó a la CPU de esta tarea y que hoy es esencial en cualquier dispositivo .


---

## 1.2 Áreas de Aplicación

La graficación por computadora está presente en múltiples industrias:

**Entretenimiento y medios:**
Producción de películas de animación y efectos especiales (CGI), videojuegos 2D y 3D, y transmisiones en vivo con gráficas en tiempo real.

**Ciencia e ingeniería:**
Simulaciones físicas y visualización científica, diseño asistido por computadora (CAD/CAM), arquitectura (renders fotorrealistas) y medicina (imágenes por resonancia magnética, tomografías 3D).

**Educación y entrenamiento:**
Simuladores de vuelo y conducción, entornos virtuales de aprendizaje y realidad aumentada (AR) aplicada a la enseñanza.

**Diseño y publicidad:**
Diseño gráfico digital, modelado de productos, animación publicitaria y prototipado visual.

---

## 1.3 Aspectos Matemáticos de la Graficación

La graficación computacional se basa en diversas ramas de las matemáticas.

### Geometría Analítica y Álgebra Lineal

Son la base para posicionar, transformar y proyectar objetos en el espacio. Las operaciones fundamentales son:

- **Traslación:** Mover un punto sumando un vector `P' = P + T`
- **Escalado:** Cambiar tamaño multiplicando coordenadas `P' = S · P`
- **Rotación 2D:** Girar un punto alrededor del origen:
```
x' = x·cos(θ) - y·sin(θ)
y' = x·sin(θ) + y·cos(θ)
```

### Coordenadas Homogéneas

Permiten representar traslaciones como multiplicaciones de matrices (4×4), unificando todas las transformaciones en una sola operación matricial. Son esenciales en OpenGL, DirectX y Blender internamente.

### Trigonometría

Fundamental para calcular posiciones en círculos, espirales y polígonos regulares. Por ejemplo, para ubicar los vértices de un polígono de `n` lados con radio `r`:

```
x = r · cos(2π · i / n)
y = r · sin(2π · i / n)
```

### Vectores y Normales

Los vectores normales a una superficie determinan cómo interactúa la luz con los objetos, siendo la base del sombreado y la iluminación 3D.

---

## 1.4 Modelos del Color: RGB, CMY, HSV y HSL

Un **modelo de color** es un sistema matemático que describe cómo representar colores mediante valores numéricos.

### RGB (Red, Green, Blue)
Modelo **aditivo** usado en pantallas y monitores. Mezcla luz de colores primarios. Cada canal va de 0 a 255 (o de 0.0 a 1.0 en Blender/shaders).

| Color | R | G | B |
|-------|---|---|---|
| Rojo | 255 | 0 | 0 |
| Verde | 0 | 255 | 0 |
| Azul | 0 | 0 | 255 |
| Blanco | 255 | 255 | 255 |
| Negro | 0 | 0 | 0 |

### CMY / CMYK (Cyan, Magenta, Yellow, Key/Black)
Modelo **sustractivo** usado en impresión. Funciona absorbiendo longitudes de onda de luz. La conversión desde RGB es:
```
C = 1 - R
M = 1 - G
Y = 1 - B
```

### HSV (Hue, Saturation, Value)
Modelo más intuitivo para el ser humano:
- **Hue (Tono):** Ángulo de 0° a 360° en el círculo cromático
- **Saturation (Saturación):** Intensidad del color (0% = gris, 100% = color puro)
- **Value (Valor/Brillo):** Luminosidad del color (0% = negro, 100% = color brillante)

### HSL (Hue, Saturation, Lightness)
Similar al HSV pero con diferente escala de luminosidad:
- **Lightness:** 0% = negro, 50% = color puro, 100% = blanco

>  **En Blender:** Los materiales con nodos usan valores RGB normalizados (0.0 a 1.0). El nodo *Hue/Saturation/Value* permite manipular colores en el modelo HSV directamente.

### Tutorial: Iluminar un cubo en Blender por sus caras

Para aplicar un color diferente a cada cara de un cubo en Blender usando Python:

```python
import bpy

# Limpiar escena
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

# Crear cubo
bpy.ops.mesh.primitive_cube_add()
cubo = bpy.context.active_object

# Colores para cada cara (RGB normalizado)
colores = [
    (1.0, 0.0, 0.0),  # Rojo
    (0.0, 1.0, 0.0),  # Verde
    (0.0, 0.0, 1.0),  # Azul
    (1.0, 1.0, 0.0),  # Amarillo
    (1.0, 0.5, 0.0),  # Naranja
    (0.5, 0.0, 1.0),  # Morado
]

# Crear y asignar un material por cara
for i, color in enumerate(colores):
    mat = bpy.data.materials.new(name=f"Color_{i}")
    mat.use_nodes = True
    bsdf = mat.node_tree.nodes.get("Principled BSDF")
    bsdf.inputs["Base Color"].default_value = (*color, 1.0)
    mat.diffuse_color = (*color, 1.0)
    cubo.data.materials.append(mat)

# Asignar cada material a su cara correspondiente
for i, poly in enumerate(cubo.data.polygons):
    poly.material_index = i
cubo.data.update()
```

 <img width="351" height="324" alt="Captura11" src="https://github.com/user-attachments/assets/e98fb57e-fc50-4b77-9a72-8bf6bd63250b" />  

---

## 1.5 Representación y Trazo de Líneas y Polígonos

### Algoritmos de Trazo de Líneas

**Algoritmo DDA (Digital Differential Analyzer)**
Calcula puntos intermedios de una línea usando incrementos decimales. Simple pero con errores de redondeo acumulados.

**Algoritmo de Bresenham**
Más eficiente que DDA. Usa solo aritmética entera para determinar el píxel más cercano a la línea real. Es el estándar en gráficos rasterizados.

### Polígonos

Un **polígono regular** de `n` lados tiene todos sus vértices equidistantes del centro. Se calcula con trigonometría como se mostró en la sección 1.3.

### Práctica: Dibujo de un Polígono en Blender

```python
import bpy
import math

bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

def crear_poligono_2d(nombre, lados, radio):
    malla = bpy.data.meshes.new(nombre)
    objeto = bpy.data.objects.new(nombre, malla)
    bpy.context.collection.objects.link(objeto)

    vertices = []
    aristas = []

    # Calcular vértices del polígono regular
    for i in range(lados):
        angulo = 2 * math.pi * i / lados
        x = radio * math.cos(angulo)
        y = radio * math.sin(angulo)
        vertices.append((x, y, 0))

    # Crear aristas que conectan los vértices
    for i in range(lados):
        aristas.append((i, (i + 1) % lados))

    malla.from_pydata(vertices, aristas, [])
    malla.update()

# Crear hexágono con radio 5
crear_poligono_2d("Poligono2D", lados=6, radio=5)
```

**Explicación del código:**
- Se calcula cada vértice usando la fórmula trigonométrica del polígono regular
- Las aristas conectan cada vértice con el siguiente usando el operador módulo `% lados` para cerrar la figura
- `from_pydata()` construye la malla con los vértices y aristas calculados

  <img width="424" height="432" alt="Captura13" src="https://github.com/user-attachments/assets/f8a3d81b-1830-4b7e-ab6f-aa091715330d" />


---

### 1.5.1 Formatos de Imagen

| Formato | Tipo | Compresión | Transparencia | Uso principal |
|---------|------|------------|---------------|---------------|
| **BMP** | Raster | Sin compresión | No | Archivos de sistema Windows |
| **JPEG/JPG** | Raster | Con pérdida | No | Fotografías, web |
| **PNG** | Raster | Sin pérdida | Sí (canal alfa) | Diseño web, iconos |
| **GIF** | Raster | Sin pérdida | Parcial | Animaciones simples |
| **SVG** | Vectorial | Sin pérdida | Sí | Logotipos, iconos escalables |
| **TIFF** | Raster | Opcional | Sí | Impresión profesional |
| **EXR** | Raster HDR | Sin pérdida | Sí | Renders de Blender, VFX |
| **WEBP** | Raster | Ambas | Sí | Web moderna |

>  **En Blender**, el formato recomendado para renders es **PNG** (calidad sin pérdida) o **EXR** (para composición profesional con canales HDR).

---

## 1.6 Procesamiento de Mapas de Bits

Un **mapa de bits** (bitmap o imagen raster) es una cuadrícula de píxeles donde cada píxel almacena un valor de color. La resolución determina la calidad: a mayor número de píxeles, mayor detalle.

### Conceptos clave

**Resolución:** Número de píxeles por unidad de medida (PPI = píxeles por pulgada). 72 PPI para pantalla, 300 PPI para impresión.

**Profundidad de color:** Bits por píxel. 8 bits = 256 colores, 24 bits = ~16 millones de colores (RGB estándar), 32 bits = 24 bits de color + 8 bits de transparencia (canal alfa).

**Canal Alfa:** Canal adicional que almacena información de transparencia. Un valor de 0 es completamente transparente y 255 es completamente opaco.

### Operaciones sobre mapas de bits

- **Escalado:** Redimensionar la imagen (interpolación bilineal o bicúbica)
- **Rotación:** Girar la imagen cierto ángulo
- **Filtros:** Aplicar efectos como desenfoque (blur), nitidez (sharpen), detección de bordes
- **Corrección de color:** Ajustar brillo, contraste, saturación
- **Composición:** Combinar varias imágenes usando modos de mezcla (multiply, overlay, screen)

### Mapas de bits en Blender

En Blender, los mapas de bits se usan como **texturas** aplicadas a los materiales de los objetos 3D. Se cargan mediante el nodo *Image Texture* en el editor de nodos y se mapean a la geometría usando coordenadas UV.

---

### Práctica: Flor de la Vida en Blender

La **Flor de la Vida** es un patrón geométrico sagrado compuesto por múltiples círculos superpuestos equidistantes, donde cada círculo periférico pasa por el centro de los círculos adyacentes.

```python
import bpy
import math

bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete(use_global=False)

radio = 2
angulo_actual = 0
paso = 60  # 360° / 6 círculos = 60° entre cada uno

# Círculo central
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0, 0, 0))

# 6 círculos periféricos
while angulo_actual < 360:
    angulo_rad = math.radians(angulo_actual)
    x = radio * math.cos(angulo_rad)
    y = radio * math.sin(angulo_rad)
    bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x, y, 0))
    angulo_actual += paso
```

**Explicación del código:**
- Se coloca un círculo en el origen como centro
- Se generan 6 círculos periféricos a una distancia igual al radio (lo que hace que cada círculo pase exactamente por el centro del anterior)
- El ángulo se incrementa en `60°` en cada iteración (`360° / 6 = 60°`) para distribuirlos uniformemente
- Las coordenadas de cada centro se calculan con `x = r·cos(θ)` y `y = r·sin(θ)`

  <img width="485" height="477" alt="Captura14" src="https://github.com/user-attachments/assets/4cb41756-8893-4b08-8072-bc34d263a0eb" />


---

## Bibliografía (Formato APA)

Foley, J. D., van Dam, A., Feiner, S. K., & Hughes, J. F. (1995). *Computer graphics: Principles and practice* (2.ª ed.). Addison-Wesley.

Hill, F. S., & Kelley, S. M. (2006). *Computer graphics using OpenGL* (3.ª ed.). Pearson Prentice Hall.

Blender Foundation. (s.f.). *Blender 4.x manual*. https://docs.blender.org/manual/en/latest/

Blender Foundation. (s.f.). *Blender Python API documentation*. https://docs.blender.org/api/current/

Shirley, P., & Marschner, S. (2009). *Fundamentals of computer graphics* (3.ª ed.). A K Peters/CRC Press.

Wikipedia. (2024, noviembre 15). *History of computer graphics*. https://en.wikipedia.org/wiki/History_of_computer_graphics

Rodríguez Morales, G. (2020). *Introducción a la graficación por computadora*. Universidad Tecnológica de México. https://www.utmachala.edu.ec/portalEIIS/wp-content/uploads/2020/03/Graficacion.pdf
