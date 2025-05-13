(UF1 Desarrollo web en entorno servidor)

## 1. Tomas de decisión

El desarrollo de una aplicación web conlleva la programación de muchos elementos que permiten al usuario elegir o ejecutar acciones diferentes que tienen un resultado u otro dependiendo de la elección.

Cada ejecución debe ser controlada y definida dentro del código, permitiendo según la selección del usuario tomar un camino u otro. 

Las **estructuras condicionales** permiten controlar y gestionar todas las ejecuciones que realiza una aplicación evaluando una condición determinada con las proposiciones `if` y `else`.

Estas estructuras son usadas cuando el valor de entrada recibido es único:

```php
if ($variable1 >= $variable2) {
	echo "variable1 es mayor igual que variable2";
}else {
	echo "variable2 es mayor que variable1";
}
```

Cuando el valor puede ser escogido entre varios de los posibles se opta por  estructuras de selección múltiple como `switch`: 

```php
switch ($nombreVariable) {
	case "valor1":
		echo "$nombreVariable contiene valor1";
		break;
	case "valor2":
		echo "$nombreVariable contiene valor2";
		break;
	case "valor3":
		echo "$nombreVariable contiene valor3";
		break;
}
```

## 2. Bucles

Los procesos de operaciones que se repiten vienen dados por los bucles.

**Estructuras repetitivas condicionales**
Cada iteración en el bucle devuelve un único resultado que vuelve a ser evaluado. En caso de satisfacer la condición se ejecuta una sentencia y, si no, el bucle finaliza. Se usa la sintaxis de **while** o **do-while**:

```php
$variable = 1;
while ($variable < 1000):
	echo $variable;
	$variable++;
endwhile;
```

**Estructuras repetitivas iterativas**
Cuando se conoce o se puede prever el número de iteraciones que se tienen que realizar. La acción se ejecuta el número de veces ya predeterminado dentro de la sintaxis del bucle, contando el número de ejecuciones como condición de evaluación.

```php
for ($variable = 1; $variable < 1000; $variable++) {
	if ($variable = 500) {
		echo "Ya se han hecho la mitad de la comprobaciones…";
	}
	echo $variable;
}
```

**Estructuras repetitivas recorrido**
Se puede hacer uso de estructuras para la interpretación y recorrido del  conjunto de resultados obtenidos.
Estas estructuras hacen un recorrido por los elementos de una matriz, array, coleccion u otro elemento independientente del tamaño de elementos que tengan.
Es el caso de los bucles for o foreach

```php
<?php
	$array = array(1, 2, 3, 4);
	foreach ($array as $valor) {
		echo "$valor";
	}
?>
```
## 3. Tipos de datos compuestos

Los **tipos de datos compuestos** son la composición de un conjunto de tipos de datos básicos.

En este tipo de datos más complejos se pueden encontrar:
- **Resultados de SQL**: Tuplas o registros de BBDD
- **Operaciones**: Productos cartesianoz, multiplicaciones, sumas,...
- **Conjuntos de datos**: Enumeraciones, arrays o colecciones...

Cada dato compuesto se almacena dentro de un conjunto de datos básicos. Por ejemplo un array o lista declarado como entero se compone de un número determinado de valores de tipo entero. 

```php
$matriz = array(1,1,2,3,5,8,13,21,34,55);
var_dump($matriz); // Muestra informacion detallada del array informacion, contenido, elementos
```

Estos tipos de datos permiten trabajar con estructuras dinámicas de datos, que resultan imprescindibles en la programación web.

Las webs y las bases de datos han tenido que adaptarse a la gran cantidad de información y hacer uso del **mapeo de datos**. Cada registro almacenado en BBDD es la representación de un objeto definido en una clase, pudiendo hacer uso de todas las propiedades relacionadas con un objeto o que implican mejor eficiencia en el almacenamiento de los datos y un enriquecimiento de información dentro de la web.

El almacenamiento de objetos en base de datos se consigue serializando los tipos de datos compuestos.

## 4. Funciones

Las **funciones** buscan encapsular en una parte del código una funcionalidad específica de una aplicación. Así puede ser repetida en diferentes partes, reutilizando el código. 

La **finalización de ejecución de una función** es retornar un valor o devolver el flujo de ejecución al punto desde el que fue llamado tras la ejecución de una o varias sentencias.

Las funciones pueden recibir parámetros o no, según su uso en estas funciones.

Para definir una función PHP usa la palabra `function` que indica al intérprete del código que comienza la declaración de una función. Esta irá seguida del nombre y acompañada de los parámetros (si son necesarios)

```php
function NombreFunction($parametros,...){
//Código que realiza la función
}

function NombreFunction($parametros,...){
	//Devolver valor
	return $valorDevuelto;
}

// Pasar un argumento como parámetro
function Duplica($num){
$num = $num * 2;
return $num;
}
echo Duplica(5);

// Pasar array como parámetro de la función
function RecogerArray($array){
var_dump($array);
}
$valores = array("Ilerna","Online");
echo RecogerArray($valores)

// Pasar parámetros por referencia
function completarCadena(&$txt)
{
	$txt .= 'en entorno servidor';
}
$ciclo = 'Desarrollo de aplicaciones web';
completarCadena($ciclo);
echo $ciclo;

// Utilizar parámetros predeterminados en funciones
function examen($modulo = "Desarrollo web en entorno servidor")
{
	return "Hoy tengo examen de $modulo.</br>";
}
//Devuelve el valor del parámetro por defecto
echo examen();
//Devuelve el valor proporcionado al parámetro
echo examen("Despliegue de aplicaciones web");

```

Además PHP incluye funciones adicionales ya creadas con propósito específico como `mysqli_connect()`, `phpinfo()`,...

**ASP.NET**  o **JSP** permite también mediante el uso de C# / Java (respectivamente) la creación de funciones específicas. Estas deben especificar (a diferencia de PHP):
- El tipo de dato que devolverán la punto de llamada de la función. Pueden retornar cualquier tipo. También puede no devolverse ningún valor, lo que debe indicarse con la palabra reservada void.
- El nombre de la función
- Los argumentos (si son necesarios)

## 5. Recuperación y utilización de información proveniente del cliente web

Dos de los métodos HTTP más importantes son, atendiendo a su propia naturaleza:
- **GET** (para solicitar información al servidor: realizando la petición desde el cliente a través de la URL. Estas peticiones suenen hacer referencia  a una página web o recurso específico del servidor. También se puede hacer una consulta de datos, aunque no es muy recomendable porque se quedan al descubierto algunas vulnerabilidades). Datos visibles enviados dentor e la URL de la página, primera variable se informa con `?`  y resto con `&`
- **POST** (para el envío de información: es posible enviar al servidor formularios de autenticación, entradas de datos, envío de parámetros útiles al servidor, etc.) Datos ocultos codificados en el cuerpo de la petición HTTP. Permite el envío de forma más segura. Aunque también tiene vulnerabilidades como podría ser la inyección SQL (de código maligno en la BBDD de la aplicación) luego no se puede afirmar que un método sea más seguro que otro.

Ambos métodos hacen uso de la URL
- Protocolo: HTTP
- Dominio: Nombre del sitio
- Directorio: Ruta o jerarquía de carpetas que indica el camino de acceso al fichero o recurso
- Fichero o recurso: Nombre de fichero o recurso almacenado en BBDD

## 6. Procesamiento de la información introducida en un formulario

Los **formularios web** son uno de los elementos más comunes para la recuperación y validación de datos de los usuarios.

- Son elementos web que facilitan la interacción con los datos disponibles en un aplicativo web. Se usan para facilitar la comunicación entre el usuario y los datos, permitiendo modificar cualquier parte del aplicativo.

- Permiten con una sola petición obtener gran cantidad de información.

- La totalidad de sitios web que requieren de autenticación de acceso emplean un formulario para hacerlo. 

- Sirven también como elemento de filtrado de una consulta de base de datos (cada campo es un criterio de la sentencia SQL)

- Una vez enviada la información, esta se procesa en el servidor. Muchas veces es necesario validar estos campos antes de enviar al servidor para evitar información incorrecta en bases de datos. 

---

Es una buena práctica de programación **realizar validaciones de los datos en diferentes puntos del aplicativo web**
- **Cliente**: Datos validados con lenguajes de entrono cliente. Como expresiones regulares de JavaScript.
- **Servidor**: Datos validados con lenguajes de entorno. Antes de ejecutar acciones en el servidor, como comprobar que el tipo de dato sea el que espera la BBDD

Junto a las validaciones se pueden **añadir restricciones en diferentes puntos para complementar la seguridad e integridad.**
- **Cliente**: Restricciones de HTML5 que son sencillas y útiles como el atributo `restrict` en los `inputs` o los propios atributos `type` 
- **Servidor**: Todos los clientes de bases de datos ofrecen restricciones para asegurar la integridad de los datos, el punto más importante para configurar en cualquier aplicativo. Puede haber varios tipos de restricción como restricciones de tipos de datos en los campos de una tabla o restricciones de eliminación de datos por integridad entre tablas.

Una vez validados, los datos se enviarán y el servidor los procesa y ejecuta la sentencia SQL correspondiente para almacenarlos. 

## 7. Comentarios

Los **comentarios**, a veces olvidados, pueden llegar a ser la guía de uso de una aplicación web completa permitiendo comprender y analizar todos los pasos de la aplicación. El uso de comentarios es la base de la documentación que permitirá a personas ajenas al desarrollo del autor, entender el código y que diferentes desarrolladores  puedan trabajar sobre él. 

Es importante considerar la **forma**:
- Se puede hacer un comentario junto a una línea para tratar de detallar alguna parte del código
- Se pueden usar estándares propios de documentación como TODO comments. Con la sintaxis TODO se puede indicar una línea de código como algo pendiente de hacer.
- Hay otros comentarios configurables para depurar y gestionar el desarrollo, que pueden ser utilizados incluso como filtros en una aplicación.
- Son un punto importante para agilizar el mantenimiento de los aplicativos debiendo ser claros, concretos y no muy extensos si no es necesario.
- La sintaxis varía según el lenguaje de programación. En PHP:
```php
//Comentario de una linea
#Comentario de una linea
/*
Comentario de
varias lineas
*/
```

---

```php
<!DOCTYPE html>
<html>
<body>
<?php
define("coche", [
    "Renault",
    "Fiat",
    "Toyota",
    "Seat",
    "Suzuki"
]);

define("color", [
    "azul",
    "rojo",
    "negro",
    "blanco",
    "gris"
]);

$n = rand(0, 4);
$c = rand(0, 4);

switch ($n) {
    case 0:
        if ($c == 1) {
            echo "Vehículo no disponible";
        } else {
            echo coche[$n] . " " . color[$c];
        }
        break;
    case 1:
        if ($c == 0) {
            echo "Vehículo no disponible";
        } else {
            echo coche[$n] . " " . color[$c];
        }
        break;
    case 2:
        if ($c == 3) {
            echo "Vehículo no disponible";
        } else {
            echo coche[$n] . " " . color[$c];
        }
        break;
    case 3:
        if ($c == 2) {
            echo "Vehículo no disponible";
        } else {
            echo coche[$n] . " " . color[$c];
        }
        break;
    case 4:
        if ($c == 2) {
            echo "Vehículo no disponible";
        } else {
            echo coche[$n] . " " . color[$c];
        }
        break;
}
?>
</body>
</html>
```

