
## 1. Introducción

Las bases de datos relacionales son ideales para aplicaciones tradicionales que trabajan con estructuras simples y poco cambiantes incluso cuando la aplicación esté desarrollada con POO y sea necesario mapeo objeto relacional (ORM)

Pero cuando la aplicación requiere otras necesidades como soporte multimedia o almacenar objetos muy cambiantes y complejos en estructura y relaciones, estas no son las más adecuadas. 

Porque nos llevaría a descomponer los objetos en diferentes tablas, muchas tablas que con llevarían muchos JOINS y disminuirían el rendimiento.

**Bases de Datos Orientadas a Objetos**
Las **Bases de Datos Orientadas a Objetos (BDOO)** o **Bases de objetos** se integran sin problemas con POO al soportar un modelo de objetos puro. Son ideales para almacenar y recuperar datos complejos permitiendo a los usuarios su navegación directa (sin necesidad de mapeo).

Estas bases de datos aparecen a finales de los 80 por:
- Necesidad de lenguajes POO de persistir objetos
- Limitaciones en BBDD relacionales por manejar solo estructuras simples

El objeto es una entidad que se puede identificar unívocamente y que describe tanto estado como comportamiento de una entidad del mundo real.

**Bases de Datos Objeto Relacionales**
Como las BDOO no terminaban de asentarse por la inexistencia de un estándar y por la aceptación, experiencia y difusión de las BD Relacionales se implementaron nuevas funciones del modelo orientado a objetos en la BBDD Relacionales. En ellas existe un mapeo subyacente (costoso y poco flexible) cuando los objetos y sus interacciones son complejos. 

## 2. Características de Bases de datos orientadas a objetos

- **Soportan modelo de objetos puros**: El lenguaje de programación y el esquema de BBDD soportan las mismas definiciones de tipos
- **Soportan características propias de la Orientación a Objetos** (Agregación, encapsulamiento, polimorfismo, herencia)
- **Identificador de objeto (OID)**: Cada objeto tiene un identificador generado por el sistema que es único para cada objeto. Cuando se necesite modificar un objeto debe recuperarse de BBDD, hacer los cambios y almacenarlo nuevamente. Los OID son independientes del contenido del objeto: Aunque la información cambie el objeto mantiene su OID. Los objetos serán equivalentes si tiene misma información y diferentes OID.
- **Jerarquía y extensión de tipos**: Se pueden definir nuevos tipos basándose en tipos predefinidos, cargándolos en jerarquía de tipos o de clases
- **Objetos complejos**: Los objetos pueden tener estructura de objeto de complejidad arbitraria a fin de contener toda la información que describe el objeto
- **Acceso navegacional de datos**: Cuando los datos se almacenan en una estructura de red densa y con estructura de diferentes niveles de profundidad, el acceso a datos se hace navegando por la estructura de objetos se expresa de forma natural con las construcciones nativas del lenguaje sin necesidad de uniones o joins. 
- **Gestión de versiones**: El mismo objeto puede estar representado por múltiples versiones. Muchas aplicaciones de BBDD que usan orientación a objetos necesitan la existencia de varias versiones del objeto ya que si estando la aplicación en funcionamiento es necesario modificar alguno de los módulos, el diseñador debe crear una versión de cada uno de ellos para efectuar cambios. 

### 2.1. Uso recomendado, ventajas e inconvenientes

**Uso recomendado**
Una BD Orientada a Objetos es ventajosa frente a BBDD Relacional si la aplicación:
- Tiene gran número de tipos diferentes
- Tiene gran número de relaciones entre objetos
- Tiene objetos con comportamientos complejos.

**Ventajas**
- Las BD Orientadas a Objetos son **transparentes**: Manipulan directamente los datos usando un entorno POO, por lo que el desarrollador solo debe preocuparse de los objetos de su aplicación en lugar de cómo almacenarlos y recuperarlo del medio físico. 
- **Gran capacidad de modelado**: Permite modelar el mundo real gracias a encapsulamiento y herencia
- **Soporte para manejo de datos complejos**: Manipula de forma rápida y ágil objetos complejos al estar la estructura dada por referencias (apuntadores lógicos) entre objetos
- **Alta velocidad de procesamiento** Como el resultado son objetos, no hay que reensamblarlos cada vez que se accede a BBDD
- **Extensibilidad**: Se pueden construir nuevos tipos de datos a partir de los ya existentes, agrupar propiedades comunes e incluirlas en superclases
- **Mejora los costes de desarrollo**: Porque posibilita la reutilización de código
- **Facilita el control de acceso y la concurrencia** Porque puede bloquear a ciertos objetos incluso en jerarquía completa de objetos
- **Funciona de forma eficiente en entornos cliente/servidor y arquitecturas distribuidas**

**Desventajas**
- **Carencia de modelo de datos universal**: No hay modelo de datos aceptado universalmente y la mayoría de modelos carecen de base teórica
- **Falta de estándares**
- **Complejidad**
- **Competencia de otros modelos** Relacionales y objeto-relacionales están muy asentadas
- **Difícil optimización de consultas** Requiere compresión de la implementación de los objetos. Pero esto compromete el concepto de encapsulación.

## 3. Gestores de bases de datos orientadas a objetos

El Sistema Gestor de Bases de Datos Orientado a Objetos (SGBDOO, ODBMS Object Database Management System) es software específico que sirve de interfaz entre la base de objetos, el usuario y las aplicaciones que la utilizan. 

Por ser SGBD tiene mecanismos que optimizan el acceso, gestionan la concurrencia, seguridad, gestión de usuarios, facilitan consulta y recuperación
Por ser OO incorpora identidad, encapsulamiento, herencia, polimorfismo control de tipos. 

Cuando aparecieron las bases de datos orientadas a objetos, un grupo formado por desarrolladores y usuarios de bases de objetos, denominado ODMG (Object-Oriented Database Management Group), propuso un estándar que se conoce como estándar **ODMG-93** y que se ha ido revisando con el tiempo, pero que en realidad **no ha tenido mucho éxito**, aunque es un punto de partida.

**Para el desarrollo de SGBDOO se siguen**
- Ampliar lenguaje de programación OO existente con capacidades de BD. Por ej.: GemStone
- Proporcionar bibliotecas de clases con capacidades tradicionales de BBDD como persistencia, transacciones, concurrencia. Ej.: ObjectStore, Versant
- Ampliar lenguaje de BD con capacidades OO: SQL 2003, Object SQL (OQL, propuesto por ODMG)

Carencia de estándar -> Problema para portabilidad e interoperabilidad. Por eso la variedad de SGBDOO es mucho menor que en las relacionales.

**Ejemplos de SGBDOO**
- **Db4o** de Versant. Open Source para Java y .NET. GPL. Su versión está descontinuada. 
- **Matisse**: DDL y DML, interfaces para C, C++, Eiffel, Java
- **ObjectDB**: Soporte para Java, C++, Python. No es libre aunque tienen versiones de prueba.
- **EyeDB**. Basado en ODMG, da DDL y DML e interfaces para C++ y Java. Es libre (GNU)
- **Neodatis**, **ObjectStore**, **Gemtone**.

### 3.1. Objetos simples y objetos estructurados

En las BD de objetos los objetos están interrelacionados por referencias entre ellos de forma similar a como los objetos se referencia entre sí en memoria.
Se distingue entre:
- **Objeto de tipo simple**: No contiene a otros objetos. Posee estructura de un solo nivel de profudndidad.
- **Objeto de tipo estructurado**: Incluye entre sus componentes a otros objetos. Se define aplicando constructores de tipos disponibles por el SGBDOO recursivamente a varios niveles de profundiad.

Entre el objeto y los componentes de cada nivel hay dos tipos de referencia:
- **Referencia de propiedad**: Componentes de un objeto se encapsulan dentro del propio objeto y se consideran parte de ese objeto. (**Relación es-parte-de**). No necesitan tener identificadores de objeto. Solo los métodos de ese objeto pueden acceder a ellos. Desaparecen si el propio objeto se elimina.
- **Referencia de asociación**: Componentes de objeto tienen objetos independientes pero es posible hacer referencia a ellos. (**Relación está-asociado-con**). Cuando el objeto estructurado debe acceder a sus componentes invoca los métodos apropiados ya que no están encapsulados en el objeto. 

Ej.: En Oficina código y dirección son parte_de mientras que jefe es independiente que esta_asociado_con. 

Las referencias de asociación son como las relaciones del modelo relacional. Pueden detectarse mutuamente en una o dos direcciones (Claves ajenas, foráneas, relaciones en el modelo relacional). Y por ejemplo la relación uno a muchos es un objeto colección que se manejará como cualquier otro objeto. 

### 3.2. Instalación del gestor de objetos Db4o

**Características de Db4o**
- Modelo de clases es el propio esquema de la BBDD. Se elimina el proceso de diseño, implementación y mantenimiento de la BBDD
- Diseñada con estrategia de proporcionar bibliotecas de clases con capacidades tradicionales de las BBDD y cero administración
- Puede trabajar como **base de datos embebida** distribuida con la aplicación y solo esta podría acceder a la BBDD. Sería invisible para el usuario final. 

Es un fichero .jar distribuible con cualquier aplicación sin instalar nada, sin drivers JDBC...

**Instalación**
La instalación consiste en:
- Instalar el motor de BBDD (clases para que funcione la API)
- Instalar aplicación para visualizar los datos con los que trabaja. 

## 4. El API de la base de objetos

**Db4o** no sirve para absolutamente nada porque ya no tiene ni soporte. Pero aún así mencionemos rapidísimamente que su API está disponible para Java y .NET

**Paquetes del API**
- **com.db4o.** Paquete principal (core) de la Base de Objetos. Las interfaces y clases más importantes que incluye son:
    - `ObjectContainer`. Es el interfaz que permite realizar las principales tareas con la base de objetos. Un `ObjectContainer` puede representar **una base de datos independiente** (stand-alone) o una **conexión a un servidor** (en línea cliente-servidor). Este interfaz proporciona métodos para almacenar `store()` consultar `queryByExample()` y eliminar `delete()` objetos de la base de datos, así como cerrar la conexión a ésta `close()` También permite confirmar commit y deshacer rollback transacciones.
    - `EmbeddedObjectContainer`. Es un interfaz que extiende a `ObjectContainer` y representa un `ObjectContainer` local atacando a la base de datos.
    - `Db4oEmbedded`. Es una clase que proporciona métodos estáticos para conectar con la base de datos en modo embebido.
    - `ObjectServer`. Es el interfaz que permite trabajar con una base de datos db4o en modo cliente-servidor.
    - `ObjectSet`. Es un interfaz que representa el conjunto de objetos devueltos por una consulta.
- **com.db4o.query**. Paquete con funcionalidades de consulta. Proporciona interfaces que permiten establecer las condiciones y criterios de un consulta y una clase para realizar consultas mediante Native Query (Consultas nativas).
- **com.db4o.config**. Paquete con funcionalidades de configuración. Contiene interfaces y clases que nos permiten configurar y/o personalizar la base de objetos según necesiades. La configuración de la base de objetos se hace por norma general antes de abrir la sesión en la misma.
    - `EmbeddedConfiguration`. Es la interface de configuración para el uso en modo embebido.

Siempre que trabajemos con bases de objetos Db4o utilizaremos el interface `ObjectContainer`, puesto que es quien representará a la base de objetos, sea embebida o no.

### 4.1. Apertura y cierre de conexiones

**Para Db4o, el paquete `com.db4o` proporciona las siguientes clases e interfaces:**

- **Apertura de conexión:**
    
    - `Db4oEmbedded`: Clase que proporciona métodos estáticos como `openFile()` para abrir una instancia de la base de datos en modo embebido. Limita a una única conexión en la base de datos.
    - `ObjectServer`: Interfaz que permite trabajar en modo cliente-servidor. Usa `Db4o.openServer()` para abrir la base de datos como servidor, y `openClient()` para abrir conexiones cliente.
- **Cierre de conexión:**
    
    - Método `close()` de la interfaz `ObjectContainer`.

**Esquema de trabajo para operar con la base de objetos:**

1. Declarar un `ObjectContainer`.
2. Abrir una conexión a la base de objetos con `openFile()`.
3. Realizar operaciones (consultas, borrados y modificaciones) dentro de un bloque `try-catch`.
4. Cerrar la conexión con `close()`.

**Ejemplo:**
```java
ObjectContainer db = Db4oEmbedded.openFile(Db4oEmbedded.newConfiguration(), "congreso.db4o");
try {
    // Operaciones con la base de datos
} catch (Exception e) {
    e.printStackTrace();
} finally {
    db.close();
}
```

### 4.2. Consultas a la base de objetos

**Tipos de consultas:**

1. **Query By Example (QBE):** Forma sencilla y básica con limitaciones.
2. **Native Queries (NQ):** Principal interfaz de consultas, permite filtrar instancias en la base de objetos.
3. **Simple Object Data Access (SODA):** Permite generar consultas dinámicas y es más potente y rápida.

**Resumen y ejemplos:**

- **Consultas por ejemplo (QBE):**

```java
Ponente proto = new Ponente("NIF123", null, null, 0);
ObjectSet<Ponente> result = db.queryByExample(proto);
```

**Consultas nativas (NQ):**

```java
List<Ponente> result = db.query(new Predicate<Ponente>() {
    public boolean match(Ponente p) {
        return p.getNombre().equals("Juan");
    }
});
```

**Consultas SODA:**

```java
Query query = db.query(); 
query.constrain(Ponente.class); 
query.descend("nombre").constrain("Juan"); ObjectSet<Ponente> result = query.execute();
```

### 4.3. Actualización de objetos simples

**Pasos para modificar objetos almacenados:**

1. Cambiar los valores del objeto.
2. Almacenar de nuevo el objeto con el método `store()`.

**Ejemplo de modificación:**

```java
Ponente ponente = db.queryByExample(new Ponente("NIF123", null, null, 0)).next();
ponente.setEmail("nuevoemail@example.com");
db.store(ponente);
```

**Para eliminar objetos:**

```java
Ponente ponente = db.queryByExample(new Ponente("NIF123", null, null, 0)).next();
db.delete(ponente);
```

### 4.4. Actualización de objetos estructurados

**Definición de objetos estructurados:**

- Objetos que contienen otros objetos (objetos hijo).
- Diferentes niveles de profundidad: Nivel 1 (objeto padre), Nivel 2 (objeto hijo), etc.

- Los objetos estructurados se almacenan asignando valores con set() y después persistiendo el objeto con store(). Al almacenar un objeto estructurado del nivel más alto, se almacenarán de forma implícita todos los objetos hijo.
- Las consultas se realizan por cualquiera de los sistemas soportados por el gestor y se podrá ir descendiendo por los diferentes niveles de profundidad.
- La eliminación o borrado de un objeto estructurado se realiza mediante el método delete(). Por defecto, no se eliminarán los objetos miembro. Para eliminar objetos estructurados en cascada o de forma recursiva, eliminando los objetos miembro, habrá que configurar de modo apropiado la base de objetos antes de abrirla, mediante el paquete com.db4o.config. En el caso de modo embebido, se hará mediante la interface EmbeddedConfiguration. En la nueva configuración se debe indicar cascadeOnDelete(true).
- La modificación se realizará actualizando los nuevos valores mediante el método set(). Por defecto las modificaciones solo afectan al nivel más alto. Para actualizar de forma recursiva todos los objeto miembro habrá que indicar en la configuración cascadeOnUpdate(true).

**Ejemplo de definición:**
```java
public class Charla {
    private String titulo;
    private int duracion;
    private Ponente ponente;

    // Métodos getters y setters
}
```

**Operaciones con objetos estructurados:**

- **Almacenamiento:**
```java
Charla charla = new Charla("Título", 60, ponente);
db.store(charla);

```


- **Consultas:**
```java
Query query = db.query();
query.constrain(Charla.class);
query.descend("ponente").descend("nombre").constrain("Juan");
ObjectSet<Charla> result = query.execute();

```


-  **Eliminación:**
```java
Charla charla = db.queryByExample(new Charla("Título", 60, null)).next();
db.delete(charla);

```


- **Actualización en cascada:**
```java
EmbeddedConfiguration config = Db4oEmbedded.newConfiguration();
config.common().objectClass(Charla.class).cascadeOnUpdate(true);
config.common().objectClass(Charla.class).cascadeOnDelete(true);

```

## 5. Lenguaje de consulta de objetos OQL

**OQL (Object Query Language)** es el lenguaje de consulta de objetos propuesto por el estándar ODMG. 

**Características**
- **Lenguaje declarativo de tipo SQL** que permite realizar consultas de modo eficiente sobre bases de datos orientadas a objetos
- **Sintaxis similar a SQL**, superconjunto de la sintaxis de la sentencia SELECT **con algunas características añadidas de los conceptos ODMG** como identidad de objeto, objetos complejos, operaciones, herencia, polimorfismo, relaciones
- **No tiene primitivas para modificar el estado**. LO NORMAL ES USAR PARA ELLO LOS METODOS DEL OBJETO
- Puede usarse como **lenguaje autónomo o incrustado** dentro de otros como C++, Smalltalk y Java. 
- Una **consulta OQL incrustada** en uno de estos lenguajes puede devolver objetos que coincidan con ese sistema de tipos en ese lenguaje
- Desde OQL es posible invocar operaciones escritas en estos lenguajes
- Permite:
	- **Consulta asociativa**: Devuelve colección de objetos
	- **Consulta navegacional**: Accede a objetos individuales y las interrelaciones entre objetos sirven para navegar entre objetos. 

### 5.1. Sintaxis, expresiones y operadores

```
SELECT [DISTINCT] <expresión, ...>
FROM <lista from>
[WHERE <condición> ]
[ORDER BY <expresión>]
```

Ejemplo:
```sql
SELECT p.nombre, p.email FROM p in Profesor WHERE p.ingreso <= 1990 ORDER BY p.nombre;
```


- En las consultas se necesita un **punto de entrada,** que suele ser el nombre de una clase.
- El **resultado de una consulta es una colección** que puede ser **tipo bag** (si hay valores repetidos) o **tipo set**(no hay valores repetidos). En este último caso habrá que especificar SELECT DISTINCT.
- En general, una consulta OQL **puede devolver un resultado con una estructura compleja especificada en la misma consulta** utilizando **struct**.
- Una vez que se establece un punto de entrada, **se pueden utilizar expresiones de caminos para especificar un camino a atributos y objetos relacionados**. Una expresión de camino **empieza normalmente con un nombre de objeto persistente o una variable iterador, seguida de ninguno o varios nombres de relaciones o de atributos conectados mediante un punto.**
- Es **posible crear objetos mutables** (no literales) **formados por el resultado de una consulta.**

**Operadores**
- Operadores de acceso: "." / "->" aplicados a un atributo, una expresión o una relación.
    FIRST / LAST (primero / último elemento de una lista o un vector).
- Operadores aritméticos: +, -, *, /, -(unario), MOD, ABS para formar expresiones aritméticas.
- Operadores relacionales: >, <, >=, <=, <>, = que permiten comparaciones y construir expresiones lógicas.
- Operadores lógicos: NOT, AND, OR que permiten enlazar otras expresiones.

**Otras características**
- Posibilidad de definir **vistas**
- **Extracción de elementos sencillos de colecciones** `set`, `bag` o `list`
- **Operadores de colecciones** como **funciones de agregación** (MAX(), MIN(), COUNT(), SUM() y AVG()) y cuantificadores (FOR ALL, EXISTS).
- **Realización de agrupaciones** mediante GROUP BY y filtro de los grupos mediante HAVING.
- Combinación de consultas mediante **JOINs**
- **Unión, intersección y resta de colecciones** mediante los operadores UNION, INTERSEC y EXCEPT.

### 5.2. Matisse, gestor de objetos con OQL

**Matisse** es un gestor orientado a objetos que incorpora características de ODMG como ODL y OQL y que tiene soporte para Java. El propio Matisse llama SQL a su lenguaje de consultas, pero nos referiremos como SQL. 

Hay un driver `matisse.jar` para interactuar con aplicaciones en Java.
Destacan de la API los paquetes:
-` com.matisse`. Paquete de cllases e interfaces básicos para trabajar con Java y una base de datos de objetos Matisse.
- `MtDatabase`. Clase que proporciona todos los métodos para realizar las conexiones y transacciones en la base de objetos.
- `com.matisse.sql`. Paquete de clases que permiten interactuar con la base de objetos vía JDBC.


### 5.3. Ejecución de sentencias OQL


Por ejemplo, para recuperar el valor de todos los atributos de los objetos tipo Profesor, escribiríamos la siguiente sentencia OQL:

`SELECT * FROM Profesor;`

Y para recuperar del atributo nombre de los objetos tipo Profesor cuyo año de ingreso es anterior al 1990, escribiríamos la siguiente sentencia :

`SELECT nombre FROM Profesor WHERE ingreso <= 1990;`

Las siguientes son algunas consideraciones y ejemplos sobre las consultas con SELECT:

- Toda sentencia SELECT finaliza en punto y coma.
- Además de la cláusula WHERE, que permite establecer un criterio de selección se pueden utilizar las cláusulas de agrupamiento GROUP BY, y de ordenación ORDER BY, entre otras. También se pueden asignar alias mediante AS, realizar búsquedas por patrones de caracteres con LIKE.
    
    **Ejemplo**: título y tema de las tesis cuyo tema contien la palabra Objeto, ordenadas por tema.
    
`    SELECT titulo AS "Tesis", tema FROM Tesis `
    
    WHERE tema LIKE '%Objeto%' ORDER BY tema; 
    
- Al recupear todos los atributos de una clase mediante SELECT *, la consulta retornará el OID de cada objeto recuperado, así como las interrelaciones o relaciones definidas para esa clase. El OID y la interrelación son del tipo string y se representan mediante un número hexadecimal. Realmente el identificador recuperado para la interrelación, hace referencia al primer objeto relacionado, incluso aunque la interrelación incluya a más de un objeto.
- Se pueden hacer JOIN de clases, y por ejemplo esto puede permitir obtener todos los objetos relacionados con otro objeto en una consulta asociativa.
    
    **Ejemplo**: nombre de cada profesor y título y tema de las tesis que dirige con JOIN
    
`    SELECT p.nombre, t.titulo, t.tema FROM Profesor p JOIN Tesis t ON t.es_dirigida = p.OID;`
    
- Mediante SELECT se pueden realizar consultas navegacionales haciendo referencia a las interrelacionaes entre objetos.
    
    **Ejemplo**: nombre de cada profesor y título y tema de las tesis que dirige, navegacional
    
`    SELECT t.titulo AS "Tesis", tema, t.es_dirigida.nombre AS "Profesor " FROM Tesis t;`
    
- También se pueden realizar consultas navegacionales a través de la referencia de los objetos (REF()). **Ejemplo**: tesis que dirigen los profesores con ingreo el 1990 o posterior
    
`    SELECT REF(p.dirige) FROM Profesor p  WHERE p.ingreo >= 1990;`


```java
import com.matisse.MtDatabase;
import com.matisse.MtException;
import com.matisse.MtObjectId;

public class CreateMatisseDB {
    public static void main(String[] args) {
        MtDatabase db = null;
        
        try {
            // Conectar al servidor Matisse
            db = new MtDatabase("localhost", 50000, "admin", "admin");
            db.open();
            
            // Crear una nueva base de datos
            db.createDatabase("mydb");
            
            // Conectar a la nueva base de datos
            db.useDatabase("mydb");
            
            // Crear tablas y esquema
            db.executeCommand("CREATE TABLE Ponente (NIF VARCHAR(20) PRIMARY KEY, Nombre VARCHAR(50), Email VARCHAR(50), Cache INTEGER)");
            db.executeCommand("CREATE TABLE Charla (Titulo VARCHAR(100), Duracion INTEGER, PonenteNIF VARCHAR(20), FOREIGN KEY (PonenteNIF) REFERENCES Ponente(NIF))");
            
            System.out.println("Database and tables created successfully.");
        } catch (MtException e) {
            e.printStackTrace();
        } finally {
            if (db != null) {
                db.close();
            }
        }
    }
}
```

```java
import com.matisse.MtDatabase;
import com.matisse.MtException;
import com.matisse.MtResultSet;

public class ExecuteOQL {
    public static void main(String[] args) {
        MtDatabase db = null;
        
        try {
            // Conectar a la base de datos
            db = new MtDatabase("localhost", 50000, "admin", "admin");
            db.open();
            db.useDatabase("mydb");
            
            // Ejecutar una consulta OQL
            String oql = "SELECT P FROM Ponente P WHERE P.Nombre = 'Juan'";
            MtResultSet rs = db.executeQuery(oql);
            
            // Procesar el resultado
            while (rs.next()) {
                String nif = rs.getString("NIF");
                String nombre = rs.getString("Nombre");
                String email = rs.getString("Email");
                int cache = rs.getInt("Cache");
                
                System.out.println("NIF: " + nif + ", Nombre: " + nombre + ", Email: " + email + ", Cache: " + cache);
            }
            
            rs.close();
        } catch (MtException e) {
            e.printStackTrace();
        } finally {
            if (db != null) {
                db.close();
            }
        }
    }
}
```

```java
import com.matisse.MtDatabase;
import com.matisse.MtException;

public class InsertData {
    public static void main(String[] args) {
        MtDatabase db = null;
        
        try {
            // Conectar a la base de datos
            db = new MtDatabase("localhost", 50000, "admin", "admin");
            db.open();
            db.useDatabase("mydb");
            
            // Insertar datos en Ponente
            db.executeCommand("INSERT INTO Ponente (NIF, Nombre, Email, Cache) VALUES ('123456789', 'Juan Perez', 'juan.perez@example.com', 100)");
            
            // Insertar datos en Charla
            db.executeCommand("INSERT INTO Charla (Titulo, Duracion, PonenteNIF) VALUES ('Introducción a Java', 90, '123456789')");
            
            System.out.println("Data inserted successfully.");
        } catch (MtException e) {
            e.printStackTrace();
        } finally {
            if (db != null) {
                db.close();
            }
        }
    }
}
```

```java
import com.matisse.MtDatabase;
import com.matisse.MtException;

public class UpdateData {
    public static void main(String[] args) {
        MtDatabase db = null;
        
        try {
            // Conectar a la base de datos
            db = new MtDatabase("localhost", 50000, "admin", "admin");
            db.open();
            db.useDatabase("mydb");
            
            // Actualizar datos en Ponente
            db.executeCommand("UPDATE Ponente SET Email = 'nuevo.email@example.com' WHERE NIF = '123456789'");
            
            System.out.println("Data updated successfully.");
        } catch (MtException e) {
            e.printStackTrace();
        } finally {
            if (db != null) {
                db.close();
            }
        }
    }
}

```

```java
import com.matisse.MtDatabase;
import com.matisse.MtException;

public class DeleteData {
    public static void main(String[] args) {
        MtDatabase db = null;
        
        try {
            // Conectar a la base de datos
            db = new MtDatabase("localhost", 50000, "admin", "admin");
            db.open();
            db.useDatabase("mydb");
            
            // Eliminar datos de Ponente
            db.executeCommand("DELETE FROM Ponente WHERE NIF = '123456789'");
            
            System.out.println("Data deleted successfully.");
        } catch (MtException e) {
            e.printStackTrace();
        } finally {
            if (db != null) {
                db.close();
            }
        }
    }
}

```

### 5.4. Ejecución de sentencias OQL por JDBC

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;

public class CreateMatisseDB {
    public static void main(String[] args) {
        String url = "jdbc:matisse://localhost:50000/";
        String user = "admin";
        String password = "admin";
        
        try {
            // Load the Matisse JDBC driver
            Class.forName("com.matisse.jdbc.Driver");
            
            // Connect to Matisse server
            Connection conn = DriverManager.getConnection(url, user, password);
            
            // Create a new database
            Statement stmt = conn.createStatement();
            stmt.executeUpdate("CREATE DATABASE mydb");
            
            // Use the new database
            stmt.executeUpdate("USE mydb");
            
            // Create tables and schema
            stmt.executeUpdate("CREATE TABLE Ponente (NIF VARCHAR(20) PRIMARY KEY, Nombre VARCHAR(50), Email VARCHAR(50), Cache INTEGER)");
            stmt.executeUpdate("CREATE TABLE Charla (Titulo VARCHAR(100), Duracion INTEGER, PonenteNIF VARCHAR(20), FOREIGN KEY (PonenteNIF) REFERENCES Ponente(NIF))");
            
            System.out.println("Database and tables created successfully.");
            
            stmt.close();
            conn.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;

public class InsertData {
    public static void main(String[] args) {
        String url = "jdbc:matisse://localhost:50000/mydb";
        String user = "admin";
        String password = "admin";
        
        try {
            // Load the Matisse JDBC driver
            Class.forName("com.matisse.jdbc.Driver");
            
            // Connect to Matisse database
            Connection conn = DriverManager.getConnection(url, user, password);
            
            // Insert data into Ponente
            String insertPonente = "INSERT INTO Ponente (NIF, Nombre, Email, Cache) VALUES (?, ?, ?, ?)";
            PreparedStatement pstmtPonente = conn.prepareStatement(insertPonente);
            pstmtPonente.setString(1, "123456789");
            pstmtPonente.setString(2, "Juan Perez");
            pstmtPonente.setString(3, "juan.perez@example.com");
            pstmtPonente.setInt(4, 100);
            pstmtPonente.executeUpdate();
            
            // Insert data into Charla
            String insertCharla = "INSERT INTO Charla (Titulo, Duracion, PonenteNIF) VALUES (?, ?, ?)";
            PreparedStatement pstmtCharla = conn.prepareStatement(insertCharla);
            pstmtCharla.setString(1, "Introducción a Java");
            pstmtCharla.setInt(2, 90);
            pstmtCharla.setString(3, "123456789");
            pstmtCharla.executeUpdate();
            
            System.out.println("Data inserted successfully.");
            
            // Close the prepared statements and connection
            pstmtPonente.close();
            pstmtCharla.close();
            conn.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;

public class UpdateData {
    public static void main(String[] args) {
        String url = "jdbc:matisse://localhost:50000/mydb";
        String user = "admin";
        String password = "admin";
        
        try {
            // Load the Matisse JDBC driver
            Class.forName("com.matisse.jdbc.Driver");
            
            // Connect to Matisse database
            Connection conn = DriverManager.getConnection(url, user, password);
            
            // Update data in Ponente
            String updatePonente = "UPDATE Ponente SET Email = ? WHERE NIF = ?";
            PreparedStatement pstmt = conn.prepareStatement(updatePonente);
            pstmt.setString(1, "nuevo.email@example.com");
            pstmt.setString(2, "123456789");
            pstmt.executeUpdate();
            
            System.out.println("Data updated successfully.");
            
            // Close the prepared statement and connection
            pstmt.close();
            conn.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;

public class DeleteData {
    public static void main(String[] args) {
        String url = "jdbc:matisse://localhost:50000/mydb";
        String user = "admin";
        String password = "admin";
        
        try {
            // Load the Matisse JDBC driver
            Class.forName("com.matisse.jdbc.Driver");
            
            // Connect to Matisse database
            Connection conn = DriverManager.getConnection(url, user, password);
            
            // Delete data from Ponente
            String deletePonente = "DELETE FROM Ponente WHERE NIF = ?";
            PreparedStatement pstmt = conn.prepareStatement(deletePonente);
            pstmt.setString(1, "123456789");
            pstmt.executeUpdate();
            
            System.out.println("Data deleted successfully.");
            
            // Close the prepared statement and connection
            pstmt.close();
            conn.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 6. Características de bases de datos objeto-relacionales

#### Introducción

Las Bases de Datos Objeto-Relacionales (BDOR) son un híbrido entre las Bases de Datos Relacionales (BDR) y las Bases de Datos Orientadas a Objetos (BDOO). Su objetivo es combinar los beneficios de ambos modelos, aunque esto implica renunciar a algunas características de cada uno.
#### Objetivos de las BDOR

1. **Mejorar la representación de los datos mediante la orientación a objetos.**
2. **Simplificar el acceso a datos manteniendo el sistema relacional.**

#### Estructura de las BDOR

- **Tablas en filas y columnas:** Se siguen almacenando datos en formato tabular aunque la estructura de filas no está restringida a contener escalares o valores atómicos.
- **Tipos estructurados:** Las columnas pueden contener tipos compuestos (vectores, conjuntos, etc.).
- **Herencia directa:** Las tablas pueden ser definidas en función de otras tablas.

#### Características Clave

Tanto las tablas como las columnas son tratados como objetos: Se hace mapeo objeto-relacional de forma transparente. 

1. **Tipos definidos por el usuario:**
    - Se pueden crear tipos de datos compuestos o estructurados.
    - Permite tener atributos multivaluados en una columna.
2. **Tipos Objeto:**
    - Creación de objetos como nuevos tipos de datos.
    - Permite relaciones anidadas.
3. **Reusabilidad:** - Los tipos de datos definidos pueden ser reutilizados en múltiples tablas.
4. **Creación de funciones:**
    - Definición y almacenamiento de funciones en el gestor de la BDOR.
    - Las funciones pueden modelar el comportamiento de un tipo objeto (métodos).
5. **Tablas anidadas:**
    - Columnas pueden ser arrays o vectores multidimensionales.
    - Soporte para tipos básicos y estructurados en tablas anidadas.
6. **Herencia:**
    - Soporte para subtipos y subtablas.

### Estándar SQL99

La norma ANSI SQL1999 (SQL99) extiende el estándar SQL92 de las Bases de Datos relacionales dando cabida a nuevas características orientadas a objetos y preservando los fundamentos relacionales.

- **Extensión de tipos de datos**.
    - Nuevos tipos de datos básicos para datos de caracteres de gran tamaño, y datos binarios de gran tamaño (Large Objects)
    - Tipos definidos por el usuario o tipos estructurados.
    - Tipos colección, como los arrays, `set`, bag y `list`.
    - Tipos fila y referencia
- **Extensión de la semántica de datos**.
    - Procedimientos y funciones definidos por el usuario, y almacenados en el gestor.
    - Un tipo estructurado puede tener métodos definidos sobre él.

Ejemplo:

```sql
CREATE TYPE profesor AS (
id INTEGER,
nombre VARCHAR (20),
sueldo_base DECIMAL (9,2),
complementos DECIMAL (9,2),
INSTANTIABLE NOT FINAL
METHOD sueldo() RETURNS DECIMAL (9,2));
CREATE METHOD sueldo() FOR profesor
BEGIN
......
END;
```

## 7. Gestores de bases de datos objeto-relacionales

A continuación te indicamos algunos ejemplos de **gestores objeto-relacionales**, tanto de código libre como propietario, todos ellos con soporte para Java:

- De código abierto:
    - **PostgreSQL**
    - **Apache Derby**
- De código propietario
    - **Oracle**
    - **First SQL**
    - **DB2 de IBM**

Actualmente se siguen SQL99 y SQL2003 aunque cada gestor incorpora sus propias particulares y diferencias. 
Por ejemplo en Oracle se pueden usar herencia de tipos y de tablas mientras que en PostgreSQL solo de tablas.

### 7.1. Instalación de PostgreSQL

El código fuente de PostgreSQL está disponible bajo la licencia BSD (libertad para usar, modificar y distribuir PostgreSQL en cualquier forma ya sea junto a código abierto o cerrado). Además PostgreSQL incluye API para Java y .NET.

Instalación de PostgreSQL. Se solicita contraseña para el usuario postgres, administrador por defecto dela Base de datos. La administración visual se puede hacer con pgAdmin. 

Suele estar en escuchando en **localhost:5432**

Para crear una BBDD se abre pgAdmin y se muestran una serie de nodos. **Databases** contiene las instancias de las bases de datos creadas y allí con New Database puede crearse una. Especificar codificación de caracteres en Definition. Puede especificarse **Spanish_Spain.1252** en Collation y Character type para asegurarse de que ordenará correctamente los campos y no habrá caracteres erróneos. 

De la BBDD cuelgan
- Schemas. Contenedores de la información. Por defecto se crea uno "public"
- Dentro del schema la información se organiza en Tables. Pueden crearse tablas sencillamente. 

### 7.2. Tipos de datos: básicos y estructurados

PostgreSQL no soporta herencia de tipos pero permite **definir nuevos tipos de datos mediante los mecanismos de extensión**.

Hay tres categorías de tipos de datos que encontramos en PostgreSQL:
- **Tipos básicos**: el equivalente a los tipos de columna usados en cualquier base de datos relacional.
- **Tipos compuestos**: un conjunto de valores definidos por el usuario con estructura de fila de tabla, y que como tal puede estar formada por tipos de datos distintos.
- **Tipos array**: un conjunto de valores distribuidos en un vector multidimensional, con la condición de que todos sean del mismo tipo de dato (básico o compuesto). Ofrece más funcionalidades que el array del estándar SQL99.  Ojo no solo vectores, permite arrays multidimensionales.

Entre los **tipos básicos**, podemos destacar:

- **Tipos numéricos**. Aparte de valores enteros, números de coma flotantes, y números de precisión arbitraria, PostgreSQL incorpora también un tipo entero auto-incremental denominado serial.
- **Tipos de fecha y hora**. Además de los típicos valores de fecha, hora e instante, PostgreSQL incorpora el tipo interval para representar intervalos de tiempo.
- **Tipos de cadena de caracteres**. Prácticamente los mismos que en cualquier BDR.
- **Tipos largos**. Como por ejemplo, el tipo BLOB para representar objetos binarios. En la actualidad presentes en muchas BDR como MySQL.
----

Los tipos compuestos de PostgreSQL son los equivalentes a los tipos estructurados definidos por el usuario del estándar SQL99. 

Creamos un tipo dirección
```sql
CREATE TYPE direccion AS (
calle varchar, 
numero integer, 
codigo_postal integer);
```

Y se define una tabla basándose en ese tipo
```sql
CREATE TABLE afiliados AS( 
afiliado_id serial, 
nombre varchar(45), 
apellidos varchar(45), 
domicilio direccion);sql
```
### 7.3. Conexión mediante JDBC
 **JDBC4 Postgresql driver**

```xml
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.2.20</version>
</dependency>
```

```java
        String url = "jdbc:postgresql://localhost:5432/nombre_de_tu_base_de_datos";
        
        // Credenciales de la base de datos
        String usuario = "tu_usuario";
        String contraseña = "tu_contraseña";
        
        Connection conn = null;
        
        try {
            // Establecer la conexión
            conn = DriverManager.getConnection(url, usuario, contraseña);
            
            if (conn != null) {
                System.out.println("Conexión establecida!");
            } else {
                System.out.println("Fallo al hacer la conexión!");
            }
        } catch (SQLException e) {
            System.out.println("Error de SQL: " + e.getMessage());
        } finally {
            try {
                if (conn != null && !conn.isClosed()) {
                    conn.close();
                }
            } catch (SQLException ex) {
                ex.printStackTrace();
            }
        }
```

La conexión se mantiene operativa hasta llamar al método `close()`
Si esta no existe, surge una **PSQLException "FATAL: no existe la base de datos ...**

### 7.4. Consulta y actualización de tipos básicos

**PostgreSQL implementa los objetos como filas, las clases como tablas, y los atributos como columnas**. Hablaremos por tanto de tablas, filas y columnas, tal y como lo hace PostgreSQL.

Para interactuar con PostgreSQL desde Java, vía JDBC, debemos enviar sentencias SQL a la base de datos mediante el uso de comandos.

Por tanto, si nuestra conexión es conn, para enviar un comando Statement haríamos lo siguiente:

- Crear la sentencia, por ejemplo.: Statement sta = conn.createStatement();
- Ejecutar la sentencia:
    - sta.executeQuery(string sentenciaSQL); si `sentenciaSQL` es una consulta (SELECT)
    - sta.executeUpdate(string sentenciaSQL); si `sentenciaSQL` es una actualización (INSERT, UPDATE O DELETE)
    - sta.execute(string sentenciaSQL); si `sentenciaSQL` es un CREATE, `DROP`, o un ALTER

### 7.5. Consulta y actualización de tipos estructurados

Imaginemos que tenemos el tipo estructurado direccion:

```sql
CREATE TYPE direccion AS (
calle varchar, numero integer, codigo_postal varchar);
```


y la tabla afiliados, con una columna basada en el nuevo tipo:

```sql
CREATE TABLE afiliados(afiliado_id serial, nombre varchar, apellidos varchar, domicilio direccion);
```

**¿Cómo insertamos valores en una tabla con un tipo estructurado?** Se puede hacer de dos formas:

- **Pasando el valor del campo estructurado entre comillas simples** (lo que obliga a encerrar entre comillas dobles cualquier valor de cadena dentro), y paréntesis para encerrar los subvalores separados por comas: INSERT INTO afiliados (nombre, apellidos, direccion).

```sql
    INSERT INTO afiliados (nombre, apellidos, direccion)
             VALUES ('Onorato', 'Maestre Toledo', '(“Calle de Rufino”, 56, 98080)');
```

    
**- Mediante la función ROW que permite dar valor a un tipo compuesto o estructurado.**

```sql
    INSERT INTO afiliados (nombre, apellidos, direccion)
             VALUES ('Onorato', 'Maestre Toledo', ROW('Calle de Rufino', 56, 98080));
```


**¿Cómo se referencia una subcolumna de un tipo estructurado?**

- Se emplea la notación punto, '.' , tras el nombre de la columna entre paréntesis, (tanto en consultas de selección, como de modificación) . Por ejemplo:
```sql
    SELECT (domicilio).calle FROM afiliados WHERE (domicilio).codigo _postal=98080
```

devolvería el nombre de la calle Maestre Toledo. Los paréntesis son necesarios para que el gestor no confunda el nombre del campo compuesto con el de una tabla.

**Y ¿cómo se elimina el tipo estructurado?**

- Se elimina con DROP TYPE, por ejemplo `DROP TYPE direccion;`

### 7.6. Consulta y actualización de tipos array

PostgreSQL permite especificar **vectores multidimensionales como tipo de dato para las columnas** de una tabla. La única condición es que todos sus elementos sean del mismo tipo.

Por ejemplo:

- Declaración de una columna de tipo vector: nombre_columna tipo_dato[]
- Declaración de una columna de tipo matriz multidimensional: nombre_columna tipo_dato[][]

donde como se ve, sólo hay que agregar uno o más corchetes '[]' al tipo de dato.

Aunque PostgreSQL permite especificar el tamaño de cada dimensión en la declaración, y acepta escribir: `nombre_columna tipo_dato[5]` o bien `nombre_columna tipo_dato[2][3] `, las versiones actuales ignoran estos valores en la práctica, de manera que los array declarados de esta forma tienen la misma funcionalidad que los del ejemplo anterior.

En realidad ninguna de estas declaraciones es conforme al estándar SQL99, que sólo contempla el tipo array como columnas de vectores unidimensionales declarados con la palabra reservada array:

### 7.7 Funciones del gestor desde Java

Recuerda que el estándar SQL99 introduce la posibilidad de crear funciones de usuario que puedan quedar almacenadas en el gestor de bases de datos, utilizando un Lenguaje Procedural (PL). Estas funciones pueden definir el comportamiento de ciertos objetos y entonces, se llaman métodos. Oracle soporta métodos en este sentido, no así el gestor PostgreSQL.

Lo que si podremos hacer en PostgreSQL es crear funciones con prestaciones para los nuevos tipos de datos, tipos estructurados y array, y llamarlas desde una aplicación Java.

En PostgreSQL se pueden construir funciones mediante diferentes lenguajes:

- **Funciones de lenguaje de consultas o funciones SQL** (Escritas en lenguaje SQL)
- **Funciones de lenguaje procedural** (Escritas en lenguaje PL/pgSQL, PL/Java, etc)
- **Funciones de lenguaje de programación** (Escritas en un lenguaje de compilado, como C o C++),

Veremos algún ejemplo de funciones en SQL. Sobre estas funciones debes saber que:

- **Los parámetros de la función** pueden ser cualquier tipo de dato admitido por el gestor (un tipo básico, un tipo compuesto, un array o alguna combinación de ellos).
- El **tipo devuelto** puede ser un tipo básico, un array o un tipo compuesto.
- Su estructura general tiene la forma:
```sql
CREATE FUNCION nombre_funcion(tipo_1,tipo_2,...)
         RETURN tipo AS $$sentencia_sql$$
                  LANGUAJE SQL
```

Y debes **tener en cuenta que:**

- Los argumentos de la función SQL se pueden referenciar en las consultas usando la sintaxis $n:, donde `$1` se refiere al primer argumento, `$2` al segundo, y así sucesivamente. Si un argumento es un tipo compuesto, entonces se usará la notación '.' para acceder a sus subcolumnas.
- Por último, al final de la función hay que especificar que la función se ha escrito en lenguaje SQL mediante las palabras clave **LANGUAJE SQL**.

Por ejemplo, desde Java podemos crear una función que convierte un tipo estructurado, por ejemplo el tipo direccion, en una cadena. Para ello, ejecutaremos un comando **Statement (sta)** con el código SQL de creación de la función:


```java
sta.execute (“CREATE FUNCTION cadena_direccion(direccion)”+
“RETURNS varchar AS 'SELECT $1.calle||' '|| CAST($1.numero AS varchar)”+
“LANGUAGE SQL”;)
```

Si una función tiene algún parámetro de tipo estructurado, no se podrá eliminar el tipo hasta que no se elimine la función. Se puede usar **DROP C nb_tipo CASCADE** para eliminar de manera automática las funciones que utilizan ese tipo.

En el siguiente enlace te puedes descargar un ejemplo donde se crean funciones del gestor y se invocan desde una aplicación Java.

Pueden crearse funciones con parámetros tanto de tipo estructurado como array.


---------------

------------------

```sql
import java.sql.*;

public class JDBCExample {

    private static final String URL = "jdbc:postgresql://localhost:5432/nombre_de_tu_base_de_datos";
    private static final String USER = "tu_usuario";
    private static final String PASSWORD = "tu_contraseña";

    // Método para establecer la conexión
    public static Connection getConnection() throws SQLException {
        return DriverManager.getConnection(URL, USER, PASSWORD);
    }

    // Método para crear una tabla
    public static void createTable(Connection conn) throws SQLException {
        String sql = "CREATE TABLE IF NOT EXISTS empleados ("
                   + "id SERIAL PRIMARY KEY, "
                   + "nombre VARCHAR(100) NOT NULL, "
                   + "apellido VARCHAR(100) NOT NULL, "
                   + "email VARCHAR(100) UNIQUE)";
        try (Statement stmt = conn.createStatement()) {
            stmt.executeUpdate(sql);
            System.out.println("Tabla creada exitosamente.");
        }
    }

    // Método para insertar datos
    public static void insertData(Connection conn, String nombre, String apellido, String email) throws SQLException {
        String sql = "INSERT INTO empleados (nombre, apellido, email) VALUES (?, ?, ?)";
        try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setString(1, nombre);
            pstmt.setString(2, apellido);
            pstmt.setString(3, email);
            pstmt.executeUpdate();
            System.out.println("Datos insertados exitosamente.");
        }
    }

    // Método para consultar datos
    public static void queryData(Connection conn) throws SQLException {
        String sql = "SELECT id, nombre, apellido, email FROM empleados";
        try (Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery(sql)) {
            while (rs.next()) {
                int id = rs.getInt("id");
                String nombre = rs.getString("nombre");
                String apellido = rs.getString("apellido");
                String email = rs.getString("email");
                System.out.println("ID: " + id + ", Nombre: " + nombre + ", Apellido: " + apellido + ", Email: " + email);
            }
        }
    }

    // Método para actualizar datos
    public static void updateData(Connection conn, int id, String nuevoEmail) throws SQLException {
        String sql = "UPDATE empleados SET email = ? WHERE id = ?";
        try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setString(1, nuevoEmail);
            pstmt.setInt(2, id);
            int rowsAffected = pstmt.executeUpdate();
            System.out.println(rowsAffected + " fila(s) actualizada(s) exitosamente.");
        }
    }

    public static void main(String[] args) {
        try (Connection conn = getConnection()) {
            // Crear la tabla
            createTable(conn);

            // Insertar datos
            insertData(conn, "Juan", "Perez", "juan@example.com");

            // Consultar datos
            System.out.println("Datos de empleados:");
            queryData(conn);

            // Actualizar datos
            updateData(conn, 1, "nuevo_email@example.com");

            // Consultar datos actualizados
            System.out.println("Datos de empleados actualizados:");
            queryData(conn);
        } catch (SQLException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```


## 8. Gestión de transacciones

Como en cualquier otro Sistema de Bases de datos, en un Sistema de bases de objetos u objeto relacional, **una transacción** es un conjunto de sentencias que se ejecutan formando una unidad de trabajo, esto es, en forma indivisible o atómica, o se ejecutan todas o no se ejecuta ninguna.

Mediante la gestión de transacciones, los sistemas gestores proporcionan un acceso concurrente a los datos almacenados, mantienen la integridad y seguridad de los datos, y proporcionan un mecanismo de recuperación de la base de datos ante fallos.

Las transacciones deben cumplir el criterio ACID.

- **Atomicidad**. Se deben cumplir todas las operaciones de la transacción o no se cumple ninguna; no puede quedar a medias.
- **Consistencia**. La transacción solo termina si la base de datos queda en un estado consistente.
- **Isolation** (Aislamiento). Las transacciones sobre la misma información deben ser independientes, para que no interfieran sus operaciones y no se produzca ningún tipo de error.
- **Durabilidad**. Cuando la transacción termina el resultado de la misma perdura, y no se puede deshacer aunque falle el sistema.

Algunos sistemas proporcionan también **puntos de salvaguarda** (savepoints) que permiten descartar selectivamente partes de la transacción, justo antes de acometer el resto. Así, después de definir un punto como punto de salvaguarda, puede retrocederse al mismo. Entonces se descartan todos los cambios hechos por la transacción después del punto de salvaguarda, pero se mantienen todos los anteriores.

Originariamente, los puntos de salvaguarda fueron una aportación del estándar SQL99 de las Bases de Datos Objeto-Relacionales. Pero con el tiempo, se han ido incorporando también a muchas Bases de Datos Relaciones como MySQL (al menos cuando se utiliza la tecnología de almacenamiento InnoDB).

### 8.1. Transacciones en base de datos objeto-relacional

JDBC permite agrupar instrucciones SQL en una sola transacción. 
Por defecto el autocommit está a true. Se debe poner a false. 

```java
if (conn.getAutoCommit() )
          conn.setAutoCommit( false );
```

- Mediante un bloque try-catch controlar si se deshace conn.rollback o confirma conn.commit la transacción iniciada con esa conexión.

### 8.2. Transacciones en un gestor de objetos

Las transacciones en un sistema de objetos puro, se gestionan mediante COMMIT y `ROLLBACK` .

U**n fallo causa un rollback de los datos**, como normalmente sucede en las bases de datos relacionales. En cuanto a la concurrencia, las bases de objetos verifican en qué momento permiten el acceso en paralelo a los datos. Este acceso concurrente implica que más de una aplicación o hilo podrían estar leyendo o actualizando los mismos objetos a la vez. Esto se suele denominar **commit de dos fases** (dos procesos pueden trabajar sobre el mismo objeto concurrentemente). Para ello se utiliza normalmente bloqueo de datos para lecturas y escrituras.

**En Db4o**:

- Siempre se trabaja dentro de una transacción.
- Al abrir un ObjectContainer se crea e inicia implícitamente una transacción.
- Las transacciones se gestionan explícitamente mediante commit y `rollback`.
- La transacción actual hace commit implícitamente cuando se cierra el ObjectContainer.

## Estándar ODMG-93 u ODMG

El **estándar ODMG** (Object Database Management Group) trata de estandarizar conceptos fundamentales de los Sistemas Gestores de Bases de Datos Orientados a Objetos (SGBDOO) e intenta definir un **SGBDOO como un sistema que integra las capacidades de las bases de datos con las capacidades de los lenguajes de programación orientados a objetos**, de manera que los objetos de la base de datos aparezcan como objetos del lenguaje de programación.

Fué desarrollado entre los años 1993 y 1994 por representantes de un amplio conjunto de empresas relacionadas con el desarrollo de software y sistemas orientados a objetos.

1. **Arquitectura del estándar ODMG**
    
    La arquitectura propuesta por ODMG consta de:
    
    - Un **modelo de objetos** que permite que tanto los diseños, como las implementaciones, sean portables entre los sistemas que lo soportan.
    - Un **sistema de gestión** que soporta un lenguaje de bases de datos orientado a objetos, con una sintaxis similar a un lenguaje de programación también orientado a objetos.
    - Un **lenguaje de base de datos** que es especificado mediante:
        
        - Un Lenguaje de Definición de Objetos (ODL)
        - Un Lenguaje de Manipulación de Objetos (OML)
        - Un Lenguaje de Consulta (OQL)
        
        siendo todos ellos portables a otros sistemas con el fin de conseguir la portabilidad de la aplicación completa.
        
    - Enlaces con lenguajes Orientados a Objetos como C++, Java, Smaltalk.
    
    **El modelo de objeto ODMG** es el modelo de datos en el que están basados el ODL y el OQL. Este modelo de objeto proporciona los tipos de datos, los constructores de tipos y otros conceptos que pueden utilizarse en el ODL para especificar el esquema de la base de datos de objetos.
    
    Vamos a destacar algunas de las **características más relevantes** del estándar ODMG:
    
    - Las primitivas básicas de modelado son los **objetos** y los **literales**.
    - Un objeto tiene un **Identificador de Objeto** (OID) y un estado (valor actual) que puede cambiar y tener una estructura compleja. Un literal no tiene OID, pero si un valor actual, que es constante.
    - El estado está definido por los valores que el objeto toma para un conjunto de propiedades.Una propiedad puede ser:
        - Un atributo del objeto.
        - Una interrelación entre el objeto y otro u otros objetos.
    - Objetos y literales están organizados en **tipos**. Todos los objetos y literales de un mismo tipo tienen un comportamiento y estado común.
    - Un objeto queda descrito por cuatro características: identificador, nombre, tiempo de vida y estructura.
    - Los tipos de objetos se descomponen en atómicos, colecciones y tipos estructurados.
        - **Tipos atómicos** o básicos: constan de un único elemento o valor, como un entero.
        - **Tipos estructurados**: compuestos por un número fijo de elementos que pueden ser de distinto tipo, como por ejemplo una fecha.
        - **Tipos colección**: número variable de elementos del mismo tipo. Entre ellos:
            - Set: grupo desordenado de elementos y sin duplicados.
            - Bag: grupo desordenado de elementos que permite duplicados.
            - List: grupo ordenado de elementos que permite duplicados.
            - Array : grupo ordenado de elemntos que permite el acceso por posición.
    
    Algunos fabricantes sólo ofrecen vinculaciones de lenguajes específicos, sin ofrecer capacidades completas de ODL y OQL.