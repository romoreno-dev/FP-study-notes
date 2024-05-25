
## 1. Concepto de mapeo objeto-relacional

**Desfase objeto-relacional** (Impedancia objeto-relacional). La incompatibilidad de sistemas de tipos de datos es un problema a la hora de almacenar los datos de un programa orientado a objetos (clases y objetos) en una base de datos relacional (RDBMS, tablas y restricciones).   

El **mapeo objeto-relacional** (Object Relational Mapping, ORM) es una técnica de programación para convertir datos entre un lenguaje POO y una base de datos relacional gracias a la persistencia. Pueden usarse características de la POO como herencia y polimorfismo. 
En definitiva, el ORM convierte datos en registros y viceversa. 

## 2. Herramientas ORM. Características y herramientas más utilizadas

### 2.1. Características

Las herramientas ORM facilitan mapeo de atributos entre la BBDD y el modelo de objetos. Puede hacerse mediante archivos declarativos (XML) o mediante anotaciones en POJOs, definiendo la correspondencia una sola vez (propiedad con cada columna, clase con cada tabla). 
Puede conectarse con la BBDD relacional para extraer la información contenida en objetos. 

**Ventajas**
- **Reducir tiempo de desarrollo **de software. Puede crearse el modelo a partir del esquema de la base de datos
- **Abstracción** de la base de datos
- **Reutilización**
- **Persistir** objetos a través de un método ORM `save`y generar el SQL correspondiente
- **Recuperar los objetos **a través de un método ORM `load`
- **Lenguaje propio** para realizar consultas
- Incentiva la **portabilidad** y la **escalabilidad**

**Inconvenientes**
- Debe **emplearse tiempo** en su aprendizaje
- **Menor rendimiento** debido al tiempo de transformación (lenguaje propio, leer registros, crear objetos)
- **Sistemas complejos relacionales son difíciles** de representar
### 2.2. Herramientas ORM más usadas


![](resources/ud03-1.png)

Citemos inicialmente:

- Java => Hibernate, iBatis, Ebean, etc..
- .NET=> Entity Framework, nHibernate, etc..
- PHP=> Doctrine, Propel, ROcks, Torpor, etc..

**Hibernate**: Framework de persistencia. Herramienta de mapeo para plataforma Java (disponible para .NET con NHibernate) que facilita el mapeo de atributos. Es software libre, distribuido con licencia GNU LGPL. Posee lenguaje de consulta HQL. Tiene plugins para agilizar el trabajo. Puede adaptarse a una BBDD ya existente. 

**Java Persistence API**: Especificación de Sun Microsystems para la persistencia de objetos Java a cualquier base de datos relacional. Desarrollada para Java EE e incluida en el estándar **EJB 3.0**. (Java Specification Request JSR 220). Se requiere Java 5 o superior al usar anotaciones, genéricos...

**Open JPA**: API de persistencia. Framwork usando sus ediciones Java SE y Java EE. 

**iBatis**: Framework de persistencia. Desarrollado pro Apache Software Foundation. Es de código libre. Sigue el mismo esquema de Hibernate: Ficheros de mapeo XML para persistir información contenida en objetos en un repositorio relacional.

## 3. Instalación y configuración de Hibernate

**Netbeans y prehistoria**

La herramienta Hibernate se encuentra como un plugin de este entorno de desarrollo. 
Para utilizarlo, debe configurarse mediante el fichero `Hibernate.cfg.xml` tiene información sobre la conexión a la BBDD y otras propiedades. 

Netbeans tiene como plugin  la BBDD Sakila como muestra gratuita disponible.

**En un tiempo actual**

1. **Crear proyecto de Maven**
```shell
mvn archetype:generate -DgroupId=com.ejemplo -DartifactId=MiProyecto -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

2. Añade **dependencia de Hibernate y del Connector-J de MySql (o de Oracle)** en el pom:
```xml
<dependencies>
    <!-- Hibernate Core -->
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate-core</artifactId>
        <version>5.6.6.Final</version>
    </dependency>

<!-- MySQL -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.28</version>
    </dependency>

<!-- Oracle -->
    <groupId>com.oracle.database.jdbc</groupId>
    <artifactId>ojdbc8</artifactId>
    <version>19.3.0.0</version>
</dependency>
</dependencies>

```


3. Configurar el fichero de configuración.


Aquí debe diferenciarse entre si va a usarse la especificación de JPA  o la implementación de Hibernate.

##### Hibernate

Se debe crear el fichero  **hibernate.cfg.xml** en el directorio **src/main/resources**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
        <!-- Configuración de la conexión a la base de datos -->
        <property name="hibernate.connection.driver_class">com.mysql.cj.jdbc.Driver</property>
        <property name="hibernate.connection.url">jdbc:mysql://localhost:3306/pruebas_roberto</property>
        <property name="hibernate.connection.username">root</property>
        <property name="hibernate.connection.password">root</property>

        <!-- En principio, opcional: Configuración de dialecto para MySQL-->
        <property name="hibernate.dialect">org.hibernate.dialect.MySQL5Dialect</property>

        <!-- Opcional: Configuración de show SQL (Para ver las consultas) -->
        <property name="hibernate.show_sql">true</property>

		<!-- Se elimina la tabla y se crea (basandose en las entidades, al iniciar la aplicacion) -->
        <property name="hibernate.hbm2ddl.auto">create-drop</property>

		<!-- Declaracion de las clases de mapeo empleadas -->
        <mapping class="org.example.model.Usuario"/>

		<!-- En lugar de buscar el fichero import.sql, buscara en src/main/resources el indicado aqui para ejecutar el script sql que aparezca -->
	        <property name="hibernate.hbm2ddl.import_files">mi-script.sql</property>
	
    </session-factory>
</hibernate-configuration>
```

A la hora de recrear tabla, las opciones de **hibernate.hbm2ddl.auto** son : 
- `create`: Crea. Si ya hay producirá error.
- `drop-create`: Elimina lo que hay. Y lo crea.
- `update`: Trata de actualizar si la tabla existe. No es adecuada para cambios estructurales complejos
- `validate`: Valida que el esquema esté correcto. 

Por defecto, Hibernate en los casos en los que se le permite crear buscará en src/main/resources el fichero import.sql. Con  **hibernate.hdm2ddl.auto** puede indicársele otro. 

4. Clase que obtenga el `SessionFactory` de `Configuration`
```java
public class HibernateUtil {
    private static final SessionFactory sessionFactory = buildSessionFactory();

    private static SessionFactory buildSessionFactory() {
        try {
            // Cargar la configuración desde el archivo nada.xml
            return new Configuration().configure().buildSessionFactory();
        } catch (Throwable ex) {
            System.err.println("Error al inicializar el SessionFactory: " + ex);
            throw new ExceptionInInitializerError(ex);
        }
    }

    public static SessionFactory getSessionFactory() {
        return sessionFactory;
    }

}
```

5. Realizar la query obteniendo el `Session`  el `Transaction`, lo que se necesite...

```java
    public static void main(String[] args) {  
  
        Session session = HibernateUtil.getSessionFactory().openSession();  

            // Las transacciones son asi...
            //Transaction transaction = session.beginTransaction();
           // session.getTransacion().commit();
           // session.getTransaction().rollback();
        try {  
            // Crear la consulta  
            Query query = session.createQuery("SELECT u FROM Usuario u");  

  
            // Ejecutar la consulta y obtener los resultados  
            List<Usuario> resultados = query.getResultList();  
  
            System.out.println("Lista usuarios");  
            resultados.forEach(v -> System.out.println(v));  
  
        } finally {  
            session.close();  
            HibernateUtil.getSessionFactory().close();
        }  
    }
```

Es posible mapear las clases programáticamente tal que así...
```java
        Configuration configuration = new Configuration()  
                .configure("nada.xml")  
                .addAnnotatedClass(Usuario.class);
```

##### JPA

En src/main/resources/META-INF/persistence.xml: 

Se debe indicar un elemento `<persitence-unit>` 
- Dentro se le le indica el `provider` (la clase que proveerá de la implementación JPA y que podría ser... `oracle.toplink.essentials.PersistenceProvider` (Toplink Essentials), `org.eclipse.persistence.jpa.PersistenceProvider` (EclipseLink), `org.hibernate.jpa.HibernatePersistenceProvider` (Hibernate))

- Se declaran las propiedades de conexión de la base de datos en `<properties>`. Aunque también prescinde de esto en el caso de que sele indique el nombre del JNDI del pool, indicando si este es JTA o no  `<jta-data-source>`, `<non-jta-data-source>`

	Este parámetro en el contexto de Java EE indica si Java Transaction API gestiona los recursos transaccionales, asegurando la seguridad de estas  (lo que suelen ofrecer servidores de aplicaciones como Widlfly) o si, por el contrario, las transacciones se gestionan de forma local. (que es lo que solemos hacer cuando manualmente efectuamos `commit` y `rollback`). Intentar hacer `commit` en una transacción cuyo pool de conexiones es JTA se traducirá en excepciones que avisan de que no es posible hacer "commit" manualmente con "autocommit set" 

- Se puede indicar que se muestren las consultas SQL por la consola `hibernate.show_sql`
- Similar a lo comentado arriba se puede elegir respecto a reejecución del DDL de las clases mapeadas sobre la base de datos al iniciar la apicación o elegir el script que por defecto se debe ejecutar `jakarta.persistence.schema-generation.database.action`, `jakarta.persistence.sql-load-script-source`

- Se indican las clases mapeadas con `<class>org.example.miClass</class>`. Se puede dar cierta restricción a la detección de clases  o no, con `<exclude-unlisted-classes>true</exclude-unlisted-classes>`. En caso de que esté a true, deben indicarse o no las detectará. (Por defecto está a false).


```xml
<?xml version="1.0" encoding="UTF-8" ?>
<persistence xmlns="https://jakarta.ee/xml/ns/persistence" version="3.0">
    <persistence-unit name="miBBDD" transaction-type="RESOURCE_LOCAL">
        <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>
        <properties>
            <property name="jakarta.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/pruebas_roberto"/>
            <property name="jakarta.persistence.jdbc.user" value="root"/>
            <property name="jakarta.persistence.jdbc.password" value="root"/>
            <!-- Opcionales -->
            <!--            <property name="jakarta.persistence.jdbc.driver" value="com.mysql.jdbc.Driver"/>-->
            <!--            <property name="hibernate.dialect" value="org.hibernate.dialect.MySQL8Dialect"/>-->
            <!-- Para mostrar las consultas a la base de datos -->
            <property name="hibernate.show_sql" value="true"/>
            <property name="jakarta.persistence.schema-generation.database.action" value="drop-and-create"/>
            <property name="jakarta.persistence.sql-load-script-source" value="mi-script.sql"/>

        </properties>
    </persistence-unit>
</persistence>
```

4. Clase que obtenga el `EntityManagerFactory` de `Persistence`
```java
public class JpaUtils {  
  
        private static final String PERSISTENCE_UNIT_NAME = "miBBDD";  
        private static EntityManagerFactory entityManagerFactory;  
  
        static {  
            try {  
                // Crear el EntityManagerFactory  
                entityManagerFactory = Persistence.createEntityManagerFactory(PERSISTENCE_UNIT_NAME);  
            } catch (Throwable ex) {  
                // Manejar cualquier error de inicialización  
                System.err.println("Error al inicializar EntityManagerFactory: " + ex);  
                throw new ExceptionInInitializerError(ex);  
            }  
        }  
  
        // Método para obtener el EntityManagerFactory  
        public static EntityManagerFactory getEntityManagerFactory() {  
            return entityManagerFactory;  
        }  
  
        // Método para obtener un EntityManager  
        public static EntityManager getEntityManager() {  
            return entityManagerFactory.createEntityManager();  
        }  
}
```

5. Realizar la query obteniendo el `EntityManager`  el `EntityTransaction`, lo que se necesite...

```java
public static void main(String[] args) {  
    EntityManagerFactory entityManagerFactory = JpaUtils.getEntityManagerFactory();  
    EntityManager entityManager = JpaUtils.getEntityManager();  
  
    try {  
            Query query = entityManager.createQuery("SELECT u FROM Usuario u");  
  
            // Ejecutar la consulta y obtener los resultados  
            List<Usuario> resultados = query.getResultList();  
  
            System.out.println("Lista usuarios");  
            resultados.forEach(v -> System.out.println(v));  
    } catch (Exception e) {  
  
    } finally {  
        // Cerrar el EntityManager  
        entityManager.close();  
  
        // Cerrar el EntityManagerFactory  
        entityManagerFactory.close();  
    }
```

## 4. Hibernate: Ficheros de configuración y mapeo. Estructura y propiedades

### 4.1. Ficheros de configuración. Propiedades


Ya se ha comentado que el archivo de configuración de Hibernate es `Hibernate.cfg.xml`. Tiene información sobre conexión de base de datos, asignaciones de recursos y otras propiedades. 

Las más conocidas según estos apuntes serían:

- **hibernate.dialect**: Dialecto o lenguaje empleado. Por ejemplo, MySQL.
- **hibernate.connection.driver_class**. Driver utilizado para la conexión con la base de datos.
- **hibernate.connection.url**. Dirección de la base de datos con la que se va a conectar Hibernate.
- **hibernate.connection.username**. Nombre del usuario que va a realizar la extracción de información. Por defecto, el nombre de usuario es root.
- **hibernate.connection.password**. Contraseña
- **hibernate.show_sql**. Para mostrar la herramienta. Por defecto, su valor es true.
### 4.2. Ficheros de mapeo. Estructura, elementos y propiedades 

Parece ser que hace siglos también se hacía mapeo por xml y no por anotaciones. En ese momento se hacian con los ficheros con el mismo nombre de la clase y extensión `.hbm.xml`.

Puede utilizarse la ingeniería inversa para crear archivos de mapeo basados en tablas de la base de datos que seleccionemos. El archivo de ingeniería inversa es `Hibernate.reveng.xml`. Se trata de un archivo XML que se puede utilizar para modificar la configuración predeterminada de Hibernate.cfg.xml con el propósito de especificar explícitamente el esquema de base de datos que se va a utilizar, filtrar las tablas que no deseamos recuperar y especificar cómo se asignan los tipos JDBC a los tipos de Hibernate.

## 5. Mapeo de colecciones, relaciones y herencia

1. **Mapeo de colecciones**: El elemento mapea la columna clave de la colección. Todos los mapeos de colección necesitan columna índice en la tabla de colección: una columna índice es una columna que mapea a un índice de array o índice de list. Una colección de valores muchos-a-muchos necesita una tabla de colección dedicada con una columna o columnas de clave foránea, columna de elemento colección y, probablemente, varias columnas índice.

2. **Mapeo de relaciones**: Para persistir, las relaciones usan transacciones. Se respeta el tipo de relación en el modelo de objetos y en el modelo relacional. Para mapear las relaciones se usan identificadores de objetos OID. La llave primaria de la tabla relacionada y se agregan como una columna más en la tabla donde se quiere establecer la relación. Dicha columna es foránea a la tabla con la que está relacionada.

3. **Mapeo de herencia**: Se puede modelar la jerarquía a una sola tabla, modelar la jerarquía completa en tablas, mapear cada tabla en tablas concretas. Según el rendimiento y escalabilidad del modelo.

## 6. Clases persistentes

La **persistencia** es la capacidad de los objetos para guardarse y recuperarse desde un medio de almacenamiento. Las clases persistentes son clases en una aplicación que sirven para representar las entidades de la base de datos. 

>El estándar Java Data Objects (JDO) define una clase con capacidad de persistencia como aquella que implementa la interfaz `javax.jdo.PersistenceCapable`. 
Las clases persistentes tienen la capacidad de definir objetos que pueden almacenarse y recuperarse y un almacén persistente de datos. La especificación JDO incorpora la figura del procesador de clases en código ejecutable Java, JDO Enhacer, que es un programa que modifica los archivos compilados de las clases, añadiendo el código ejecutable necesario para realizar la grabación y recuperación transparente de los atributos de las instancias persistentes.
>
>JDO permite a los programadores y programadoras convertir sus clases en persistentes, de forma que los objetos pertenecientes a clases concretas definidas por el programador pueden mantener su estado, con la única limitación de que el estado esté compuesto por los atributos persistentes que sean independientes del contexto de ejecución: tipos primitivos, tipos de referencia e interfaz y algunas clases del sistema que permiten modelar el estado como por ejemplo la clase Array, Date, etc.
>
>Para poder indicar las clases y atributos que son persistentes, se utiliza un fichero de configuración XML, que se denomina descriptor de persistencia.. Para que las instancias de las clases persistentes pueden mantenerse en los sistemas gestores de bases de datos, es necesario establecer la correspondencia entre los objetos y su estado persistente.

No todas las instancias de una clase persistente deben tener capacidad de persistence.
Puede ser
- **Transitorio (transient)**: No asociada a `EntityManager` o `Session` y tampoco en base de datos. Pueden ser instancias recién creadas que no han sido enlazadas con el gestor de persistencia. No se reflejarán en BBDD hasta no convertirse en persistentes (`persist()`, `merge()`, ...)
- **Persistence (managed, gestionada)**: Asociada a un `Session` o `EntityManager` activo y gestionada por JPA. Cuando una entidad está managed, cualquier cambio en su estado resultará en una actualización de la base de datos en el momento del commit cuando se haga commit de la transacción
- **Disociado (detached, no gestionada)**: Instancia persistente que sigue en memoria después de que termine la sesión. Probablemente está  en la base de datos pero el EntityManager desconoce,  ya no está asociada. Puede ocurrir cuando se cierra el `EntityManager` o si se elimina la instancia del contexto de persistencia. Podrían tener cambios que se pueden fusionar con un `EntityManager` activo para persistir cambios en la base de datos. 
- **Borrado (Removed)**: El objeto está marcado para ser borrado de la base de datos. Existe en la aplicación Java y se borrará de la base de datos al terminar la sesión.
-----

Con `persist()`, un objeto de Java transient pasa a estar managed.

Si por ejemplo se intenta hacer `remove()` de un objeto no controlado...
`java.lang.IllegalArgumentException: Removing a detached instance com.arquitecturajava.Persona#pedro`

 `merge()` obliga al `EntityManager` a convertir una entidad detached en managed. Ojo, managed es la instancia que devuelve, no la que pasa por parámetro. 

##### Persist vs Merge

##### Persist
- Si X es una **entidad nueva, se vuelve gestionada**. La entidad X se introducirá en la base de datos en el commit de la transacción o como resultado de la operación flush.
- Si X es una **entidad gestionada previamente existente**, es ignorada por la operación persist. Sin embargo, la operación persist se propaga a las entidades referenciadas por X, si las relaciones desde X hacia estas otras entidades están anotadas con el elemento de anotación cascade=PERSIST o cascade=ALL, o especificadas con el elemento de descriptor XML equivalente.
- Si X es una **entidad eliminada**, se vuelve **gestionada**.
- Si X es un **objeto desasociado,** puede lanzarse la excepción `EntityExistsException` cuando se invoca la operación persist, o la excepción `EntityExistsException` u otra `PersistenceException` puede lanzarse en el momento de la operación flush o commit.
- Para todas las entidades Y referenciadas por una relación desde X, si la relación hacia Y ha sido anotada con el valor de elemento cascade=PERSIST o cascade=ALL, la operación persist se aplica a Y.

##### Merge
- Si X es una **entidad desasociada**, el estado de X se copia sobre una instancia de entidad gestionada X' existente de la misma identidad o se crea una nueva copia gestionada X' de X.
- Si X es una **instancia de entidad nueva**, se crea una nueva instancia de entidad gestionada X' y el estado de X se copia en la nueva instancia de entidad gestionada X'.
- Si X es una instancia de **entidad eliminada**, la operación merge lanzará una `IllegalArgumentException` (o la confirmación de la transacción fallará).
- Si **X es una entidad gestionada**, es ignorada por la operación merge; sin embargo, la operación merge se propaga a las entidades referenciadas por las relaciones desde X si estas relaciones han sido anotadas con el valor de elemento cascade=MERGE o cascade=ALL.
- Para todas las entidades Y referenciadas por relaciones desde X que tengan el valor de elemento cascade=MERGE o cascade=ALL, Y se fusiona recursivamente como Y'. Para todas estas Y referenciadas por X, X' se establece para hacer referencia a Y'. (Nótese que si X es gestionada, entonces X es el mismo objeto que X').
## 7. Sesiones; estados de un objeto

En Hibernate se usa el objeto `Session` usando la clase `SessionFactory`.
Un `Session` es un objeto que representa una unidad de trabajo con la BBDD. Se representa el gestor de persistencia, pudiendo cargar y guardar objetos.

Intentarme está formada por una cola de sentencias SQL necesarias para poder sincronizar el estado de la sesión con la BBDD.
La sesión tiene una lista de objetos persistentes. Se corresponde con el **primer nivel de caché**.

La sesión permite definir el alcance de un contexto determinado en Hibernate. 

Se deben cerrar las sesiones cuando se completa todo el trabajo de una transacción. 

## 8. Carga, almacenamiento y modificación de objetos

Para cargar un objeto de acceso a datos en la aplicación de Java, el método `load()` de la clase `Session` suministra un mecanismo para capturar una instancia persistente. El método `load()` acepta un objeto `Class` y carga el estado de una nueva instancia de esa clase, inicializada en estado persistente. 

El método `load()` lanzará una excepción irrecuperable si no existe la fila de base de datos correspondiente. Si no se está seguro de que exista una fila correspondiente, debe usarse el método `get()`, el cual consulta la base de datos inmediatamente y devuelve null si no existe una fila correspondiente

Existen dos métodos que se encargan de recuperar un objeto persistente por identificador: `load()` y `get()`. La diferencia entre ellos radica en cómo indican que un objeto no se encuentra en la base de datos: `get()` devuelve un nulo y `load()` lanza una excepción `ObjectNotFoundException`.

Aparte de esta diferencia, `load()` intenta devolver un objeto proxy, siempre y cuando le sea posible (no esté en el contexto de persistencia). Con lo que es posible que la excepción sea lanzada cuando se inicialice el objeto proxy. Esto es conocido como **carga perezosa**.

En el caso que se obtenga un proxy, no tiene impacto sobre la base de datos (no se ejecuta ninguna consulta), hasta que no se inicializa el mismo. Muy útil cuando se obtiene una referencia de un objeto para asociarlo a otro. (No es necesario obtener el objeto).Se modifica un objeto persistente.

```java

Claro, puedo proporcionar un ejemplo utilizando Hibernate para ilustrar la diferencia entre los métodos load() y get() en el contexto de recuperar un objeto persistente por su identificador.

Supongamos que tenemos una clase Usuario que mapea a una tabla en nuestra base de datos, y queremos recuperar un usuario específico por su identificador.

java
Copiar código
import org.hibernate.Session;
import org.hibernate.Transaction;
import org.hibernate.query.Query;

public class HibernateExample {

    public static void main(String[] args) {
        Session session = HibernateUtil.getSessionFactory().openSession();
        Transaction transaction = null;

        try {
            transaction = session.beginTransaction();

            // Utilizando el método get()
            Usuario usuarioGet = session.get(Usuario.class, 1L);
            System.out.println("Usuario obtenido con get(): " + usuarioGet);

            // Utilizando el método load()
            Usuario usuarioLoad = session.load(Usuario.class, 2L);
            System.out.println("Usuario obtenido con load(): " + usuarioLoad);

            // Haciendo cambios en el objeto persistente
            usuarioGet.setEdad(40);

            transaction.commit();
        } catch (Exception e) {
            if (transaction != null) {
                transaction.rollback();
            }
            e.printStackTrace();
        } finally {
            session.close();
            HibernateUtil.getSessionFactory().close();
        }
    }
}
```

### 8.1. Almacenamiento y modificación de objetos persistentes

Para almacenar objetos:
1. Se instancia un objeto nuevo (transitorio)
2. Se obtiene un `Session` y se inicia la transacción `beginTRansaction()`
3. Se llama al método `save()` que introduce el objeto en el contexto de persistencia y devuelve el identificador del objeto persistido.
4. Para que se sincronicen en BBDD, se debe realizar `commit()` de la transacción. Dentro del objeto `Session` se llama al método `flush()`. Es posible llamarlo explícitamente también.
5. Finalmente se cierra la sesión con `close()` para liberar el contexto de persistencia y devolver la referencia al objeto al estado disociado.

Cualquier cambio a su estado de persistencia se persiste cuando se hace `flush()`
No es necesario invocar a ningún método en particular para que las modificaciones sean persistentes. La manera más sencilla de actualizar el estado de un objeto es cargarlo con `load()` y manipularlo directamente mientras la sesión esté abierta.

Los objetos persistentes pueden borrarse con `Session.delete()` que quitará el objeto de BBDD (la aplicación aún puede contener referencia al objeto quitado). 

Lo ideal no es mandar a la interfaz de usuario el objeto de la transacción sino usar datos versionados para garantizar el aislamiento.
Hibernate provee la reasociación de entidades desprendidas usando `Session.update()` o `Session.merge()`

Siendo estrictos... podría llamarse sin una transacción. Pero no si el Contexto de Persistencia es de tipo `PersistenceContextType.TRANSACTION` (caso de contexto de persistencia de contenedor en un entorno de aplicación Java EE). En ese caso `persist()`, `merge()`, `remove()` arrojarán un `TransactionRequiredException`

Contextos de transacciones: https://stackoverflow.com/questions/2547817/what-is-the-difference-between-transaction-scoped-persistence-context-and-extend
(Muy interesante)
## 9. Consultas SQL

Con `createSQLQuery()`
O en el caso de JPA `createNativeQuery()`

Retornarán una lista de objetos `Object[]`. Hibernate usa `ResultSetMetadata` para deducir el orden real y los tipos de valores escalares retornados. 

```java
sess.createSQLQuery("SELECT * FROM Personas").list();
sess.createSQLQuery("SELECT ID,NOMBRE, EDAD FROM PERSONAS").list();
```


**Consulta de entidades**

```java
sess.createSQLQuery("SELECT * FROM PERSONAS").addEntity(Persona.class);
sess.createSQLQuery("SELECT ID,NOMBRE,EDAD FROM PERSONAS").addEntity(Persona.class);
```

En este caso los valores serán mapeados con la entidad `Persona`

## 10. Lenguajes propios de herramientas ORM. El lenguaje HQL

- El lenguaje de la especificación JPA es JPQL. Especificación de consultas de persistencia para Java. 
- Hibernate implementa JPQL con el lenguaje de consulta HQL (Hibernate Query Language) parecido a SQL. Es completamente orientado a objetos y comprende herencia, polimorfismo, asociación. 
- Se encarga de convertirlo a SQL y ejecutarlo.
- HQL es case-insensitive. Pero no da igual con las clases que se estén recuperando y sus propiedades, ahí sí se distinguen mayúsculas y minúsculas.

**Características de HQL**
- Soporte completo para operaciones relacionales. Consultas SQL en forma de objetos. 
- Devolución de resultados en forma de objetos.
- Consultas polimórficas. Se puede declarar resultado usando superclase e Hibernate se encargará de crear objetos adecuados para las subclases correctas
- Características avanzadas: Paginación, fetch joind, inner y outer joins... Proyecciones, funciones de agregación y agrupamientos, ordenamientos, consultas
- Independiente del manejador de base de datos (siempre que esta soporte la característica que se quiere usar)
- Las consulta se lanzan sobre las clases de negocio, ese es el modelo en Java. 

```java
Query query = session.createQuery("FROM Persona");
List<Persona> personas = query.list();

Query query = session.createQuery("FROM Persona WHERE edad > :edad");
query.setParameter("edad", 18);
List<Persona> personas = query.list();

SQLQuery query = session.createSQLQuery("SELECT * FROM personas");
query.addEntity(Persona.class);
List<Persona> personas = query.list();

Criteria criteria = session.createCriteria(Persona.class);
criteria.add(Restrictions.gt("edad", 18));
List<Persona> personas = criteria.list();

Query query = session.createQuery("SELECT COUNT(*) FROM Persona");
Long totalPersonas = (Long) query.uniqueResult();

Query query = session.createQuery("FROM Persona ORDER BY nombre");
query.setFirstResult(0);
query.setMaxResults(10);
List<Persona> personas = query.list();

Query query = session.createQuery("FROM Persona p WHERE p.id IN (SELECT f.persona.id FROM Factura f WHERE f.importe > :importe)");
query.setParameter("importe", 1000); // Cantidad mínima de importe
List<Persona> personas = query.list();
```

## 11. Gestión de transacciones

En la gestión de transacciones no se produce bloqueo de objetos en la memoria.  La aplicación puede esperar el comportamiento definido por el nivel de aislamiento de sus transacciones de las bases de datos. Gracias a la Session, la cual también es un caché con alcance de transacción. Para realizar con éxito la gestión de transacciones, ésta se van a basar en el uso del objeto `Session`.

El objeto `Session` se obtiene a partir de un  `SessionFactory` representa configuración particular de un conjunto de metadatos de mapping objeto relacionales.  

Cuando se crea el objeto `Session` , se le asigna la conexión de la base de datos que va a utilizar. Una vez obtenido el objeto `Session` , se crea una nueva unidad de trabajo ( `Transaction`) utilizando el método `beginTransaction`. Dentro del contexto de la transacción creada, se pueden invocarlos métodos de gestión de persistencia proporcionados por el objeto `Session`, para recuperar, añadir, eliminar o modificar el estado de instancias de clases persistentes. También se pueden realizar consultas. Si las operaciones de persistencia no han producido ninguna excepción, se invoca el método `commit` de la unidad de trabajo para confirmar los cambios realizados. En caso contrario, se realiza un `rollback` para deshacer los cambios producidos. Sobre un mismo objeto `Session` pueden crearse varias unidades de trabajo. Finalmente se cierra el objeto Session invocando su método `close`.
Finalmente al finalizar la aplicación debe cerrarse el `SessionFactory` también para evitar fugas de recursos en el servidor de aplicaciones.

Aquí ejemplito:

```java
Session session = HibernateUtil.getSessionFactory().openSession();
Transaction tx = null;
try 
{
          tx = session.beginTransaction();
// Utilizar la Session para saveOrUpdate/get/delete/...tx.commit();
} catch (Exception e) 
{
          if (tx != null) 
          {
               tx.rollback();
               throw e;
          }
} finally {
          HibernateUtil.getSessionFactory().close();
}// Al finalizar la aplicación ...HibernateUtil.shutdown( );
```


-------------
------------

## 12. Entity
- Clase que representa una tabla
- Se anota con `@Entity`
- Si el nombre de la tabla no coincide, indicarlo con `@Table`  (name, unique, nullable, insertable, updatable, columnDefinition, table, length, precision, scale)
- Clave primaria con `@Id`.  Este ID se anota con  `@GeneratedValue` para indicar que se genera automáticamente y se indica el método de generación.

```java
`@GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "ALUMNOS_SEQUENCE_GENERATOR")`
`@SequenceGenerator(sequenceName = "ALUMNOS_SEQUENCE", allocationSize = 1, name = "ALUMNOS_SEQUENCE_GENERATOR")`


`@GeneratedValue(strategy = GenerationType.IDENTITY)`
```

GenerationTipe **TABLE**, **SEQUENCE**, **IDENTITY**, **UUID**, **AUTO**

- Si no coincide con el atributo se usa `@Column`

Puede tener anotaciones específicas de acciones:
```java
@PrePersist @PostPersist
@PreUpdate @PostUpdate
@PreRemove @PostRemove
```


Otras anotaciones que podríamos ver son:
- `@Size`: Restricción de tamaño. min, max , message
- `@Temporal`: Indicando la fecha.  `TemporalType` `DATE` (fecha), `TIME` (hora), `TIMESTAMP` (fecha y hora)
- `@Basic`: Algunas indicaciones con atributos como fetch (defecto EAGER), optional (defecto true)
- `@NotNull:Restricción de no nulo.
- `@EmbeddedId`: Se indica que es un ID (PK) formada por varios y embebida en clase propia
- `@Embedabble`: La clase propia que contiene esos atributos. 

- `@NamedQueries` `@NamedQuery`  name, query. Alias de queries en la propia entidad
- `@XmlRootElement`: Elemento raíz
- `@XmlTransient`: Indica que no sea serializado. (Métodos getter de listas)

## 12.1 Uso de Lombok

```xml
<dependency>  
    <groupId>org.projectlombok</groupId>  
    <artifactId>lombok</artifactId>  
    <version>1.18.30</version>  
    <scope>provided</scope>  
</dependency>  
```

Normalmente, Lombok se integra con el IDE (como IntelliJ IDEA o Eclipse)  
durante el desarrollo para proporcionar funcionalidades como la generación automática de código.  
Sin embargo, **en tiempo de ejecución, no es necesario incluir Lombok en el JAR**, ya que el código generado por Lombok ya se ha insertado en las clases compiladas.  
Por lo tanto, al especificar `<scope>provided</scope>` para Lombok, asegurando que no se  
incluya en el JAR final, reduciendo así el tamaño del archivo y evitando posibles conflictos de  
dependencia en el entorno de ejecución.