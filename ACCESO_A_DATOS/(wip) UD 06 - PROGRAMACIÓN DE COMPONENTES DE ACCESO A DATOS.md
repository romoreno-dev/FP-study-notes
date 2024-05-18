
## 1. Concepto de componente. Características

**Componente software**: Clase creada para ser reutilizada y que puede ser manipulada por una herramientas de desarrollo de aplicaciones visual. Se define por su _estado_ que se almacena en un conjunto de **propiedades**, que pueden ser modificadas para adaptar el componente al programa en el que se inserta. Tiene un **comportamiento** que se define por los _eventos_ antes los que responde y los _métodos_ que ejecuta ante dichos eventos. 

Los componentes:
- Tienen una** interfaz bien definida** formada por sus **propiedades** y **métodos**
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

Esto se consigue:
- Mediante **reflexión** (API Reflection `java.lang.reflect` de Java) que busca los métodos definidos por get o set, establece reglas en la construcción de la clase para que mediante esa nomenclatura específica se puede encontrar la interfaz del componente (esto es un "patrón de diseño" dicen los apuntes).
- Examinando una clase asociada de información del componente `BeanInfo` que describe sus características para ser reconocidos. 

## 6. Persistencia del componente



## 7. Propiedades simples e indexadas



## 8. Propiedades compartidas y restringidas



## 9. Herramientas para el desarrollo de componentes visuales



## 10. Empaquetado de componentes



## 11. Elaboración de un componente de ejemplo



