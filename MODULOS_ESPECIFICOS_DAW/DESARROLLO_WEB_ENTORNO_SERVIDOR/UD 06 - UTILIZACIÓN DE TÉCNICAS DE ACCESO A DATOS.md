(UF3 Técnicas de acceso a datos)
## 1. Tecnologías que permiten acceder a datos desde una aplicación web

El **acceso a base de datos** es uno de los puntos clave en el desarrollo y construcción de cualquier tipo de aplicación web. La forma en la que se leen, modifican, almacenan y eliminan los datos puede tener gran influencia en el rendimiento de una web.

**Tecnologías que permiten el acceso a datos**
- **Database manager system (DBMS)**: Sistema manejador de bases de datos formado por un conjunto de programas que se encarga de gestionar el almacenamiento de una BBDD. Ej.: SQL Server, MySQL, Oracle.
- **API**: Métodos o funciones que permiten mediante llamadas el acceso a determinados servicios de la aplicación web.
- **Lenguajes de programación** Cualquiera que permita interpretar la sintaxis de acceso a datos. Ejs.: PHP, Prolog, ASP, ActionScript, ADA, Python, Pascal, C#, Basic, Java
- **Mapeo de datos**: El mapeo objeto-relacional (ORM) permite relacionar los objetos de una aplicación con su correspondiente tabla en una base de datos relacional. Así, **cada clase en el modelo de dominio tendrá su tabla en el modelo de datos**. Es la técnica más extendida y usada en el desarrollo de aplicaciones web. Ejs.: Hibernate y cualquier implementación de Java Persistence API, Doctrine, etc.

Es importante elegir qué tecnología emplear dependiendo de los requisitos de la aplicación porque será el vínculo entre esta y la base de datos.

La creación de una base de datos busca hacer uso de los registros en ellas almacenadas para mostrar esa información en las páginas web. 

**Para obtener los datos y mostrarlos en un HTML se necesita**
- Que **el software que se encarga de interpretar el lenguaje de programación escogido se comunique con el sistema gestor de la base de datos**. Debe estar identificado y autorizado en la base de datos.
- **Preparar la sentencias SQL** a ejecutar
- **Ejecutar la sentencias en la base de datos** para obtener el conjunto de datos solicitado
- **Recorrer el conjunto de datos** mediante estructuras de control proporcionadas por el lenguaje de programación
## 2. Establecimiento de conexiones

Una **conexión a base de datos** es la forma en la que un servidor de base de datos y su aplicación cliente se comunican entre sí. 

## 3. Ejecución de sentencias SQL. Recuperación y edición de información


## 4. Ejecución de sentencias SQL. Utilización de conjuntos de resultados


## 5. Creación de aplicaciones web con acceso de escritura a bases de datos


## 6. Transacciones




## 7. Pruebas y documentación




## 8. Trabajar con bases de datos en PHP


// Ver cositas previas MySQL... etc.

Hay dos formas de comunicarse con una base de datos desde PHP:
- Utilizar una extensión nativa programada para un SGBD concreto
- Utilizar una extensión que soporte varios tipos de datos

Antes se usaba la extensión nativa **mysql**. Actualmente lo habitual es elegir entre **MySQLi** (nativa) y **PDO**. Estas extensiones usan un driver de bajo nivel para comunicarse con el servidor MySQL. Antes solo estaba disponible **libmysql** pero después también se preparó PHP para usar un nuevo driver mejorado: **mysqlnd**, el driver nativo de MySQL.

**MySQLi** ofrece interfaz dual permitiendo acceder a las funcionalidades de la extensión usando objetos o funciones de forma indiferente.

`new mysqli($host,$user,$password,$database)`: Realiza la conexión
`mysqli_connect_errno`: Comprueba la conexión
`mysqli_query($conexion, $query)`: Realiza una query
`mysqli_fetch_assoc($result)`: Trae resultados de una consulta en forma de query asociativo
`mysqli_autocommit($conexion, $boolean)`: Activar o desactivar el autocommit
`mysqli_commit($conexion)`: Commit de la transacción
`mysqli_rollback($conexion)`: Rollback de la transacción
`mysqli_close($conexion)`: Cerrar la conexión

**Por ejemplo, para establecer conexión y consultar su versión**
```php
// Forma 1.:Uso de constructor y metodos POO
$conexion = new mysqli('localhost', 'usuario', 'password', 'base_de_datos');
print $conexion->server_info;

// Forma 2.: Uso de llamadas a funciones
$conexion = mysqli_connect('localhost', 'usuario', 'password', 'base_de_datos');
print mysqli_get_server_info($conexion)
```

Seguidamente podemos **comprobar si la conexión es correcta** y consultar para **configurar la codificación de caracteres**
```php
// Comprobar si la conexion es correcta
if (mysqli_connect_errno()) {
	echo "La conexion a la BBDD MySQL ha fallado: ".mysqli_connect_error();
} else {
	echo "Conexión realizada correctamente!!";
}

// Consulta para configurar la codificacion de caracterees
mysqli_query($conexion, "SET NAMES 'utf8'");
```


#####  Consultar
```php
// Realizar la query
$notas = mysqli_query($conexion, "SELECT * FROM notas");


// Tomar el resultado (Variable nota con el contenido de iterar el resultado de fetch_assoc)
while($nota = mysqli_fetch_assoc($notas)) {
	var_dump($nota);
	echo '<h2>'.$nota['descripcion'].'</h2>';  // Imprimir el campo titulo del array
	echo $nota['descripcion'].'<br/>';  // Imprimir el campodescrip. del array
}

//------------------------------------------------------------

// Tambien se podria tomar el resultado pero verificando antes si hay resultados disponibles
if (mysqli_num_rows($notas) > 0) {
    // Iterar sobre los resultados
    while ($nota = mysqli_fetch_assoc($notas)) {
        echo '<h2>' . $nota['titulo'] . '</h2>'; // Imprimir el campo titulo
        echo '<p>' . $nota['descripcion'] . '</p>'; // Imprimir el campo descripcion
        echo '<hr>';
    }
} else {
    echo "No hay notas disponibles.";
}
```

#####  Insertar
```php
$sql = "INSERT INTO notas VALUES(null, 'Nota desde PHP', 'Esto es una nota en PHP', 'green')";
$insert = mysqli_query($conexion, $sql);

if ($insert) {
	echo "DATOS INSERTADOS CORRECTAMENTE"
} else {
	echo "Error: ".mysqli_error($conexion);
}
```

##### Actualizar
```php
// Query para actualizar un registro en la tabla 'notas'
$sql = "UPDATE notas SET titulo = 'Nota actualizada', descripcion = 'Descripción actualizada', color = 'blue' WHERE id = 1";
$update = mysqli_query($conexion, $sql);

if ($update) {
    echo "DATOS ACTUALIZADOS CORRECTAMENTE";
} else {
    echo "Error: " . mysqli_error($conexion);
}
```

##### Eliminar
```php
// Query para eliminar un registro de la tabla 'notas'
$sql = "DELETE FROM notas WHERE id = 1";
$delete = mysqli_query($conexion, $sql);

if ($delete) {
    echo "REGISTRO ELIMINADO CORRECTAMENTE";
} else {
    echo "Error: " . mysqli_error($conexion);
}
```

**Para activar las transacciones lo que se hace es desactivar el autocommit**

```php
// Iniciar la conexión a la base de datos
$conexion = mysqli_connect("localhost", "usuario", "contraseña", "basedatos");

// Desactivar el modo autocommit para controlar la transacción manualmente
mysqli_autocommit($conexion, false);

try {
    // Primera consulta: Insertar una nueva nota
    $sql1 = "INSERT INTO notas (titulo, descripcion, color) VALUES ('Nota 1', 'Descripción 1', 'red')";
    $insert1 = mysqli_query($conexion, $sql1);

    // Segunda consulta: Insertar otra nota
    $sql2 = "INSERT INTO notas (titulo, descripcion, color) VALUES ('Nota 2', 'Descripción 2', 'blue')";
    $insert2 = mysqli_query($conexion, $sql2);

    // Verificar si ambas consultas se ejecutaron correctamente
    if ($insert1 && $insert2) {
        mysqli_commit($conexion); // ✅ Confirmar transacción si todo está bien
        echo "Transacción completada con éxito.";
    } else {
        throw new Exception("Error en la consulta"); // Lanzar error si una falla
    }
} catch (Exception $e) {
    mysqli_rollback($conexion); // ❌ Revertir cambios en caso de error
    echo "Transacción fallida: " . $e->getMessage();
}

// Restaurar el modo autocommit
mysqli_autocommit($conexion, true);

// Cerrar la conexión
mysqli_close($conexion);
```
























