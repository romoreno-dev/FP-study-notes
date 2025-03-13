(UF4 Control de Versiones y Documentación)

## 1. Documentación

En la realización de la documentación de una aplicación conviene documentar: 
- La **interfaz**: Canal a través del cual el usuario (del nivel especificado) se comunica con software de nivel más bajo, con su propio equipo, una máquina remota, un dispositivo o un usuario, entre otras. (QUÉ hace una función ,método, clase, parámetros a pasar, qué devuelve. Útil para las personas que usan funciones o clases diseñadas por otros)
- La **implementación**: Indicará el funcionamiento de cada componente o función. Es útil para quienes tienen que depurar o actualizar los bloques de código de la aplicación. (CÓMO está implementada la función, cómo se lleva a cabo cada paso)
- La **toma de decisiones**: Se indicará por qué se ha decidido realizar cada acción de la aplicación. Interesante a la hora de implementar la aplicación por parte de los desarrolladores y a nivel funcional por parte de los responsables de desarrollo (POR QUÉ se ha implementado de una forma y no de otra.)

Aunque la implementación no debe ser transcrita fuera del código, la interfaz sí debe ser puesta en un documento independiente del código fuente (**manual de uso**).
Sin embargo, si hay cualquier cambio o modificación del código, esto debe quedar reflejado en el manual de uso lo que puede implicar doble trabajo.

Existe la forma de automatizar el proceso para que se genere la documentación a través del código fuente utilizando herramientas como **phpDocumentor** para PHP o **JavaDoc** para Java.

Los entornos de programación modernos son capaces de obtener la información de los comentarios, mostrándola en el "autocompletado" de código, lo cual se convierte en una herramienta estupenda (e imprescindible en lenguajes como PHP en los que no es necesario declarar el tipo de argumento)

La **documentación es parte importante del proyecto**, tanto como el código porque gracias a ella se puede mantener la aplicación adelante y, en caso de trabajar en equipo, conocer y saber el funcionamiento de las partes realizadas por el resto. 
## 2. Herramientas externas para la generación de documentación. Instalación, configuración y uso

**phpDocumentor** se comporta de forma parecida a como lo hace JavaDoc. Mediante comentarios o etiquetas sencillas se define lo que realiza cada clase, método o función del código.

Se permite generar la documentación de varias formas y en distintos formatos como desde la línea de comandos, la interfaz web o el código.

Deben indicarse los siguientes parámetros:
- **Directorio donde se encuentra el código**
- De forma opcional, los **paquetes (@package) que quieren documentarse**, ficheros incluidos o excluidos
- **Directorio donde se generará la documentación**
- **Indicar si la documentación será pública** (solo interfaz) o interna (se mostrarán bloques private y comentarios @internal)
- El **formato de salida de la documentación** (HTML, PDF, XML). 

**Doxy-gen** sirve de alternativa a phpDocumentor, siendo un programa que trabaja en PHP, mientras que phpDocumentor es una colección de código.

#### Funcionamiento de phpDocumentor

En phpDocumentor la información es distribuida en bloques **DocBlock** que se colocan justo antes del elemento que a documentar y el formato es:

```
Descripción breve (una sola línea)
/**
*Comentario extenso
*Cada línea irá con *
*/
<- Se ignorará esta línea
```

Los elementos para documentar serán:
- define
- function
- class
- class vars
- include/require/include_once/require_once
- global variables

Utilizando la marca **@package** puede documentarse a nivel global el fichero.

En cada DocBlock se pueden incluir marcas que tendrán distintos significados como: 
- **@access**: si es private, no se genera documentación (salvo que se indique explícitamente). Se usa  cuando solo se quiere para generar documentación sobre la interfaz (métodos públicos), pero no sobre la implementación (métodos privados)
- **@author**: Indicar el autor del código
- **@copyright**: Información sobre derechos
- **@deprecated**: Indica que el elemento no se debe usar porque está obsoleto y en futuras versiones puede no estar disponible.
- **@example**: Ruta hacia un fichero con código PHP. phpDocumentor mostrará el código resaltado.
- **@ignore**: Impide phpDocumentor documente un determinado elemento
- **@internal**: Muestra información en documentación interna para desarolladores pero no en la pública
- **@link**: Incluye un enlace a un recurso
- **@see**: Crea enlaces internos a la documentación de un elemento
- **@since**: Indica que el elemento está disponible desde determinada versión del paquete
- **@version**: Indica la versión actual del elemento
- **@global**: Permite especificar el uso de variables globales dentro de una función
- **@param**: Para documentar parámetros que reciben una función
- **@return**: Muestra el valor devuelto por una función

#### Instalación de phpDocumentor

- Como requisito previo PHP y Apache deben funcionar de forma correcta
```
# Prueba Apache
curl http://localhost
# Prueba PHP
echo "10" | php   # Debe dar 10 de resultado
# Comprobar que Apache ejecuta código PHP creando el siguiente archivo y llamando
echo "<?php phpinfo(); ?>" >> /var/www/html
curl http://localhost/phpinfo.php
```

- El proceso de instalación de phpDocumentor

1.- Instalar el paquete **php-pear**:
```
apt-get install php-pear
```
2.- Configurar phpDocumentor para indicarle a pear la carpeta donde estará el contenido web
```
pear config-set data_dir /var/www
```
3.- Instalar phpDocumentor
```shell
# Desde repositorio
pear install -alldeps PhpDocumentor
# O descargando dicho paquete 
Wget sourceforge.Net/projects/phpdocu/files/ phpdoc/phpdocumentor-1.4.3/Phpdocumentor-1.4.3.Tgz
# Al finalizar la instalacion indicar un directorio de salida cambiando el propiatario a www-data para que pueda trabajar sin limitaciones
mkdir /var/www/docs
chown www-data /var/www/docs
```
4.- En el navegador comprobar que la instalación ha sido satisfactoria si se escribe http://localhost/phpdocumentor
#### Configuración de phpDocumentor

Se puede trabajar con phpDocumentor:
- Desde la **línea de comandos**
```shell
# Patron
phpdoc -o [formato_documentacion] -d [carpeta_proyectos_php] -t [carpeta_ archivos_documentacion]

# Ejemplo
# Se indica que se genre documentacion en formato HTML de los proyectos de la carpeta /var/www y se almacene dicha documentacion en la carpeta /var/www/docs/
phpdoc -o HTML:frames:phpedit -d / var/www/ -t / var/www/docs/
```

- Desde el **entorno web**
1. Debe configurarse accediendo a la ruta donde se ha instalado phpDocumentor (phpdocumentor/user) para duplicar el achivo `default.ini` y ponerle un nombre distinto como por ejemplo `proyecto.ini`. 
2. Este archivo se edita estableciendo una ruta donde guardar la documentación (`target`) y una ruta en la que se encontrarán los archivos del proyecto (`directory`)
3. Para crear la documentación, se escribe en el navegador la ruta http://localhost/PhpDocumentor y se escoge en el menú la opción _Config_, se selecciona el fichero del proyecto y se pulsa en _Go_ para  la documentación. 
4. Para acceder a la documentación generada deberíamos seleccionar el documento "index.html" de la carpeta donde se almacenan los documentos generados y se vería la página principal de la documentación.

PhpDocumentor puede crear su propia documentación que está en una subcarpeta tutorials. Debe especificarse el directorio raíz de phpDocumentor para que se compilen estos tutoriales (y solo procesará la documentación de tutorials vinculada a algún código fuente; no se pueden compilar solo tutoriales). En este caso como proyecto se debe especificar "phpDocumentor"
## 3. Instalación, configuración y uso de JavaDoc

**Javadoc** es un estándar usado para documentar las clases de Java. (Generar APIs, Application Programing Interface en formato HTML de un archivo de código fuente Java). Busca que la información de las clases no se quede obsoleta con el paso del tiempo, por lo que los comentarios son insertados en el código. La herramienta extrae los comentarios y genera documentación HTML.

Los documentos de Javadoc están destinados a describir funciones de clases y métodos para que otro programador lo lea y use la clase correspondiente. 

Los comentarios Javadoc comienzan con `/**` y terminan con `*/`. Cada línea comienza con ` * `. También reconocerá las etiquetas que comenzarán con `@` y que irán situadas al principio de una línea. 

Hay dos tipos de etiquetas:
- Las de **bloque** solo se pueden usar en la sección de etiquetas que siguen a la descripción principal. Son de la forma `@etiqueta`
- Las **inline** se pueden usar tanto en la descripción principal como en la sección de etiquetas. Tienen la forma de `{@tag}`

Los comentarios pueden incluir unos indicadores que comiencen por `@` y que se colocan al comienzo de la línea. (Salvo en las líneas dedicadas a la descripción del  método) No es obligatorio su uso por lo que un método puede ir sin indicadores.  Algunos de los que podrían citarse son: @author, @version @param @return @see @throws @decrecated


**Instalación de Javadoc**
Se trabajará en Ubuntu con el entorno Eclipse `apt-get install eclipse`. Simplemente en la sección Project (¡todos los demás IDEs lo tienen también!) se selecciona Generate Javadoc, donde se puede generar la documentación e indicar la ruta donde se quiere que se guarde.

**Creación y uso de plantillas de código**
Se pueden generar plantillas HTML con el contenido de comentarios usando ciertas convenciones en el código de Java. Así es como ha sido creada la API de Java.

Las plantillas:
- Son sugerencias de código asociadas a una palabra clave
- En NetBeans se definen en Preferences > Options > Editor > Code Templates
- Pueden ahorrar mucho trabajo
- Usan nombres similares a las construcciones Java que encapsulan como (try, for, while,...)
- Hay plantillas Javadoc predefinidas, aunque también pueden definirse y crearse plantillas personalizadas

Las plantillas están formadas por un **nombre**, **descripción**, **contexto** en función de lenguaje y *pattern* que será el código de la plantilla. En el código puede usarse texto fijo o variables predefinidas como:
- **$(cursor)**: Posición del cursor
- **$(enclosing_type)**: Tipo de la clase
- **$(enclosing_method)**: Nombre del método
- **$(year)**: Año en curso
- **$(time)**: Hora en curso

```java
/**
 * Clase $(enclosing_type): Descripción de la clase.
 */
public class ExampleClass {
	/**
	 * $(enclosing_method): Descripción del método.
	 *
	 * @param param1 Descripción del primer parámetro.
	 * @param param2 Descripción del segundo parámetro.
	 * @return Descripción del valor de retorno.
	 * @since $(year)
	 */
	public int exampleMethod(int param1, String param2) {
	    // Código del método
	    return 0; // Valor de retorno de ejemplo
	}
	
	/**
	 * sum: Suma dos números enteros.
	 *
	 * @param a Primer número entero.
	 * @param b Segundo número entero.
	 * @return La suma de ambos números.
	 * @since 2025
	 */
	public int sum(int a, int b) {
	    return a + b;
	}
}
```


## 4. Sistema de control de versiones. Seguridad de los sistemas de control de versiones

Los **sistemas de control de versiones** se encargan de realizar copias de las distintas versiones en un directorio. Cada vez que se realice una copia , se pedirá que se añada un comentario. 
Con el guardado de las distintas versiones se puede obtener fácilmente cualquiera de ellas, ver los comentarios añadidos o compararlas entre sí.

Se recomienda su uso al realizar proyecto entre varios desarrolladores para obtener las versiones del proyecto desde un mismo sitio común. También es recomendado al usarlo de forma individual para controlar las versiones del proyecto.

### 4.1. Conceptos básicos

- **Revisión**: Visión en un momento dado del estado de archivos y directorios. Pueden tener asociados metadatos como identidad de quién hizo las modificaciones, fecha y hora en la que se almacenaron los campos, razón de los cambios, de qué revisión/rama se deriva, palabras o términos clave.
- **Copia de trabajo o árbol de trabajo**: Archivos y directorios controlados por el control de versiones en edición activa. Asociado a una rama de trabajo concreta.
- **Rama de trabajo o desarrollo**: Conjunto ordenado de revisiones. La más reciente se denomina principal. Se llama _main_ o _head_ a la revisión más reciente. Las ramas se pueden separar y juntar según sea necesario formando un grafo de revisión. 
- **Repositorio**: Lugar dónde se almacenan las revisiones. Puede ser archivo, base de datos, colección de archivos... y estar almacenado en local o en remoto (servidor)
- **Conflicto**: Sucede cuando varias personas hacen cambios contradictorios sobre un mismo archivo (o varios). Los sistemas de control de versiones solo informan del conflicto. Se llama **resolución** al proceso para solucionarlo.
- **Cambio**: Modificación en un archivo bajo control de versiones. Cuando se unen los cambios en un archivo o varios generando una versión unificada se dice que se ha hecho una **combinación** o integración. 
- **Parche**: Lista de cambios generada al comparar revisiones y que puede usarse para reproducir automáticamente las modificaciones hechas en código. 

Con el sistema de control de versiones se consigue tener el repositorio siempre actualizado. Se trabajará sobre una copia local y después se actualizará el repositorio con dicha copia. Así no es necesario tampoco el acceso continuo al repositorio. Los sistemas de control que permiten el acceso continuo son más transparentes pero existe también el bloqueo de ficheros. 

### 4.2. Procedimiento habitual de trabajo en un sistema de control de versiones

1.- Descargar los ficheros inicial del repositorio (ckeckout)
2.- Ciclo de trabajo: 
- Modificación de los ficheros
- Actualización de los ficheros (update). Actualizados de forma local para luego subirse al repositorio
- Resolución de conflictos (si los hay. Se informará a los usuarios para su resolución
- Actualización de ficheros en el repositorio. Modificación de los ficheros en el repositorio. Se comprueba que las versiones estén actualizadas.

Entre las tareas o **funciones que los sistemas de control de versiones permiten**:
- Realizar copias del proyecto al mismo tiempo
- Realizar cambios en ficheros
- Comparar versiones
- Unir cambios realizados por distintos usuarios sobre los mismos ficheros
- Actualizar la copia local con la del servidor
- Mantener distintas ramas de un proyecto

### 4.3. Sistemas de control de versiones centralizados y distribuidos

- La forma más simple de realizar copia de los archivos de un proyecto es copiar todo el directorio a otro lugar sabiendo la fecha en que se realizó. Este método es propenso a errores.
- Para remedirlo, se diseñó el **sistema de control de versiones locales**. **RCS** se basa en la copia de parches (diferencias de archivos de una versión a otra) en un formato especial en el disco. Puede recrearse cómo son los distintos archivos sumando los parches.
- Para colaborar varios desarrolladores a la vez surgen los **sistemas de control de versiones centralizados (CVS)**. Contienen los  archivos en un único servidor y varios clientes se descargan los archivos desde ese lugar. Ahí, cada desarrollador sabe en qué están trabajando el resto de personas del proyecto. También al ser un servidor centralizado en el momento en el que deje de funcionar el resto de usuarios no pueden realizar su trabajo o incluso podrían perder toda la información en caso de fallo.
- Los **sistemas de control de versiones distribuidos (DVCS)**. En ellos (Git, Mercurial, Bazaar o Darcs) los clientes no descargan únicamente la última versión de los archivos sino que los replican continuamente al repositorio. Si el servidor falla, cualquier cliente puede restaurar los elementos del repositorio. A cada descarga, se realiza una copia completa de todos los datos. 

## 5. Git como sistema de control de versiones

- **Git** es un sistema de control de versiones escrito en **C**. 
- Fue creado en **2005** y se hizo popular al ser elegido para el kernel de Linux.
- Es **rápido** y eficiente en grandes proyectos, teniendo **gran capacidad de ramificación**
- Git almacena los datos como un **conjunto de instantáneas**. **Cada vez que se realiza algún cambio, Git deja reflejado el estado actual de los archivos y hace una referencia a ese estado.**
- Cada operación es realizada de forma **local**, necesitando solo archivos y recursos locales.
- Tiene **integridad**, ya que todo es verificadomediante una suma de comprobación antes de ser almacenado, siendo imposible realizar cambios sin que sean detectados por Git.

### 5.1. Funcionamiento

Los archivos de Git **pueden encontrarse de tres formas**:
- **Confirmado** (commited): Almacenados de forma segura en BBDD local
- **Modificado** (modified): Modificado sin ser confirmado en BBDD local
- **Preparado** (staged): Marcado en la versión actual y listo para la confirmación.

Hay tres **secciones principales** en Git:
- **Directorio de Git** (Git directory): Almacena metadatos y BBDD de objetos para el proyecto. Es la carpeta que se copia al realizar la copia de un repositorio a otro
- **Directorio de trabajo** (Working directory): Copia de una versión del proyecto
- **Área de preparación** (Staging area): Almacena la información que irá en la próxima confirmación

Los **pasos de trabajo** en el uso de Git son:
1.- Modificar archivos en el directorio de trabajo
2.- Preparar los archivos añadiendo instantáneas en el área de preparación
3.- Confirmar los cambios

Si una versión concreta está en el directorio de Git se considera confirmada (commited). Si ha sufrido cambios desde que se obtuvo del repositorio pero ha sido añadida al área de preparación está preparada (staged). Si ha sufrido cambios desde que se obtuvo del repositorio pero no se ha preparada está modificada (modified)

### 5.2. Instalación de Git
Primero debe disponerse de librerías `curl`, `zlib`, `openssl`, `expat` y `libiconv`. Para instalarlas puede ejecutarse:
```shell
wget http://kernel.org/pub/software/scm/git/git-1.7.6.tar.bz2
```

Después se instala con:
```shell
apt-get install libcurl4-gnutls-dev libexpatl-dev gettext libz-dev
```
O bien descargándolo de forma manual con http://git-scm.com

Cuando ha finalizado la descarga se compila e instala el paquete con los siguientes pasos:
```shell
tar -xjvf git-1.7.6.tar.bz2
cd git-1.7.6
apt-get build-dep git-core
apt-get install libssl-dev
make prefix=/usr/local all doc
make prefix=/usr/local install install-doc
```

Para comprobar que la instalación se ha realizado correctamente se ejecuta el comando:
```shell
git -version
```

### 5.3. Configuración de Git

```shell
# Mostrar opciones disponibles
git config -help
# Establecer nombre de usuario y direccion de correo (Usando la opcion --global se define la informacion para todo el sistema, sin tener que hacerlo de nuevo. Para cambiar los datos se escribira sin la opcion --global)
git config --global user.name “alumno”
git config --global user.email alumno@ejemplo.com
# Para indicar el editor de texto que se iniciara al escribir algun mensaje
git config --global core.editor emacs
# Comandos de ayuda
git help <comando>
git <comando> --help
man git-<comando>
# Instalacion del entorno web
apt-get install gitweb
# Creacion de directorios
mkdir /home/usuario/git
mkdir /home/usuario/www_git
```

Edición del fichero gitweb en Apache `/etc/apache2/conf.d/gitweb`

```xml
Alias /git /home/usuario/www_git
	<Directory /home/usuario/www-git >
	Allow from all
	AllowOverride all
	Order allow, deny
	Options +ExecCGI
	DirectoryIndex gitweb.cgi
	<files gitweb.cgi>
	SetHandler cgi-script
	</files>
	</directory>
SetEnv GITWEB_CONFIG /etc/gitweb.conf
```

Y mover los archivos de gitweb al directorio de Apache creado:

```shell
mv -v /usr/share/gitweb/* /home/usuario/www_git
mv -v /usr/lib/cgi-bin/gitweb.cgi /home/usuario/www_git
```

Se harán cambios en configuración de gitweb

```shell
#nano /etc/gitweb.conf
$projectroot = ‘/home/usuario/git/’;
$git_temp = “/tmp”;
#$home_link = $my_uri || “/”;
$home_text = “indextext.html”;
$projects_list = $projectroot;
$stylesheet = “/git/gitweb.css”;
$logo = “/git/git-logo.png”;
$favicon = “/git/git-favicon.png”;
```

Y se reinicia el servidor de Apache.

```shell
# Se creara una carpeta del proyecto
cd /var/cache/git
mkdir proyecto.git
cd proyecto.git
git init
echo "Breve descripcion del proyecto" > .git/description
git config --global user.name "Nombre"
git config --global user.email "tu@correo.com"
git add
git commit -a

```

La publicación de un repositorio Git a través del **protocolo Git Daemon**, que permite compartir repositorios de manera eficiente a través de la red usando el protocolo `git://`.
`#git daemon –base-path=/var/cache/git –detach –syslog –export-all`

El servicio de Git que ejecuta un servidor para hacer público el repositorio:
```shell
cd /var/cache/git/proyecto.git
touch .git/git-daemon-export-ok
```

Deben darse permisos de escrituras a algún usuario no root para que pueda hacer cambios en el repositorio.

Podrá accederse a él usando
```shell
# Desde comandos
git clone git://servidor/proyecto.git
# Desde navegador entrando en http://localhost/git/()
```
Para **borrar archivos** desde punto concreto puede usarse:
```
git log
git reset -hard [HASH_DEL_COMMIT]
```

Para **saltar a un estado anterior temporalmente**
```
git checkout [HASH_DEL_COMMIT]

# Para volver
git checkout master
```
Para **restaurar algún archivo en particular**: 
```
git checkout [HASH_DEL_COMMIT] algunarchivo otroarchivo
```

Cuidado porque **checkout** puede sobreescribir archivos sin avisar. Es recomendable hacer commit antes de ejecutar cualquier comando de checkaout

Para obtener una copia del proyecto `git clone git://servidor/ruta/a/archivos`

### 5.4. Seguridad y documentación en Git

Cada directorio de trabajo en Git es un repositorio independiente donde cada acceso se realiza a través del protocolo Git montado sobre SSH o usando HTTP no siendo necesario usar ningún servidor web.

Los desarrolladores pueden subir sus proyectos al repositorio sin que sean revisados `git push`.
En el repositorio público deben estar habilitados los accesos:
- Acceso directo por sistema de ficheros con permisos de escritura para el usuario sobre el directorio del repositorio
- Acceso remoto vía SSH y permiso de escritura para el usuario sobre el directorio del repositorio
- Acceso HTTP con WebDav debidamente configurado
- Acceso mediante protocolo Git con servicio `receive-pack` activado en el `git daemon`
