
La documentación de aplicaciones es importante en cualquier proyecto. Sin embargo, es un proceso tedioso al que a veces no se dedica suficiente tiempo. Por dicho motivo, a veces es recomendable automatizar el desarrollo de documentación.
## 1. Archivos de ayuda. Formatos

**Ayuda contextual**
Ofrece a través de elementos visuales o de texto, un acceso más rápido y directo a la función que desea realizar.

- **Tooltips**: Elementos que aparecen cuando el ratón se posiciona para dar al usuario alguna ayuda sobre ese elemento
- **Ficheros de ayuda**: Ofrecen ayuda al usuario al pulsar F1. (ApplicationCommands.Help es una clase a la que pertenecen los comandos más frecuentes como operaciones de apertura y cierre, imprimir, copiar y pegar)

## 2. Herramientas de generación de ayudas

Durante el desarrollo de código, es posible ayudarse de comentarios que se detallan sobre él para documentar de qué trata. 
Se conoce como **metainformación** y se escribe precedido de los caracteres `///` delante del código. 

**GhostDoc**
- Extensión de VisualStudio que permite generar de forma automática documentación XML con toda la información sobre los comentarios de un código determinado junto con sus principales funciones. Se hace uso de la documentación correspondiente que le facilita Microsoft o el proveedor de la librería usada.

- **Instalación**: A la hora de crear la documentación en XML se deben seguir los siguientes pasos:
	- Opción para compilar
	- Opción de archivo de documentación XML
	- Definir el nombre junto con la ruta correspondiente

**SandCastle**
- Creada por Microsoft y se usa también para crear documentación correspondiente a un documento determinado pero basándose en el estilo MSD de .NET con comentarios XML que estén asociados.
- Se basa en línea de comandos y no cuenta con una GUI definida. 

- **Instalación**: Se deben instalar una serie de paquetes

- **Interfaz gráfica Help File Builder**: Permite que el usuario pueda tener todo más accesible, mejorando el entorno visual. 

**HelpNDoc**
Alternativa a SandCastle que permite generar diferentes archivos de ayuda en formatos como .chm, .pdf o .html.
Se debe crear un nuevo proyecto, seleccionar datos correspondientes a nombre, indioma y tabla de contenidos y realizar las configuraciones de la herramienta. 

## 3. Tablas de contenidos, índices, sistemas de búsquedas, entre otros

Con las tablas de contenidos se puede elaborar la estructura correspondiente de un proyecto.
En ellas se pueden identificar títulos de los temas / subtemas que intervienen en el proyecto.
La tabla puede contener el número de página o no.

(Valiente mierda...)
## 4. Tipos de manuales

Mientras se desarrolla un proyecto, se generan diferentes tipos de documentación que deben entregarse a los usuarios correspondientes para que cuenten con la información determinada del producto desarrollado. 

#### Manual de instalación

Detalles necesarios para realizar la instalación: aspectos del software según el sistema operativo, aplicaciones necesarias, características del hardware, cantidad de RAM. 
Puede existir una versión **reducida** que implica instalación rápida con los valores por defecto o **detallada** donde se explica de forma ampliada todos los aspectos que intervienen en la instalación. 

#### Documentación de configuración

Se deben hacer constar todos los parámetros que tengan que ver con la configuración de una aplicación, además de los cambios que se puedan producir en el momento en el que funcione la aplicación.

Se tratan aspectos como software, hardware, visuales, etc. 
Se define la forma en la que se ejecutan las aplicaciones o librerías que necesita el proyecto. 

Se tendrán en cuenta aspectos variables y sus consecuencias en el funcionamiento.

Se puede distinguir entre configuración **normal** o **avanzada** (parecida a la anterior pero detallando de forma exhaustiva aspectos complejos para usuarios con mayor experiencia y conocimiento como los administradores)

#### Manual de usuario

También puede existir versión **rápida** y **detallada** (amplía las opciones a la hora de realizar posibilidades de la aplicación).

Este manual puede incorporarlo la interfaz de usuario de una aplicación. El usuario real debe identificar en las imágenes la interfaz real de la aplicación.

Hay distintos tipos de versiones de manual: principiante, inicial, medio, avanzado y experto; esto implicará profundizar más o menos en las diferentes aplicaciones (describiendo cada acción y valores que debemos proporcionar o elegir)

##### Partes
- **Introducción**: Para qué sirve la aplicación. Qué funcionalidades tiene cada rol en ella.
- **Propósito general de la aplicación**: Qué soluciona
- **Guía de instalación**: Cómo instalarla y ejecutarla
- **Guía de uso**: De cada rol con capturas de pantalla
- **Mensajes de error**: Capturas de pantalla y descripción de los errores
- **Preguntas o dudas más frecuentes (FAQ)**

#### Guía de usuario

Mismo objetivo que el del manual de usuario pero buscando indicar de forma rápida y sencilla ciertas funcionalidades del producto.

#### Guía rápida

Breve resumen muy sintetizado de todos los aspectos importantes.

#### Manual de administración

Se detalla la instalación, la administración del sistema. Y el proceso de configuración de los componentes que forman parte del sistema. 





