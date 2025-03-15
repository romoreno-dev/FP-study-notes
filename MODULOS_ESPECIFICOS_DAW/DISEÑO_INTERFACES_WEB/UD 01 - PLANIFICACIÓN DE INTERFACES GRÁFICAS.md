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



## 8. Componentes de una interfaz web



## 9. Mapa de navegación. Prototipos



## 10. Maquetación web. Elementos de ordenación

Centrardiv

## 11. Plantilla de diseño

Las **plantillas de diseño** son sitios webs prediseñados que pueden usarse como base a la hora de diseñar una web. 
Simplemente se adaptará la plantilla a las necesidades planteadas, facilitando la tarea del diseñador y ahorrando tiempo.
Existen gran cantidad de sitios web que suministran plantillas de forma económica y que permiten incluso el alojamiento gratuito de los sitios durante un tiempo determinado.
