
## 1. Concepto de componente. Características

**Componente software**: Clase creada para ser reutilizada y que puede ser manipulada por una herramientas de desarrollo de aplicaciones visual. Se define por su _estado_ que se almacena en un conjunto de **propiedades**, que pueden ser modificadas para adaptar el componente al programa en el que se inserta. Tiene un **comportamiento** que se define por los _eventos_ antes los que responde y los _métodos_ que ejecuta ante dichos eventos. 

Los componentes:
- Tienen una **interfaz bien definida** formada por sus **propiedades** y **métodos**
- Se **distribuyen mediante un paquete instalable** con lo necesario para su funcionamiento
- Deben ser **independientes de otras bibliotecas** y componentes.
Es considerado componente si:
- **Se puede modificar para adaptarse a la aplicación** en que se integra
- Tiene **persistencia**, se guarda el estado de sus propiedades cuando han sido modificadas
- Tiene **introspección**, permite a un IDE reconocer elementos de diseño como nombres de funciones miembro o métodos y definiciones de clase y devolver la información
- Puede gestionar **eventos**.

**Ventajas**
- Más sencillo
- Menos tiempo en desarrollar
- Coste inferior
- Disminuyen errores de software gracias al control de calidad

Los controles gráficos de interfaz usados en NetBeans o Designer de QT cumplen con los requisitos para ser componentes: elementos reutilizables, manejados por una herramienta de desarrollo visual (modificar tamaño, color, permanecen después de cerrarla, tienen interfaz formada por métodos y propiedades accesibles...)

El componente busca recoger en una entidad que sea fácilmente reutilizable un segmento de código con funcionalidad cerrada. Ventajas como reutilización, disminución de código, más robustez y tolerancia a fallos al estar ampliamente probados.

## 2. Propiedades y atributos

El estado queda definido por un conjunto de **atributos**: Variables definidas por el nombre y el tipo de dato que toman valores completos. Suelen ser privados y no verse desde fuera. 

Las **propiedades** son un tipo de atributo que representa características del componente (apariencia, comportamiento) y son accesibles desde fuera de la clase, formando parte de su interfaz. Suelen estar asociadas a un atributo interno.

Accesible es que tiene **getter** (leer valor) y **setter** (establecer valor)

```java
public <TipoPropiedad> get<NombrePropiedad>();
public boolean is<NombrePropiedad>();
public void set<NombrePropiedad>(<TipoPropiedad> valor);
```

Distinguiremos entre
- Propiedades **simples**: Representan un único valor
- Propiedades **indexadas**: Un array de valores
- Propiedades **ligadas**: Notifican a listeners cuando el valor de la propiedad cambia, permitiéndoles hacer alguna acción.  Se hace creando un evento que contiene información acerca de la propiedad (nombre, valor previo, nuevo valor) y lo pasa a los listeners interesados en el cambio.
- Propiedades **restringidas**: Similar a ligadas pero los listeners tienen opción de vetar cualquier cambio en el valor de dicha propiedad. 
#### El primer JavaBean

(Veamos Oracle Forms: Producto de software para crear pantallas que interactúan con BBDD Oracle.)

1. Crear nueva aplicación desde JDeveloper
2. Crear nuevo proyecto
3. Crear clase de Java `Timer`
4. Incorporar al proyecto la librería `frmall.jar`
5. La clase `Timer.java`:
```java
import oracle.forms.ui.VBean;
import oracle.forms.properties.ID;
import oracle.forms.handler.IHandler;
import oracle.forms.ui.CustomEvent;
import java.lang.Runnable;

public class Timer extends VBean implements Runnable
{
	static IHandler mHandler;

	// Propiedades de la clase
	protected static final ID POWER = ID.registerProperty("POWER");
	protected static final ID TIME = ID.registerProperty("TIME");
	protected static final ID REPEAT = ID.registerProperty("REPEAT");
	
	//Valor enviado al formulario cuendo timer expira
	protected static final ID AVISOTIMEREXPIRADO = ID.registerProperty("AVISOTIMEREXPIRADO");
	
	//Constructor
	public Timer() {
		super();
	}
	
	//Inicialización de la clase
	public void init (IHandler handler) {
		super.init(handler);
		mHandler = handler;
	}
	
	// Al usar en el formulario la p.u. Set_Custom_Property
	public boolean setProperty(ID property, Object value) {
		if (property == POWER) {
			String sParam = (String)value ;
		}
	}

	// Desde Java para comunicarse con el formulario. Se dispara el trigger WHEN-CUSTOM-ITEM-EVENT del item tipo "Bean Area" donde se ha asignado la clase Timer.jar
	public Object getProperty(ID property)
	{
		if (property == TIME)
		{
		}
	}
	
	//Envío de un mensaje al formulario
	public void dispatch_event() {
		CustomEvent ce = new CustomEvent(mHandler, AVISOTIMEREXPIRADO);
		dispatchCustomEvent(ce);
	}
}
```

6. Deploy to JAR file

7. El JavaBean desde el formulario se usa:


-  (set) Asignar valor a propiedad del JavaBean
`Set_Custom_Property( ‘item_name’, record_number, ‘property_name’, ‘property_value’ ) ;`

- (get) Recuperar valor de propiedad del JavaBean
`Varchar2 := Get_Custom_Property( ‘item_name’, record_number, ‘property_name’ ) ;`

- Crear item del tipo "Bean Area" y asiognar el nombre de la clase. El tipo BeanArea debe tener Canvas asignado.
- Crear trigger WHEN-CUSTOM-ITEM-EVENT en el item "Bean Area". Se disparará cuando el Timer expire
- Crear items para que el usuario decida el tiempo en ms y si el timer se ha de repetir o no
- Crear botón para arrancar el timer

```
set_custom_property('B.TIMER', 1, 'TIME', :TIME);
set_custom_property('B.TIMER', 1, 'REPEAT', :REPEAT);
set_custom_property('B.TIMER', 1, 'POWER', 'START');
```

- Crear botón para parar el timer
`set_custom_property('B.TIMER', 1, 'POWER', 'STOP');`

- Crear botón para recuperar valores de propiedades del timer
```
GET_TIME := get_custom_property('B.TIMER', 1, 'TIME');
:GET_REPEAT := get_custom_property('B.TIMER', 1, 'REPEAT');
```

8.  Copiar fichero Timer.jar en <ORACLE_HOME>\\forms\\Java
9. Formsweb.cfg   archive_jini=...,Timer.jar

## 3. Editores de propiedades

El componente debe identificar sus propiedades detectando parejas de operaciones get/set mediante introspección.

El entorno de desarrollo podrá editar automáticamente cualquier propiedad de tipos básicos o de clases `Color` y `Font`. Si es algo más complejo habrá que crear un editor de propiedades propio, esto es, una herramientas para personalizar un tipo de propiedad en particular. 

Los editores de propiedades se usan en la ventana propiedades, determinando el tipo de propiedad, buscando un editor de propiedades apropiado y mostrando el valor actual de la propiedad.

En tecnología Java esto es programar una clase que implemente la interfaz `PropertyEditor` que da métodos específicos sobre cómo mostrar una propiedad en la hoja de propiedades. El nombre de la clase debe ser el de la propiedad seguido de la palabra Editor. 

`PropertyEditorSupport`, que implementa `PropertyEditor`da los editores más empleados, incluyendo tipos básicos, `Color` y `Font`. (No habría por ejemplo para atributos compuestos)

Al tener todos los editores, la clase debe empaquetarse con el componente para que use el editor creado cuando se necesite editar la propiedad. Así, al añadir un componente en un panel, aparecerá la hoja de propiedades con la lista de propiedades del componente y los editores asociados en cada una de ellas. El IDE llama a los métodos getter para mostrar el valor, si cambia el valor llama al método setter para actualizarlo. Esto puede afectar (o no) al componente en el momento del diseño. 

-----

El `JavaBean` debe
- Implementar `Serializable`
- Tener constructor sin parámetros
- Tener introspección. Los IDES deben reconocer ciertas pautas de diseño para conocer sus propiedades y conducta.

## 4. Eventos. Asociación de acciones a eventos

Los componentes reaccionan ante acciones del usuario (click del ratón, pulsación de una tecla). Esto genera un **evento** que el componente captura y procesa ejecutando alguna función. El componente también puede **lanzar evento y que el tratamiento sea en otro objeto**. 

El componente reconoce el evento y responde ante él si:
- Se crea una clase para los eventos que se lancen
- Se define una interfaz que represente el listener asociado al evento (Con una operación que procese el evento)
- Se definen dos operaciones para añadir y para eliminar listeners. Si tiene más de un listener deben almacenarse internamente esos oyentes en estructuras como `ArrayList` o `LinkedList`

## 5. Introspección. Reflexión

**Introspección**: Permite a las herramientas de programación visual arrastrar y soltar un componente en la zona de diseño determinando dinámicamente qué métodos de interfaz, propiedades y eventos del componente están disponibles.

Esto se consigue en los JavaBeans:
- Mediante **reflexión** (API Reflection `java.lang.reflect` de Java) que busca los métodos definidos por get o set, establece reglas en la construcción de la clase para que mediante esa nomenclatura específica se puede encontrar la interfaz del componente (esto es un "patrón de diseño" dicen los apuntes).
- Examinando una clase asociada de información del componente `BeanInfo` que describe sus características para ser reconocidos. 

## 6. Persistencia del componente

**Persistencia**: Almacenar el estado de una clase para que perdure a través del tiempo. Para hacerlo, debe almacenarse en un archivo y ser recuperado posteriormente. 

Se llama **serializar** al proceso de almacenar el estado de la clase en un archivo y **deserializar** al proceso de recuperarlo.

Como todos los componentes deben persistir todos deben implementar la interfaz `java.io.Serializable` (serialización automática) o `java.io.Externalizable` (serialización programada).

##### **Serialización automática o serialización por defecto**:
- Implementa interfaz `Serializable`. Serialización automática mediante uso de _Java Object Serialization_.
Para ello: 
- Las clases deben tener constructor sin argumentos que será llamado cuando un objeto sea "reconstituido" desde un fichero `.ser`
- Todos los campos son serializados, salvo `static` y `transient`.  Así, con el modificador `transient` se podrán especificar los campos que no se quieren serializar y las clases que no son serializables. 
- Se puede programar una serialización propia si es necesario implementando los métodos `writeObject` y `readObject`
```java
private void writeObject(java.io.ObjectOutputStream out) throws IOException;
private void readObject(java.io.ObjectInputStream in) throws IOExcept;
```
#### **Serialización programada:**
- El componente implementa la interfaz `Externalizable` y sus dos métodos para guardar el componente con un formato específico.
Para ello:
- Debe tener constructor sin argumentos
- Necesita implementación de los métodos `readExternal()` y `writeExternal()`

## 7. Propiedades simples e indexadas

Propiedad **simple**:
- Representa un único valor, número, booleano o texto.
- Tiene asociados los métodos getter y setter para rescatar ese valor y, obviamente, será de solo lectura o de solo escritura si falta alguno de estos métodos de acceso.

Propiedad **indexada**: Es un conjunto de elementos, que suelen representarse mediante un lector y suele identificarse mediante los siguientes patrones de operaciones para leer o escribir elementos individuales del vector o el vector entero.
Es útil para propiedades en las que no se tiene un número concreto (no se sabe cuántos elementos va a tener)

```java
public <TipoProp>[] get<NombreProp>()
public void set<NombreProp> (<TipoProp>[] p)
public <TipoProp> get<NombreProp>(int posicion)
public void set<NombreProp> (int posicion, <TipoProp> p)
```

Veamos un ejemplillo de propiedad indexada:
```java
private String[] miembros = new String[0];  

public String[] getMiembros() {  
    return miembros;  
} 

public void setMiembros(String[] miembros) {  
    this.miembros = miembros;  
}  

public String getMiembros(int posicion) {  
    return miembros[posicion];  
}  
  
public void setMiembros(int posicion, String miembro) {  
    this.miembros[posicion] = miembro;  
}
```

## 8. Propiedades compartidas y restringidas

##### Propiedad compartida
Una clase tiene **propiedad compartida o ligada** si:
- Posee una propiedad que puede cambiar
- Notifica a otros objetos interesados cuando el valor de esta propiedad cambia

**Al cambiar la propiedad**, se crea un objeto (de una clase heredada de `ObjectEvent`) que contiene información como nombre, valor precio y nuevo valor y lo pasa a otros objectos oyentes interesados en el cambio.

**Los oyentes deben ser registrados o desregistrados como auditores en la clase que contiene la propiedad**

**Registrar oyentes para cualquier propiedad de la clase.**
```java
public void addPropertyChangeListener (PropertyChangeListener l)
public void removePropertyChangeListener (PropertyChangeListener l)
```

**Registrar oyentes para propiedades específicas.**
```java
public void addPropertyNameListener(PropertyChangeListener l) public void removePropertyNameListener(PropertyChangeListener l)
```

La notificación del cambio se realiza a través de la generación de un `PropertyChangeEvent`. 

**Los objetos que desean escuchar los cambios** implementan la interfaz `PropertyChangeListener`. Esta interfaz tiene un método `propertyChange(PropertyChangeEvent e)` que debe ser implementado. Este método es llamado cada vez que haya un cambio en la propiedad. 

##### Propiedad restringida
Similar a la propiedad ligada pero en este caso los objetos oyentes a los que se les notifica el cambio tienen la opción de veta cualquier cambio en el valor de dicha propiedad.

Se aplican los métodos de propiedades simples e indexadas y, también, estos métodos de registro de eventos:
```java
public void addPropertyVetoableListener(VetoableChangeListener l)
public void removePropertyVetoableListener(VetoableChangeListener l)
public void addPropertyNameListener(VetoableChangeListener l)
public void removePropertyNameListener(VetoableChangeListener l)
```

Los objetos con capacidad de escuchar  y vetar implementan la interfaz `VetoableChangeListener`con el método `vetoableChange()`
Si no aprueban el cambio pueden arrojar un `PropertyVetoException` para informar al componente de que el cambio no se ha aprobado.
## 9. Herramientas para el desarrollo de componentes visuales

**BeanBox**: Primera herramienta creada para trabajar con JavaBeans. Puede definirse como un contenedor de Beans. En ella se pueden escribir los Beans y luego arrastrarlos dentro del BeanBox y comprobar si funcionan cómo se esperan. Fue sustituida por Netbeans.

**BeanBuilder**:  Versión mejorada de BeanBox. Se daba un enfoque al proyecto que se desarrollaba porque permitía el enlazado de componentes de forma gráfica y ver sus propiedades en tiempo de diseño pero sin crear archivos `.ser` para la serialización sino usando archivos XML.

**Netbeans**: Proporciona base completa para todo el ciclo de vida de creación del Bean y ayudas para la escritura de código (añadir propiedades, getter, setter, generación de eventos... Además es muy sencillo desde el administrador de paleta incorporar nuevos beans desde sus archivos .jar y añadirlos a una aplicación)
Además permite la creación de la clase `BeanInfo` para el componente, que puede gestionar el modo en el que el componente aparece en la herramienta de desarrollo indicando qué propiedades deben aparecer, cuáles deben estar ocultas, si hay un editar de propiedades asociado... es una de las bases de la introspección en Java. 

Se puede generar un BeanInfo automáticamente desplegando el menú contextual de la clase que implementa el componente en el inspector de proyectos de NetBeans y seleccionando "Editor BeanInfo". Si no existe, preguntará si se quiere crear y tras esto mostrará el código. 
Este método permite manejo de propiedades heredadas de forma automático desde el BeanInfo (ejemplo, cuando la clase hereda de `JPanel` o `JFrame`)
## 10. Empaquetado de componentes

El componente debe empaquetarse para poder distribuirlo después. Es necesario un paquete `jar` con todas las clases que forman el componente (o componentes porque pueden incluirse varios en un mismo jar):
- Componente
- Objetos `BeanInfo`
- Objetos `Customizer`
- Clases de utilidades o recursos que requiera el componente

El jar debe incluir un fichero de manifiesto (.mf) que describa su contenido. La clase del componente va acompañada de Java-Bean: True, indicando que se trata de un JavaBean.

```.mf
Manifest-Version: 1.0
Name: demo/Componente.class
Java-Bean: True
Name: demo/ComponenteBeanInfo.class
Java-Bean: False
Name: demo/ClaseAuxiliar.class
Java-Bean: False
Name: demo/Imagen.png
Java-Bean: False
```

El .jar se genera con Netbeans mediante **Clean and Build**, que deja el .jar en el directorio /dist del proyecto.
También se puede hacer por consola:
```shell
jar cfm Componente.jar manifest.mf Componente.class ComponenteBEanInfo.class ClaseAuxiliar.class Imagen.png proyecto.jar
```

## 11. Elaboración de un componente de ejemplo

El uso de componentes está muy relacionado con la creación de aplicaciones web.

La tecnología **JSP** emplea el Modelo-Vista-Controlador (MVC) para separar el desarrollo de la base de datos (Modelo), de la interfaz hecha con HTML en combinación con JSP (Vista), de la lógica de negocio (Controlador) cuya implementación más sencilla y fácil de gestionar por JSP es un JavaBean que acceda a la base de datos y recupere fácilmente la información que contiene.

### 11.1 Modelo

Se plantea una base de datos muy sencilla en MySQL:

Aquí las sentencias DDL y DML

```sql
-- 
-- Base de datos: `alumnos` 
-- 
-- -------------------------------------------------------- 
-- 
-- Estructura de tabla para la tabla `alumnos` 
-- 
CREATE TABLE IF NOT EXISTS `alumnos` ( 
  `DNI` varchar(9) NOT NULL, 
  `Nombre` varchar(50) NOT NULL, 
  `Apellidos` varchar(70) NOT NULL, 
  `Direccion` varchar(100) NOT NULL, 
  `FechaNac` date NOT NULL, 
  PRIMARY KEY (`DNI`) 
) ENGINE=MyISAM DEFAULT CHARSET=latin1; 
-- 
-- Volcar la base de datos para la tabla `alumnos` 
-- 
INSERT INTO `alumnos` (`DNI`, `Nombre`, `Apellidos`, `Direccion`, `FechaNac`) VALUES 
('12345678A', 'José Alberto', 'González Pérez', 'C/Albahaca, nº14, 1ºD', '1986-07-15'), 
('23456789B', 'Almudena', 'Cantero Verdemar', 'Avd/ Profesor Alvarado, n27, 8ºA', '1988-11-04'), 
('14785236d', 'Martín', 'Díaz Jiménez', 'C/Luis de Gongora, nº2.', '1987-03-09'), 
('96385274f', 'Lucas', 'Buendia Portes', 'C/Pintor Sorolla, nº 16, 4ºB', '1988-07-10');
```

### 11.2 Controlador (lógica del modelo)

Representa la lógica de negocio de una aplicación (parte del sistema que se encarga de las tareas relacionadas con los procesos de un negocio, como ventas, control de inventario, contabilidad...). Encapsula las reglas de negocio (políticas, normas, operaciones, definiciones y restricciones presentes en una organización y que son de vital importancia para alcanzar los objetivos para los que esta se creo) en componentes fáciles de probar, mejoran la calidad del software y promueve la reutilización.

El estado define el conjunto actual de valores del modelo e incluye métodos para cambiar esos valores; estos recogen parte de la lógica de negocio. Deben ser independientes del protocolo para acceder a ellos. 

El componente se encarga de conectar con la base de datos y ejecutar la sentencia deseada. A través de los métodos puede posicionarse en cada fila de la consulta y almacena en las propiedades cada uno de los campos. Las acciones definen los cambios permitidos para los estos en respuesta a los eventos. 

----

Los pasos para elaborar un componente son:
1. Creación del componente
2. Adición de propiedades
3. Implementación de su comportamiento
4. Gestión de los eventos
5. Uso de componentes ya creados en NetBeans
-----
### 11.3 Estructura del JavaBean

- Propiedades que se corresponden con los campos de la tabla alumnos
- Clase auxiliar `Alumno` para crear un vector de alumnos donde se cargará el contenido de la tabla
- Vector de alumnos
- Constructor (sin argumentos) que:
	- Realiza conexión a BBDD
	- Realiza consulta
	- Guarda resultados en estructura local al componente
	- Establece valores de propiedades
	- Cierra la conexión
- Métodos para recorrer los resultados recargando las propiedades cada vez que cambien
	- `obtenerFilas()`: Hace consulta sobre la base de datos y almacena los resultados sobre un vector interno, actualizando propiedades. 
	- `seleccionarFilas(i)`: Se posiciona en elemento i del vector y actualiza las propiedades
	- `seleccionarDNI(String DNI)`: Busca en vector interno registro que coincide con DNI y actualiza propiedades. 

### 11.4 Creación del componente

- Se crea un proyecto Netbeans de tipo **Java Application** (sin clase principal y sin configurar como proyecto principal). El proyecto se llama **AlumnoBean**. 
- Se añade un archivo nuevo de tipo Componente JavaBeans (debe implementar Serializable para gestionar la persistencia del componente y tener constructor sin argumentos)

### 11.5 Añadir propiedades

El componente tendrá como propiedades las mismas que los campos de la base de datos. Se declaran los atributos `private` o `protected` y los métodos `getter` y `setter`, base de la instrospección.

El asistente de NetBeans permite indicar propiedades indexadas o restringidas, simplemente marcándolo.

### 11.6 Implementar el comportamiento

Se programa el comportamiento del componente. 
La idea es que al crear el componente se cargue el contenido de la tabla alumno de la base de datos en un vector de uso interno que va a servir para no tener que estar conectándonos constantemente (gran cantidad de accesos por parte de múltiples usuarios que pueden llegar a saturar la base de datos). Se programa el constructor para que realice la carga de datos. En un primer momento los valores de las propiedades serán los del primer alumno recuperado.

Se generan un par de métodos para recuperar información de un registro según su posición o según su clave.

### 11.7 Gestión de eventos

Eventos: Para generar acciones en respuesta a los cambios de estado. 
Los componentes Java usan el modelo de delegación de eventos para gestionar la comunicación entre objetos.

Cada vez que se inserte un alumno nuevo que generará un evento que alerte de esta modificación.
- Una **clase** que implemente los eventos. Esta clase hereda de `java.util.EventObject` En el ejemplo se llamará **BDModificadaEvent**.
- Una **interfaz** que defina los métodos a usar cuando se genere el evento. Implementa `java.util.EventListener`. En este caso la gestión del evento se hará a través del método **capturarBDModificada** de la interfaz **BDModificadaListener**. También se tiene un objeto de tipo **DBModificadaListener** llamado receptor que representa aquellos programas que contienen al componente AlumnosBean susceptibles de recibir el evento.
- Dos métodos, `addEventoListener` y `removeEventoListener` que permitan al componente añadir oyentes y eliminarlos. En principio se deben encargar de que pueda haber varios oyentes. Solo se va a tener un oyente, pero se suele implementar para admitir a varios.
- Implementar el método que lanza el evento, asegurándose de que todos los oyentes reciban el aviso. En el ejemplo propuesto lo que se hace es lanzar el método que se creó en la interfaz que describe al oyente.


Interviene en la implementación del evento... Una clase que defina el evento y una interfaz que defina los métodos a implementar.

### 11.8 Uso de componentes previamente elaborados en Netbeans

Una vez construido, se incorpora a la paleta de Netbeans.
- Si es propio, se usa "Clean and Build" para generar el fichero .jar
- Si es de terceros, se necesita disponer del .jar

El fichero .jar se importa desde las propiedades del proyecto con la nueva aplicación. 

La gestión de eventos pasa por crear una clase que implemente la interfaz `BDModificadaListener`

```java
public class AccedeBD implements BDModificadaListener{

//en el constructor se indica  que se va a estar escuchando si se produce el evento:
AccedeBD()
{
         alumnos = new AlumnoBean();
         alumnos.addBDModificadaListener( (BDModificadaListener)this );
}

// se sobrescribe el método capturarBDModificada(BDModificadaEvent ev) para  escribir un mensaje cuando se produzca el evento.
public void capturarBDModificada(BDModificadaEvent ev)
{
    System.out.println("Se ha añadido un elemento a la base de datos");
}
```
