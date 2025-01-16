
Las **interfaces GUI (graphic user interface)** han ayudado a mejorar la productividad de muchas tareas y permiten que el usuario se acerque al mundo informático sin necesidad de poseer un conocimiento técnico. 

Las librerías se componen de clase y cada clase tiene unos métodos para su uso en la creación de GUIs: 
- **Component**: Superclase de todas las clases de la interfaz gráfica 
- **Container**: Agrupación de componentes
- **JComponent**: Se dibujan directamente los lienzos (canvas)

**Elementos básicos de la GUI**
- `JFrame`: Ventana principal de la aplicación (no contenida en más ventanas)
- `JDialog`: Cuadro de diálogo
- `JApplet`: DESAPARECIDÍSIMO!!!! Para crear applets tipo Swing. Subclase de `Applet`.
- `JPanel`: Contenedor invisible que mantiene componentes de la interfaz y que se puede anidar colocándose en otros paneles o ventanas. Sirve también de lienzo.
- `JScrollPane`: Panel con barras de desplazamiento. 

## 1. Concepto de componente y características

El **componente** tiene autonomía y funcionalidad para existir por sí solo y se puede adaptar a diferentes situaciones. 

El diseño de componentes permite diseño modular, con bajo acoplamiento.
Ejemplos: Conversos de monedas, conversiones de archivos,...

Las ventajas del **desarrollo de software basado en componentes** son:
- Reutiliza software
- Simplifica las pruebas: Pruebas probando cada componente antes de probar el conjunto completo
- Simplifica el mantenimiento del sistema: Desarrollador puede actualizar y/o agregar componentes según sea necesario
- Mayor calidad: La calidad de la aplicación basada en componentes mejora con el tiempo

Puede comprarse componentes a terceros que ya los tengan implementados permitiendo:
- Ciclos de desarrollo más cortos
- Mejor retorno sobre la inversión (ROI)
- Mejorar la funcionalidad

## 2. Propiedades y atributos

Veamos los controles predefinidos en Visual Studio. Los que pueden seleccionarse están definidos en una lista (caja de herramientas), siendo los más comunes en el diseño de interfaces: etiquetas, botones, desplegables.

En las **librerías WPF** los componentes se crean a partir de la clase `UserControl` y permiten heredar todas sus propiedades métodos y eventos. Debe elegirse la clase que más se acerque a las necesidades del usuario para ayudar al diseño en un menor tiempo de implementación.

![](DESARROLLO_INTERFACES/resources/ud03-1.png)

## 3. Elementos generales

**Importante**: La propiedad `name` debe definirse para todos los elementos de la interfaz para así conocer de forma rápida qué tipo de control representa ese identificador (en lugar de dejar su nombre por defecto).

Veamos elementos generales y alguna de sus propiedades

**Button**: Realiza una acción u otra de forma exclusiva.
- **Content**: Texto a mostrar
- **IsCancel**: Acción cuando se pulsa Esc
- **IsDefault**: Acción cuando se pulsa Intro
- **DataContext**: Controles dentro de un control contenedor de un origen de datos
- **IsEnabled**: Control activo o no
- **ToolTip**: Trozo de texto visualizable cuando se posiciona el puntero del ratón sobre el control

**TextField**: Caja de texto en la que el usuario puede introducir información
- **Text**: Texto que se introduce
- **UndoLimit**: Cantidad de operaciones de deshacer permitidas

**ListBox**: Lista con una serie de elementos que pueden ser seleccionados por el usuario.
- **Items**: Conjunto de elementos de la lista
- **ItemsSource**: Origen de los datos
- **SelectedIndex**: Elemento de la lista. Asigna el valor de -1 si no existe el elemento.

**ComboBox**: Lista de cajas de texto con sus propiedades correspondientes.
- **IsDropDownOpen**: Permite seleccionar un elemento de la lista
- **IsEditable**: Si la caja de texto es editable permite introducir texto
- **IsReadOnly**: No permite modificar los elementos. Es de solo lectura

**CheckBox**: Elemento que se va a utilizar para definir diferentes opciones pudiendo seleccionar más de una opción. 
- **ClickMode**: Especifica si puede liberarse el evento click. Tiene opciones Release (cuando se libera la pulsación), Press (cuando se produce la pulsación), Hover (cuando se pasa por encima)
- **Content**: Texto asociado al elemento
- **IsChecked**: Estado del elemento (seleccionado o no)
- **IsThreeState**: Especifica los tres estados diferentes que puede tener el control

**RadioButton**: Como el CheckBox pero con opciones excluyentes unas de otras. 

**Image**: Añadir imágenes en una interfaz haciendo referencia a los diferentes recursos.
- **Source**: Ruta del archivo
- **Strech**: Ajustar el tamaño de una imagen al espacio disponible de la aplicación
- **StrechDirection**: Forma en la que se lleva a cabo el ajuste

### 3.1. Creación básica de un componente WPF

Para crear un componente WPF puede partirse de la clase `UserControl` o reutilizar alguno(s) control(es).

- **Control personalizado**: Se puede partir de un control sencillo como el TextField. La caja de texto permite solo valores numéricos y, si se introduce otra cosa, avisa con mensaje de error. Puede iniciarse con el control propio `TextBox` y extender esta clase añadiendo la funcionalidad deseada. Puede añadirse la librería `PresentationFramework` dentro del proyecto. 
- **Definición de propiedades**: Las propiedades asociadas a los componentes gráficos se definen usando aquellas propiedades determinadas de una clase para hacer uso de sus comportamientos. Pueden ser simples o indexadas.
- **Testing del componente**: Para probarlo, es necesario otro proyecto que pueda ejecutarse por sí mismo. (Ej.: La aplicación de un formulario)
- **Métodos**: Crear métodos para componentes gráficos es similar a crear una función perteneciente a una clase que defina al componente. 

## 4. Eventos, asociación de acciones a eventos

**Evento**: Representa a la acción determinada que puede desempeñar un usuario y que está asociada a un componente específico. Al ejecutar un evento se producen una serie de acciones. 
### Creación de un evento

Se llama evento a la función que se desencadena tras haber realizado una acción sobre un componente en cuestión.
El **principal elemento de un evento** es el **manejador (handler)** especificado mediante:
```csharp
This.TextChanged+=new System.Windows.Controls.TextChangedEventHandler(manejador);
```

Siendo `manejador` una rutina que tiene una firma (signature) que cumple todos los requisitos que tiene asignados.

### Diseño de eventos

Se pueden diseñar de dos formas:
- Haciendo uso de un evento ya definido y modificarlo hasta conseguir adaptarlo a las necesidades del usuario
- Creando un evento desde cero partiendo de un nuevo componente

El manejador puede hacerse en la clase parcial de código asociada al archivo XAML. Es un método que tiene un subrutina (0pública o privada) en la clase. La subrutina cuenta con dos parámetros:
- El primero: **sender**. Representa el objeto asociado al manejador
- El segundo: con información específica sobre un determinado evento. 

### Eventos enrutados

El evento enrutado permite pasar un evento desde un hijo hasta sus padres (estructura de árbol).
Al propagarlo con una ruita ascendente, los manejadores asociados al evento puede compartir la instancia de datos del evento por lo que, con un cambio, este es propagado a partir de ese punto. En este caso el objeto **sender** cambiará siendo el elemento que esté asociado al manejador. 
### Escuchadores (listeners)

Encargados de controlar los eventos. Están a la escucha, esperando que el evento se produzca. Según cuál sea es necesario un listener u otro ya que estos están formados por una serie de métodos que se deben implementar aunque solo se use uno. Los listeners se encuentran en **java.awt.event**
### Asociación de acciones a eventos

#### Acciones

| MÉTODOS                                       | EVENTOS                                             | ESCUCHADOR                                                                              |
| --------------------------------------------- | --------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `public void actionPerformed (ActionEvent e)` | `JButton`: Clic o pulsar Intro cuando tiene el foco | `ACTIONLISTENER`: Clic sobre el componente o si se hace Intro cuando este tiene el foco |
|                                               | `JList`: Doble clic en un elemento de una lista     |                                                                                         |
|                                               | `JMenuItem`: Seleccionar una opción del menú        |                                                                                         |
|                                               | `JTextField`: Pulsar Intro cuando tiene el foco     |                                                                                         |
#### Tecla del teclado

| MÉTODOS                               | EVENTOS                                 | ESCUCHADOR                                                          |
| ------------------------------------- | --------------------------------------- | ------------------------------------------------------------------- |
| `public void keyTyped(KeyEvent e)`    | `keyTyped`: Al pulsar y soltar la tecla | `KEYLISTENER`: Al pulsar la tecla. Cambia la forma según el método. |
| `public void keyPressed(KeyEvent e)`  | `keyPressed`: Al pulsar la tecla        |                                                                     |
| `public void keyReleased(KeyEvent e)` | `keyReleased`: Al soltar la tecla       |                                                                     |

#### Focus

| MÉTODOS                                 | EVENTOS                               | ESCUCHADOR                                                                             |
| --------------------------------------- | ------------------------------------- | -------------------------------------------------------------------------------------- |
| `public void focusGained(FocusEvent e)` | `LostFocus`: Cuando se pierde el foco | `FOCUSLISTENER`: Cuando un componente gana o pierde el foco (el que está seleccionado) |
| `public void focusLost(FocusEvent e)`   |                                       |                                                                                        |

#### Click de ratón

| MÉTODOS                                   | EVENTOS                                          | ESCUCHADOR                                                          |
| ----------------------------------------- | ------------------------------------------------ | ------------------------------------------------------------------- |
| `public void mouseClicked(MouseEvent e)`  | `mouseClicked`: Pinchar y soltar                 | `MOUSELISTENER`:  Cuando se lleva a cabo alguna acción con el ratón |
| `public void mouseEntered(MouseEvent e)`  | `mouseEntered`: Entrar en componente con puntero |                                                                     |
| `public void mouseExited(MouseEvent e)`   | `mouseExited`: Salir de componente con puntero   |                                                                     |
| `public void mousePressed(MouseEvent e)`  | `mousePressed`: Presiona el botón                |                                                                     |
| `public void mouseReleased(MouseEvent e)` | `mouseReleased: Soltar el botón                  |                                                                     |
#### Movimiento de ratón

| MÉTODOS                                  | EVENTOS                                                    | ESCUCHADOR                                  |
| ---------------------------------------- | ---------------------------------------------------------- | ------------------------------------------- |
| `public void mouseDragged(MouseEvent e)` | `mouseDragged`: Click y arrastrar un componente            | `MOUSEMOTIONLISTENER`: Movimiento del ratón |
| `public void mouseMoved(MouseEvent e)`   | `mouseMoved`: Cuando se mueve un puntero sobre un elemento |                                             |

## 5. Persistencia del componente

La **persistencia** permite almacenar, recuperar y transferir el estado de los objetos. 

### 5.1. Serialización (Marshalling)

Se codifica un objeto en un medio de almacenamiento para transmitirlo a través de una conexión de red (en bits, en formato XML...). Pueden usarse esos formatos para replicar objetos idénticos al original, incluyendo su estado interno. 

Utilizado para transportar objetos a través de un red, para hacer persistente un objeto en un archivo o en una base de datos o para distribuir objetos idénticos en varios aplicaciones o localizaciones. 

### 5.2. Base de datos orientada a objetos

En este SGBD los objetos de la BBDD son objetos del lenguaje de programación. Así pueden trabajar bien con lenguajes como Java, C++, C# o Visual Basic.NET, mejorando el rendimiento a la hora de manipular tipos de datos complejos. Generan costes de desarrollo más bajos. 
### 5.3. Motor de persistencia

Traduce de objetos a registros y de registros a objetos. Tanto cuando se quiere grabar un objeto como cuando se quiere recuperarlo.
El motor de persistencia es el mismo para todas las aplicaciones. 

## 6. Herramientas para desarrollo de componentes visuales

El diseño de componentes visuales como botones e iconos puede hacerse con herramientas como:
- **GIMP**: Libre y versátil. Importante guardar relación adecuada en las dimensiones a la hora de diseñar un componente visual.
- **Adobe Photoshop**: Editor de gráficos rasterizados. Usado en retoque de fotografías y gráficos y también para crearlos; en buena calidad. 
- **Glade y Blend**: Glade permite desarrollar de forma rápìda interfaces de usuario almacenadas en XML. Blend permite crear interfaces de usuario en aplicaciones de escritorio Windows.


## 7. Java Swing

**Java Swing** es una biblioteca de interfaces gráficas de usuario (GUI) que forma parte de Java SE. Swing permite crear aplicaciones con interfaces gráficas ricas, basadas en componentes como botones, tablas, menús, etc. Todos los componentes Swing son parte del paquete `javax.swing` y extienden la clase `JComponent`.

### 7.0 Almacenes de componentes

### 7.1. Componentes y contenedores comunes en Java Swing

**Contenedores**: Son almacenes de componentes
- Superiores: `JApplet` (Deprecated, eliminado), `JFrame`, `JDialog`
- Intermedios: `JPanel`, `JScrollPane`, `JSplitPane`, `JTabbedPane`, `JToolbar` y otros más especializados.
-----

- **JFrame**: Ventana principal de aplicación Swing. Contenedor apropiado para todos los demás objetos.

- **JPanel**: Panel de contenedores para agrupar otros componentes (siempre recomendable que el `JFrame` tenga un `JPanel` encima). Componentes que permite desplegar textos o mensajes estáticos. 

- **JLabel**: Muestra texto o imágenes

- **JTextField**: Campo de texto de una sola línea Componente que permite capturar datos y/o desplegar datos o información.

- **JTextArea**: Campo de texto de varias líneas

- **JCheckBox**: Casilla de verificación 

- **JButton**: Botón. Permite controlar o dirigir conductas y codigos de los demás elementos de la aplicación.

- **JRadioButton**  y **JRadioGroup**: Botones de opción 

- **JSlider**: Seleccionar dato numérico de algún rango determinado

- **JTable**: Mostrar datos en formato de tabla

- **JComboBox**: Caja de selección 

- **JDialog**: Puede ser -según su tercer parámetro- modal (bloquea interacción con ventana principal) o no modal.

- **JOptionPane**: Forma más directa de mostrar mensajes simples, pedir entradas o confirmaciones sin necesidad de `JDialog

- *JMenuBar*. Es la barra de menú principal. Una barra horizontal alargada en la que se colocarán las distintas opciones. Si miras en tu navegador, arriba, verás una barra de estas con opciones como "Archivo", "Editar", etc.

- **JMenu**. Es una de las cosas que se pueden añadir a un `JMenuBar` o a otro `JMenu`. Cuando añadimos uno de estos, tendremos un algo que al pinchar despliega un nuevo menú. Si en tu navegador, arriba donde pone "Archivo" pinchas con el ratón, verás que se despliega un menú con más opciones como "Abrir", "Guardar como", etc. Puede haber varios `JMenu` uno dentro de otro

- **JMenuItem**.  Es el que cuando lo pinchas hace algo útil, como "guardar como", "abrir", etc.

- **JSeparator**. Este sólo sirve para poner una rayita y separar varios JMenuItem. Por ejemplo, dentro de "Editar", las opciones "Copiar", "Cortar" y "Pegar" suelen
estar separadas con rayitas de otras opciones en el mismo menú.

```java
JFrame frame = new JFrame("Mi Ventana");
frame.setSize(400, 300); // Tamaño de la ventana en pixeles ancho x alto
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); // Accion que debe realizarse al cerrar la ventana

/* Otras opciones
- JFrame.HIDE_ON_CLOSE. Se oculta pero se sigue ejecutando en segundo plano
- JFrame.DO_NOTHING_ON_CLOSE. No hace nada. Se puede controlar manualmente lo que sucede

    // Agregar un listener para detectar el cierre de la ventana
        addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                // Mostrar un mensaje de confirmación cuando el usuario intente cerrar
                int response = JOptionPane.showConfirmDialog(null, 
                        "¿Estás seguro de que deseas salir?", "Confirmar Salida", 
                        JOptionPane.YES_NO_OPTION);
                
                // Si el usuario elige "Sí", cerrar la ventana, si elige "No", no hacer nada
                if (response == JOptionPane.YES_OPTION) {
                    System.exit(0);  // Terminar la aplicación
                }
            }
        });

- JFrame.DISPOSE_ON_CLOSE. Ventana se destruye pero el proceso no necessariamente termina

    public static void main(String[] args) {
        // Crear y mostrar la ventana
        DisposeOnCloseExample ventana = new DisposeOnCloseExample();
        ventana.setVisible(true);
        
        // Imprimir un mensaje indicando que la aplicación sigue ejecutándose
        System.out.println("La aplicación sigue en ejecución...");
    }

*/
frame.setLocationRelativeTo(null) // Se centra la ventana con respecto al componente que se indique. En este caso no se indica nada, se queda en el centro de la pnatalla.
frame.setVisible(true); // Hace visible el JFrame

JPanel panel = new JPanel();
frame.add(panel);

JButton button = new JButton("Haz clic");
panel.add(button);

JLabel label = new JLabel("Este es un texto");
panel.add(label);

JTextField textField = new JTextField(20);
panel.add(textField);

JTextArea textArea = new JTextArea(5, 20);
panel.add(textArea);

JCheckBox checkBox = new JCheckBox("Aceptar términos");
panel.add(checkBox);

JRadioButton radioButton1 = new JRadioButton("Opción 1");
JRadioButton radioButton2 = new JRadioButton("Opción 2");
ButtonGroup group = new ButtonGroup();
group.add(radioButton1);
group.add(radioButton2);
panel.add(radioButton1);
panel.add(radioButton2);

String[] columnNames = { "Nombre", "Edad" };
Object[][] data = { { "Juan", 25 }, { "Ana", 30 } };
JTable table = new JTable(data, columnNames);
panel.add(new JScrollPane(table));  // Necesitamos un JScrollPane para que sea desplazable

JComboBox<String> comboBox = new JComboBox<>(new String[] {"Opción 1", "Opción 2", "Opción 3"});
panel.add(comboBox);


JDialog dialog = new JDialog(frame, "Ventana Emergente", true); // El tercer parámetro true hace el dialog modal
dialog.setSize(200, 150);
// Establecer la ubicación del diálogo al centro de la ventana principal
dialog.setLocationRelativeTo(frame);
dialog.setVisible(true);

// Mensaje simple en cuadro de diálogo
JOptionPane.showMessageDialog(null, "¡Operación completada exitosamente!", "Éxito", JOptionPane.INFORMATION_MESSAGE);

// Cuadro de confirmacion. Yes/No
int respuesta = JOptionPane.showConfirmDialog(null, "¿Estás seguro de que deseas eliminar este archivo?", "Confirmación", JOptionPane.YES_NO_OPTION);
if (respuesta == JOptionPane.YES_OPTION) {
    System.out.println("El archivo será eliminado.");
} else {
    System.out.println("Operación cancelada.");
}

// Cuadro de texto para ingresar un valor
String nombre = JOptionPane.showInputDialog(null, "¿Cómo te llamas?", "Entrada de Usuario", JOptionPane.QUESTION_MESSAGE);
System.out.println("El nombre ingresado es: " + nombre);

// Cuadro mas flexible que permite personalizar botones
Object[] opciones = {"Sí", "No", "Cancelar"};
int seleccion = JOptionPane.showOptionDialog(null, "¿Quieres continuar?", "Pregunta", JOptionPane.YES_NO_CANCEL_OPTION, JOptionPane.QUESTION_MESSAGE, null, opciones, opciones[0]);
if (seleccion == JOptionPane.YES_OPTION) {
    System.out.println("El usuario seleccionó 'Sí'.");
} else if (seleccion == JOptionPane.NO_OPTION) {
    System.out.println("El usuario seleccionó 'No'.");
} else {
    System.out.println("El usuario canceló.");
}

// Y un JOptionPane con imagen...
     // Cargar la imagen desde un archivo
    ImageIcon icon = new ImageIcon("ruta/a/tu/imagen.jpg");

    // Mostrar un cuadro de mensaje con la imagen
    JOptionPane.showMessageDialog(
    null,                      // Componente principal (null para centrar en la pantalla)
            "¡Mensaje con imagen!",    // Mensaje de texto
            "Título del Diálogo",      // Título del cuadro de diálogo
            JOptionPane.INFORMATION_MESSAGE,  // Tipo de mensaje (puede ser información, advertencia, etc.)
            icon                        // El icono (imagen) que se mostrará
        );
```

En  `JOptionPane`

`showMessageDialog(Component parentComponent, Object message, String title, int messageType, Icon icon)`

Se tienen las siguientes constantes para describir el tipo de mensaje (`messageType`):
- `JOptionPane.PLAIN_MESSAGE` --> -1
- `JOptionPane.ERROR_MESSAGE` --> 0
- `JOptionPane.INFORMATION_MESSAGE` --> 1
- `JOptionPane.WARNING_MESSAGE` --> 2
- `JOptionPane.QUESTION_MESSAGE` --> 3

Y luego también está este otro método para los  cuadros con opción, debiendo elegir el tipo  de opción:

`showOptionDialog(Component parentComponent, Object message, String title, int optionType, int messageType, Icon icon, Object[] options, Object initialValue)`

Todos los contenedores llevan una disposición por defecto aunque existen otras ya incorporadas y que pueden definirse mediante el método `setLayout(...)` como: 
- **FlowLayout**: Centrados comenzando a la izquierda hasta llenar la línea y pasar a la siguiente
- **BorderLayout**: Componentes en lateral o en el centro indicando una dirección (eat, west, north, south, center)
- **GridLayout**: Componentes en rejilla rectangular nxm
- **BoxLayout**: De acuerdo con dos ejes: Vertical u horizontal
- **GridBagLayout**: Requiere restricciones para ir modificando las dimensiones de cada componente conforme se va agregando. `GridBagContraints`

Los layouts pueden ser combinados haciendo uso en los elementos que se necesiten (anidándolos)

##### Métodos curiosos
`setText(String txt)`: Cambiar el texto
`setSize(int ancho, int alto)`: Cambiar el tamaño del objeto
`setFont("Helvetica", 1, 20)`: Cambiar el tipo de fuente
`setBackground(0,255,0)`: Cambiar el color de fondo del objeto
`setForeground(0, 255,0)`: Cambiar el color del texto
`setBorderPainted(Boolean b`: Resaltar borde del objeto. Solo para `JButton`, `JRadioButton`, `JCheckBox`
`setLocation(nuevaX, nuevaY)`: Cambiar localización del objeto
`setBounds(10,10,400,300)`: Definir tamaño y ubicación
`setToolTipText(...)`: Que al pasar el ratón por encima aparezca texto
`enabled(...)`: Si el componente está activado
`setResizable(boolean)`: Si se puede cambiar de tamaño de un contenedor...
`setUndecorated(boolean)`: Quitar el marco de un `Frame`
### 7.2. Eventos y acciones en Java Swing

**Evento** es una acción que ocurre en la interfaz de usuario como hacer click en un botón. **Todos** los eventos vienen de la clase `java.awt.event`
Para responder a los eventos se usan **listeners**

**Delegación de eventos**
El modelo de Java se basa en la _delegación de eventos_: el evento se produce en un determinado componente, por ejemplo un botón. Dónde se produce el evento se denomina “fuente del evento”. A continuación el evento se transmite a un ”manejador de eventos” (`event listener`) que este asignado al componente en el que se produjo el evento. El objeto que escucha los eventos es el que se encargará de responder a ellos adecuadamente.

Cuando un usuario interactúa con un interface de usuario, por ejemplo pulsando un botón, se genera un evento que tiene los siguientes elementos:
1. Fuente del evento o **event source** .Es el componente swing que origina el
evento.
2. El escuchador o **event listener**. Es el encargado de atrapar o detectar que se
ha producido un evento.
3. El manejador del evento o **event handler** Es un método que recibe un objeto
del tipo de evento que se ha producido, lo descifra, ejecuta el código asociado y
devuelve el control al usuario.

#### 7.2.1. Tipos de eventos

![](DESARROLLO_INTERFACES/resources/ud03-2.png)

- **ActionEvent**: Al efectuar acción sobre componente (click, doble click...)
- **AdjustmentEvent**:  Cuando se ajusta valor del componente
- **ComponentEvent**: Cuando se redimensiona un componente
- **ItemEvent**: Cuando se modifica el estado del elemento de un componente
- **TextEvent**:  Cuando el contenido textual de un componente cambia
- **FocusEvent**: Cuando cambia el foco de un componente
- **InputEvent**: Cuando se realizan operaciones especiales con el teclado o ratón (ctrl + alt...)
- **ContainerEvent**: Cuando se añaden o eliminan componentes en un contenedor
- **WindowEvent**: Cuando se realiza acción sobre una ventana
- **KeyEvent**: Cuando el usuario presiana una tecla
- **MouseEvent**: Cuando el usuario realiza una acción con el ratón
#### 7.2.2. Tipos de listeners u oyente de eventos

Son interfaces de Java con declaraciones de métodos para capturar las situaciones que producen un evento. 

Los más importantes son

| Listener               | Métodos                                                                                                                   |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **ActionListener**     | `actionPerformed`                                                                                                         |
| **AdjustmentListener** | `adjustmentValueChanged`                                                                                                  |
| **ComponentListener**  | `componentHidden`<br>`componentMoved`<br>`componentResized`<br>`componentShown`                                           |
| **ContainerListener**  | `componentAdded`<br>`componentRemoved`                                                                                    |
| **FocusListener**      | `focusGained`<br>`focusLost`                                                                                              |
| **ItemListener**       | `itemStateChanged`                                                                                                        |
| **KeyListener**        | `keyPressed`<br>`keyReleased`<br>`keyTyped`                                                                               |
| **MouseListener**      | `mouseClicked`<br>`mouseEntered`<br>`mouseExited`<br>`mousePressed`<br>`mouseReleased`                                    |
| **TextListener**       | `textValueChanged`                                                                                                        |
| **WindowListener**     | `windowActivated`<br>`windowClosing`<br>`windowDeactivated`<br>`windowDeiconified`<br>`windowIconified`<br>`windowOpened` |
Con `windowOpened` se puede conseguir que un método se ejecute nada más abrir laventana. Por ej. para cargar un `JComboBox` o un `JTable` añadiendo el  evento al `JFrame`


- **ActionListener**: Escuchador de eventos de acción (hacer click en botón,...)

```java
button.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent e) {
        // Código a ejecutar cuando se hace clic en el botón
        System.out.println("¡Botón clickeado!");
    }
});


// Java 8+
button.addActionListener(e -> { System.out.println("¡Botón presionado!"); });


// DISTINGUIR QUE BOTON CAUSA LA ACCION
// Con event.getSourcE()
public void actionPerformed (ActionEvent e)
{
	Object fuente = e.getSource();
	if (fuente==boton1)
		metodoParaBoton1();
	else if (fuente==boton2)
		metodoParaBoton2();
	else if (fuente==boton3)
		metodoParaBoton3();
}


// O usar un boton de cerrar
jcerrar.addActionListener(new java.awt.event.ActionListener() {
	public void actionPerformed(java.awt.event.ActionEvent e) {
	System.exit(0); }
});

// O un boton sumar que rescata los valores almacenados en JTextField y los envia a una JLabel
jButtonsumar.addActionListener(new java.awt.event.ActionListener() {
public void actionPerformed(java.awt.event.ActionEvent e) {
	int v1=Integer.parseInt(jTextFieldprimervalor.getText());
	int v2=Integer.parseInt(jTtextFieldsegundovalor.getText());
	int suma=v1+v2;
	jLabel1resultado.setText(String.valueOf(suma));
}
});
```


- **MouseListener**: Escuchador de eventos de ratón

```java
button.addMouseListener(new MouseAdapter() {
    public void mouseClicked(MouseEvent e) {
        System.out.println("¡Hiciste clic en el botón!");
    }
});
```

- **KeyListener**: Escuchador de eventos de teclado (presionar, soltar teclas)

```java

panel.addKeyListener(new KeyAdapter() { 
	// Inmediata
	@Override
	public void keyPressed(KeyEvent e) {
	    int keyCode = e.getKeyCode(); // Obtiene el código de la tecla presionada
	    System.out.println("Tecla presionada: " + KeyEvent.getKeyText(keyCode));
	}
	
	// Tras soltar
	@Override
	public void keyReleased(KeyEvent e) {
	    int keyCode = e.getKeyCode();
	    System.out.println("Tecla soltada: " + KeyEvent.getKeyText(keyCode));
	}
	
	// Se basa en el carácter real, no en el código de la tecla
	@Override
	public void keyTyped(KeyEvent e) {
	    char c = e.getKeyChar(); // Obtiene el carácter que fue tipeado
	    System.out.println("Carácter tipeado: " + c);
	}
}

// Un KeyAdapter para controlar que solo se usen números
myTextField.addKeyListener(new KeyAdapter(){
@override
public void keyTyped(keyEvent e){
	char caracter=e.getKeyChar(); // declaramos un character que recoge la tecla pulsada
	if(caracter<’0’ || carácter >’9’)
		e.consume() // llamamos al método consume(), que no va a hacer eco de la tecla pulsada hasta que no sea un numero
}
});
```

#### 7.2.2. Y si fuese una imagen...

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class ImageWithLabelAndListener {
    public static void main(String[] args) {
        // Crear el JFrame principal
        JFrame frame = new JFrame("Imagen con Listener en JLabel");
        frame.setSize(400, 400);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        // Crear un JPanel para organizar los componentes
        JPanel panel = new JPanel();

        // Crear un ImageIcon con la imagen
        ImageIcon imageIcon = new ImageIcon("ruta/a/tu/imagen.jpg");

        // Crear un JLabel y asignar la imagen al JLabel
        JLabel imageLabel = new JLabel(imageIcon);

        // Agregar un MouseListener al JLabel
        imageLabel.addMouseListener(new MouseAdapter() {
            @Override
            public void mouseClicked(MouseEvent e) {
                // Detectar el clic sobre la imagen
                JOptionPane.showMessageDialog(null, "¡Imagen clickeada!");
            }
        });

        // Agregar el JLabel al JPanel
        panel.add(imageLabel);

        // Agregar el JPanel al JFrame
        frame.add(panel);

        // Hacer visible el JFrame
        frame.setVisible(true);
    }
}
```

#### 7.3 Uso visual (GUI Designer)

#### En Netbeans 

Haz clic derecho en el paquete donde deseas crear la clase y selecciona **"New"** > **"JFrame Form"**.

#### En IntelliJ

1. Habilitar el Diseñador de IU Archivo → Configuración → Complementos → UI Designer
2. Habilitar generar Java clase Archivo → Configuración → Editor → Diseñador de GUI → cambiar Generar GUI en "código fuente Java"

3. Vaya a la vista del proyecto y haga clic con el botón derecho en el nombre del paquete donde desea que se almacene la clase Java generada. En el menú contextual, elija Nuevo → Formulario de GUI y establezca la clase enlazada
	En el diseñador, automáticamente colocará un Jpanel en la ventana. Elija Jpanel y primero configure el Administrador de diseño en GridLayoutManager (IntelliJ).
	
	Agregando componentes según sea necesario, asegúrese de dar algún valor al "nombre de campo". Este valor se convertirá en el nombre de este componente en la clase de formulario.
	
	Puede obtener una vista previa del formulario haciendo clic derecho y luego elegir la vista previa.
	
	Cuando haya terminado, cambie el administrador de diseño para Jpanel a "GridBagLayout".

4. Haga clic en Build → Make Project para generar Java códigos fuente y almacenarlos en el enlace Java clase.

Para poder ejecutar nuestra aplicación, necesitamos hacer el método main y
como mínimo estas sentencias:

```xml
JFrame frame = new JFrame();
// El marco necesita un panel donde estén los componentes.
// Necesario: Dar nombre a componente JPanel en el UI Designer. Crear getter en formulario que lo devuelva. 
frame.setContentPane(new nombreClase.getPanel());
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
frame.pack();
frame.setVisible(true);
```
