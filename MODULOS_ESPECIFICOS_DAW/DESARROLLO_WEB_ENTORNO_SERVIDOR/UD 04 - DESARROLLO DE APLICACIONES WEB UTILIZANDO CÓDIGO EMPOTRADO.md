(UF1 Desarrollo web en entorno servidor)

## 1. Mantenimiento del estado

Al navegar puede haber cambios como pasar de una pestaña a otra, avanzar por una compra o por una transferencia, etc. Esto son **acciones que obligan a mantener determinados datos o estado de un cliente**. 

Las **sesiones** son el mecanismo que permite garantizar y controlar que los recursos son ejecutados de forma correcta. 
Gracias a ellas, un usuario puede seguir realizando cualquier acción sin necesidad de autenticarse en cada una de las pestañas. 

**Las sesiones se pueden establecer de las siguientes formas:**
- **A través de la URL**: Los datos son enviados como parámetros dentro de la URL bajo el uso del método GET. Se identifica al usuario en el servidor y este retorna un identificador denominado SID (número generado de forma aleatoria por el servidor) a dicho usuario. Cuando el recurso solicitado se abandone, la sesión caduca y es necesario renovar el SID.
- **Cookies:** El cliente almacena en su navegador un archivo que guarda los datos necesarios para mantener la sesión abierta. El servidor utiliza ese archivo para verificar la identificación del cliente. 

- PHP permite el uso de ambos tipos de identificación.
- Las sesiones no se generan automáticamente a menos que sea especifiado. Estas se deben generar dentro del código utilizando las funciones del lenguaje.

Una vez que el usuario se autenticado se debe iniciar la sesión (la función debe situarse al comienzo del código asociado en cada sitio web). En PHP esto se hace invocando la función predefinida `session_start()`

```php
<?php
	session_start();
	if (!isset($_SESSION['temps'])) {
		$_Session['temps'] = 0;
	} else {
		$_SESSION['temps'] = time();
	}
?>
```

Una vez iniciada la sesión es posible trabajar con las funciones de sesión que se identifican por el nombre que se indique en su interior. Al igual que las variables del lenguaje, estas definen el tipo de dato que tienen según el contenido que almacenen: 
```php
$_SESSION['nombre'] ;
```
Estas variables estarán disponibles siempre que la sesión esté activa. Al finalizar al sesión, debe destruirse empleando también el método correspondiente. `unset`

```php
unset($_SESSION['temps']);
```

## 2. Cookies (galletas)

Las **cookies** son pequeños archivos que permiten almacenar los datos de sesión asociados a un usuario una vez que se ha identificado y ha sido validado desde el servidor.

- Son **útiles** **pero** es posible que a través de ellas se acceda a sitios sin permiso o se generen **problemas de seguridad** (por eso muchas páginas web bloquean su uso, en cuyo caso se crearán sesiones por código). También el uso de las cookies ha sido usado por sitios web para adquirir información sobre usos e intereses habituales de los usuarios durante su navegación para así mostrar a cada usuario todos los productos que puedan ser potencialmente interesantes para él. Las alertas sobre su uso están formalizadas de forma legal y los sitios deben avisar a los usuarios si las usan.
- Pueden contener **datos de carácter sensible** por lo que es importante controlar su envío al servidor.
- La gestión puede hacerse con la función **`setcookie()`** en PHP. Esta permite crear una cookie cuyos parámetros de configuración se establecen según el desarrollador desee: **nombre, valor, tiempo de vida, ruta, dominio y seguro**
- El valor de la cookie puede ser recuperado con la variable `$_COOKIE`

**Crear una cookie**
Indicar nombre, valor a almacenar y tiempo que va a perdurar
```php
<?php
	/*
	--nombre: El nombbre con el que referenciamos la cookie
	--valor: El valor que almacenara la cookie
	--$t: el tiempo de expiración que tendrá la cookie
	*/
	setcookie(“nombre”,”valor”,time() + $t);
?>
```

**Acceder a su valor**
```php
<?php
	//Visualizamos el valor de la cookie
	echo $_COOKIE["nombre"];
?>
```


**Actualizar su valor**
```php
<?php
	//Actualización de una cookie
	setcookie("programa","late motive");
	echo $_COOKIE["programa"];
	//Al recoger un dato en una cookie con el mismo nombre
	//el valor de esta se actualiza
	setcookie("programa","la resistencia");
	echo $_COOKIE["programa"];
?>
```

**Eliminar una cookie**
```php
<?php
	//Eliminamos una cookie
	unset($_COOKIE["nombre"]);
	//Otra forma de eliminar una cookie
	setcookie("nombre","valor",time() - 1);
?>
```

## 3. Seguridad: usuarios, perfiles, roles ,cookies

La **seguridad** es uno de los aspectos que más problemas e inquietudes generan en los desarrolladores web.
Es necesario intentar **establecer los mejores y más fiables mecanismos de seguridad dentro de cualquier tipo de aplicación**.

**Control de usuarios**
Primero se debe comprobar el **control de usuarios**. Cualquier aplicación divide a los usuarios en función de una serie de perfiles o roles. Estos indican al servidor si tienen permiso de acceso a los diferentes recursos de la web.

Para su gestión existen softwares que pueden ayudar al administrador del sitio a configurar los accesos. La organización jerárquica de estos permisos se recoge en una lista **ACL** (Access Control List). 
Se puede crear una ACL que actúe de intermediaria entre el cliente y la base de datos, realizando una autenticación basada en grupos y roles asignados.

---

Respecto a las cookies, estas podrían usarse para extraer información sobre usuarios cuando navegan pero nunca pueden leer datos almacenados dentro del equipo de un usuario ni realizar instalaciones indeseadas. 

## 4. Autenticación de usuarios

La **autenticación de usuarios** se suele llevar a cabo mediante el envío de formularios.
Es un proceso validado por el servidor que gestiona el acceso que se devuelve al usuario. 

Como las webs y aplicaciones de escritorio han crecido considerablemente, el usuario se ve obligado a registrarse y a recordar una contraseña en cada una de las webs, lo que puede incomodarle. Para evitarlo aparecen las **tecnologías de autenticación centralizada**  como **OpenID** y **OAuth**. 

Estas tecnologías buscan centralizar el acceso a cualquier tipo de servicio web mediante el uso de plataformas ya verificadas (Facebook, Twitter, Google+, Hotmail, etc.)

El proceso consiste en abrir una pasarela de acceso a un servicio externo que, mediante un formulario de acceso, permite generar una sesión para ese usuario sin necesidad de registro previo.
Los datos de acceso recabados a través de plataforma externa se almacenan en BBDD para permitir obtener los permisos necesarios y asignarlos al usuario en cuestión.
Así los servidores de almacenamiento de control de identidad y de generación y control de tokens pueden descargarlo.

Estas tecnologías suponen un problema de dependencia con un sistema externo que debe ser fiable.

## 5. Adaptación a webs existentes

La exigencia y el dinamismo de las webs **exige un continuo proceso de adaptación**.

Hay normas de obligatorio cumplimiento y, una vez que se realiza el desarrollo completo de  la web, deben ser revisadas como por ejemplo:
- sistemas de autenticación correctos
- se garantizan requisitos mínimos para la privacidad de los datos
- se realiza el envío y la recepción de datos a través de pasarelas encriptadas, etc.

Muchas veces la creación de una nueva web se hace adaptándose con base a las ya existentes, cuyo funcionalidad dentro del mercado es la misma.

## 6. Pruebas y depuración


Las **pruebas** con el mecanismo por el que es posible comprobar si una aplicación web cumple con las condiciones y requisitos especificados.

- **Forman parte del ciclo de vida** de creación de las aplicaciones.
- **Debe llevarse a cabo teniendo en cuenta una serie de entradas y obteniendo como resultado una salida cuyos resultados han sido definidos con anterioridad**. Si los resultados obtenidos son los esperados, el desarrollo del programa es correcto; si no es así se puede afirmar que existe un error  en alguna parte del programa que debe ser solucionado.
- **Tipos de pruebas**: Validando la parte lógica (pruebas de caja blanca); Sobre las interfaces o servicios web (pruebas de caja negra)
- **Deben integrarse y realizarse de manera repetitiva** para poder detectar a tiempo el mayor número posible de errores
- Es bueno tratar de dividir el código en funcionalidades, intentando aislar unas partes de otras para que en caso de producirse algún fallo este no se arrastre a otras partes. (**Pruebas unitarias:** se ejecuta una parte del código sin que el resto de las funciones se vean afectadas. La mayoría de lenguajes de programación web permiten estas pruebas)
- En el desarrollo de cualquier aplicación o servicio web y de forma paralela a las pruebas se recomiendan los **procesos de depuración**. Permiten comprobar y realizar un seguimiento de la ejecución en tiempo real de dicha aplicación o página web. Así es posible comprobar los recursos utilizados por la aplicación. Analizar los valores que van tomando permite verificar que son correctas y controlar el flujo de ejecución. Para ello es necesario usar uso de IDEs que soporten el lenguaje de programación utilizado como Eclipse y Microsoft Visual Studio.



----
```php
setcookie(“Tamaño_Fuente”,25,time()+(86400*30));
setcookie(“Ancho_Pantalla”,1024,time()+(86400*30));
echo $_COOKIE[“Tamaño_Fuente”];
echo $_COOKIE[“Ancho_Pantalla”];
```

---

```php
<?php
session_start();

$mensaje_error = "";
$usuario_válido = isset($_SESSION["login"]) && $_SESSION["login"] === true;

if (isset($_POST["enviar"])) {
    $usuario_válido = $_POST["usuario"] == "admin" && $_POST["contraseña"] == "2021";
    
    if (!$usuario_válido) {
        $mensaje_error = "Nombre de usuario incorrecto.";
    } else {
        $_SESSION["login"] = true;
    }
}

if ($usuario_válido) {
    header("Location: /admin.php");
    die();
}
?>
```
