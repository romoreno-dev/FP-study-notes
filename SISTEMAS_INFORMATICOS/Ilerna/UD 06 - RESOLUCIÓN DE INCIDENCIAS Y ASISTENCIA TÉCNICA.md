
## 6.1. Interpretación, análisis y elaboración de documentación técnica. Interpretación, análisis y elaboración de manuales de instalación

La **documentación técnica** de elaborarse tanto a la hora de documentar las tareas a realizar, como a la hora de ofrecer información a colaboradores y usuarios. 

**Características que debe contemplar**
- **Guía de referencia rápida**: Incluir una guía rápida que, a modo de esquema, recopile las funciones más frecuentes. Ej.: La opción de Ayuda de muchas aplicaciones web con pequeñas guías rápidas para orientar a los usuarios.
- **Adecuación al nivel de los destinatarios**: Tener en cuenta a quién va dirigida la documentación. Todos los destinatarios deben ser capaces de entenderla y, si son avanzados, considerar su nivel para no dar un exceso de información.
- **Características específicas del paquete de software**: No solo hablar del software, sino también de su versión ya que las características (licencia, propiedades) pueden variar de una versión a otra.
- **Capturas de pantalla**: Incluir imágenes que documenten el uso y manejo del sistema o la aplicación. Capturar con Impr Pant o Snagit o Gyazo.
- **Posibles problemas y errores**: Incorporar lista de posibles problemas y errores que el usuario puede encontrarse, junto con su solución. Estas listas deben actualizarse continuamente con los errores que van surgiendo entre versiones o actualizaciones por lo que debe ser escalable.
- **Glosario**: Para explicar términos con los que el destinatario no esté familiarizado, definiéndole y explicándole las palabras técnicas.

## 6.2. Instalación y configuración de sistemas operativos y aplicaciones. Licencias de cliente y licencias de servidor

Cada usuario (o grupo) requiere un sistema y unas aplicaciones específicas. Los usuarios solo deben tener acceso al software que necesitan y este y su configuración deben cubrir sus necesidades (Centro de Software de Ubuntu, Agregar o quitar programas de Windows). 

En la instalación del sistema operativo consideramos:

**Arranque desde el disco o pendrive de instalación**
El sistema se instalará con un disco externo o con un pendrive que lo habremos booteado  con Nero Burning Room (si vives en 2005), Daemon Tools, Rufus, Linux Live u otros.
Para ello en la BIOS o UEFIBIOS se deberá haber confirmado que se da prioridad de arranque al soporte elegido frente a las demás unidades. También la placa base puede tener la opción de modificar el dispositivo de arranque sin acceder a la BIOS (para evitar tener luego que volver a entrar a modificarla).

Debe considerarse el aspecto de las licencia y de cuales son necesarias (cliente, servidor,...) ya que las características y el precio varían. 

Los procesos de instalación de sistemas operativos pueden llevarse a cabo en numerosos equipos con la alternativa de la instalación desatendida. 

## 6.3. Instalaciones desatendidas e implementación de archivos de respuesta

Permite instalar el sistema y otras aplicaciones en multitud de equipos. No solicitan que se elijan opciones sino que bastan unos clics iniciales para que la instalación se inicie y no pare hasta completarse.

Las instalaciones desatendidas se pueden conseguir de dos formas:

**Forma 1: Crear la instalación desatendida a partir del software**
Ubuntu ofrece esta posibilidad mediante **Kickstart**. Se instala con `sudo apt-get install system-config-kickstart`
El programa tiene una interfaz gráfica a la que puede accederse desde Herramientas y configurar las opciones de idioma, zona horaria y demás detalles de la instalación.

**Forma 2: Crear una imagen de disco a partir de un sistema configurado**
Se instala y se configura a la perfección el sistema y las aplicaciones en equipo. Tras esto, se replican los contenidos en un pendrive, DVD o unidad de red y, a partir de él, se podrán obtener copias idénticas al disco duro original volcando toda la información de forma desatendida. Se puede hacer mediante aplicaciones como Macrium Reflect.

Los **archivos de respuesta** son ficheros que contienen definiciones y valores de configuración que se usan como guía durante la instalación.

En Windows son ficheros con extensión xml en los que se pueden especificar opciones sobre cómo crear las particiones del disco, como realizar la configuración de pantalla o los favoritos de internet. Tienen el nombre `unattend.xml`.

En Windows 10 también se pueden usar archivos de respuesta con la herramienta Sysprep y también con la herramienta "Administración y mantenimiento de imágenes de implementación (DISM)"
## 6.4. Servidores de actualizaciones automáticas

Los **servidores de actualizaciones automáticas** surgen para evitar que todos los ordenadores se actualicen al mismo tiempo provocando el colapso de la red.
Un buen ejemplo es Windows Server Update Services. Para ello debe contarse con un servidor Windows Server donde instalar el rol para realizar este servicio con el servidor elegido. 

La instalación de este rol requiere espacio de almacenamiento en disco duro para almacenar las descargas de las actualizaciones. Debe considerarse el tamaño y velocidad del disco, puesto que funcionará como almacén de consulta para el resto de equipos de la red.

En la configuración del rol se pueden gestionar todos los parámetros para no colapsar la red de trabajo: Configurar horas en las que se quiere llevar a cabo la actualización y la forma de hacerla, gestionar el tipo de descarga de la instalación descartando las que puedan ser más costosas y/o provocar cambios importantes en los equipos.
Windows tiene reportes y estadísticas de este servicio.
## 6.5. Partes de incidencias y protocolos de actuación

Se conoce como **incidencias** a aquellos eventos que no forman parte de las operaciones habituales de los servicios de red o locales. Provocan ralentizaciones, interrupciones,... por lo que deben contemplarse dos necesidades vitales:
- **Reanudación de los servicios**: Reanudar las operaciones lo más rápidamente posible para minimizar el impacto en la organización
- **Prevención de futuras incidencias**: Mecanismos para evitar en la medida de lo posible que la incidencia se vuelva a producir.

**Tipos de incidencias**
Hay de dos tipos:
- **Incidencias conocidas:** Cuando una incidencia específica coincide con problemas habituales, se busca una solución temporal mientras se indaga sobre una medida definitiva. Es importante aplicarla inmediatamente.
- **Incidencias desconocidas:** Si una incidencia no se ha producido con anterioridad y hay que registrarla.

Para registrar incidencias y prevenir fallos futuros los usuarios y los colaboradores deben realizar partes que permitan contar con un listado de incidencias. Los pasos una vez recopiladas las incidencias son:
1.- Clasificación de incidencias
2.- Investigación, posibles diagnósticos y soluciones
3.- Resolución de la incidencia y restablecimiento del servicio
4.- Incidencia archivada para futuras referencias

Es importante contar con tanta información como sea posible por lo que el parte debe recoger datos como la fecha y hora de la incidencia, el equipo físico en el que se ha producido y el software y el hardware instalado.

A partir de ahí se debe contar con un protocolo que dicte qué medidas tomar y que se debe elaborar a partir de las experiencias previas. 

Para generar la documentación de las incidencias hay varios métodos aunque se destacarán únicamente dos:

1. **Incidencias en documentos**
Se utilizan en entornos pequeños, con pocos usuarios y equipos, con una gestión de infraestructura liviana. No hay aplicación o formato fijo, aunque debe recopilarse la información principal, que se almacenará con formatos diferentes y habitualmente se consultarán con programas como Microsoft Excel.

2. **Incidencias en aplicaciones**
Las incidencias son gestionadas por aplicaciones en entornos grandes, donde la cantidad de máquinas y usuarios necesita ser gestionada para un correcto desempeño de sus funciones. Gran variedad de aplicaciones (Jira, Redmine, etc.) tanto de escritorio como web. 
Estas aplicaciones suponen un canal de comunicación entre usuarios y técnicos, permitiendo transmitir la incidencia y almacenarla. 

Este método ofrece escalabilidad, solventa la comunicación entre departamentos de forma sencilla y permite recopilar los datos para obtener reportes de forma sencilla y visual. 
## 6.6. Administración remota

Las **herramientas de administración remota** permiten tomar el control remoto de un ordenador a través de la conexión de red y solventar sus incidencias. El administrador ejecutará el software para tomar el control y los clientes tendrán un servicio o aplicación que se ejecutará automáticamente cada vez que el sistema arranque, de forma que el equipo permanecerá accesible siempre remotamente.

Windows brinda herramientas de asistencia remota bajo el nombre "Conexión a escritorio remoto"

También existen otras alternativas como TeamViewer permitiendo conexión entre sistemas Windows y Linux.

Otra opción más práctica es UltraVNC, que permite trabajar a través de la red local. Es software libre y permite visualizar el escritorio desde otro ordenador y trabajar con él en todas sus facetas. Esta se trata de un paquete compuesto por dos aplicaciones independientes:
 - Un **Server**: Debe agregarse al equipo que se desea controlar
 - Un **Viewer**: Debe añadirse al ordenador desde el que se desea ejercer el escritorio remoto.
Se instala UltraVNC Server en los ordenadores en red. Se descargan ficheros adicionales para Vista (Vista addons files) y un controlador que mejorará el rendimiento en sistemas como Vista o XP (Download the mirror driver). En Windows 10 no será necesaria ninguna de esas opciones.
Tras esto, se ejecuta UltraVNC Server en el equipo que se desea controlar y se configura para que se ejecute automáticamente siempre que se arranque (agregar como servicio). 

Posteriormente, se instala y se ejecuta UltraVNC Viewer en el ordenador desde el que se desea ejercer el control. 

**Otras herramientas de gestión remota**
- **SSH** (Secure Shell, intérprete de órdenes seguro). Protocolo mediante el cual es posible acceder a la línea de comando del ordenador. 
- **Putty**: Otro software de control remoto.