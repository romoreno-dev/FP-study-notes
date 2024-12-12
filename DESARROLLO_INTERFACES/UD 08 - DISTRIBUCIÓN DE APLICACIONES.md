
Una de las funciones más importantes del IDE es el despliegue de paquetes. Importante el generar un archivo ejecutable tras realizar el proceso de compilación creando diferentes paquetes de instalación mediante un asistente guiado.

### La gestión de versiones

Existe un sistema de versionado que depende de una serie de factores como tipo de producto y fabricante.
Suele incluir la secuencia `major.minor`. 

Se suelen utilizar **las versiones impares como versiones beta y las pares como versiones liberadas**

Los informes se llevarán a cabo siempre identificando la versión del producto.

`[assembly:AsemblyVersion("2.1.1524.1")]`
- Major
- Minor
- Build
- Revision
## 1. Componentes de una aplicación. Empaquetado

#### Paquetes
Existen paquetes que constan de componentes individuales y otros están formados por un conjunto de aplicaciones relacionadas entre ellas. 
Cuando se crea un paquete, se puede distribuir a otros usuarios  y organizaciones. 

Los paquetes se clasifican en: 

- **Paquetes gestionados**: 
Se utilizan para vender o distribuir aplicaciones a los clientes. Es conveniente que se creen en una organización `Developer Edition` para que los desarrolladores encargados de crearlos tengan control para su gestión y venta. No hay problema en las actualizaciones por lo que, cuando aparecen modificaciones o eliminaciones, no las realizan para no correr riesgos. 

Ventajas: Protegen la propiedad. Compatibles con otras versiones. Tienen capacidad para añadir divisiones o parches a versiones anteriores. Son capaces de enviar actualizaciones de parches y permiten asignar nombres únicos a cada uno de sus componentes para evitar conflictos en el proceso de instalación. 

- **Paquetes no gestionados**: 
Usados en proyectos de código abierto. Suelen brindar a los desarrolladores los fundamentos principales de una determinada aplicación.
Es posible realizar modificaciones oportunas en la organización en la que se han instalado. 
El desarrollador encargado de crear el paquete sin gestionar no es el que tiene asignado el control de los componentes, por lo que no puede modificarlos. 

- **Componentes**: 
Conjunto de elementos (objeto personalizado) que forman un paquete. Los distintos componentes de un paquete pueden ser unificados para crear determinadas funciones. 

En los paquetes sin gestionar los componentes no se pueden actualizar; en los paquetes gestionados es posible actualizar algunos de ellos. 

- **Firma de componentes**: 
Componentes en los que debe verificarse su origen para garantizar su autenticidad. Por ejemplo, verificando su firma. 

## 2. Instaladores

**Creación de paquetes de instalación**
Al publicar un paquete de instalación se puede especificar el lugar desde el que se va a realizar (servidor web / FTP)

Después de realizar la instalación en un paquete, puede ser necesario implementar una serie de componentes del paquete para que esté disponible para los usuarios que forman parte de la generación. 

El modo de instalación de un proyecto define si es accesible desde un servidor web, desde un solo punto de la red o desde el propio escritorio usando diferentes menús. 

Los paquetes de actualización incorporan configuraciones importantes que permiten crear soluciones personalizadas. El paquete de instalación tiene un repositorio donde se publican las versiones de sus archivos de instalación junto con las instalaciones y el cliente puede acceder a él mediante un enlace. 

Deben considerarse en el paquete de instalación el listado de archivos que instalar así como los prerrequisitos que deben cumplir antes de comenzar con el proceso (como el uso de frameworks).

**Opciones de publicación de software**. 
Las opciones de publicación se dividen en cuatro secciones según un aspecto concreto del despliegue:
- **Descripción**: Se definen datos básicos del archivo de publicación: Nombre, idioma de publicación, configuración y carpeta que contendrá el software dentro del menú inicio
- **Implementación**: Dato clave como creación de página web a partir de la cual se realiza el despliegue, extensión del paquete, verificaciones de integridad, comenzar de forma automática al insertar un CD. 
- **Manifiesto:** Comportamiento de la aplicación a la hora de controlar el acceso. (Ejecución a través del menú inicio, ejecución a través de URL, acceso directo en el escritorio...)
- **Asociaciones de archivo**: Configuraciones del icono de la aplicación y extensión del sistema. 

Se puede generar archivo **setup** en la opción generar de Visual Studio. En el editor se debe haber configurado dónde se van a almacenar los archivos setup. 
Una vez generado, en la carpeta `Repositorio` están todos los archivos instalables, para seleccionar aquellos archivos deseados. 
Los instalables pueden facilitarse a las personas que se interesen por el programa. 

**Secuencia de instalación**
- Ejecutar instalador
- Opciones definidas a la hora de instalar
- Información y advertencias de los requisitos
- Directorio o carpeta de instalación
- Requisitos previos que deben tenerse y/o opción de instalarlos
- Confirmación e instalación
- Creación del acceso directo en el escritorio

## 3. Paquetes autoinstalables

**Nuget** es de código abierto y simplifica el empaquetado de paquetes y su instalación.
La persona que desarrolla el código no tiene por qué descargar, descomprimir y ejecutar las opciones referentes al proyecto. 

Nuget: 
- Descarga el archivo que contiene el paquete
- Extrae el contenido
- Realiza referencias a los ensamblados
- Copia el contenido completo 
- Aplica características específicas de cada paquete
- Ejecuta scripts de automatización 

**Creación de paquete con Nuget**
Un paquete con Nuget se crea sencillamente ya que solo hay un ensamblado para representar un componente. Pasos:
- Se crea un proyecto de tipo `class library`
- Se genera el manifiesto NuSpec para el proyecto (archivo correspondiente al paquete con el manifiesto de los metadatos básicos como autor, descripción, dependencias etc.). Debe tener formato simple para que todos puedan acceder a él y se ejecuta desde el directorio en que se encuentra el proyecto
- Es posible actualizar los metadatos de ensamblado del proyecto. Su fin es asegurar que no haya discrepancias entre este y el del punto anterior.
- Con `NuGet.exe` se crea el paquete mediante el comando `nugetpack`  que se encuentra en el mismo directorio del proyecto y del archivo `NuSpec`
`Nugetpack nombreProyecto.csproj`

**Creación de paquete Nuget con interfaz gráfica**
La interfaz gráfica puede obtenerse en www.nuget.org

Mientras se realiza el proceso de instalación se puede comprobar los archivos que se encuentran en la dirección URL. Los clientes solo descargan la instalación y no es necesario que lancen el paquete completo.

Una vez instalado, pueden crearse paquetes de forma sencilla usando las tareas comunes o el menú archivo.

Los datos pertenecientes a un paquete completo que se pueden editar (metadatos) permiten que el desarrollador haga uso de sus valores a través de la interfaz. 

## 4. Herramientas para crear paquetes de instalación

Visual Studio anteriormente disponía de plantillas para generar paquetes de instalación aunque en versiones actuales ha sido retirado.

Se utiliza la aplicación WiX (Windows Installer XML). Esta herramienta permite crear paquetes de instalación de Windows y, una vez compilados, generar su ejecutable correspondiente. (www.wixtoolset.org)

Con WiX se pueden crear paquetes a partir de código XML con extensión `.msi` o `.msm`. Está bien conectado con Visual Studio y una vez instalada es posible usarla para crear como una extensión más. 

En cualquier archivo se apreciará lo siguientE:

```xml
//Raíz del archivo
<Product> //Creación de un producto que representa al instalador
<Package> //Comprensión del paquete
<Media> //Dispositivo en el que se divide la instalación.
//Casi siempre es un solo dispositivo.
<Directory> //Ruta en la que se va a instalar el archivo
<Component> //Componente de la instalación
<File> //Ficheros que se van a instalar
<Feature> //Configuraciones disponibles en la instalación:
//típicas, personalizadas, detalladas
```

En la instalación se deben poder modificar:
- del sistema de archivos (carpetas, archivos, acceso directo)
- del registro del sistema operativo (nuevos registros o modificar ya creados)
- de tipos de archivo (asociaciones de archivos en el sistema)
- de acciones personalizadas o verificaciones del despliegue (asegurarse de que se cumplen los requisitos)

Y todos esos cambios deben estar representados en el archivo XML. 
Finalmente también debe indicarse el tipo de archivo de salida del instalador una vez compilado el XML (frecuentes .msi (Windows Installer Package) o .exe (Executable Package))

## 5. Personalización de la instalación: logotipos, fondos, diálogos, botones, idioma, entre otros

### 5.1. Colores
- Es secundario. No es necesidad básica
- Es fuente de información secundaria. No confiar como único medio de información
- Evitar colores llamativos
- Aplicar conjunto limitado de colores. Colores apagados, sutiles y complementarios es más apropiado en interfaces de corte empresarial y académicas. Se recomiendan colores primarios y cálidos. 
- Uso de paletas de clores da unificación, consistencia y formalidad 
- El usuario debe poder personalizar cualquier parte que considere importante

#### 5.2. Fuentes
- No más de tres fuentes y tamaños de letra en la aplicación
- Para organizar información y establecer enfasis en la frase
- Estilo mayúsculas de encabezado: Iniciar en mayúsculas todas las palabras de los elementos salvo un(a), el, la, los, las, y, pero, mas, para, todavia,...
- Estilo mayúsculas de oración: En mayúscula la primera letra de la palabra inicial y cualquier otra palabra normalmente iniciada en mayúscula
- Evitar fuentes cursiva y serif
- Limitar número de fuentes y estilos usados
- Usar negritas adecuadamente
- Usar fuente estándar del sistema para elementos comunes de la interfaz; estandarizando su aplicación con las demás ventanas
- Frases breves y concisas: Lenguaje claro, sin errores gramaticales ni ortográficos. Mensajes de aviso deben ser positivos y de ayuda al usuario. 

#### 5.3. Iconos
- No deben ser llamativos y deben ir acompañados de una palabra inferior que indique su función (abrir, cerrar, aceptar,...)