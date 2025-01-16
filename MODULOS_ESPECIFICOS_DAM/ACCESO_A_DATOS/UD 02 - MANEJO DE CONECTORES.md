
## 1. Introducción. El desfase objeto-relacional

**Conceptos**
- **Base de datos relacional**: Presenta información en tablas con filas y columnas
- Tabla o relación: Colección de objetos del mismo tipo (filas o tuplas)
- **Clave primaria**: Identifica de forma unívoca a cada fila de la misma
- **Sistema gestor de bases de datos (DBMS)**: Gestiona modo en que los datos se almacenan, mantienen y recuperan. En las relacionales es (RDBMS)
- **JDBC**: Java mediante (JDBC, Java Database Connectivity) permite simplificar el acceso a bases de datos relacionales, proporcionando un lenguaje mediante el cual las aplicaciones pueden comunicarse con los motores de bases de datos. Sun desarrolló esta API con tres objetivos en mente:
	- Ser **API Con soporte SQL**: Poder construir sentencias SQL e insertarlas en llamadas al API de Java
	- **Aprovechar experiencia de las APIs de bases de datos existentes**
	- Ser **lo más sencillo posible**

**Desfase objeto-relacional**
El **desfase objeto-relacional** o **impedancia objeto-relacional** es el conjunto de dificultades técnicas que surgen cuando una base de datos relacional se usa en conjunto con un programa escrito en PO. En definitiva, es la diferencia de aspectos que hay entre la POO y la BBDD en aspectos como:
- El lenguaje de programación. POO vs lenguaje de acceso a datos
- Tipos de datos. En una restricciones en los usos de tipos (BBDD), en la otra tipos de datos complejos (POO)
- Paradigma de programación: Durante el proceso de diseño y desarrollo de software debe hacerse traducción del modelo orientado a objetos e clases al modelo de entidad-relación. Uno maneja objetos y otro tablas y tuplas o filas. Deben diseñarse dos diagramas diferentes para el diseño de la aplicación.

El modelo relacional trata con relaciones y conjuntos por su naturaleza matemática. El modelo de POO trata con objetos y asociaciones entre ellos. Hay un problema en el momento de querer persistir los objetos de negocio. 

La escritura y lectura mediante JDBC implica:
- Abrir conexión
- Crear sentencia SQL
- Copiar todos los valores de las propiedades del objeto en la sentencia, ejecutarla y almacenar el objeto

Esto es fácil en caso simple pero complicado si el objeto posee muchas propiedades o si se necesita almacenar un objeto que a su vez posee una colección de otros elementos (mucho más código, creación de sentencias SQL es tediosa)

## 2. Protocolos de acceso a base de datos. Arquitectura JDBC

Sun Microsystems para desarrollar el JDBC buscó los aspectos de éxito de un API de este tipo como ODBC (Open Database Connectivity), desarrollado por Microsoft para tener un estándar de bases de datos en entorno Windows.

Aunque la industria aceptó ODBC como medio principal para acceso a BBDD en Windows, este no se introduce bien en el mundo Java debido a la complejidad que presenta ODBC.
JDBC quiere que sea tan sencillo como sea posible pero dando a los desarrolladores máxima flexibilidad. 

La **API JDBC** soporta dos modelos de procesamiento para acceder a base de datos: De dos y de tres capas. 
- **Modelo de dos capas**: La aplicación se comunica directamente a la fuente de datos. Necesita un conector JDBC que pueda comunicar con la fuente de datos específica a la que acceder. Los comandos se envían a la BBDD y los resultados se devuelven al usuario. La fuente de datos puede estar ubicada en otra máquina a la que el usuario se conecta por red (configuración cliente / servidor)

- **Modelo de tres capas**: Los comandos se envían a una capa intermedia de servicios que envía los comandos a la fuente de datos. Todo pasa por esa capa intermedia. 


**JDBC** se distribuye en dos paquetes:
- java.sql (J2SE)
- javax.sql (J2EE)

### 2.1. Conectores o Drivers

- **Conector o driver** es el conjunto de clases encargadas de implementar las interfaces de la API y de acceder a la base de datos.
- Para poder conectarse a una BBDD, la aplicación necesita tener un driver adecuado.
- El conector suele ser un fichero .jar que contiene una implementación de todas las interfaces del API JDBC
- Cuando se construye aplicación de BBDD, JDBC oculta lo específico de cada base de datos de forma que el desarrollador solo se ocupa de la aplicación.
- ** El conector es proporcionado por el fabricante de la base de datos**
- El código de la aplicación no depende del driver, ya que se trabajan los paquetes `java.sql` y `javax.sql`
- JDBC ofrece clases para: Establecer conexión a BBDD, Ejecutar consulta, Procesar resultados. 
- En principio, todos los conectores deben ser compatibles con ANSI SQL-2 Entry Level (ANSI SQL-2 se refiere a los estándares adoptados por el American National Standards Institute en 1992. Entry Level se refiere a una lista específica de capacidades de SQL.) Los desarrolladores de drivers pueden establecer que sus conectores conocen estos estándares.

![](ACCESO_A_DATOS/resources/ud02-1.png)

#### Conector de Tipo 1 (JDBC-ODBC Bridge)

Proporcionan un puente entre al API JDBC y el API ODBC. El driver JDBC-ODBC Bridge traduce las llamadas JDBC a ODBC y las envía a la fuente de datos JDBC.

Ventajas:
- No necesita driver específico de cada BBDD de tipo ODBC
- Soportado por muchos fabricantes, acceso a muchas BBDD
Inconvenientes:
- Hay plataformas que no lo tienen implementado
- Rendimiento no óptimo. La llamada JDBC se realiza a través del puente al conector ODBC y de ahí al interface de conectividad de la BBDD. El resultado recorre el camino inverso
- Se tiene que registrar manualmente en el gestor de ODBC, teniendo que configurar el DSN (Data Source Names, Nombres de fuentes de datos)

Este driver va incluido en el JDK.

#### Conector de Tipo 2 (API Nativa)

- Convierten llamadas JDBC a llamadas específicas de la BBDD para bases como SQL Server, Informix, Oracle, Sysbase.
- Se comunica directamente con el servidor de BBDD. Debe haber código en la máquina cliente.
Ventaja:
- Rendimiento mucho mejor que el conector 1.
Inconveniente:
- La librería de base de daros del vendedor necesita cargarse en cada máquina cliente. Los drivers tipo 2 no pueden usarse para Internet.

Tanto Driver de tipo 1 como Driver de Tipo 2 usan código nativo vía JNI (Java Native Interface), por lo que son más eficientes. 

(Oracle OCI Driver)

#### Conector de Tipo 3 (JDBC-Net pure Java driver)

**Aproximación de tres capas**. Las peticiones JDBC a la base de datos pasan a través de la red al servidor de capa intermedia (**middleware**). Este servidor traduce este protocolo independiente del sistema gestor a protocolo específico del sistema gestor y se envía a la BBDD. Los resultados llegan de vuelta al middleware y se enrutan al cliente.

Ventajas: 
- Útil para **aplicaciones en internet**.
- Este driver está basado en servidor, por lo que **no se necesita ninguna librería de base de datos en las máquinas clientes**.
- Un driver de tipo 3 **proporciona soporte para balanceo de carga,** funciones avanzadas de SysAdmin como auditoría...

#### Conector de Tipo 4 (Protocolo nativo)

- Son conectores que **convierten directamente las llamadas JDBC al protocolo de red usado por el SGBD**. Permite una llamada directa desde la máquina cliente al servidor del SGBD.
- Buena solución para acceso en **intranets**.
- **No es necesaria traducción adicional o capa middleware**. Mejor rendimiento que en tipos 1  2.
- **No necesita software especial** en cliente o en servidor.
- Enteramente escrito en Java. 

Inconveniente:
- El usuario necesita un **driver para cada base de datos.** 

En el caso concreto de Oracle, su _driver_ de tipo IV se denomina THIN. En el caso de MySQL Connector/J

```java
public class Ejemplo_conexion_oracle {
    public static void main(String[] args) {
        try {
            Class.forName("oracle.jdbc.driver.OracleDriver");
            Connection  conexion = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:SID","USER","PASS");
        } catch (SQLException | ClassNotFoundException ex) {
            System.out.println("Error en la conexión de la base de datos");
        }
         
    }
}
```

```java
```java
public class Ejemplo_conexion_oracle {
    public static void main(String[] args) {
        try {
            Class.forName("com.mysql.jdbc.Driver");
            Connection  conexion = DriverManager.getConnection("jdbc:mysql://localhost:3306/test","USER","PASS");
        } catch (SQLException | ClassNotFoundException ex) {
            System.out.println("Error en la conexión de la base de datos");
        }
         
    }
}
```

## 3. Conexión a base de datos

Establecer conexión base de datos en Java

```java
DriverManager.getConnection(String url, String user, String password);
```

Devuelve un objeto `Connection`que representa conexión con la base de datos.

`DriverManager` itera sobre la colección de drivers hasta reconocer la URL especificada. Si no encuentra conector adecuado se lanza `SQLException`

```java
Connection conexion = null;

try {
    // Registrar el controlador JDBC
    Class.forName("com.mysql.cj.jdbc.Driver");
            
    // Establecer conexión
	conexion = DriverManager.getConnection(URL, USUARIO, CONTRASEÑA);
} catch (SQLException e) {
    System.out.println("Error al conectar a la base de datos: " + e.getMessage());
} catch (ClassNotFoundException e) {
    System.out.println("Controlador JDBC no encontrado: " + e.getMessage());
} finally {
    // Cerrar la conexión al finalizar
    if (conexion != null) {
        try {
            conexion.close();
        } catch (SQLException e) {
            System.out.println("Error al cerrar la conexión: " + e.getMessage());
        }
    }
}
```

#### Conectarse a base de datos Access con Java

- Se **descargará** el **driver** `ucanaccess` y  se **añadirá** al **proyecto**.
- El **driver** se registrará con `Class.forName("net.ucanaccess.jdbc.UcanaccessDriver");`
- Y la **conexión** se obtendrá de forma similar a esta `conexion** = DriverManager.getConnection("jdbc:ucanaccess://src\\BaseDatos\\Proyecto.accdb");`

### 3.1. Instalar el conector

Debe haberse instalado el conector JDBC. Este es el que implementa la funcionalidad de las clases de acceso a datos y proporciona la comunicación entre la API JDBC y el SGBD. Se traducen los comandos del API JDBC al protocolo nativo del SGBD. 

Podría incluirse el jar o la dependencia en Maven:
```xml
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.27</version>
    </dependency>
```

### 3.2. Pool de conexiones

El proceso de abrir y cerrar una conexión puede ser lento y costoso en entornos en los que se necesita un acceso concurrente y masivo a una base de datos (entornos distribuidos, entornos web...). 

La versión 3.0 de JDBC proporciona un pool de conexiones que funciona de forma transparente. Al iniciar un servidor Java EE, automáticamente el pool de conexiones crea un número de conexiones físicas iniciales.

Cuando un objeto Java del servidor Java EE necesita una conexión a través del método `datasource.getConnection()`, la fuente de datos `javax.sqlDataSource` habla con el pool de conexiones y este le entrega una conexión lógica `java.sql.Connection` que es recibida por el objeto Java. 

Cuando el objeto Java del servidor Java EE quiere cerrar conexión a través de `connection.close()`, la fuente de datos le devuelve al pool de conexiones la conexión lógica en cuestión.

De forma transparente: Ante picos de demanda, el pool de conexiones crea más conexiones físicas. Ante disminuciones, elimina conexiones físicas de objetos de tipo `Connection`.


#### A. A partir del JNDI

(Java Naming and Directory Interface). API de Java para servicios de directorio.  suele usarse en entornos de servidor con recursos compartidos, servicios disponibles... Inicialmente hay un registro de objetos en el contexto de nombres JNDI durante la inicialización. Luego pueden ser recuperados y usados del `InitialContext` cuando sea necesario.

http://artemisa.unicauca.edu.co/~dabravo/jndi_esp_1/

Pool de conexiones transparente JNDI (entiendo que asociado a servidores de JavaEE):
```java
//Initial Context es el punto de entrada para
// comenzar a explorar un espacio de nombres.
javax.naming.Context ctx = new InitialContext();
dataSource = (DataSource) ctx.lookup("java:comp/env/jdbc/Basededatos");
```

Solicitando conexión lógica 
```java
connection = dataSource.getConnection();
```


------------

#### B. Realizado por el desarrollador

```xml
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-dbcp2</artifactId>
    <version>2.9.0</version> <!-- Versión actualizada -->
</dependency>
```

```java
import org.apache.commons.dbcp2.BasicDataSource;
import java.sql.Connection;
import java.sql.SQLException;

public class ConexionBD {
private static final BasicDataSource dataSource = new BasicDataSource();

    static {
        try {
            dataSource.setDriverClass("com.mysql.cj.jdbc.Driver");
            dataSource.setJdbcUrl("jdbc:mysql://localhost:3306/nombre_basedatos");
            dataSource.setUser("usuario");
            dataSource.setPassword("contraseña");
            
            // Configuración adicional (opcional)
            dataSource.setInitialPoolSize(5);
            dataSource.setMaxPoolSize(20);
            dataSource.setMinPoolSize(5);
            dataSource.setMaxIdleTime(300); // 5 minutos de tiempo máximo de inactividad para una conexión
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static Connection getConnection() throws SQLException {
        return dataSource.getConnection();
    }

    // Método para cerrar el DataSource
    public static void cerrarDataSource() {
        dataSource.close();
    }
}
```

```java
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class Ejemplo {
    public void ejemploConsulta() {
        try (Connection conexion = ConexionBD.getConnection();
             PreparedStatement statement = conexion.prepareStatement("SELECT * FROM tabla");
             ResultSet resultSet = statement.executeQuery()) {

            while (resultSet.next()) {
                // Procesar los resultados
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```


-----------

```
Cuando solicitas una conexión mediante `DriverManager`, estás obteniendo una conexión física a la base de datos. `DriverManager` establece una conexión directa con la base de datos utilizando el controlador JDBC correspondiente y te devuelve una instancia de `Connection`, que representa una conexión física activa con la base de datos.

Por otro lado, cuando solicitas una conexión mediante `DataSource`, generalmente estás obteniendo una conexión lógica o una referencia a una conexión física desde un pool de conexiones. Los `DataSource` administran un pool de conexiones que están previamente establecidas y listas para su uso. Cuando solicitas una conexión a través de un `DataSource`, este te devuelve una conexión que ya está establecida y lista para ser utilizada. Esto significa que la conexión puede ser física, pero ha sido previamente creada y está siendo reutilizada desde el pool de conexiones, en lugar de ser creada directamente en ese momento.
```
## 4. Creación de base de datos

La BBDD  podría crearse usando las herramientas proporcionadas por el fabricante de la base de datos o ejecutando las sentencias DDL desde un programa en Java. Usualmente lo hará el administrador de bases de datos a través de las herramientas que proporciona el sistema gestor.

**No todos los conectores JDBC soportan creación de bases de datos mediante DDL**. La sentencia `CREATE DATABASE` no es parte del estándar SQL, depende del SGBD. 

Por JDBC uno puede conectarse, manipular: crear, modificar, borrar, añadir datos en tablas. Pero la creación de la base de datos mejor hacerlo con la herramienta específica para ello. 

```java
		// Paso 1: Cargar el controlador JDBC
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
            return;
        }

        try (
            // Paso 2: Establecer la conexión
            Connection conn = DriverManager.getConnection(url, user, password);
            Statement stmt = conn.createStatement();
        ) {
            // Paso 3: Crear la base de datos
            String sql = "CREATE DATABASE PATATA";
            stmt.executeUpdate(sql);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
```

## 5. Operaciones: ejecución de consultas

La aplicación debe:
1. **Cargar** el driver necesario para comprender el protocolo que usa la BBDD
2. **Establecer** una conexión con BBDD
3. **Enviar** consultas SQL y procesar el resultado
4. **Liberar** recursos al terminar
5. **Gestionar** errores que se puedan producir

Se usa:
`Statement`: Sentencias sencillas en SQL
`PreparedStatement`: Consultas preparadas como las que tienen parámetros
`CallableStatement`: Ejecutar procedimientos almacenados en base de datos.

```java
// Statement
try (Connection conexion = ConexionBD.getConnection();
    Statement statement = conexion.createStatement()) {

String sql = "SELECT * FROM tabla";
ResultSet resultSet = statement.executeQuery(sql);

while (resultSet.next()) {
                // Procesar los resultados
    }
} catch (SQLException e) {
    e.printStackTrace();
}

// PreparedStatement
try (Connection conexion = ConexionBD.getConnection();
    PreparedStatement statement = conexion.prepareStatement("SELECT * FROM tabla WHERE id = ?")) {

	statement.setInt(1, id);
	ResultSet resultSet = statement.executeQuery();
	
	while (resultSet.next()) {
	        // Procesar los resultados
	}
} catch (SQLException e) {
    e.printStackTrace();
}

// CallableStatement
try (Connection conexion = ConexionBD.getConnection();
    CallableStatement statement = conexion.prepareCall("{call nombre_procedimiento(?, ?)}")) {
	//Parametro de entrada
    statement.setInt(1, 123);
    //Parametro de salida
    statement.registerOutParameter(2, java.sql.Types.INTEGER);
    statement.execute();

    int resultado = statement.getInt(2); // Obtener el valor del parámetro de salida
            // Procesar el resultado
} catch (SQLException e) {
    e.printStackTrace();
}
```


Tenemos:
- Consultas: `SELECT` -> `executeQuery()` (Retornará un `ResultSet`)
- Actualizaciones: `INSERT`, `UPDATE`, `DELETE`, sentencias DDL -> `executeUpdate()` (Retornará un entero con las filas afectadas)
- Para cualquier SQL: `execute()` . Lo que hace es retornar `true` si el primer resuletado es `ResultSet` y en caso contrario `false.`

### 5.1. Consultas con MR-Access

1. Con **JDK7** y anteriores: En un primer caso utilizaremos un acceso mediante puente JDBC-ODBC. Dicho puente da acceso a bases de datos ODBC, pero no está soportado en JDK8 y **sólo funciona para Windows**.  Este driver está incorporado dentro de la distribución de Java, por lo que no es necesario incorporarlo explícitamente en el classpath.
2. Con **JDK8** y posteriores: Un segundo caso será usando UCanAccess un driver JDBC **puro** Java (multiplataforma) para acceder a bases de datos Access ( ficheros .mdb y .accdb) sin necesidad de ODBC. Será necesario instalar las librerías de UcanAccess.
#### Puente JDBC-ODBC, Conector Tipo 1 (Windows - No soportado Java 8)

- **Definir fuente de datos JDBC**. Windows. Programa de definición de fuente de datos ODBC puede estar en el Panel de control > Herramientas administrativas > Orígenes de datos ODBC. En la pestñaa DSN de usuario se encuentran los ODBC instalados en el sistema. 

- **Instalar driver JDBC**. Las clases e interfaces para trabajar con BBDD relacional las establece el API JDBC. Algunas clases están parcialmente diferidas, otras sin implementar. Cada sistema gestor debe responsabilizarse de implementar las clases que dan acceso a BBDD. Cada tipo de BBDD se trabaja con conjunto diferente de class (driver JDBC).
Cargar (registrar) el driver: `Class.forName("jdbc:odbc:admdb")`
Realizar conexión a BBDD: `Connection con = DriverManager.getConnection("jdbc:odbc:admdb");`

#### Driver JDBC puro, Conector Tipo 3 (Multiplataforma - Soportado Java 8)

- Añadir UCanAccess (driver JDBC Java puro para escribir y leer en bases de datos Access sin necesidad de ODBC). Necesita Jackcess y HSQLDB. 
- Listo!
```java
Connection conn=DriverManager.getConnection("jdbc:ucanaccess://farmacia.mdb");

// O con el fichero en una carpeta relativa al proyecto...
Connection conn=DriverManager.getConnection("jdbc:ucanaccess://Carpeta/farmacia.mdb");
```

### 5.2. Ejemplo

Las consultas realizadas a BBDD usan `Statement` y `PreparedStatement`.  Creados a partir de una conexión.

```java
Statement stmt = connection.createStatement();
```

La clase `Statement` tiene los métodos `executeQuery` y `executeUpdate` para consultas y actualizaciones respectivamente. Ambos métodos soportan consultas en SQL-92. 

`executeUpdate` retorna número de registros insertados, actualizados o eliminados. 

`executeQuery` devuelve objeto `ResultSet` para recorrer el resultado de la consulta usando un cursor. 

Decir cuál de los dos puede servir para consultas DDL o para consultas de tipo Insert, Update, Delete → **executeUpdate**. 
**ExecuteQuery** solo sirve para SELECT.

```java
stmt.executeUpdate("CREATE TABLE Clientes "
 + "(DNI char(9) NOT NULL, "
 + "nombre varchar(20), "
 + "apellidos varchar(40), "
 + "direccion char(30), "
 + "email char(30),"
 + "telefono char(10),"
 + "PRIMARY KEY(DNI))");
```

### El `ResultSet` y sus curiosidades...

Con el `ResultSet` podemos navegar de un resultado al siguiente. 

-------------------------

Con el método `next()` avanza el cursor. Para obtener columna del registro se usan métodos `get...()`. 

El cursor tiene método `wasNull()` que permite informar si el último valor leído con `get()` es nulo.

```sql
try (Connection connection = ConexionBD.getConnection();
    Statement statement = connection.getStatement()) {

	var query = "SELECT nombre FROM pacientes";
	try (ResultSet rs = statement.executeQuery(query)) {
	if (rs.next() {
		do {
			String usuario = rs.getString("nombre");
			System.out.println(usuario);
		} while (rs.next());
	}
} catch (SQLException e) {
		e.printStackTrace();
}
```


-------------
##### Movimientos del cursor

Hay una fila virtual antes del primer resultado y una fila después del último resultado.
El primer `rs.next()` se usa para saltar a la primera. (Sea con if y do-while o sea con while).

Por defecto, los `ResultSets` solo pueden ir hacia adelante. (`TYPE.FORWARD.ONLY`)

Se pueden establecer de forma diferente con el primer parámetro deñ constructor como:
**TYPE_SCROLL_INSENSITIVE**: Capta el momento inicial pero no será sensible a los cambios. 

```java
`connection.createStatement(ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.CONCUR_READ_ONLY)`. 
```

**TYPE_SCROLL_SENSITIVE**: Se de cuenta de los cambios que se producen en el `ResultSet`

```java
connection.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_READ_ONLY)
```


Pueden usarse métodos como `absolute(int)` o `relative(int)`, `afterLast()`, `beforeFirst()` para posicionar el cursor...
Ojo, `beforeFirst` y `afterLast`  nos permiten tocar esas filas virtuales que mencionamos.
`rs.previous()` para moverse en otro sentido....

------------
##### Actualizar el cursor

Debe indicarse el sistema de concurrencia que se debe usar.
Por defecto es `ResultSet.CONCUR_READ_ONLY` (No permite actualizar)
Pero puede ponerse para modificar datos con `ResultSet.UPDATABLE`

 **Modificar filas**

```java
rs.updateBoolean(String columnLabel, boolean newValue);
rs.updateInt("precio", rs.getInt("precio") + 1);
rs.updateString("nombre" , "Alfonso");
rs.updateRow(); // Hace efectiva las modificaciones
```

 **Borrar filas**
```java
rs.deleteRow(); // Borra una fila. Lo correcto y mas seguro es tener en el ResultSet el registro que se quiere borrar. (en lugar de hacer un ResultSet grandisimo y un if)
```

**Insertar filas**

```java
rs.moveToInsertRow(); // Vamos a una fila virtual que permite insertar fila
rs.updateInt("paciente_id", 1);
rs.updateBoolean("confirmado", true);
rs.updateObject("fecha_cita", new Date());
rs.updateTimestampt("fecha_cita", Timestamp.valueOf(new Date()));
rs.updateString("nombre", "Aniceto");
rs.insertRow();
```

Fíjate que al estar en `ResultSet.TYPE_SCROLL_SENSITIVE` podría verse este nuevo resultado al ir a `rs.last()`
### 5.3. Consultas preparadas

Las consultas preparadas se representan con `PreparedStatement`. Son consultas precompiladas, más eficientes y con posibilidad de tener parámetros. Tendrán mucho mejor rendimiento consultas que se realicen frecuentemente. 

El parámetro se indica con el carácter `?`. Se establecen con `set...` dando la posición del parámetro en la consulta y el valor. 

Finalmente se ejecuta con `executeQuery()` o `executeUpdate()`, según la consulta. 

```java
PreparedStatement pstmt = con.preparedStatement("SELECT * from medicamentos");
PreparedStatement pstmt = con.preparedStatement("SELECT * from medicamentos WHERE codigo = ? ");
pstmt.setString(1, "712786");
ResultSet rs = pstmt.executeQuery();
```
## 6. Ejecución de procedimientos almacenados 

Es un procedimiento o subprograma almacenado en BBDD. Pueden ser:
- Procedimientos almacenados
- funciones que devuelven un valor que puede  usarse en otras sentencias SQL.
Un procedimiento almacenado típico tiene:
- Nombre
- Lista de parámetros
- Sentencias SQL.

Supón que tenemos este procedimiento en Oracle

```sql
CREATE OR REPLACE PROCEDURE obtener_empleados (
    departamento_id IN NUMBER,
    empleados OUT SYS_REFCURSOR
) AS
BEGIN
    OPEN empleados FOR
    SELECT * FROM empleados WHERE dept_id = departamento_id;
END obtener_empleados;
```

Y en Java:
```java
import java.sql.CallableStatement;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;

public class Main {
    public static void main(String[] args) {
        String url = "jdbc:oracle:thin:@//localhost:1521/XE"; // URL de conexión a la base de datos
        String user = "tu_usuario"; // Nombre de usuario de la base de datos
        String password = "tu_contraseña"; // Contraseña de la base de datos

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            // Llamada al procedimiento almacenado
            CallableStatement cstmt = conn.prepareCall("{call obtener_empleados(?, ?)}");

            // Establecer parámetros de entrada
            cstmt.setInt(1, 10); // Departamento ID
            // Registrar el parámetro de salida (cursor)
            cstmt.registerOutParameter(2, OracleTypes.CURSOR);
            // Ejecutar la llamada al procedimiento almacenado
            cstmt.execute();
            // Obtener el resultado del cursor
            ResultSet rs = (ResultSet) cstmt.getObject(2);
            // Procesar los resultados
            while (rs.next()) {
                System.out.println("ID: " + rs.getInt("id") + ", Nombre: " + rs.getString("nombre"));
            }

            // Cerrar recursos
            rs.close();
            cstmt.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## 7. Transacciones

Para consultas SQL que deben ejecutarse en conjunto, puede asegurarse que no se quedarán a medio camino con el uso de **transacciones**. (O todo o nada)

Se garantiza así: **Atomicidad, consistencia, aislamiento y durabilidad (ACID)**.

### 7.1. Commit y Rollback


Tras las operaciones se realiza el commit, y si ocurre una excepción, al capturarla realizaríamos el rollback.

```sql
BEGIN
…
SET AUTOCOMMIT OFF
update cuenta set saldo=saldo + 250 where dni=”12345678-L”;
update cuenta set saldo=saldo - 250 where dni=”89009999-L”;
COMMIT;
…
EXCEPTION
   WHEN OTHERS THEN
      ROLLBACK ;
END;
```

Es conveniente planificar bien la aplicación para minimizar el tiempo en el que se tengan transacciones abiertas ejecutándose, ya que consumen recursos y suponen bloqueos en la base de datos que puede parar otras transacciones. En muchos casos, un diseño cuidadoso puede evitar usos innecesarios que se salgan fuera del modo estándar AutoCommit.

----

###### Autocommit en JDBC:

Por defecto, la propiedad autocommit de un objeto Connection está establecida en true, lo que significa que cada sentencia SQL se ejecuta como una transacción independiente y se confirma automáticamente después de ejecutarse. Sin embargo, puede desactivarse el autocommit y controlar manualmente las transacciones.

```java
conn.setAutoCommit(false);
```


```java
public class Main {
    public static void main(String[] args) {
        String url = "jdbc:oracle:thin:@//localhost:1521/XE";
        String user = "tu_usuario";
        String password = "tu_contraseña";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            conn.setAutoCommit(false);

            // Ejecutar varias sentencias SQL dentro de la transacción
            Statement stmt = conn.createStatement();
            stmt.executeUpdate("INSERT INTO tabla (columna1, columna2) VALUES ('valor1', 'valor2')");
            stmt.executeUpdate("UPDATE tabla SET columna3 = 'nuevo_valor' WHERE columna1 = 'valor1'");
            
            // Confirmar la transacción
            conn.commit();
            System.out.println("Transacción completada.");

        } catch (SQLException e) {
            // Manejar la excepción
            e.printStackTrace();
            
            // Revertir la transacción en caso de error
            try {
                conn.rollback();
                System.out.println("Transacción revertida.");
            } catch (SQLException ex) {
                ex.printStackTrace();
            }
        }
    }
}
```
## 8. Excepciones y cierre de conexiones

 Las conexiones con una base de datos consumen muchos recursos en el sistema gestor. Por ello, conviene cerrarlas con el método close siempre que vayan a dejar de ser utilizadas, en lugar de esperar a que el recolector de basura de Java las elimine.
También conviene cerrar las consultas (`Statement` y `PreparedStatement`) y los resultados (`ResultSet`) para liberar los recursos.
Una excepción es una situación que no se puede resolver y que provoca la detención del programa de manera abrupta. Se produce por una condición de error en tiempo de ejecución.

```java
Connection conn = null;
try {
    conn = DriverManager.getConnection(url, user, password);
    // Realizar operaciones con la conexión
} catch (SQLException e) {
    // Manejar la excepción
    e.printStackTrace();
} finally {
    try {
        if (conn != null) {
            conn.close();
        }
    } catch (SQLException e) {
        e.printStackTrace();
    }
}
```

```sql
Connection conn = null;
Statement stmt = null;
try {
    conn = DriverManager.getConnection(url, user, password);
    stmt = conn.createStatement();
    // Realizar operaciones con la conexión y el Statement
} catch (SQLException e) {
    // Manejar la excepción
    e.printStackTrace();
} finally {
    try {
        if (stmt != null) {
            stmt.close();
        }
    } catch (SQLException e) {
        e.printStackTrace();
    }
    try {
        if (conn != null) {
            conn.close();
        }
    } catch (SQLException e) {
        e.printStackTrace();
    }
}
```

```java
try (Connection conn = DriverManager.getConnection(url, user, password);
     Statement stmt = conn.createStatement()) {
    // Realizar operaciones con la conexión y el Statement
} catch (SQLException e) {
    // Manejar la excepción
    e.printStackTrace();
}
```

