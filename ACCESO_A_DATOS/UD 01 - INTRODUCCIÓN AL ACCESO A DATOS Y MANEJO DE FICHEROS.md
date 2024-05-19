
## 1. Introducción al Acceso a datos. Estrategias.

Una aplicación informática se puede dividir en:
- El **programa** que realiza las operaciones deseadas con los datos necesarios
- Los **datos** con los que opera el programa. Estos pueden ser obtenidos por diversos métodos (leídos por teclado, escaneados, leídos por soporte secundario... )

Cuando se programa, interesa la **persistencia**: Que el programa guarde los datos introducidos o los resultados obtenidos de forma que al terminar la ejecución no se pierdan y puedan ser recuperados posteriormente. Se podrá hacer usando ficheros, bases de datos que se guardarán en dispositivos de memoria no volátil. (En cambio el almacenamiento RAM mediante variables o vectores es temporal; Los datos en almacenamiento secundario son datos persistentes)

**Acceso a datos** consiste en conocer los tipos de almacenamiento de datos y cómo acceder a ellos. 

Las estrategias conocidas de acceso a datos para gestionar la persistencia de los datos son:
1. Ficheros
2. Bases de datos
	1. Relacionales
	2. Orientadas a objetos
	3. Objecto-relacionales
3. Mapeo objeto-relacional (ORM)
4. Bases de datos XML
5. Componentes - JavaBeans

Las bases de datos eliminan el problema de información redundante o inconsistente; globalizan y centralizan la información; garantizan la integridad de la información; garantizan la independencia de datos (separación entre programa y datos, se puede hacer cambios en la información que contiene la base de datos o acceder de diferente manera sin tener que cambiar aplicaciones)

No hay un método de acceso a datos que sea mejor que otro de manera absoluta. Debe considerarse la aplicación a construir y estudiar qué tipo de sistema de almacenamiento es mejor usar.
Conocidas las alternativas, pueden compararse las prestaciones en el problema de persistencia concreto que se presenta en el sistema de información en estudio. 

## 2. Ficheros

En las antiguas aplicaciones informáticas la información se guardaba en ficheros. 
Los desarrolladores de aplicaciones debían construir el programa conociendo detalladamente las posiciones de los datos para saber de qué posición hasta qué posición estaba cada dato, control de duplicados, problema de concurrencia... 

Aún se usan algunos ficheros como en los casos de configuración o de log. 

Los ficheros deben guardar datos siguiendo un patrón o estructura bien definida. Son interesantes los ficheros XML para transmisión de datos,para exportaciones, hay bases de datos modernas que guardan sus datos empleando XML...

El XML se emplea en tecnologías de comunicación como WML (lenguaje de formato inalámbrico) y WAP (protocolo de aplicaciones inalámbricas).

Han surgido librerías de conversión de la información almacenada de XML a formatos como PDF, textos, hojas de cálculo...

**Tipos de fichero**
- De texto
- Binarios
**Formas de acceso a ficheros**
- Secuencial
- Aleatorio
- Concatenación (tuberías / pipes)

## 3. Bases de datos

Recordamos que una **base de datos** es un sistema de información orientado hacia los datos que pretende recuperar y almacenar información de manera eficiente y cómoda. Surge en un intento de resolver dificultades del procesamiento tradicional de datos, considerando que los datos suelen ser independientes de las aplicaciones. 

**Ventajas**
- Independencia de los datos respecto a los procedimientos. El usuario tiene visión abstracta de los datos sin necesidad de conocimientos sobre la implementación de ficheros de datos índices... Esto es un ahorro en costes de desarrollo. La modificación de BBDD o de programas no implica cambios entre sí. Sin independencia, el mantenimiento de las bases de datos supondría el 50% de los recursos dedicados al desarrollo de una aplicación
- Disminución de redundancias
- Disminución de la posibilidad de que haya inconsistencia de datos
- Mayor integridad
- Mayor disponibilidad
- Mayor seguridad
- Mayor privacidad
- Mayor eficiencia en recogida, codificación y entrada en el sistema
- Interfaz con el pasado y el futuro: Base de datos abierta a reconocer información organizada por otro software
- Compartición de datos: Los datos pueden ser accedidos por varios usuarios simultáneamente, teniendo previstos procedimientos para salvaguardar la integridad de los mismos.

Un **sistema de ficheros convencional** solo se usará cuando la cantidad de datos sea tan reducida que no justifique las desventajas del uso de sistemas de base de datos. Por ejemplo: Guardar datos de resultado de la instalación de un programa. 

### 3.1. Bases de datos relacionales

Modelo de base de datos relacional - Edgar Codd 1969

Objetivo: Proporcionar método declarativo para especificar datos y consultas.
En el diseño de BBDD se establece la información que contendrá la base de datos, se recupera la información deseada y el SGBD es el que: describe estructura de datos para almacenarlos, gestiona procedimientos de recuperación para obtener las consultas deseadas.

Las BBDD relacionales son adecuadas para grandes cantidades de datos, compartir datos entre programas, búsquedas rápidas...

La desventaja es que no presentan buen modelo de las relaciones entre datos ya que todo son tablas bidimensionales de filas y columnas. (A veces pueden ajustarse mal al modelo real)

Se caracterizan porque:
- Están muy extendidas
- Son robustas
- Permiten interoperabilidad entre aplicaciones
- Permiten compartir datos entre aplicaciones
- Son comunes en muchos sistemas y tecnologías (Java, C++...)

**Otros modelos**
Otros modelos tradicionales serían los modelos **jerárquico** y en **red**. Algunos sistemas antiguos pueden usar estas arquitecturas, en centros de datos donde se manejan grandes volúmenes de información y la complejidad de los sistemas imposibilita en términos económicos su migración.

**El modelo relacional fue el primer modelo de BBDD definido de manera formal**. Primero se formularon modelos informales para las bases de datos jerárquicas y en red que, existían antes que las relacionales, pero fueron descritas como modelo después del modelo relacional. 

### 3.2. Bases de datos orientadas a objetos

En los modelos clásicos de BBDD existían problemas al representar cierta información y modelar ciertos aspectos del mundo real: Se pueden representar gran cantidad de datos pero las operaciones y representaciones sobre ellos son simples.

Pasar del modelo de objetos de programación al modelo relacional de base de datos, para almacenar información, genera dificultades. 

Los sistemas de bases de datos orientados a objetos soportan un **modelo de objetos puro** porque no están pasados en extensiones de otros modelos clásicos como el relacional.

El lenguaje de programación y el esquema de la base de datos usan **las mismas definiciones de tipos**.

##### Manifiesto de Malcolm Atkinson sobre sistema de bases de datos orientados a objetos

**Características obligatorias de orientación a objetos**
- 1) Deben soportarse **objetos complejos**.
- 2) Deben soportarse **mecanismos de identidad** de los objetos.
- 3) Debe soportarse la **encapsulación**.
- 4) Deben soportarse **tipos** y **clases**.
- 5) Los tipos o clases deben ser capaces de **heredar** de sus ancestros.
- 6) Debe soportarse **sobrecarga**, **sobreescritura** y **enlace dinámico.**
- 7) El **DML** debe ser **computacionalmente** **completo**.
- 8) El **conjunto** de todos los **tipos de datos** debe ser **ampliable**.
- 9) Debe proporcionarse **persistencia** a los datos.
- 10) El SGBD debe ser capaz de gestionar bases de datos de muy gran **tamaño**.
- 11) El SGBD debe soportar a usuarios **concurrentes**.
- 12) El SGBD debe ser capaz de **recuperarse de fallos** hardware y software.
- 13) El SGBD debe proporcionar una **forma simple de consultar los datos**.

**Características opcionales**
- 1) **Herencia múltiple**.
- 2) **Comprobación de tipos e inferencia de tipos**.
- 3) Sistema de base de datos **distribuido**.
- 4) **Soporte de versiones**.

El acceso a datos puede ser más rápido que con bases de datos orientadas a objetos (que son las bases de datos tradicionales) porque no hay necesidad de usar JOINS, que sí se necesitan en relaciones tabulares.
El objeto puede recuperarse directamente sin una búsqueda, usando punteros.

Las necesidades de las aplicaciones actuales con respecto a las bases de datos son:
- Soporte para objetos complejos y datos multimedia.
- Jerarquías de objetos o tipos y herencia.
- Gestión de versiones.
- Modelos extensibles mediante tipos de datos definidos por el usuario.
- Integración de los datos con sus procedimientos asociados.
- Manipulación navegacional (en vez de declarativa) y de conjunto de registros.
- Interconexión e interoperabilidad (capacidad de dos o más sistemas o componentes para intercambiar información y utilizar la información intercambiada).

**Ejemplos de SGBD orientados a objetos**:
- 1. Matisse
- 2. ObjectStore
- 3. Versant Object Database

### 3.3. Comparativa entre relacionales (RDBMS) y orientadas a objetos (ODBMS)

Se ha demostrado que los ODBMS son superiores para ciertos tipos de tareas.
Muchas operaciones se realizan usando interfaces navegacionales más que declarativas y este acceso a datos navegacional es implementado muy eficientemente. 

Las bases de datos orientadas a objetos son transparentes (no se ensucia la construcción de la aplicación): El desarrollador se debe de preocupar solo por los objetos de su aplicación, en lugar de cómo deben ser almacenados y recuperados en un medio físico.

Entre las ventajas de SGBDOO frente a SGBDR destacaríamos:
- Mayor **capacidad de modelado**: El modelo de datos orientado a objetos permite modelas el mundo real de forma mucho más fiel: Los objetos tienen estado y comportamientos; Los objetos pueden almacenar las relaciones con otros objetos; Los objetos pueden agruparse para formar objetos complejos (herencia)
- **Extensibilidad** ya que pueden construirse nuevos tipos de datos a partir de los existentes; Pueden agruparse propiedades comunes e incluirlas en superclases reduciendo redundancia; Pueden reusarse las clases llevando a más fácil mantenimiento y menor tiempo de desarrollo
- **Lenguaje de consulta más expresivo**. El acceso navegacional (navegando a través de los nodos, referencias de un objeto) es mejor que el acceso declarativo del modelo relacional (joins...)
- **Adaptación a aplicaciones** avanzadas de bases de datos: Sistemas de diseño CAD, CASE, multimedia...
- **Prestaciones**: Mejor rendimiento. Tanto en bancos de prueba como en aplicaciones tradicionales de bases de datos, como el procesamiento de transacciones en línea (OLTP)
- **Reglas de acceso**: Se accede mediante interfaces creadas por las clases, dándo una independencia a cada objeto que las bases de datos relacionales no permiten
- **Clave**: En el modelo relacional, las claves primarias tienen forma representable en texto; Los objetos no necesitan representación visible del identificador. 

Entre las desventajas:
- **Reticencia del mercado**
- **Carencia de un modelo de datos universalmente aceptado**. Además, muchos modelos carecen de una base teórica o teoría matemática coherente que le sirva de base
- **Carencia de experiencia**. 
- **Panorama actual**: Los SGBD relacionales y los objeto-relacionales están muy extendidos. El modelo relacional tiene una base teórica. SQL es estándar aprobado, ODBC, JDBC son estándares de facto. 
- **Dificultades en optimización**: La optimización necesita realizar una comprensión de la implementación de los objetos para poder acceder de forma eficiente. Esto compromete el concepto de encapsulación (ocultamiento del estado en POO de forma que solo pueda cambiar mediante las operaciones definidas para ese objeto)

### 3.4. Bases de datos objeto-relacionales

Base de datos Objeto Relacional (BDOR),  aquella que ha evolucionado desde el modelo relacional a otro extendido que incorpora conceptos del paradigma orientado a objetos. Un Sistema de Gestión Objeto-Relacional (SGBDOR) contiene ambas tecnologías: relacional y de objetos. 

En BBDD Objecto-relacional, el diseñador puede crear sus propios tipos de datos y crear métodos para esos tipos de datos. 

Por ejemplo
```sql
CREATE TYPE persona AS OBJECT
(nif VARCHAR2(9),
 nombre VARCHAR2(30),
 direccion VARCHAR2(40), 
 telefono VARCHAR2(15),
 fecha_nac DATE
);
```

En el caso de BBDD Oracle, el SGBD en la versión 8i fue extendido con conceptos del modelo de base de datos orientadas a objetos. 
Aunque las estructuras de datos siguen siendo tablas, los diseñadores pueden usar muchos mecanismos de orientación a objetos para definir y acceder a los datos. 

Se reconoce el concepto de objeto: Un objeto tiene un tipo, se almacena en cierta columna de cierta tabla y tiene un identificador único (OID, Object Identifier). Estos identificadores se pueden referenciar a otros objetos y representar relaciones de asociación y agregación.

**Ventaja**: Los usuarios pueden pasar sus aplicaciones actuales sobre bases de datos relacionales a este nuevo modelo sin tener que reescribirlas. Posteriormente se podrán ir adaptando las aplicaciones y bases de datos para que usen funciones orientadas a objetos.

El modelo objeto-relacional amplía al relacional porque:
- Aumenta la variedad en los tipos de datos (Nuevos tipos de datos. Tipos complejos como registros, conjuntos, referencias, listas, pilas, colas, vectores)
- Extensiones en el control de la semántica (procedimientos almacenados y funciones que tengan código en algún lenguaje como SQL, Java, C)
- Compartir librerías de clases existentes (reusabilidad)

Entre los productos comerciales de BBDD Objeto-relacional se puede destacar:
DB2 Universal Database de IBM, Universal Server de Informix, INGRES II de Computer Associates, ORACLe, SyBASE, PostgreSQL.

## 4. Acceso a bases de datos mediante conectores

Existen estándares que facilitan a los programas informáticos manipular la información almacenada en las bases de datos.

Java: API JDBC (Java Database Connectivity).

Modelo relacional: Arquitectura normalizada y optimizada que muchas empresas poseen, basadas en sentencias SQL, importancia estratégica para el crecimiento del mapeo objeto-relacional y los mecanismos de persistencia.

**Driver JDBC** es un componente software que posibilita a una aplicación Java interaccionar con la base de datos.

![](resources/ud01-3.png)

La API JDBC define interfaces y clases para aplicaciones de bases de datos en Java, realizando conexiones de base de datos.
Está situado en la base de cada marco de trabajo de mapeo objeto-relacional. 

Con JDBC, el desarrollador puede enviar sentencias SQL, PL/SQL a una base de datos relacional. JDBC permite embeber SQL dentro del código de Java. 

El uso de conectores JDBC **independiza de la base de datos** que utilice. Aunque hay un trabajo de traducción para mapear los campos devueltos por cada consulta a la colección de objetos correspondiente. También hay que trabajar las sentencias de actualización, inserción y eliminación para cada uno de los campos. 

También está el controlador ODBC (Open Database Connectivity) usado por Microsoft para tener acceso a bases de datos relacionales en diversas plataformas.
Hay un estándar que existe de puente entre JDBC-ODBC en versiones Solarios y Windows de la plataforma Java para que se pueda usar ODBC en programa Java. 

## 5. Mapeo objeto relacional (ORM)

Muchas aplicaciones se desarrollan con POO pero los datos se almacenan en BBDD relacionales, basadas en sentencias SQL (como estamos viendo en este tema).

Este sistema de trabajo de las empresas es la base para el continuo crecimiento del mapeo objeto relacional (O/R) y está asociado a los mecanismos de persostencia.

Cuando se programan sistemas orientados a objetos, se invierte gran cantidad de tiempo en desarrollar objetos persistentes (convertir objetos del lenguaje de programación a registros de la base de datos y viceversa)

El **mapeo objeto-relacional** es una técnica de programación para convertir datos entre el sistema de tipos utilizado en un lenguaje de programación orientado a objetos y el sistema utilizado en una base de datos. Evitar el **desfase objeto-relacional**.

Se puede usar un framework que haga estas tareas de modo transparente, evitando al programador usar SQL y la gestión del acceso a base de datos quede centralizada en un componente único, permitiendo su reutilización.

### Capa de persistencia y framework de mapeo

**Capa de persistencia**: Parte de la aplicación que permite almacenar, recuperar, actualizar, eliminar el estado de los objetos que necesitan persistir en un sistema gestor de datos. 

El ORM es una capa que permite relacional objetos con un modelo de datos relacional, ocultando todo el mecanismo de conexión al motor de base de datos y no teniendo que escribir sentencias SQL para la gestión de los datos.

Traduce entre dos modelos: de objetos a registros y de registros a objetos. Si el programa quiere grabar un objeto, llama al motor de persistencia y este traduce el objeto a registros y llama a la base de datos para que los guarde. 

El programa solo ve que puede guardar y recuperar objetos. La base de datos solo ve que guarda y recupera registros. 

Alternativas
- Open source: Hibernate y Spring
- Basadas en el estándar: EJB 3.0 y JDO (Java Data Objects) 
- TopLink

Cada mecanismo de mapeo O/R tiene dependencia del conector JDBC para comunicarse con la base de datos de forma eficiente. Debe ser óptimo o debilita al framework. Es importante por eso seleccionar el driver JDBC que mejor se adapte a la aplicación. 

"El motor de persistencia no es un framework O/R"

- **JPA**: Especificación que define cómo debe realizarse la persistencia y el mapeo objeto-relacional.
- **Motor de Persistencia**: Implementa la especificación JPA. Utiliza un framework ORM para realizar el trabajo de mapeo y persistencia.
- **Framework ORM**: Proporciona las capacidades necesarias para hacer el mapeo y la persistencia de objetos a tablas de bases de datos.

Supongamos que usamos Hibernate como motor de persistencia en una aplicación JPA. Hibernate es tanto un framework ORM como un motor de persistencia JPA. Aquí hay un ejemplo de cómo se integran:

**Entity Class utilizando JPA:**

```java
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class Cliente {
    @Id
    private Long id;
    private String nombre;

    // Getters y setters
    public Long getId() { return id; }
    public void setId(Long id) { this.id = id; }
    public String getNombre() { return nombre; }
    public void setNombre(String nombre) { this.nombre = nombre; }
}
```


**persistence.xml configurando Hibernate como el motor de persistencia:**

```xml
<persistence xmlns="http://xmlns.jcp.org/xml/ns/persistence" version="2.2">
    <persistence-unit name="miUnidadDePersistencia">
        <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>
        <class>com.miapp.Cliente</class>
        <properties>
            <property name="javax.persistence.jdbc.url" value="jdbc:h2:mem:test"/>
            <property name="javax.persistence.jdbc.user" value="sa"/>
            <property name="javax.persistence.jdbc.password" value=""/>
            <property name="javax.persistence.jdbc.driver" value="org.h2.Driver"/>
            <property name="hibernate.dialect" value="org.hibernate.dialect.H2Dialect"/>
        </properties>
    </persistence-unit>
</persistence>
```

En este caso:

- **JPA** define las anotaciones y la API para trabajar con la entidad `Cliente`.
- **Hibernate** actúa como el motor de persistencia (implementando JPA) y también como el framework ORM que realiza el mapeo objeto-relacional y la gestión de la base de datos.

### Conclusión

El "motor de persistencia" no es un framework ORM, pero utiliza uno para cumplir con la especificación JPA. El motor de persistencia implementa las interfaces y el comportamiento definidos por JPA, mientras que el framework ORM proporciona las funcionalidades necesarias para hacer efectivo ese mapeo y gestión de la persistencia.
## 6. Bases de datos XML

Las limitaciones de la tecnología de bases de datos relacionales, llevan al surgimiento de nuevas bases de datos como las bases de datos XML.

Estas bases de datos almacenan los datos estructurados como XML sin necesidad de traducir los datos a estructura relacional o de objeto.

Se puede distinguir entre:
- **Bases de datos nativas XML**: Modelo lógico de documentos XML. El SGBD almacena y recupera documentos de acuerdo a dicho modelo. Productos ejemplo: eXist, Aache Xindice, Berkeley dbXML...
- **Bases de datos compatibles con XML (XML-enabled)**: Bases de datos, generalmente objeto-relacionales, que admiten entradas de datos en forma de XML y proporcionan salidas en este mismo formato. Productos ejemplo: Oracle, DB2 (Viper)...

Las bases de datos XML nativas permiten trabajar con XQL (eXtensible Query Language) similar a SQL en base de datos relacional.

Trabajar con bases de datos XML nativas conlleva:
- Describir datos mediante definiciones de tipos de datos (DTD) o esquemas XML
- Definir nuevo esquema de base de datos XML nativa o mapa de datos a usar para almacenar y obtener datos. 
## 7. Desarrollo de componentes

En los inicios los ordenadores eran caros y los desarrolladores baratos. Ahora los ordenadores son baratos y los desarrolladores caros. Además los requisitos de las aplicaciones cada vez son más complejos -> Es necesario usar técnicas de orientación a objetos para intentar que el código que se desarrolle sea reutilizable. 

- El **componente** es una unidad de software que realiza función bien definida y posee interfaz bien definida. 
- El **componente software** tiene interfaces especificadas contractualmente pudiendo ser desplegado independientemente e interaccionar con otros componentes para formar un sistema. 
- La **interfaz** es el punto de acceso a los componentes, permitiendo a los clientes acceder a los servicios proporcionados por el componente. 
- Dividendo en trozos el software se reduce la complejidad, se permite la reutilización y se acelera el proceso de ensamblaje.
- Los creadores de componentes puede especializarse creando objetos cada vez más complejos y de mayor calidad. 
- La interoperabilidad entre componentes:
	- Aumenta la competencia
	- Reduce los costes
	- Facilita la construcción de estándares
- Software rápido, mejor calidad, menor coste. 

- El componente software debe especificar sus dependencias de contexto (necesidades para funcionar correctamente): interfaces requeridas, entorno de ejecución: máquina necesaria, sistema a utilizar. 

- El origen de los JavaBeans está en la necesidad de Java de **disponer de tecnología de objetos y componentes reutilizables**. Y de **mejorar el proceso para crear interfaces de usuario**, acercándose a la facilidad de otros productos como Visual Basic de Microsoft. 

Un **JavaBean** es un componente software reutilizable basado en la especificación JavaBean de Oracle que se puede manipular visualmente en una
herramienta de desarrollo.

El JavaBean presenta como propiedades:
- **Portabilidad**. Arquitectura neutral de componentes que puedan usarse en otras plataformas y entornos.
- **Reusabilidad**. Bloques en la construcción de aplicaciones complejas.
- **Introspección**. Reconocimiento de pautas de diseño, nombres de funciones miembros o métodos y definiciones de clases para permitir mirar dentro del bean y conocer propiedades y comportamiento. 
- **Personalización**. En tiempo de diseño se pueden modificar las características y comportamiento del bena. 
- **Persistencia**. Puede guardar su estado y recuperarlo posteriormente mediante serialización. Cuando un ejemplar de bean se serializa se convierte en un flujo de datos que se almacenará en algún sitio, probablemente en un fichero. Otra aplicación podrá restaurarlo por deserialización.
- **Comunicación entre eventos**. Mecanismo de notificación entre objeto fuente y objectos receptores. 

## 8. Introducción al Manejo de ficheros. Clases asociadas a las operaciones de gestión de ficheros y directorios

Los **datos persistentes** persisten más allá de la ejecución de la aplicación que los trata. Los ordenadores almacenan sus datos dentro de ficheros en unidades de almacenamiento secundario (discos duros, discos ópticos...).

Se conoce como **flujo de Entrada/Salida** a las operaciones que son un flujo de información del programa con el exterior.

![](resources/ud01-2.png)

En Java, las operaciones de entrada salida se pueden realizar mediante el paquete estándar `java.io` que incorpora interfaces, clases y excepciones para este fin permitiendo:
- Lectura de entradas desde un flujo de datos
- Escritura de entradas a un flujo de datos
- Operar con ficheros en el sistema de ficheros local
- Gestionar la serialización de objetos

![](ud01-1.png)

### 8.1. Clase `File`

- Representación abstracta de ficheros y directorios
- Permite examinarlos y manipularlos, independientemente de la plataforma. Examinar el nombre, descomponerlo en su rama de directorios, crear el fichero si no existe...
- Sus instancias representan **nombres de archivo**, no los archivos en sí mismos
- Es posible que no exista archivo a ese nombre, por lo que deberán controlarse las _excepciones_

- Lo recomendable a la hora de indicar las rutas es usar `File.separator`, válido para todas las plataformas.
##### Algunos métodos estáticos 
- `createTempFile(prefix, suffix)`: Crea nuevo fichero con nombre único. En este caso crea una fichero temporal y devuelve un objeto `File` que apunta a él. Permite asegurarnos de tener un nombre de archivo no repetido.
-  `listRoots()`: Lista los nombres de archivo (`File`) de la raíz del sistema de archivos.

##### Algunos métodos de instancia

- `renameTo(File dst)` : **Renombrar** el archivo. Objeto `File` dejará de referirse al renombrado porque el `String` con el nombre del archivo del objecto `File` no cambia.
- `delete()` : Borra el archivo
- `deleteOnExit()`: Borra al finalizar la ejecución de la JVM
- `setLastModified(long time)`: Establecer fecha y hora de modificación 
- `mkdir()`: Crear un directorio
- `mkdirs()`: Crea los directorios superiores
- `list()`, `listFiles()`: Lista directorios. Uno devuelve un `String[]`, el otro un `File[]`
- `exists()`: Saber si un fechero existe o no
- `createNewFile()`: Crea fichero vacío con el nombre del `File` si y solo sí no existe. Devuelve `boolean` true si no existía y fue creado, false si ya existía.  (Excepciones `IOException`, `SecurityException`)
- `isDirectory()`: Para saber si el elemento es un directorio


### 8.2. Interfaz `FilenameFilter`

Permite filtrar ficheros por un determinado criterio (fecha, tamaño...).
La clase que la implementa debe implementar su método `boolean accept(File dir, String name)`

Ejemplo:

Dado el directorio:
```java
File directory = new File("ruta/a/tu/directorio"); 
```

Es posible filtrar por determinada extensión:

```java
//------------------JAVA 7 -------------------------
// Filtro para archivos con extensión .txt 
FilenameFilter textFileFilter = new FilenameFilter() { 
	@Override
	public boolean accept(File dir, String name) { 
		return name.endsWith(".txt"); 
	} 
}; 
String[] files = directory.list(textFileFilter);

//------------------JAVA 8 -------------------------

String[] files = directory.list((file, name) -> name.endsWith(".txt"));

```

O por nombre: 

```java
//------------------JAVA 7 -------------------------
// Filtro para archivos con extensión .txt 
FilenameFilter textFileFilter = new FilenameFilter() { 
	@Override
	public boolean accept(File dir, String name) { 
		return name.endsWith(".txt"); 
	} 
}; 
String[] files = directory.list(textFileFilter);

//------------------JAVA 8 -------------------------

String[] files = directory.list((file, name) -> name.endsWith(".txt"));
```
### 8.3. Operaciones con ficheros y directorios
##### Creación de fichero

```java
try {
	File file = new File("C:\Usuarios\romoreno-dev\Documentos\prueba.txt");
	if (file.createNewFile()) {
		System.out.println("Fichero creado");
	} else {
		System.out.println("Fichero no creado (ya existe)");
	}
} catch (Exception e) {
	e.getMessage();
}
```

##### Creación de directorio

```java
try {
	boolean exist new File("ruta/a/tu/directorio").mkdirs();
	if (exist) {
		System.out.println("Directorios creados");
	} else {
		System.out.println("Directorios no creados");
	}
} catch (Exception e) {
	e.getMessage();
}
```


##### Borrado de directorios

Para borrar un directorio, debe borrarse primero cada uno de directorios y ficheros que contenga. Se pueden ir recorriendo recursivamente para ir borrando todos los ficheros.

```java
    public static boolean deleteDirectory(File directory) {
        if (!directory.exists()) {
            return false; // El directorio no existe
        }

        if (directory.isDirectory()) {
            // Listar todos los archivos y subdirectorios
            File[] files = directory.listFiles();
            if (files != null) {
                // Recorrer y eliminar cada archivo y subdirectorio
                for (File file : files) {
                    if (file.isDirectory()) {
                        // Llamar recursivamente para eliminar subdirectorios
                        deleteDirectory(file);
                    } else {
                        // Eliminar archivo
                        file.delete();
                    }
                }
            }
        }

        // Eliminar el directorio después de que su contenido haya sido eliminado
        return directory.delete();
    }
```

### 8.4. Flujos

Un **flujo** es una abstracción de aquello que produce o consume información. Mediante los flujos se realizan las operaciones de E/S. 
La vinculación del flujo al dispositivo físico la hace el sistema de entrada y salida del núcleo de Java. Es decir, las clases y métodos de E/S van a ser las mismas independientemente del dispositivo con el que se actúe. El núcleo de Java sabrá si tiene que tratar con el teclado, el monitor, el sistema de archivos, un socket de red...

**Los flujos deben cerrarse**. Para ello es bueno usar el try-with-resources implementado en Java 7 (que llama al método `close()` de todas aquellas clases que implementen `AutoCloseable` cuando termine el bloque try-catch-finally. 

Si hay flujos que necesitan uno de otro (ej.: `ObjectInputStream` que necesita de `FileInputStream` bastará con cerrar el último, en este caso `ObjectInputStream` y los demás quedarán cerrados también)

En el paquete `java.io` se definen dos tipos de flujos:
- **Flujos basados en bytes (byte streams - 8 bits)**: Gestión de entradas y salidas de bytes. Su uso está orientado a la lectura y escritura de datos binarios. Su tratamiento está determinado por las clases abstractas `InputStream` y `OutputStream` que definen los métodos que deberán ser implementados por las subclases. 
- **Flujos basados en caracteres (character streams - 16 bits)**: Lectura y escritura de flujos de caracteres Unicode. Su tratamiento está determinado por las clases abstractas `Reader` y `Writer`.
#### 8.4.1. La importancia del uso de Buffer

Si se usan directamente clases para escribir o leer como `FileOutputStream`, `ObjectOutputStream`, `DataOutputStream`, `FileWriter`, `FileInputStream`, `ObjectInputStream`, `DataInputStream`, `FileReader` cada vez que se efectúa una lectura o escritura se hace físicamente en el disco duro. Para leer o escribir pocos caracteres cada vez el proceso es costoso y lento debido a los muchos accesos al disco duro. 

Es bueno añadir un buffer intermedio. `BufferedOutputStream`, `BufferedWriter`, `BufferedInputStream`, `BufferedReader`. Estas clases controlarán los accesos al disco. Así, al escribiendo se guardarán los datos hasta que haya suficientes como para hacer una escritura eficiente. Al leer, la clase leerá más datos de los pedidos, ofreciendo en las siguientes lecturas lo que tiene almacenado hasta que necesite leer otra vez físicamente. 

### 8.4.2. Flujos basados en bytes

Los archivos binarios guardan una representación de los datos en el archivo. Al guardar texto no guardan el texto en sí, sino su representación en código UTF-8 (8-bit Unicode Transformation Format)

Heredan de `OutputStream`:
- **`FileOutputStream`**: Escribe bytes en un fichero. Si el archivo existe, se borrará salvo que se indique en el constructor el parámetro append a true ( `FileOutputStream(Sring filePath, boolean append)`)
- **`ObjectOutputStream`**:  Convierte objetos y variables en vectores de bytes que pueden ser escritos en un `OutputStream`
- **`DataOutputStream`**: Da formato a tipos primitivos y objetos String, convirtiéndolos en un flujo de forma que cualquier `DataInputStream` los pueda leer. Empiezan por write: `writeByte()`, `writeFloat()`...

Heredan de `InputStream`:
- **`FileInputStream`**: Lee bytes de un fichero
- **`ObjectInputStream`**: Convierte en objetos y variables los vectores leídos de un InputStream
- **`DataInputStream`**.

#### A. FileOutputStream y FileInputStream

`write()` , `read()`

```java
String filename = "example.txt";
String text = "Hola, aquí estamos escribiendo en un archivo de texto.";

try (FileOutputStream fos = new FileOutputStream(filename)) {
        // Convertimos la cadena a bytes y escribimos esos bytes en el archivo
    fos.write(text.getBytes(StandardCharsets.UTF_8));
} catch (IOException e) {
    System.out.println("Error al escribir en el archivo: " + e.getMessage());
}

try (FileInputStream fis = new FileInputStream(filename)) {
    // Leemos el archivo byte por byte y lo almacenamos en un StringBuilder
    StringBuilder text = new StringBuilder();
    int character;
    while ((character = fis.read()) != -1) {
        text.append((char) character);
    }

    // Imprimimos el contenido del archivo
    System.out.println("Contenido del archivo:");
    System.out.println(text.toString());
} catch (IOException e) {
        System.out.println("Error al leer el archivo: " + e.getMessage());
}
```

#### B. Con BufferedOutputStream y BufferedInputStream

```java
String filename = "example.txt";
String text = "Hola, aquí estamos escribiendo en un archivo de texto.";

try (FileOutputStream fos = new FileOutputStream(filename);
	BufferedOutputStream bos = new BufferedOutputStream(fos)) {
        // Convertimos la cadena a bytes y escribimos esos bytes en el archivo
    bos.write(text.getBytes(StandardCharsets.UTF_8));
} catch (IOException e) {
    System.out.println("Error al escribir en el archivo: " + e.getMessage());
}

try (FileInputStream fis = new FileInputStream(filename)
	BufferedInputStream bis = new BufferedInputStream(fis)) {
    // Leemos el archivo byte por byte y lo almacenamos en un StringBuilder
    StringBuilder text = new StringBuilder();
    int character;
    while ((character = bis.read()) != -1) {
        text.append((char) character);
    }

    // Imprimimos el contenido del archivo
    System.out.println("Contenido del archivo:");
    System.out.println(text.toString());
} catch (IOException e) {
        System.out.println("Error al leer el archivo: " + e.getMessage());
}
```

#### C. DataOutputStream y DataInputStream

`writeUTF()`, `writeInt()`, `readUTF()`, `readInt()`...

```java
// ESCRITURA
String filename = "binary-data.dst";

try (DataOutputStream dataOutputStream = new DataOutputStream(new FileOutputStream(filename))) {
    dataOutputStream.writeUTF("Hola aqui estamos");
    dataOutputStream.writeInt(6);
} catch (IOException e) {
    System.out.println(e.getMessage());
}

// LECTURA
try (DataInputStream dataInputStream = new DataInputStream(new FileInputStream(filename))) {
	String text = dataInputStream.readUTF();
	int number = dataInputStream.readInt();

    System.out.println("Texto: " + text);
    System.out.println("Número: " + number);
} catch (IOException e) {
    System.out.println(e.getMessage());
}
```


#### D. ObjectOutputStream y ObjectInputStream

`writeObject()`, `readObject()`...

Se crea una clase simple que implemente `Serializable`. Se le puede agregar el atributo `serialVersionUID`. 

Este es un identificador único de versión para una clase serializable. Se utiliza durante la deserialización para verificar que el remitente y el receptor de un objeto serializado han cargado clases para ese objeto que son compatibles con respecto a la serialización. Si el `serialVersionUID` de la clase receptora no coincide con el `serialVersionUID` de la clase del remitente, entonces la deserialización resultará en una excepción `InvalidClassException`.

Cuando serializas un objeto, la información sobre el objeto y su estructura se almacena en el archivo. Si posteriormente cambias la estructura de la clase (por ejemplo, agregas o quitas campos), el `serialVersionUID` ayuda a Java a determinar si la versión de la clase que está tratando de deserializar es compatible con la versión que se serializó.

Si no defines explícitamente un `serialVersionUID`, el compilador de Java generará uno automáticamente basado en varios aspectos de tu clase, como los nombres de los campos, los métodos, las clases y las interfaces implementadas. Sin embargo, este valor generado automáticamente puede cambiar si haces cambios en la clase, incluso si esos cambios no afectan la compatibilidad de serialización.

```java
public class Person implements Serializable {
    private static final long serialVersionUID = 1L;
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }

    // Getters y setters (opcional)
}
```

```java
// ESCRITURA
String filename = "person.dat";
Person person = new Person("John Doe", 30);

try (FileOutputStream fos = new FileOutputStream(filename);
             ObjectOutputStream oos = new ObjectOutputStream(fos)) {

    oos.writeObject(person);
    System.out.println("Objeto escrito en el archivo");
} catch (IOException e) {
    System.out.println("Error al escribir el objeto: " + e.getMessage());
}

// LECTURA
try (FileInputStream fis = new FileInputStream(filename);
             ObjectInputStream ois = new ObjectInputStream(fis)) {

    Person person = (Person) ois.readObject();
    System.out.println("Objeto leído del archivo: " + person);
} catch (IOException | ClassNotFoundException e) {
    System.out.println("Error al leer el objeto: " + e.getMessage());
}
```

Ejemplo para copiar de un fichero a otro desde la línea de comandos:

```java
    public static void main(String[] args) {
      if (args.length != 2) {
        System.out.println("Uso: java Main <archivo_origen> <archivo_destino>");
            return;
        }

        String origen = args[0];
        String destino = args[1];

        try (FileInputStream fuente = new FileInputStream(origen);
             FileOutputStream salida = new FileOutputStream(destino, true)) {

            // Buffer para almacenar temporalmente los datos leídos
            byte[] buffer = new byte[1024];
            int longitud;

            // Leer datos del archivo de origen y escribirlos en el archivo de destino
            while ((longitud = fuente.read(buffer)) > 0) {
                salida.write(buffer, 0, longitud);
            }

            System.out.println("¡Archivo copiado correctamente!");
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }

    }
```

### 8.4.3. Flujos basados en caracteres


Al trabajar con ficheros de texto, lo recomendado es trabajar con las clases `Reader` y `Writer` porque son las optimizadas para trabajar con caracteres y texto en general ya que tienen en cuenta que cada carácter Unicode está representado por dos bytes.

Heredan de `Writer`:
- `FileWriter`: Para escritura hacia un fichero de texto. Crea un flujo de salida que trabaja con caracteres en vez de con bytes.
- `StringWriter`: Escribe caracteres en un objeto String permitiendo la construcción de cadenas de caracteres en memoria
- `OutputStreamWriter`: Convierte caracteres en bytes, se usa para escribir caracteres en un `OutputStream`
- `PrintWriter`: Dispone de métodos mucho más específicos

Heredan de `Reader`:
- **`FileReader`**: Para lectura desde un fichero de texto. Crea un flujo de entrada que trabaja con caracteres en vez de con bytes.
- **`StringReader`**: Lee  caracteres desde un objeto String permitiendo lectura de caracteres desde una cadena
-  **`InputStreamReader`**: Convierte bytes en caracteres. Se usa para leer caracteres de un `InputStream` (Por ejemplo `System.in`).  Forma sencilla de manipular el teclado. 

 Buffers: `BufferedReader` (`readLine()`) y `BufferedWriter` ( `write()`, `newLine()`) Para montar un buffer sobre un flujo de entrada de tipo FileReader o de salida de tipo FileWriter. 

#### A. Con Buffers

```java
String filename = "input.txt";

try (FileWriter fileWriter = new FileWriter(filename);
    BufferedWriter bufferedWriter = new BufferedWriter(fileWriter)) {

    bufferedWriter.write("Hola, mundo!");
    bufferedWriter.newLine();
    bufferedWriter.write("¡Este es un archivo de texto generado con BufferedWriter!");
    System.out.println("Datos escritos correctamente.");
} catch (IOException e) {
    System.out.println("Error de E/S: " + e.getMessage());
}

try (FileReader fileReader = new FileReader(filename);
    BufferedReader bufferedReader = new BufferedReader(fileReader)) {

	String line;
    while ((line = bufferedReader.readLine()) != null) {
                System.out.println(line);
    }
} catch (IOException e) {
	System.out.println("Error de E/S: " + e.getMessage()); 
}
```

#### B. Sin Buffers

```java
String filename = "input.txt";

try (FileWriter fileWriter = new FileWriter(outputFilename)) {
    fileWriter.write("Hola, mundo!");
    fileWriter.write("\n");
    fileWriter.write("¡Este es un archivo de texto generado con FileWriter!");
    System.out.println("Datos escritos correctamente.");
} catch (IOException e) {
    System.out.println("Error de E/S: " + e.getMessage());
}

try (FileReader fileReader = new FileReader(filename)) {
    int character;
	while ((character = fileReader.read()) != -1) {
	        System.out.print((char) character);
	}
} catch (IOException e) {
            System.out.println("Error de E/S: " + e.getMessage());
}
```


## 9. Internacionalización

**Charset** (Juego de caracteres): Conjunto de caracteres que pueden ser representados o usados en el sistema o aplicación.  Tabla que traduce de un número a un carácter (codepoint).

**ISO-8859-1** (ISO-Latin-1), tabla idéntica a ASCII para números menores de 128 y entre 128 y 255 incluye todos los caracteres necesarios para lenguas usadas en Europa occidental excepto algunos como el € (esos vienen incluidos en **ISO-8859-15**).

Consorcio **Unicode** lanzó juego de caracteres que pudiese incluir todos los caracteres usados en el mundo. 

**Encoding** (Codificación): Algoritmo seguido para guardar (para representar en forma de bytes) los caracteres. 

Unicode empezó usando dos bytes por caracter (UCS-2, encoding que se sigue usando en Windows y en Java). 
Según la arquitectura el byte menos significativo puede ser el primero o el segundo: UCS-2LE (LittleEndian), UCS-2BE (BigEndian). Para distinguir qué variante se está usando se le añade al principio del texto el carácter 0xFEFF "ZERO WIDTH NO-BREAK SPACE" (también conocido como el "BOM", Byte Order Marker).

Si uno se encuentra BOM se sabe que se está leyendo UTF-16 en el orden correcto. 
Si se encuentra con un BOM reflejado (0xFFFE) se sabe que se está leyendo al revés; este no existe en Unicode. 

Cuando UCS-2 se quedó corto y se necesitó ir más allá del 0xFFFF, se añadió una extensión y se le llamó UTF-16, donde se usan dos caracteres especiales (surrogates pair) para indicar que los bytes siguientes están fuera del plano básico. 

Se creó otra codificación alternativa UTF-32 (UCS-4) que consistía en guardar cada codepoint con 4 bytes (en realidad con 3 bastan pero se añade uno extra. Por eso en Linux wchar_t mide 4 bytes y en Windows mide 2).

Definitivamente surgió UTF-8: Es idéntico a ASCII para todos los caracteres inferiores a 128  usa uno o varios bytes extra (hasta 4 bytes) cuando tiene que almacenar un número superior a 128.

Cualquier texto ASCII en inglés es un texto UTF-8 válido. Los textos Europeos son un 2% más grandes que usando ISO-8859-15 (caracteres acentuados aumentan de tamaño). 
Los textos con alfabetos pequeños sin nada en común con el inglés aquí necesitarían más. UTF-8 no usa byte 0 en su codificación y funciones como strcpy funcionan bien con él. 

Textos en Windows con UTF-8  es posible que el editor añada un BOM. Windows sigue añadiéndolo para distinguir texto codificado en UTF-8 del codificado con otro encoding. Es mejor guardarUTF-8 sin BOM para evitar que las webs escriban tres bytes de más al principio de cada web. 

Como comentario, no basta con conocer el caracter que se quiere mostrar al usuario para saber qué grafías (glyph) debe mostrarse en pantalla. Algunos idiomas como el árabe son contextuales y el mismo carácter puede tener 4 grafías diferentes según esté solo, empiece la palabra, esté en medio o la termine. Otros comparten caracteres pero cambia ligeramente su grafía como hanzi (chino), kanki (japonés), hanja (coreano)  que son scripts de origen común pero con el tiempo ha evolucionado. En un mismo documento habrá que indicar de alguna forma que una parte del texto está en un tipo y otro en otro.
Igual sucede con el serbio (latín o cirílico pero en el cirílico algunas grafías cambian respecto al cirílico ruso). 
Ningún navegador cambiará las grafías según el idioma elegido, pero deberá usarse correctamente el atributo lang ya que la pronunciación sí que influirá, por ejemplo, en los lectores de texto para invidentes. 

## 10. Formas de acceso a un fichero

- **Acceso secuencial**: Datos leídos desde el comienzo del fichero hasta el final (que muchas veces no se conoce a priori). Es el caso de la lectura de teclado o la escritura en consola de texto (no se sabe cuándo terminará de escribir el ordenador)
- **Acceso aleatorio**: Acceso de forma no secuencial, desordenada. El archivo debe estar disponible en su totalidad en el momento de ser accedido.
- **Concatenación (tuberías, pipes)**: Conexiones entre programas que se ejecutan simultáneamente dentro de la misma máquina. Lo que uno produce es recibido por el otro. 

### 10.1. Operaciones básicas sobre ficheros de acceso secuencial

Entre operaciones de acceso secuencial puede estar el acceso para Crear fichero o abrirlo para grabar datos, Leer datos, Borrar información, Copiar datos de un fichero a otro, Búsqueda de información , Cerrar un fichero. 

Veamos un ejemplo de cómo encontrar a una `Persona` en un fichero de acceso secuencial:

```java
import java.io.*;

public class BusquedaArchivoSecuencial {
    public static void main(String[] args) {
        String nombreArchivo = "personas.dat";
        String nombreBuscado = "Juan"; // Nombre de la persona que queremos buscar

        try (ObjectInputStream entrada = new ObjectInputStream(new FileInputStream(nombreArchivo))) {
            boolean encontrado = false;
            Persona persona;
            
            while ((persona = (Persona) entrada.readObject()) != null) {
                if (persona.getNombre().equals(nombreBuscado)) {
                    System.out.println("Persona encontrada: " + persona);
                    encontrado = true;
                    break; // Salir del bucle una vez encontrada la persona
                }
            }
            
            if (!encontrado) {
                System.out.println("Persona no encontrada.");
            }
        } catch (EOFException e) {
            // Se alcanzó el final del archivo, se puede manejar si es necesario
        } catch (FileNotFoundException e) {
            System.out.println("No se encontró el archivo.");
        } catch (IOException e) {
            System.out.println("Error de E/S: " + e.getMessage());
        } catch (ClassNotFoundException e) {
            System.out.println("Clase no encontrada: " + e.getMessage());
        }
    }
}
```
### 10.2. Operaciones básicas sobre ficheros de acceso aleatorio

Para acceder de forma aleatoria, existe la clase **`RandomAccessFile`**
Esta clase: 
- Permite leer y escribir sobre el fichero (no se necesitan dos clases diferentes)
- Necesita que se le especifique el modo de acceso al instanciar (solo lectura o lectura y escritura)
- Tiene métodos específicos de desplazamiento como `seek(long posicion)` o `skipBytes(it desplazamiento)` para moverse de un registro a otro del fichero o posicionarse en un lugar concreto.

Los archivos de acceso directo tienen sus registros de un **tamaño fijo** o **predeterminado**

```java
RandomAccessFile(File file, String mode)
RandomAccessFile(String name, String mode)
```

##### Modos

| "r"   | Open for reading only. Invoking any of the write methods of the resulting object will cause an [`IOException`](https://docs.oracle.com/javase/8/docs/api/java/io/IOException.html "class in java.io") to be thrown. |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "rw"  | Open for reading and writing. If the file does not already exist then an attempt will be made to create it.                                                                                                         |
| "rws" | Open for reading and writing, as with "rw", and also require that every update to the file's content or metadata be written synchronously to the underlying storage device.                                         |
| "rwd" | Open for reading and writing, as with "rw", and also require that every update to the file's content be written synchronously to the underlying storage device.                                                     |

##### Escribir
```java
String s = "Escribo";  
// Abrir el fichero  
try (RandomAccessFile randomAccessFile = new RandomAccessFile("mifichero.txt", "rw");){  
    // Ir al final del fichero  
    randomAccessFile.seek(randomAccessFile.length());  
    // Escribir  
    randomAccessFile.writeBytes(s);  
} catch (FileNotFoundException e) {  
    throw new RuntimeException(e);  
} catch (IOException e) {  
    throw new RuntimeException(e);  
}
```

#### Leer
```java
StringBuilder cad = new StringBuilder();  
try (RandomAccessFile randomAccessFile = new RandomAccessFile("miArchivo.txt", "r");){  
    int sizeRegistro = 25;  
    long numRegistros = randomAccessFile.length()/sizeRegistro;  
   
    // El registro que se quiere buscar  
    int numRegistro = 5;  
    int posicion = numRegistro * sizeRegistro;  
    randomAccessFile.seek(posicion);  
      
    for (int i = 0; i < 25; i++) {  
        byte b = randomAccessFile.readByte();  
        cad.append((char) b);  
    }  
  
    System.out.println(cad);  
      
      
} catch (IOException e) {  
    throw new RuntimeException(e);  
}
```

## 11. Ficheros XML. Analizadores sintáticos (parser) y vinculación (binding)

### 11.1. Conceptos previos y definiciones

Se llama **parsing XML** o **análisis léxico-sintáctico XML** , llevado a cabo por parsers o analizadores de XML al proceso mediante el cual se lee y analiza un documento XML para comprobar que está bien formado y, posteriormente, pasar el contenido a una aplicación cliente que necesite consumir esa información.

La aplicación que consume información XML debe:
- Leer fichero de texto codificado
- Cargar información en memoria
- Procesar esos datos para obtener resultados

Se llama **schema** a la especificación XML que dicta los componentes permitidos en un documento XML y las relaciones entre componentes. 

Los XML deben estar bien formados y, si tienen schema, deben ser válidos. 

### 11.2. Introducción JAXB

**JAXB** es Java Architecture for XML Binding, una interfaz que simplifica el acceso a documentos XML representando la información obtenida del XML en formato Java.  (Vincular esquemas XML a representaciones Java)

A partir del documento XML se pueden obtener árboles de contenido para operar con ellos y generar documentos XML con la estructura inicial pero modificados.

- **Parsear** es escanear el documento y dividirlo lógicamente en piezas discretas
- **Binding**: Vincular un schema es generar el conjunto de clases Java que representan el esquema

Algunos parsers conocidos son SAX (Simple API for XML) o DOM (Document Object Model)

--------------

JAXB proporciona la capacidad de serializar (marshalling) objetos Java a XML y deserializar (unmarshalling) XML a objetos Java. 

Permite almacenar y recuperar datos en memoria en cualquier formato XML sin necesidad de implementar rutinas XML de carga y salvaguarda para la estructura de clases del programa.

**Compilador de esquema de JAXB** (schema compiler): Liga un esquema fuente a un conjunto de elementos de programa derivados. La vinculación se hace mediante lenguaje de vinculación basado en XML.
- **Binding runtime**: Framework que da operaciones de unmarshalling y marshalling para acceder, manipular y validar contenido XML usando un esquema derivado o elementos de programa.
- **Marshalling**: Aplicación cliente convierte el árbol de objetos Java JAXB a ficheros XML. Codificación de un objeto en un medio de almacenamiento, normalmente un fichero. El marshaller usa UTF-7 cuando genera los datos XML.
- **Unmarshalling**: Convertir datos XML a objetos Java JAXB derivados. 

En definitiva, permite generar una serie de clases Java que podrán ser llamadas en las aplicaciones a través de métodos getter y setter para obtener o establecer los datos de un documento XML.
### 11.3 Funcionamiento JAXB

1. **Escribir el esquema**
2. Generar los **ficheros fuente de Java** (POJOs) usando el **compilador de esquema**
3. **Construir el árbol de objetos de Java** (árbol de objetos o árbol de contenido) instanciando las clases generadas o invocando el método `unmarshall` de una clase generada y pasarlo en el documento (toma un documento XML válido y construye una representación de árbol de objetos)
4. **Acceder al árbol de contenido con la aplicación y modificar los datos**
5. **Generar documento XML** desde el árbol de contenido. Invocando al método marshall sobre el objeto raíz del árbol. 

**Funcionamiento ampliado de JAXB**.
>- Crear un esquema (fichero .xsd) que contendrá las estructura de las clases que deseamos utilizar.
>- Compilar con el JAXB compiler (bien con un IDE como NetBeans o desde línea de comandos con el comando **xjc**) ese fichero .xsd, de modo que nos producirá los POJOs, o sea, una clase por cada uno de los tipos que hayamos especificado en el fichero .xsd. Esto nos producirá los ficheros .java.
>- Compilar esas clases java.
>- Crear un documento XML: validado por su correspondiente esquema XML, o sea el fichero .xsd, se crea un árbol de objetos.
>- Ahora se puede parsear el documento XML, accediendo a los métodos gets y sets del árbol de objetos generados por el proceso anterior. Así se podrá modificar o añadir datos.
>- Después de realizar los cambios que se estimen, se realiza un proceso para sobrescribir el documento XML o crear un nuevo documento XML.

------------

##### Ejemplito

- Tenemos un XMLSchema (albaran.xsd)
- Se crea un nuevo proyecto de tipo Java Application. En la ventana de proyectos se elige New > Other > XML > JAXB Binding. Se escribe un binding name y se selecciona el .xsd. Se generan los POJOs automáticamente. 
- Se crea un fichero XML (albaran.xml)
- Se crea una clase para modificar el fichero XML

```java
public class ModificaAlbaPed {  
    public static void main(String[] args) {  
        try {  
// Crear una instancia para poder manipular las clases generadas, que están en el paqute jaxb.albaran  
            JAXBContext jaxbContext = JAXBContext.newInstance("jaxb.albaran");  
  
// Crear un objeto de tipo Unmarshaller para convertir datos XML en un árbol de objetos Java  
            Unmarshaller u = jaxbContext.createUnmarshaller();  
  
// La clase JAXBElement representa a un elemento de un documento XML en este caso a un elemento del documento albaran.xml  
            JAXBElement jaxbElement = (JAXBElement) u.unmarshal(  
                    new FileInputStream("C:\\albaran.xml"));  
  
// El método getValue() retorna el modelo de contenido (content model) y el valor de los atributos del elemento  
            PedidoType pedidoType = (PedidoType) jaxbElement.getValue();  
  
// Obtenemos una instancia de tipo PedidoType para obtener un Objeto de tipo Direccion  
            Direccion direccion = pedidoType.getFacturarA();  
  
// Establecemos los datos  
            direccion.setNombre("Jose Javier");  
            direccion.setCalle("Zafiro 3");  
            direccion.setCiudad("Molina");  
            direccion.setProvincia("Murcia");  
            direccion.setCodigoPostal(new BigDecimal("30500"));  
  
// Crear un objeto de tipo Marshaller para posteriormente convertir el árbol de objetos Java a datos XML  
            Marshaller m = jaxbContext.createMarshaller();  
  
// Crear el resultado XML no formateado para lectura de las personas, con saltos de línea, etc  
            m.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, Boolean.TRUE);  
  
// Escribir el elmento obtenido como primer parámetro por la salida estándar, el segundo parámetro  
            m.marshal(jaxbElement, System.out);  
            // Si queremos actualizar el fichero usar 
            //m.marshal(jaxbElement, new FileOutputStream("albaran.xml"));
        } catch (JAXBException je) {  
            System.out.println(je.getCause());  
        } catch (IOException ioe) {  
            System.out.println(ioe.getMessage());  
        }  
    }  
}
```

## 12 Librerías para conversión de XML a otros formatos

Muchas empresas guardan información en ficheros o bases de datos con formatos XML.
Existen productos o herramientas informáticas para convertir documentos XML a otros formatos. 
Por ejemplo, en Lenguaje de marcas se ven las transformaciones XLS para convertir en XML, HTML, doc.

Veamos ahora **JasperReport**
### 12.1 JasperReport

Herramienta que consta de un poderoso motor para la generación de informes. Está escrita en Java, empaquetada en un JAR y puede usarse como librería. 
Es de código abierto y gratuita con licencia GPL. 
Permite generar informes de todo tipo en Java de una forma sencilla. En formatos PDF, XLS, HTML, RTF, CSV, XML...

Descarga: https://sourceforge.net/projects/jasperreports/files/jasperreports/

Una vez descargado en Netbeans se haría click en Tools > Libraries > New Library para añadir la librería.
En Classpath tab se añade el fichero `jasperreports-miversion.jar` de la carpeta `dist` y algunos `commons-....` que puedan ser necesarios. (beanutis, collections, digester, javaflow, logging). Igualmente se indica el directorio fuente (src) de JasperReport. 
En Javadoc se añade la carpeta API de jasperreports. 

Directorios al descomprimir:
- **build**: Librería JasperReports sin empaquetar
- **demo**: Ejemplos de uso de la librería. Algunos preparados para ser compilados con Ant
- **dist**: Librería empaquetada en fichero JAR 
- **docs**: Referencia rápida en formato XML
- **lib**: Librerías necesarias para JasperReports (exportar distintos formatos, incluir gráficos)
- **src**: Ficheros fuente de la librería

#### A. Diseño

Las plantillas de JasperReports son ficheros XML con extensión **.jrxml**. Es un archivo XML que mantiene la estructura de un archivo DTD definido en el motor de JasperReports.
Debe estar validada con
```xml
<!DOCTYPE jasperReport PUBLIC "-//JasperReports//DTD Report Design//EN" "http://jasperreports.sourceforge.net/dtds/jasperreport.dtd">
```

Puede ponerse en Maven con 
```xml
<dependency>  
    <groupId>net.sf.jasperreports</groupId>  
    <artifactId>jasperreports</artifactId>  
    <version>3.7.5</version>  
</dependency>
```

(Última versión **6.21.3**; 17 de abril de 2024)

Tiene las secciones:
- **title**: Título del informe
- **pageHeader**: Encabezado del documento
- **columnHeader**: Encabezado de las columnas
- **detail**: Detalle del documento. Cuerpo.
- **columnFooter**: Pie de la columna
- **pageFooter**: Pie del documento
- **summary**: Cierre del documento

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jasperReport xmlns="http://jasperreports.sourceforge.net/jasperreports"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://jasperreports.sourceforge.net/jasperreports http://jasperreports.sourceforge.net/xsd/jasperreport.xsd"
              name="reporte_ejemplo"
              pageWidth="595" pageHeight="842"
              columnWidth="555" leftMargin="20" rightMargin="20" topMargin="20" bottomMargin="20"
              uuid="ce7f8d0b-d7b7-4d3d-8b12-36240dc238b8">
    
    <!-- Título del informe -->
    <title>
        <band height="50">
            <staticText>
                <reportElement x="0" y="0" width="555" height="50" uuid="517e32af-64c4-4b82-860a-2d6506be0294"/>
                <textElement textAlignment="Center">
                    <font size="20" isBold="true"/>
                </textElement>
                <text><![CDATA[Título del Informe]]></text>
            </staticText>
        </band>
    </title>
    
    <!-- Encabezado de página -->
    <pageHeader>
        <!-- Aquí puedes colocar elementos como el nombre de la empresa, el logotipo, etc. -->
    </pageHeader>
    
    <!-- Encabezado de columnas -->
    <columnHeader>
        <band height="30">
            <!-- Definición de las cabeceras de las columnas -->
            <staticText>
                <reportElement x="0" y="0" width="100" height="30" uuid="062a35ff-8499-47e5-b61e-0bbec74a5ab0"/>
                <text><![CDATA[Nombre]]></text>
            </staticText>
            <staticText>
                <reportElement x="100" y="0" width="100" height="30" uuid="287c1601-8b21-4389-b26e-d6e8a0ec2330"/>
                <text><![CDATA[Apellido]]></text>
            </staticText>
            <staticText>
                <reportElement x="200" y="0" width="100" height="30" uuid="cc7ad76e-d167-4f48-b869-b5de16171e7b"/>
                <text><![CDATA[Edad]]></text>
            </staticText>
        </band>
    </columnHeader>
    
    <!-- Detalle del informe -->
    <detail>
        <band height="30">
            <!-- Aquí se colocarían los datos de cada registro -->
        </band>
    </detail>
    
    <!-- Pie de columna -->
    <columnFooter>
        <!-- Aquí puedes incluir sumarios o totales parciales para las columnas -->
    </columnFooter>
    
    <!-- Pie de página -->
    <pageFooter>
        <!-- Aquí se incluiría información como números de página, fechas, etc. -->
    </pageFooter>
    
    <!-- Resumen del informe -->
    <summary>
        <!-- Aquí se colocaría cualquier información de resumen o cierre del informe -->
    </summary>
</jasperReport>

```

#### B. Compilación

Debe compilarse tras el diseño. Se hace a través del método `compileReport()`. El diseño se transforma en objeto serializable de tipo net.sf.jasperreports.engine.JasperReport que se guarda en disco. 

#### C. Rellenar el informe con datos

Los métodos `fillReportXXXX()` realizan la carga de datos del informe, pasándole como parámetros el objeto de diseño (o el archivo que lo representa en formato serializado .jasper) y la conexión JDBC a la base de datos desde donde se obtendrá la información que se necesite. 

Se obtiene un objeto que representa al documento listo para ser impreso, un objeto serializable de tipo `JasperPrint`. Este objeto puede ser guardado en disco, impreso, enviado a pantalla, transformado en PDF, XLS, XSV...
#### D. Visualización

Se puede mostrar un informe por pantalla, imprimirlo, obtenerlo en tipo específico de fichero...

**Mostrar informe por pantalla**: `JasperViewer` que en su método `main()` recibe el informe a mostrar
**Imprimir el informe**: `JasperPrintManager` Métodos `printReport()`, `printPage()`, `printPages()`
**Exportar los datos a formato de archivo específico**: `exportReportXXX()`

### 12.2. JasperReports y NetBeans

- Crear proyecto de tipo Java Application y darle nombre
- Botón derecho sobre el nombre del proyecto > Properties > Categories > Libraries > Add Library > elegimos JasperReports-xxxx > Add Library > Ok
- Carpetas en las que se guardarán las plantillas y los informes generados. `report` y como subdirectorios `templates` y `results`. 
- Se crea plantilla File > Empty File . `HolaMundo.jrxml`con el siguiente código:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE jasperReport PUBLIC "-//JasperReports//DTD Report Design//EN" "http://jasperreports.sourceforge.net/dtds/jasperreport.dtd">
<jasperReport name="HelloReportWorld">
    <parameter name="author" class="java.lang.String"/>

    <detail>
        <band height="200">
            <staticText>
                <reportElement x="0" y="0" width="500" height="20"/>
                <text><![CDATA[Informe ¡Hola Mundo!]]></text>
            </staticText>
        </band>
    </detail>
    <columnFooter>
        <band height="200">
            <textField>
                <reportElement x="0" y="0" width="200" height="30"/>
                <textElement>
                    <font size="14" isBold="true"/>
                </textElement>
                <textFieldExpression><![CDATA["Autor: " + $P{author}]]></textFieldExpression>
            </textField>
        </band>
    </columnFooter>
</jasperReport>
```


- Y el código siguiente: 
```java
public class Main {
    public static void main(String[] args) throws Exception {
        String reportSource = "src/main/resources/reports/templates/HolaMundo.jrxml";
        String reportsDest = "src/main/resources/reports/results/HolaMundo";

        Map<String, Object> params = new HashMap<>();
        params.put("author","romoreno-dev");
        try {
            JasperReport jasperReport = JasperCompileManager.compileReport(reportSource);
            JasperPrint jasperPrint = JasperFillManager.fillReport(jasperReport, params, new JREmptyDataSource());

            JasperExportManager.exportReportToHtmlFile(jasperPrint, reportsDest+".html");
            JasperExportManager.exportReportToPdfFile(jasperPrint, reportsDest+".pdf");

            JasperViewer.viewReport(jasperPrint);
        } catch (JRException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

- **JasperCompileManager.compileReport**: Toma la plantilla jrxml y la compila a bytecode (instancia `JasperReports`), serializable a disco como fichero jasper. Las plantillas compiladas pueden (y deben) reutilizarse sin recompilarlas salvo que cambie el código fuente de la plantilla. 
 
- **JasperFillManager.fillReport**: Toma el informe compilado (instancia `JasperReports`), unos parámetros definidos por el desarrollador y unos datos `JasperReports` y rellena la instancia informe con parámetros y datos retornando una instancia `JasperPrint`. Esta es una representación de objeto del informe completo. 
        
- **JasperExportManager.exportReportToHtmlFile**: Con la instancia `JasperPrint` y la ruta de destino de fichero  se crea fichero HTML con contenido del informe. 

Se admiten formatos PDF, XML, CSV (comma-separated values), XLS, RTF, fichero de texto y se pueden crear ficheros de formato personalizados para exportar con la API extensible de JasperReports. 

- **JasperExportManager.viewReport**. Muestra el informe generado en el visor **JasperReport Viewer.**