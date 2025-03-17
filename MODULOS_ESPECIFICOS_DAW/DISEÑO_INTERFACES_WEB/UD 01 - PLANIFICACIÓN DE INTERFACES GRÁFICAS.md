(UF1 Diseño de la interfaz)
## 1. Elementos de diseño. Percepción visual

Al desarrollar un sitio web debe tenerse en cuenta **qué** se ofrecerá en la interfaz y **qué elementos** se incluirán en ella.
La parte visual de los elementos (tamaño, ubicación, tipografía, colores,...) influirán directamente en el usuario del sitio web, que la podrá interpretar de una forma u otra.

El diseñador primero debe:
- **pensar en los valores a asignar en cada elemento y valorar la relación entre sus diseños** y su percepción
- **buscar un equilibrio entre los elementos que forman la interfaz** para conseguir un sentido gráfico de su diseño que facilite la comunicación eficaz. No debe usar demasiados elementos innecesarios que pueden provocar distracción, exceso de ruido y dificultar la comprensión del mensaje. 

Una vez asimilada la información, deben buscarse soluciones que se adapten a este propósito: **Se determinará el área de diseño**, asignándose un tamaño para determinar el espacio del que se dispone para la composición gráfica.

La **composición gráfica**:
- Puede estar formada por uno o varios elementos
- Puede estar compuesta solo por texto o solo por imágenes
- Puede tener espacios en blanco o combinar diferentes elementos gráficos
- Debe ser lo más adecuada a lo que se quiere comunicar

## 2. Color, tipografía, iconos

Los elementos más destacados en las composiciones son: Color, tipografía e iconos. El tipo y la cantidad de los elementos depende de la información que se quiera transmitir.
### 2.1. Color

Los colores se basan en el estándar RGS (red, green, blue). Se puede conseguir cualquier otro color mediante la combinación de estos tres. La intensidad de los colores se presenta en números hexadecimales desde 00 hasta FF. Para indicar que se trata de un valor de color se pone una almohadilla delante.

Colores RGB:
- Rojo `#FF0000` (255,0,0) 
- Verde `#00FF00` (0,255,0) 
- Azul `#0000FF` (0,0255) 
- Negro `#000000` (0,0,0) (No activando ningun color)
- Blanco `#FFFFFF` (255,255,255)  (Activando todos los colores)
- Amarillo `#FFFF00` (255,255,0)
- Fucsia `#FF00FF` (255,0,255)
- Gris plata `#C0C0C0` (192,192,192)
- Azul marino `#000080` (0,0,128)
- Verde oliva `#808000` (128,128,0)

También pueden obtenerse los colores haciendo referencia a su nombre en inglés. 

La **combinación de colores requiere un carácter artístico del desarrollador** que puede no tener por lo que todo proyecto grande está compuesto también por diseñadores que se dedican exclusivamente a esta función. 
También existen programas informáticos que realizan la acción de combinar los colores de forma automática y armónica para facilitar el desarrollo de proyectos sin contar con un diseñador (Colorpix, Color Schemer Online, What Is Color,...). Estos programas permiten
- Buscar imágenes que satisfagan un patrón concreto de colores
- Obtienen código a partir de un color seleccionado
- Crear combinaciones a partir de un color determinado

### 2.2. Tipografía

La **tipografía** es el arte y la técnica de diseñar, componer y organizar los tipos de letra para hacer que un texto sea legible, atractivo y funcional.

Para elegir una buena tipografía debe considerarse: 
- El tamaño
- El color
- El espacio entre letras
- El interlineado, etc. 

**No se aconseja usar más de tres fuentes en un mismo sitio web**

Los navegadores y sistemas operativos pueden limitar la selección de un tipo de letra concreto. Para evitarlo es conveniente la elección de un tipo de letra generalizado para obtener el mismo aspecto en todos (o definir varias fuentes para que, si no se dispone de una, se pueda aplicar alguna de las otras)

Algunas de las propiedades CSS que permiten modificar la tipografía son:

| Propiedad     | Valor                       | Significado         |
| ------------- | --------------------------- | ------------------- |
| `font-family` | Fuente                      | Nombre de la fuente |
| `font-size`   | Tamaño                      | Tamaño de la fuente |
| `font-style`  | normal \| italic \| oblique | Estilo de la fuente |
| `font-weight` | normal \| bold \| grosor    | Grosor de la fuente |
### 2.3. Iconos

**Icono** es la técnica mediante la cual se designan imágenes gráficas (generalmente pequeñas, pictogramas) con el objetivo de **relacionar acciones en concreto con ellas**, siendo uno de los elementos gráficos más empleados. 
Se evita tener que dar grandes explicaciones textuales para realizar una acción determinada, mejorando la visualización del sitio web.

Los iconos deben estar también **estandarizados** para que tengan un mejor impacto en el usuario y no se produzca una mala interpretación (debe hacerse una buena **elección de imágenes**)
## 3. Interacción persona-ordenador

La **interacción persona-ordenador** (IPO) permite estudiar de forma ordenada el intercambio de información existente entre usuario y ordenador.

Se llama *intercambio de información eficiente* cuando se produce una buena comunicación, reduciéndose los errores y consiguiéndose satisfacción por parte del usuario. 

La mayoría de sistemas son interactivos y su éxito o fracaso dependerá de la interfaz entre el usuario y el ordenador.

Es esencial que **la interfaz gráfica esté siempre pensada mirando por las necesidades que requiera el usuario**. También debe estar pensada para distintos tipos de usuarios, con distintos grados de preparación, intentando cubrir las expectativas de todos y adaptándose al mayor número de personas posibles. 
## 4. Interpretación de guías de estilo. Elementos.

Los **manuales de estilo** son un grupo de normas que pueden ser utilizadas tanto para el diseño de documentos como para la redacción de estos. 
Se suelen usar manuales de estilo para medios escritos, orales y gráficos. Estos cuentan con un conjunto de normas lingüísticas y de estilo que propician que el lenguaje sea más eficaz, coherente y correcto. 

_Ejemplo del manual de estilo del Gobierno de Navarra_ (https://gobiernoabierto.navarra.es/sites/default/files/manual_estilo_simplificacion_aprobado.pdf)

Aplicado al diseño de las interfaces web, la **guía de estilo** es un documento en el que se definen las pautas junto con las normas de calidad que debe tener en cuenta una interfaz web en un determinado sitio web. 

El diseño de las interfaces web se centra en:
- **Planificación**: Qué es lo que se quiere hacer
- **Coordinación**: Del equipo de desarrollo encargado del diseño

La guía de estilo asegura estos puntos ya que:
- **Garantiza la coherencia** de un sitio web.  Aporta aspectos sobre la calidad de su uso, accesibilidad, diseño gráfico,...  Considera cuestiones sobre colores y otros elementos de diseño.
- **Aglutina en torno a un mismo objetivo todo el conjunto del equipo de trabajo**. 

## 5. Generación de documentos y sitios web

Los **gestores de contenidos** (**CMS, Content Management System**) permiten crear diferentes sitios web a partir de cero. Es la interfaz que permite controlar una o varias bases de datos donde se encuentra alojado el contenido web. Este sistema permite controlar el contenido y el diseño de forma independiente. Ejs.: Wordpress, Joomla, Drupal, OpenCMS.

- Pueden crearse utilizando plantillas prediseñadas que facilitan la tarea. 
- Un administrador determinado puede originar contenidos sin necesidad de conocer el tema a fondo.
- Algunos de estos gestores están basados en tecnologías webs mediante lenguaje PHP/HTML y sistemas de bases de datos MySQL. 
- Muchos de los CMS son de código y licencia libres

## 6. Aplicaciones para el desarrollo web

Las **aplicaciones para el desarrollo web** facilitan las tareas de planificar, diseñar, desarrollar y mantener un sitio web. Así el diseñador no tiene por qué partir de cero sino que puede partir de ellas y, con menos esfuerzo, dedicar sus conocimientos y tiempo a otros aspectos más importantes.

Se clasifican en:
- **General**: Se utiliza para programas con interés general, cualquier tipo de usuario
- **Diseño**: Referentes al diseño de las distintas páginas web
- **Multimedia**: Realizar animaciones
- **Programación**: Orientadas a los desarrolladores que crearán el sitio web
- **Editores y validadores HTML**: Permiten la edición de lenguaje de marcado HTML
- **Editores y validadores CSS**: Permiten la creación, edición, validación de lenguaje de marcado CSS. 

## 7. Lenguajes de marcas

Los lenguajes de marcas (HTMl, XML, RDF) permiten forman un sitio web. Estos son un tipo de lenguaje que no tiene variables, ni funciones aritméticas. Se combina el texto con etiquetas.

**HTML (Hypertext Markup Language)** es el lenguaje más conocido para el desarrollo de páginas web. Se puede utilizar para definir estructura y determinar el contenido. 
- Dispone de etiquetas que informan al navegador de la presentación dentro de un documento (título, tamaño, posición, vínculos)
- El texto irá limitado entre una etiqueta de apertura y otra de cierre (entre corchetes angulares, cumpliendo normas sintáticas). `<nombre_etiqueta>...</nombre_etiqueta>`
- En la **versión 1.0** solo se mostraban textos con estilo (títulos ,parráfos, viñetas, listas,...)
- En 1995 se publica la **versión 2.0** de HTML por parte del W3C (World Wide Web Consortium) que se encargó de crear estándares para todos los temas relacionados con la web. Aportaba compatibilidad con navegadores y nuevas etiquetas (imágenes, tablas, vínculos, formularios)
- La **versión 3.0** empresas como Netscape y Microsoft aportaron nuevas etiquetas. Aparecieron lenguajes como PHP (Hypertext Preprocessor) y ASP (Active Server Pages) que se propusieron para funcionar con BBDD y aprovechar la interactividad con la web.
- La **versión 4.0** en 1998 incorpora las hojas de estilo CSS, el uso de scripts, mejora la accesibilidad web, agilidad en formularios y permite realizar tablas complejas. Aparece Java con juegos y aplicaciones.
- **HTML5** es el estándar actual surgido en 2004 por la asociación Web Hypertext Application Technology Working Group (WHATWG) formada por Mozilla, Opera y Apple. Se consigue una revolución en el desarrollo web ya que se permite incluir elementos multimedia, entre otras funcionalidades. 

## 8. Componentes de una interfaz web

Los **componentes de la estructura de una interfaz web** son **todas las partes** que forman parte de un sitio web.
A lo largo de los años los diferentes diseños han avanzado hacia la **unificación** mostrando interfaces bien definidas mediante componentes gráficos que permiten que, independientemente del usuario, pueda acceder a la interfaz. 

Existen una serie de elementos asentados utilizados en la mayoría de interfaces como pies de páginas, formularios, cabecera,...

Dentro de los componentes más principales de la interfaz web se podría mencionar:
- *Header* (cabecera)
- *Body* (cuerpo)
- *Footer* (pie)

**Cabecera**
La **cabecera** (header) es la zona situada en la parte superior de la interfaz web.
- Se usa para situar el logotipo de la empresa o su nombre.
- Puede ir acompañada de otros elementos de diseño como imágenes, textos descriptivos o formularios de acceso.

Los principales **objetivos de la cabecera** son:
- **Identificar el sitio web con la empresa que representa** a través del logo tipo y del nombre
- **Identificar y unificar todas las páginas** que pertenezcan al mismo sitio web
- **Separar el borde superior de la interfaz de la parte central** para facilitar la visualización

- La jerarquía visual hace que la cabecera esté en la **parte superior de la interfaz** y el logotipo en la parte izquierda. 
- No son obligatorias pero la forma más empleada sería **rectangular**. 
- Debe seleccionarse la que en cada caso presente un mayor impacto visual de acuerdo con el tema que se esté tratando. 

**Sistemas de navegación**
Los **sistemas de navegación** permiten navegar por las distintas páginas que componen una página web. 
- Es frecuente que se presenten en forma de **menús** con una serie de opciones mediante las cuales el usuario puede interaccionar al seleccionarlas.
- Pueden **incorporar iconos, textos o ambos**. Es posible incorporar efectos dinámicos que permitan ofrecer interacción con las diferentes opciones. 
- Son importantes porque permiten que el usuario se mueva por las diferentes partes sin que se estorben los elementos. 
- Pueden hacerse mediante capas usando CSS y JavaScript.
	- **Menú de árbol**: Las opciones pueden aparecer y desaparecer según las acciones que el usuario ejecute sobre las funciones principales
	- **Menú de pestaña (lista)**: Simula el aspecto de un archivador. La pestaña que esté activa en primer plano tiene un color distinto al del resto de pestañas. 
- Suelen situarse en la **parte lateral izquierda** por motivos de funcionalidad y uso. Si son demasiadas opciones es recomendable usar **menús dobles** y jerarquizas las diferentes opciones, así el usuario podrá acceder de forma sencilla. 

**Cuerpo de página**
En el **cuerpo** se muestran los contenidos.
- Debe estar **situado en la zona más importante**: Parte central (si la hay), bajo la cabecera y al lado de un menú lateral para navegación (si lo hay)
- Los **contenidos pueden variar** dependiendo de si es una página con formulario, tablas o fichas,...
- Aunque **existen elementos que deberán estar presente en todas las páginas**: Generalmente **estará formado por un título que identifica la página** (en la parte superior de esta) y **dispone de menú de navegación**.
- Es **conveniente que las palabras del menú tengan un tamaño mayor o un color distinto** para que destaque sobre el resto de la página, al ser este un elemento clave para la navegación.

**Pie de página**
El **pie de página** (footer) está situado en la parte inferior de la web bajo el cuerpo de la página.
- Permite visualizar distintos enlaces a servicios concretos: Formularios de contacto, ofertas de empleo, etc. O referencia a la empresa propietaria del sitio web o a la persona que ha desarrollado la web.
- Si el pie de página dispone de menú, suele utilizarse como menú auxiliar que permite a los usuarios navegar por la interfaz web sin necesidad de volver al menú principal. 

**Espacios en blanco**
- Son un elemento esencial de las interfaces web porque son encargados de definir las zonas que no tienen elementos gráficos.
- Los desarrolladores los usan como cualquier otro elemento, definidos desde el momento inicial.
- Logran un diseño no sobrecargado y bien delimitado. 

## 9. Mapa de navegación. Prototipos

Los **mapas de navegación** se utilizan para representar la estructura de las páginas de un sitio web, facilitando tanto al desarrollador como al usuario conocer qué páginas llevan a otras.
Se debe realizar un esquema que permita visualizar las secciones en las que se ha dividido el sitio web y la relación entre los bloques antes de diseñar el sitio web.

Los mapas pueden representarse de forma gráfica, dónde la página principal actúa como elemento raíz a partir del cual salen las diferentes ramificaciones. 

En ocasiones la complejidad del diseño hace difícil comprender lo que el cliente quiere transmitir al equipo de desarrollo y los objetivos a conseguir, por eso los **prototipos** son herramientas que permiten optimizar tiempo, mostrando un esquema del sitio web una vez se finalice pero empleando mucho menos tiempo que si se hubiese realizado realmente. 
Es como crear un borrador a partir del que se desarrollará la idea del sitio web. 

El prototipo resuelve:
- Qué elementos formarán la interfaz de cada página
- Qué elementos tendrán en común las distintas páginas
- En qué orden se verán las páginas (orden del mapa de navegación)
- Qué aspectos tener en cuenta para desarrollar el sitio web (aspectos técnicos de accesibilidad y usabilidad)

Después de tener el mapa de navegación y los prototipos, lo siguiente es realizar el desarrollo del sitio web mediante plantillas elaboradas o alguna propia.

## 10. Maquetación web. Elementos de ordenación

La **maquetación** toma como referencia el espacio disponible para situar en él los elementos que forman la página web.

Se encarga de **separar el contenido de la presentación**. Así se consigue el mantenimiento y cambio de los contenidos de forma sencilla.

Antes la maquetación se realizaba usando tablas (`<table><tr><td>`) pero el código era complejo de entender y los navegadores tenían problema a la hora de analizar la página. Actualmente se realiza maquetación usando capas (`<div>`), conocidas como divisiones o contenedores.
**Distribución de elementos en la interfaz: capas**
- Se podrían mencionar **capas** y **marcos**

Las capas (div, layout) son contenedores en los que se pueden colocar los diferentes elementos. Se caracterizan por:
- **Anidamiento**: Unas pueden estar ubicadas dentro de otras. Se define cómo se posicionan, el tamaño que tendrán y dónde estarán ubicadas.
- **Diferentes bloques con contenido HTML, posicionados de forma dinámica**. Requieren del uso de CSS, posicionando el elemento mediante cambios del estilo (no quedan definidas completamente con HTML).

```html
<!DOCTYPE html>
<html>
	<body>
		<p>Esto es un texto</p>
		<div style="background-color:lightblue">
			<h3>Título del div</h3>
			<p>Texto dentro del div</p>
		</div>
		<p>Resto de la web</p>
	</body>
</html>
```

### 10.1. Desmontando el mito del desarrollador backend: Cómo centrar un div.

```html
<div class="parent">
	<div class="child">El div centrado</div>
</div>
```

**Usar flexbox**
En el contenedor del padre, se le indica que sus hijos deben estar centrados.

```css
.parent {
	display: flex;
	justify-content: center;
	align-items:center;
	height: 100vh; 
}
```

**Usar grid**
```css
.parent {
  display: grid;
  place-items: center; /* Equivalente a flexbox pero más corto */
  height: 100vh;
}
```

**Usar `margin:auto`** (Centrar solo horizontalmente)
```css
.child {
  width: 200px;
  margin: 0 auto;
}
```

**Usar `position:absolute`** (No recomendado)
```css
.parent {
  position: relative;
  height: 100vh;
}
.child {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

---
```css
body {
	display: flex;
    flex-wrap: wrap; /* Permite que los elementos pasen a la siguiente fila */
    justify-content:center;
}
```

---
## 11. Plantilla de diseño

Las **plantillas de diseño** son sitios webs prediseñados que pueden usarse como base a la hora de diseñar una web. 
Simplemente se adaptará la plantilla a las necesidades planteadas, facilitando la tarea del diseñador y ahorrando tiempo.
Existen gran cantidad de sitios web que suministran plantillas de forma económica y que permiten incluso el alojamiento gratuito de los sitios durante un tiempo determinado.
