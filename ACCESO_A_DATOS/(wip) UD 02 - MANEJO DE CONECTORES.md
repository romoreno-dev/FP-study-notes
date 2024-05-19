
## 1. Introducción. El desfase objeto-relacional

## 2. Protocolos de acceso a base de datos. Arquitectura JDBC

### 2.1. Conectores o Drivers

#### De tipo 1 y Tipo 2

#### De Tipo 3 y Tipo 4

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
#### Puente JDBC-ODBC (Windows - No soportado Java 8)

#### Driver JDBC (Multiplataforma - Soportado Java 8)

### 5.2. Ejemplo

### 5.3. Consultas preparadas

## 6. Ejecución de procedimientos almacenados en Base de Datos

### 6.1. Procedimientos almacenados en MySQL

## 7. Transacciones

### 7.1. Commit y Rollback

## 8. Excepciones y cierre de conexiones

### 8.1. Excepciones


### 8.2. Cierre de conexiones



