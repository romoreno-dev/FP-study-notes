
## 1. La interfaz de usuario

**Interfaz de usuario** es todo lo que el usuario puede ver y con lo que puede interactuar en cualquier aplicación.  Android incluye componentes prediseñados que pueden usarse como objetos **layout** (contenedores para organizar), **views** (controles con los que el usuario interactúa), **dialogs**, **notifications**, **menus**...

Los ficheros generados de la aplicación Android están escritos en Java y en XML. Será posible
- **Programación Java imperativa**: Igual que en desarrollo de interfaces de Java pero con clases de Android
- **Definición XML declarativa**: Por ficheros XML se define la estructura que tendrá cada pantalla y los componentes que la integran. Implementación de la lógica en Java. 

Veamos los componentes imprescindibles necesarios para implementar de forma fácil interfaces de usuario intuitivas, uniformes y de fácil manejo para el usuario final.

### 1.1. La pantalla de Android

Objetivo: Que la aplicación pueda instalarse en el mayor número posible de terminales (smartphones, tables...).

Android considera varios factores respecto a la pantalla:
- **Tamaño**: Longitud de la pantalla en diagonal, medida en pulgadas. Agrupada en **small**, **normal**, **large**, **extra large**
- **Densidad**: Cantidad de píxeles en un área física de pantalla. Medida en puntos por pulgadas (DPI). Agrupada en densidad low (**LDPI**), medium (**MDPI**), high (**HDPI**), extra high (**XHDPI**)
- **Resolución**: Cantidad de píxeles de la pantalla en horizontal y en vertical. Las aplicaciones lo que tienen en cuenta es el tamaño y la densidad, no la resolución.
- **Píxeles independientes de la densidad (DP)**: Unidad de píxel virtual que se usa en la definición de un diseño de interfaz de usuario para expresar las dimensiones del diseño o posición de forma independiente a la densidad. Un píxel independiente de la densidad representa un píxel físico en pantalla de 160 DPI (densidad media). En tiempo de ejecución, el diseño de la interfaz se adapta de forma transparente al usuario escalando al tamaño adecuado según la pantalla que tenga el dispositivo.

**Pantallas más comunes según tamaño y densidad**

![](PROGRAMACION_MULTIMEDIA_DISPOSITIVOS_MOVILES/Andalucía/resources/ud02-1.png)

Compatibilidad de pantallas: http://developer.android.com/guide/practices/screens_support.html

## 2. Layouts de Android

Para desarrollar interfaces de usuario, Android utiliza las clases `View` y `ViewGroup` que hereda de la anterior. 
Un objeto `View` es aquel que dibuja algo en la pantalla con la que el usuario va a actuar.
Los objetos `ViewGroup` se conocen como **Layout**. Contienen los objetos `View` de la pantalla o contienen otro Layout.

Se podría instanciar un objeto `View` por código pero la forma más efectiva es hacerlo con XML:

Veamos el ejemplo de un layout (`ViewGroup`) con dos `View`: un `TextView` y un `Button`

Se sigue una jerarquía de vistas siendo `LinearLayout` el nodo raíz. 

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
          android:layout_width="fill_parent" 
          android:layout_height="fill_parent"
          android:orientation="vertical" >
     <TextView android:id="@+id/text"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:text="Esto es un objeto de tipo TextView" />
     <Button android:id="@+id/button"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:text="Botón" />
</LinearLayout>
```

Al mostrar la interfaz, el sistema operativo le pide al nodo raíz que realice las siguientes operaciones: 
- **Indicar su tamaño (medición)**: Dependerá del tamaño de las vistas que contiene. Recorre la jerarquía de vistas de arriba a abajo para conocer el tamaño de cada `ViewGroup`o `View` que contenga. Para eso llama al método `onMeasure()` de cada vista.
- **Indicar su posición (diseño)**: Se recorre la jerarquía de vistas preguntando qué posición ocupan en base al tamaño establecido. Se llama al método `onLayout()` de cada vista.
- **Que se dibuje (dibujo):** Se recorre la jerarquía de vistas y, por cada una se crea un objeto `Canvas` que dibuja el componente según su tamaño y posición. Se llama al método `onDraw()` de cada vista. 
Finalmente, se muestra la interfaz al usuario. 

Estos métodos se ejecutan en todos los `View` y `ViewGroup`, incluyendo el nodo raíz.

¡OJO! Anidar muchas vistas o crear una interfaz compleja provocará que se necesite más tiempo y recursos de cómputo para dibujar la interfaz. 

Entre los layouts más utilizados están
- **FrameLayout**: Todas las vistas se colocan en la esquina superior izquierda y ocupan todo el espacio de la pantalla
- **LinearLayout:** Se colocan una detrás de otra en vertical u horizontal
- **TableLayout:** Se colocan en celdas dentro de filas y columnas
- **ScrollView:** Se visualiza una barra de desplazamiento si no pueden verse en su totalidad en la pantalla
- **ConstraintLayout:** Posicionamiento relativo. Vistas se colocan con restricciones respecto a otras vistas o bien con respecto al padre. 
- Layouts legacy (Editor de diseño > Palette > Legacy): GridLayout, ListView, TabHost, RelativeLayout, GridView. 
	- **GridLayout:** Organiza las vistas en una cuadrícula con filas y columnas, permitiendo una alineación precisa de los elementos.
	- **ListView:** Muestra una lista de elementos desplazables verticalmente, útil para grandes cantidades de datos que se repiten.
	- **TabHost:** Permite la navegación entre diferentes vistas mediante pestañas, cada pestaña muestra un contenido diferente.
	- **RelativeLayout:** Posiciona las vistas en relación con otras vistas o con el contenedor padre, proporcionando una disposición flexible y dinámica.
	- **GridView:** Muestra elementos en una cuadrícula desplazable, ideal para mostrar datos en una estructura similar a una tabla, con cada celda conteniendo un elemento.

### 2.1. Atributos genéricos

Los atributos de `View` y `ViewGroup` permiten modificar las propiedades de cada objeto de forma personalizada. Debe conocerse qué atributos se pueden modificar según el tipo de objeto al que haga referencia el atributo.

Estos atributos quedan definidos en la clase `LayoutParams` de cada `ViewGroup`. Formato `android:nombre_atributo`.

Los más comunes que pueden aparecer en cualquier componente (View) y en cualquier layout (GroupView):
- **android:id**  Identificador asociado que permite identificar a la `View` de forma única. Se le asigna un tipo de dato String en el XML y, cuando sea compilada, el ID será referenciado como un Integer. `android:id"@+id/texto1`
- **android:heigth** y **android:width** Definir anchura y altura del objeto. Se pueden definir dimensiones directamente pero lo recomendable es usar **WRAP_CONTENT** (solo cogerá el espacio necesario para representarse con respecto al padre) y **MATCH_PARENT** (cogerá todo el espacio del padre) (antes de API 8 **FILL_PARENT**). 
- **android:padding** y  **android:margins** Crear espacio alrededor de los objetos. Con margin se establece espacio fuera del objeto con respecto a otros objetos de alrededor. Con padding, espacio dentro del objeto, por ejemplo en un Button la distancia desde el texto del boton a las líneas del mismo.
- **android:gravity**  Alinear objetos. Por defecto se alinean a la izquierda. 

### 2.2. Acceder a vistas en código

Cuando se genera un proyecto con Android Studio, automáticamente se crea el fichero `R.java` donde se identifican todos los objetos y recursos creados y que **no debe modificarse manualmente**. 

Se accede a los recursos de dos formas:
- **Por código Java**. Utilizando la sintaxis `nombre_paquete.R.tipo_recurso.nombre_recurso`, pudiéndose omitir el nombre del paquete si quiere referirse a recursos dentro del mismo.
```java
setContentView(R.layout.activity_main);
ImageView imageView = (ImageView)findViewById(R.id.myimageview);
imageView.setImageResource(R.drawable.myimage);
```

El método `findViewById()` se utiliza para buscar una vista dentro de la jerarquía de vistas infladas desde un archivo XML de diseño. Se utiliza en archivos de actividad o fragmento Java para obtener referencias a vistas específicas y manipularlas dinámicamente en tiempo de ejecución.

- **Por XML**.. Siguiendo la síntaxis `@[<nombre_paquete>:]<tipo_recurso>/<nombre_recurso>`. 
```xml
android:paddingBottom="@dimen/activity_vertical_margin"
android:text="@string/hello_world"
```
### 2.3. FrameLayout

- Todos los objetos `View` se organizan en la esquina superior izquierda, uno encima de otro. 
- Debe definirse la transparencia de los elementos que no se quieran mostrar en un momento determinado en la aplicación  `android:visibility`
- - `<FrameLayout> </FrameLayout>`

Ejemplo: Tres `Views`: `TextView`, `Button`, `ProgressBar`, dejando visible solo el botón. En la ejecución se puede cambiar el atributo `android:visibility` de los demás objetos para mostrarlo por pantalla. 

```xml
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity" >
 
    <TextView
        android:id="@+id/textView1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/Texto"
        android:visibility="invisible"
        android:textAppearance="?android:attr/textAppearanceLarge" />
 
    <Button
        android:id="@+id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/Boton" />
 
    <ProgressBar
        android:id="@+id/progressBar1"
        style="?android:attr/progressBarStyleLarge"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:visibility="invisible" />
 
</FrameLayout>
```

### 2.4. LinearLayout

- Las vistas se disponen de forma consecutiva en la pantalla. 
- Con `android:orientation` se puede poner vertical u horizontal
- `<LinearLayout> </LinearLayout>`

Ejemplo: Definamos un `LinearLayout` que tenga la anchura y altura del objeto padre (match_parent), es decir, de la pantalla. Definir espacio izquierdo y derecho (padding) de 16 dp y orientación vertical. 

Coloquemos tres `EditText` y un `Button` 

Los textos tienen anchura la del elemento padre (con el padding, claro), altura la que necesite y un `android:hint` con texto predefinido sobre lo que se debe escribir. 

El botón tiene anchura determinada y altura la que necesite. Con `android:layout_gravity="right` el botón queda alineado a la derecha.

Por defecto, se hace un reparto entre las vistas que contiene el layout. Pero con **`android:layout_weigth`** se puede asignar un peso para repartir el espacio disponible. Si no se indica nada, coge el espacio necesario. Si se indica algún valor, deja más espacio a las vistas que tengan valor más alto y menos a las que tengan valor más bajo. 

Importante que `android:layout_with` sea de 0dp en diseño horizontal  o que `android:layout_heigth` sea de 0 dp en diseño vertical para que el peso se ajuste correctamente. 

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingLeft="16dp"
    android:paddingRight="16dp"
    android:orientation="vertical" >
    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="@string/para" />
    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="@string/asunto" />
    <EditText
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:gravity="top"
        android:hint="@string/mensaje" />
    <Button
        android:layout_width="100dp"
        android:layout_height="wrap_content"
        android:layout_gravity="right"
        android:text="@string/enviar" />
</LinearLayout>
 
```

Parámetros del LinearLayout: https://developer.android.com/reference/android/widget/LinearLayout.LayoutParams

Podríamos asignarle un peso 50, 30, 20 a botones y cosas así. 
### 2.5. TableLayout

- Las vistas se disponen en forma de tabla, mediante filas y columnas que organizan las vistas.
- Para definir cada una de las filas se usará `<TableRow>` dentro de las cuáles se insertan los elementos deseados considerando cada uno de ellos como una columna de la tabla. 
- `<TableLayout> </TableLayout>`

Veamos un ejemplo en el que se usa:
En la primera fila dos `EditText`, cada uno en una columna.
En la segunda fila en la primera columna un `EditText` con altura `200dp` y en la segunda columna un `Button`

El ancho de la columna viene definido por el máximo ancho de los elementos que hay en cada columna. Se puede modificar con atributos: 

- `android:stretchColumns`: Para especificar cuál es la columna que se debe estirar para llenar el espacio disponible en la tabla. Puede definirse múltiples columnas separadas por comas, y el sistema distribuirá el espacio adicional entre estas columnas.
    
- `android:shrinkColumn`: Para especificar qué columnas que se pueden reducir para ajustarse al contenido si la tabla no tiene suficiente espacio. Puede definirse definirse múltiples columnas separadas por comas.
    
- `android:collapseColumn`: Para especificar cuáles son las columnas que se deben colapsar cuando el contenido de una fila es demasiado ancho y no cabe en la pantalla. Cuando una columna está colapsada, el contenido se corta y se muestra un indicador de truncamiento.

```xml
<TableLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingLeft="16dp"
    android:paddingRight="16dp">
    <TableRow>
     <EditText
          android:layout_width="match_parent"
          android:layout_height="wrap_content"
                android:hint="@string/para" />
     <EditText
                android:layout_width="match_parent"
                  android:layout_height="wrap_content"
                android:hint="@string/asunto" />      
    </TableRow>
    <TableRow>
     <EditText
                  android:layout_width="match_parent"
                android:layout_height="200dp"
                android:gravity="top"
             android:hint="@string/mensaje" />
     <Button
          android:layout_width="100dp"
              android:layout_height="wrap_content"
            android:layout_gravity="right"
            android:text="@string/enviar" />
    </TableRow>
</TableLayout>
```
### 2.6. ScrollView

- Hereda de `FrameLayout`
- Contenedor de objetos demasiado grandes para mostrarse en la pantalla. Se añade automáticamente una barra de desplazamiento para visualizar el objeto al completo.
- `<ScrollView> </ScrollView>

- Suele usarse en combinación con otro tipo de Layouts (como LinearLayout) para organizar su contenido

- Con `android:fillViewport` puede indicarse si se quiere que el objeto `ScrollView` ocupe la pantalla completa. A `true` se expandirá incluso si el contenido de dentro del `ScrollView` no es suficientemente largo como para requerir desplazamiento vertical. A `false` solo ocupará el espacio necesario para mostrar su contenido.

Veamos un ejemplo:

```xml
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
        android:id="@+id/scrollview1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:fillViewport="true"
        android:paddingRight="5dp">
      <LinearLayout
            android:id="@+id/linearlayout1"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical">
                 <TextView
                      android:id="@+id/textView1"
                      android:layout_width="match_parent"
                      android:layout_height="wrap_content"
                    android:textAppearance=
                         "?android:attr/textAppearanceMedium"
                      android:text="@string/contenido" 
                      android:layout_weight="2"/>
                   <Button
                      android:id="@+id/button1"
                       android:layout_width="wrap_content"
                       android:layout_height="wrap_content"
                     android:text="Leido" />
     </LinearLayout>
</ScrollView>
```

### 2.7. ConstraintLayout

- `<ConstraintLayout> </ConstraintLayout>`

Permite construir UI complejas sin anidamientos. Todas las vistas se encuentran en el mismo nivel. 
Se evita lo que era necesario antes de anidar diferentes `ViewGroup`. (Uso de `LinearLayout` dentro de un `RelativeLayout`para intentar centrar dos botones horizontalmente)

Las interfaces se crean de forma más sencilla que cuando se usaba el `RelativeLayout`. Las vistas se relacionan mediante **restricciones** o **constraints**.

La interfaz puede construirse usando el Editor de diseño de Android estudio. No es necesario editar el XML, puede hacerse de forma gráfica a través de **Design** arrastrando los widgets desde el panel Pallete hasta la vista de diseño. 
Las vistas del diseño aparecerán en el Component Tree donde se mostrará la jerarquía de vistas en el diseño.
Se selecciona el componente en el diseño y, a continuación, en el panel Attributes aparecen los atributos que se han definido pudiendo modificarlos o definir un atributo nuevo. 

Con el icono **Design** y **Blueprint** puede escogerse cómo quiere verse el diseño en el editor. 

- **Design** muestra vista real de la interfaz
- **Blueprint** muestra el contorno de cada vista y en el `ConstraintLayout` las relaciones establecidas (propiedades , margen, guía...) es una radiografía del diseño. 
- Puede ponerse Design + Blueprint una al lado de otra.

La barra de herramientas de este Layout permiten: 
![](PROGRAMACION_MULTIMEDIA_DISPOSITIVOS_MOVILES/Andalucía/resources/ud02-2.png)
- **View options**: (El ojo) Qué restricciones se quieren ver y en qué vista (Design o Blueprint). Puede verse todas las restricciones con "Show All Constraints" y los márgenes con "Show Margins" u ocultar toda esa información "Fade Unselect Views"
- **Autoconnect** (El imán): Al estar activa, cuando se desplaza una vista hacia los lados, crea automáticamente restricción con el padre en base a la posición de la vista y a la proximidad a ambos lados del padre. 
- **Default Margin**: (Cuadrito de texto con ___ dp) Permite crear un margen al valor indicado según se añade las restricciones a la vista. Ej.: Se quiere que todas las vistas de la izquierda tengan margen de 16 dp respecto al padre. Así se inicializa por defecto a 16dp y al conectar vista con el padre se crea automáticamente este padre. 
- **Clear All Constraint**. (Cable con cruz) Elimina todas las relaciones
- **Infer Constraints** (Varita mágica) Agrega restricciones que faltan en base a diseños y probabilidades. Puede que no se parezca a lo que se quiere. Podría añadirse una vista, pulsar el icono y luego modificarlo.
- **Pack** (cajitas): Al seleccionar varias vistas con Ctrl para efectuar acciones (empaquetar, expandir, distribuir) de forma conjunta.
- **Align** Al seleccionar varias vistas con Ctrl posibles alineaciones de componentes. Align -> Verticals Center (restricción imagenes se alinean en parte inferior y superior con vecina)
- **Tools**: Líneas guía, barreras, grupos, capas.... 

Tutorial: Comenzar con `ConstraintLayout` https://www.kodeco.com/9193-constraintlayout-tutorial-for-android-getting-started#toc-anchor-009

#### 2.7.1. Posición y tamaño de las vistas

Para posicionar una vista en `ConstraintLayout` se debe añadir una restricción (constraint) con respecto a otra vista o al nodo raíz y debe cumplir las reglas:
- Cada vista debe tener **dos restricciones**: **Una** para el eje **horizontal** (comienzo y final) y **otra** para el eje **vertical** (arriba, abajo y linea base)
- Al crear una restricción **se debe realizar entre puntos de anclaje que cumplen el mismo plano**: Un punto de anclaje al comienzo de una vista solo puede unir a un punto de anclaje que esté al comienzo o final de otra vista.
- Cada **punto de anclaje solo puede usarse para crear una restricción**. Pero **puede ser destino de varias restricciones** siempre y cuando sean **vistas diferentes.** 

![](PROGRAMACION_MULTIMEDIA_DISPOSITIVOS_MOVILES/Andalucía/resources/ud02-3.png)

En la imagen:

1. **Guías cuadradas.** Aparece en las esquinas. Ajusta el tamaño del componente en dp
2. **Guía base**. Rectángulo con orillas redondas. Se usa para alinear en contenido de la vista con la línea base.  Posicionar en la misma línea uno y otro `app:layout_constraintBaseline_toBaselineOf="@+id/txvUser"
3. **Restricciones**. Puntos de anclaje representados como círculos. La restricción puede ser

	- Una línea en zig-zag: Dos restricciones que actúan como fuerzas opuestas que separan el componente y hay espacio sobrante a ambos lados del componente porque bien el ancho o el alto tiene asignado el valor `wrap_content`. A la izquierda se ve restricción única que indica que la vista comienza donde finaliza txvUser y a la derecha otra que indica que finaliza en el padre o parent. Si el componente no ocupa todo el año, el sistema centrará la vista en el espacio disponible. 
```xml
app:layout_constraintStart_toEndOf="@+id/txvUser"
app:layout_constraintEnd_toEndOf="parent"
```

- Una línea continua: No hay dos restricciones opuestas. Se sitúa al inicio del padre y en la parte de arriba del padre. 
```xml
app:layout_constraintStart_toStartOf="parent"<br />
app:layout_constraintTop_toTopOf="parent"
```

- Márgenes: Señalados con líneas continuas junto con el valor del margen en dp. 

```xml
android:layout_marginStart="32dp"
android:layout_marginTop="64dp"
```

Si seleccionamos el componente edtUSer aparece el _widget_ **Attributes** y se pueden realizar las siguientes operaciones:
1. **Modificar los márgenes** que se han aplicado. Mediante el desplegable se puede seleccionar valores por defecto o bien escribir directamente el valor del margen.
2. **Crear conexiones** con respecto al padre.
3. **Eliminar una restricción** ya creada pulsando sobre el círculo o punto de anclaje.
4. **Seleccionar las restricciones** que se han creado en la pestaña **Design** del **Editor.**
5. **Modificar el tamaño de los componentes.** Estos símbolos representan cómo se calcula el tamaño de la vista. Si haces clic en el símbolo cambiarás entre los diferentes tipos de configuración:

![](PROGRAMACION_MULTIMEDIA_DISPOSITIVOS_MOVILES/Andalucía/resources/ud02-4.png)

1. **Fixed**: se ha especificado un tamaño fijo en el cuadro de texto en dp. 
2. **Wrap Content:** el tamaño de la vista será el tamaño necesario para poder mostrar el contenido.
3. **Match Constraints**: la vista se expande tanto como sea posible para cumplir con las restricciones de cada lado después de aplicar los márgenes de la vista. Para que se cumpla esta restricción se debe asignar el valor 0dp a `layout_width` si se quiere que se expanda horizontalmente o a `layout_height` para que se expanda verticalmente

![](PROGRAMACION_MULTIMEDIA_DISPOSITIVOS_MOVILES/Andalucía/resources/ud02-5.png)

#### 2.7.2. Sesgo, guías, barreras y cadenas

El componente no ocupa todo el ancho. Se centra en el espacio disponible si tiene `android:layout_width="wrap_content"`. el Layout ofrece un parámetro `_bias` que permite desplazar la vista en términos de porcentajes (0% a 100%) o de fracciones (0 a 1) en el eje horizontal o vertical con respecto a los anclajes que tiene el componente. Es lo que se conoce como **sesgo**. 
Si se mueve el sesgo horizontal en edtUser al valor 30%, lo que hace es que la vista se desplaza hacia la izquierda dejando 1/3 del espacio disponible a la izquierda y 2/3 a la derecha. Este comportamiento se utiliza para garantizar que una vista tenga la misma posición independientemente de la densidad y tamaño de la pantalla.

La **guía** es una herramienta que se utiliza en la vista de diseño para poder alinear las vistas en base a un elemento pero que no se verá en el diseño de nuestra aplicación. Esta guía evita añadir en todos las vistas un margen concreto sino que se añade la restricción que la vista empieza al principio de la guía: `app:layout_constraintStart_toStartOf="@+id/guideline"`
 Hay un icono de guía en la parte superior del diseño y se puede alternar entre los tipos haciendo clic repetidamente en el icono. Por defecto se indica un desplazamiento fijo en dp desde el borde inicial del layout `ConstraintLayout`, a continuación el desplazamiento fijo contando desde el final de la pantalla y finalmente el porcentaje del  desplazamiento en base al ancho de la pantalla.

La **barrera** es una vista "invisible", pero que su efecto se muestra en tiempo de ejecución. Al igual que pasa con la guía, las vistas se limitan a la barrera, de forma que si una vista crece (porque el texto a mostrar **aumenta ya que hay un cambio de idioma en el dispositivo**), la barrera ajustará su tamaño a la altura o anchura más grande de los elementos referenciados sin que se solape ninguna vista. Las barreras pueden ser verticales u horizontales y pueden crearse en la parte superior, inferior, izquierda o derecha de las vistas referenciadas.

Es curioso ver el código de las barreras en XML. En primer lugar se debe establecer la dirección de la barrera. En el ejemplo ConstraintLayoutLogin la barrera se posiciona al final de txvUser o txvPassword dependiendo de cuál sea el más grande. A continuación se necesita un atributo para definir los ID de las múltiples vistas a las que hace referencia la barrera.

Ejemplo de barrera: 
```xml 
<android.support.constraint.Barrier"<br />
android:id="@+id/barrier"<br />
android:layout_width="wrap_content"<br />
android:layout_height="wrap_content"<br />
app:constraint_referenced_ids="edtUser,edtPassword"<br />
```

Las **cadenas** son un tipo específico de restricción que permite compartir espacio entre las vistas que pertenecen a la cadena y controlar cómo se divide el espacio disponible entre ellas. Esta restricción se utiliza mucho para centrar dos botones con respecto al eje horizontal. Para crear una cadena se siguen los siguientes pasos:
1. Añadir dos botones btnLogin y `btnSignUp`. 
2. Seleccionar los botones pulsando la tecla **Ctrl** -> opción **Chains** del menú contextual -> **Create Horizontal Chain**. 
Se puede comprobar como una cadena une las dos vistas.

Si se quiere explorar algunos de los modos de cadena, hay que hacer clic en una de las vistas de la cadena en el panel **Component Tree**, mostrar el menú contextual y seleccionar la opción  **Cicle Chain Mode**. Se puede simplificar en tres modos:

1. **Empaquetado (_paqued_)**: los elementos se agrupan en el centro del espacio disponible. En esta opción se puede utilizar márgenes para separar las vistas ligeramente. Con esta opción y utilizando las _bias se pueden centrar todas las vistas aplicando un sesgo de 0.5 o bien desplazar la cadena hacia un lado.
2. **Distribución (spread):** los elementos se extienden por el espacio disponible, como se muestra arriba.
3. **Separación en el interior (_spread_inside_):** similar a la opción anterior, pero las vistas finales de la cadena no se extienden.

No existe un atributo específico en XML que se asigne a todas las vistas sino que se establece el atributo `app:layout_constraintHorizontal_chainStyle="spread"` en una de las vistas de la cadena.

## 3. Eventos de usuario

El diseño de la interfaz de usuario se realiza por XML. Con Java se proporcionan mecanismos apropiados para la interacción con el usuario. 
- **Eventos**: Acciones que los usuarios realizan sobre el dispositivo móvil u algún objeto de la pantalla.
- **Listeners:** (escuchadores). Componentes que gestionan los eventos. Suele existir un listener por evento. Son clases abstractas en las que el desarrollador debe implementar el método que recibirá el evento.
- **Método que registran los listeners**: Son métodos que permiten registrar los listeners para ser usandos (`setOnClickListener()`por ejemplo para `onClickListener()`).

Para registrar los listeners pueden usarse varias técnicas: 

**Implementación anónima**: Se crea clase anónima del escuchador con la implementación del evento dentro y su registro se hace desde la clase de la actividad

```java
// Registramos el escuchador
Button boton = (Button)findViewById(R.id.button1);
boton.setOnClickListener(miEscuchador); 
 
//Implementamos  el evento dentro del Listener
private OnClickListener miEscuchador = new OnClickListener() {
    public void onClick(View v) { 
     TextView texto = (TextView)findViewById(R.id.textView1);
     texto.setText(R.string.despedida);
    }
};
```

Y con lambdas... ¡aún más sencillo!

```java
    Button boton = (Button)findViewById(R.id.button_first);  
    boton.setOnClickListener(v -> {  
        TextView texto = findViewById(R.id.textview_first);  
        texto.setText(R.string.app_name);  
    });  
```

**Implementación en la misma clase**: La clase de la actividad implementa la interfaz del escuchador y se registra desde aquí. Es opción recomendada porque tiene menos gasto de memoria (o eso dicen los apuntes del tiempo de mi abuela)

```java
public class MainActivity extends Activity implements OnClickListener 
     ...
     // Registramos el escuchador
     Button boton =(Button)findViewById(R.id.button1);
     boton.setOnClickListener(this); 
}
//Implementamos el evento
public void onClick(View v) {
     TextView texto = (TextView)findViewById(R.id.textView1);
     texto.setText(R.string.despedida);
}
```

Tipos de eventos: https://developer.android.com/develop/ui/views/touch-and-input/input-events?hl=es-419

## 4. Componentes de la interfaz

Los `Views` se pueden organizar en tres grupos:
- **Controles básicos**: Típicos botones, imágenes, etiquetas, cuadros de texto... Aparecen en la mayoría de las pantallas de una aplicación.
- **Controles de selección:** Seleccionar una opción de un listado. Listas fijas o desplegables y tablas.
- **Controles personalizados**: Pueden crearse controles personalizados para un diseño más personalizado de lo que ofrecen los controles convencionales.

### 4.1. Controles básicos

#### TextView

Muestra un campo de texto al usuario. No es editable por este. Atributos:
- `android:text`: Se establece el texto por defecto. 
- `android:background`: Color de fondo
- `android:textColor`: Color del texto (hexadecimal)
- `android:textSize`: Valor en sp, tamaño del texto
- `android:textStyle` : Estilo del texto en normal, negrita, cursiva

#### EditText

El usuario puede editar su contenido para introducir dato en la aplicación. Atributos los mismo que el `TextView` y además: 
- `android:inputType`: Tipo de texto que el usuario introducirá. 
- `android:hint`: Texto sugerido semitransparente
- `android:textColorhighlight`: Color del texto seleccionado

 `text`: Entrada de texto normal.
 `textPassword`: Entrada de texto para contraseñas, el texto se oculta.
`textEmailAddress`: Entrada de texto para direcciones de correo electrónico.
`textPersonName`: Entrada de texto para nombres de personas.
`number`: Entrada de números.
`phone`: Entrada de números de teléfono.
`datetime`: Entrada de fecha y hora.
`date`: Entrada de fecha.
`time`: Entrada de hora.
`textMultiLine`: Entrada de texto multilinea.

#### Button

Botón para realizar una acción programada con el evento `onClick`. Puede usarse atributo `android:onclick="sendMessage"` referenciando a método definido en la clase `Activity` con declaración:
```java
public void sendMessage(View view)
```
No es necesario implementar el escuchador `onClickListener` en el botón.

#### Switch

Botón a modo de interruptor con dos opciones: Encendido y apagado. Atributos:
- `android:checked`: Modificar estado
- `android:text`: Texto en base a su estado

#### CheckBox

Mostrar listado de opciones que puede marcar o desmarcar. Hereda indirectamente de `TextView` por lo que se le pueden asignar los atributos de este y además:
- `android:checked`: Para inicializar el estado del control. 

#### RadioButton

Igual que `CheckBox` puede tener opción de marcado y desmarcado pero las opciones forman un grupo con la clase `RadioGroup` y solo puede haber una opción marcada. 

#### ImageButton

Igual que `Button` pero se muestra una imagen en vez de texto. Atributos:
- `android:src`: Indicar recurso imagen que se encuentra en `/res/drawable`
- `android:contentDescription`: Describir mediante texto la imagen del botón para que sea accesible. 

#### ImageView

Introducir imagen, sin funcionalidad. Se utiliza `android:src` para indicar la imagen a visualizar.
#### FloatingActionButton

Aparece con Material Design. Es un botón redonde que se eleva por encima del contenido de la pantalla principal y permite al usuario realizar una acción que se destaca entre las demás. Por ejemplo, en un listado la opción "Añadir". Se suele modificar el atributo `colorAccenty` y el icono que lo identifica con `src`

![](PROGRAMACION_MULTIMEDIA_DISPOSITIVOS_MOVILES/Andalucía/resources/ud02-6.png)
### Otros
`TextClock`, `CalendarView`, `ProgressBar`, `RatingBar`...

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <!-- TextView -->
    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="TextView"
        android:layout_marginBottom="16dp"/>

    <!-- EditText -->
    <EditText
        android:id="@+id/editText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="EditText"
        android:layout_marginBottom="16dp"/>

    <!-- Button -->
    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Button"
        android:layout_marginBottom="16dp"/>

    <!-- Switch -->
    <Switch
        android:id="@+id/switchBtn"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Switch"
        android:layout_marginBottom="16dp"/>

    <!-- CheckBox -->
    <CheckBox
        android:id="@+id/checkBox"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="CheckBox"
        android:layout_marginBottom="16dp"/>

    <!-- RadioButton -->
    <RadioButton
        android:id="@+id/radioButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="RadioButton"
        android:layout_marginBottom="16dp"/>

    <!-- ImageButton -->
    <ImageButton
        android:id="@+id/imageButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/ic_launcher_foreground"
        android:layout_marginBottom="16dp"/>

    <!-- ImageView -->
    <ImageView
        android:id="@+id/imageView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/ic_launcher_foreground"
        android:layout_marginBottom="16dp"/>

    <!-- FloatingActionButton -->
    <com.google.android.material.floatingactionbutton.FloatingActionButton
        android:id="@+id/fab"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/ic_launcher_foreground"
        android:layout_marginBottom="16dp"/>

    <!-- TextClock -->
    <TextClock
        android:id="@+id/textClock"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:format24Hour="HH:mm:ss"
        android:layout_marginBottom="16dp"/>

    <!-- CalendarView -->
    <CalendarView
        android:id="@+id/calendarView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="16dp"/>

    <!-- ProgressBar -->
    <ProgressBar
        android:id="@+id/progressBar"
        style="?android:attr/progressBarStyleHorizontal"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="16dp"/>

    <!-- RatingBar -->
    <RatingBar
        android:id="@+id/ratingBar"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="16dp"/>

</LinearLayout>
```

### 4.2. Controles de selección, Adapters

Para los controles de selección s necesario apoyarse de los adaptadores. Son controladores que heredan de la clase `AdapterView`. 
Podemos citar `Spinner`, `RecyclerView`, `GridView`, `Gallery`, `ListView`

El adaptador es un objeto que busca:
- Poblar de datos necesarios a la vista. (`Arrays`, `List`, `Cursor`). Dispone de varios tipos de adaptadores en función de los datos que gestiona. 
- Crear la vista `View` con los datos que se representarán en el control de selección `AdapterView` vinculado al adaptador. 

![](PROGRAMACION_MULTIMEDIA_DISPOSITIVOS_MOVILES/Andalucía/resources/ud02-7.png)

En el **control de selección** se pueden mostrar muchos datos pero se consumen pocos recursos porque el adaptador solo crea los objetos `View` que se visulizan en pantalla o que están a punto de moverse, ahorrando memoria. 
El número de vistas a mostrar es constante y no se eliminan, sino que se reutilizan. El adaptador modifica el objeto `View` con la información del elemento a visualizar. 

- **ArrayAdapter:** provee de datos a un control de selección a partir de un Array de objetos de cualquier tipo.
- **SimpleAdapter:** mapea los datos de los diferentes controles definidos en un _layout.xml_.

#### 4.2.1. ArrayAdapter

**Creación de un spinner de ciudades**

1. En primer lugar se define el modelo:

```java
public class City {

   private String code;
    private String name;

    public City(int code, String name) {
        this.code = code;
        this.name = name;
    }

    @NonNull
    @Override
    public String toString() {
        return this.name;
    }
}
```

**Debe implementarse el método `toString`** Porque `ArrayAdapter` crea una vista para cada elemento de la lista llamando a este método y colocando el contenido en un `TextView` del layout que se pasa como parámetro.

2. Porque para crear un `ArrayAdapter` se pasan tres parámetros:
- **Contexto**: La `Activity` que contiene el `Spinner`
- **Layout**: Que se usará para dibujar cada elemento del spinner. Por ejemplo `android.R.layout.simple_spinner_item` que viene definido por Android y contiene un `TextView` con un id llamado `text1`. Este componente se actualiza con el valor del `toString()` `City`
- La **Colección de datos** creada previamente

3. También se define un **Layout** del diseño de la lista que aparece mediante el método `setDropDownViewResource(int)`. Puede usarse uno definido por Android como `android.R.layout.simple_spinner_dropdown_item`

4. Finalmente debe unirse el `Spinner` con el `Adapter` mediante `setAdap`ter()

```java
List<City> citiesList = new ArrayList<>();
citiesList.add(new City(1, "Málaga"));
citiesList.add(new City(2, "Córdoba"));
citiesList.add(new City(3, "Granada"));

ArrayAdapter<String> adapter = new ArrayAdapter<City>(this,
android.R.layout.simple_spinner_item, listCity);

arrayAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
spinnerCity.setAdapter(arrayAdapter);
```

#### 4.2.2. Eventos

Para escuchar el cambio de elemento seleccionado en el control del `Spinner` debe crearse una instancia nueva de la clase anónima `AdapterView.OnItemSelectedListener` e implementar el método:

```java
public void onItemSelected(AdapterView<?> adapterView, View view, int i, long id)
```

Este método tiene los parámetros
- **AdapterView\<?> adapterView** : Control donde ocurre el evento. Genérico para que sea `ListView` (Típica lista de Android) `GridView` (Cuadritos) o `Spinner` (Combito desplegable)
- **View view**: Objeto `View` que contiene el `TextView` que muestra el nombre de la ciudad
- **int position**: Posición del elemento en la lista en la que ha sido seleccionado
- **long id**: Id de la fila del elemento que se seleccionó. 

### 4.3. RecyclerView

El `RecyclerView` es una versión mejorada del `ListView`

Antes al usar listas era frecuente tener que personalizar el `Adapter` extendiendo de la clase `BaseAdapter` para poder implantar el **View Holder**.
Y es que al manejar gran cantidad de datos se vio que las listas eran ineficientes porque, cada vez que se hacía un desplazamiento en la lista, se creaba de nuevo cada objeto `View` con todos los controles que tuviera. 

El patrón **ViewHolder** que consiste en crear una clase que represente a la vista. Esta clase tiene como atributos los objetos `View` que se tengan que actualizar en cada fila.

---
#### Funcionamiento del ViewHolder

Al iniciar el listado se comprueba para una vista si se ha creado algún objeto `View`. 

Si el parámetro `convertView` del método `getView()`del adapter es nulo significa que aún no se ha creado y, por tanto:
1. Se crea un objeto `View` inflando el fichero XML que representa a cada elemento
2. Se crea objeto `ViewHolder`
3. Se inicializan atributos del `ViewHolder` al resultado de buscar cada componente en el objeto `View` mediante `findById()`
4. Se almacena el objeto `ViewHolder` dentro del objeto `View` mediante el método `setTag(Object object)`
5. Se devuelve el objeto `View`

Si no es nulo, se obtiene el objeto `ViewHolder` mediante el método `getTag()` de la vista. 

Así, se evita tener que llamar continuamente al método `findViewById()` para actualizar los controles de la vista. 

![](PROGRAMACION_MULTIMEDIA_DISPOSITIVOS_MOVILES/Andalucía/resources/ud02-8.png)

Android adoptó este patrón con el `RecyclerView` que obliga a usar la clase `RecyclerView.ViewHolder`. 
El `RecyclerView` reutilizará eficientemente las vistas y el usuario no tiene que hacer ninguna comprobación. 

El `RecyclerView` permite mostrar la información de diferentes formas y cambiar su diseño en tiempo de ejecución. (El `ListView` solo permite listar los elementos en formato vertical)
Puede tener los siguientes Manager:
- `LinearLayoutManager`: Definir listas verticales y horizontales
- `StaggeredLayoutManager`: Definir listas escalonadas (como imágenes de tamaños diferentes)
- `GridLayoutManager`: Los elementos se visualizan en cuadrícola (como las imágenes iguales de la Galería)

Se puede implementar: 
- `RecyclerView.ItemDecorator` para decorar las filas agregando bordes o líneas divisorias
- `RecyclerView.ItemAnimator` para agregar animaciones

El `RecyclerView` tiene la dificultad a la hora de implementar los eventos clics en el elemento (Con `ListView` era simple porque implementa la interfaz `AdapterView.OnItemClickListener`)
#### 4.3.1. Adapter

`RecyclerView.Adapter` es un `Adapter` específico de `RecyclerView` que se encarga de manejar la colección de datos y vincularla con la vista.
La vista es un objeto de la clase `RecyclerView.ViewHolder` que contiene las referencias a las `View` de cada elemento de la lista.

**Pasos para crear un Adapter:**
1. Crear clase interna `ViewHolder` para obtener las referencias a los componentes visuales.
2. Crear el constructor del `RecyclerView` que reciba el conjunto de datos (`ArrayList)
3. Crear los métodos (añadir, editar, eliminar) para gestionar el conjunto de datos
4. Sobrescribir método `onCreateViewHolder()` que infla el Layout que representa a los elementos y devuelve una instancia de la clase `ViewHolder`
5. Sobrescribir el método `onBindViewHolder()` que enlaza cada dato con cada `ViewHolder`
6. Sobrescribir el método `getItemCount()` que devuelve el número de elementos a mostrar en el `RecyclerView`

```java
public class RVAdapter extends RecyclerView.Adapter<RVAdapter.PersonViewHolder> {

	// Lista
    private List<Person> persons;

	º// Clase interna
    public static class PersonViewHolder extends RecyclerView.ViewHolder {

        CardView cv;
        TextView personName;
        TextView personAge;
        ImageView personPhoto;

        PersonViewHolder(View itemView) {
            super(itemView);
            cv = (CardView)itemView.findViewById(R.id.cv);
            personName = (TextView)itemView.findViewById(R.id.person_name);
            personAge = (TextView)itemView.findViewById(R.id.person_age);
            personPhoto = (ImageView)itemView.findViewById(R.id.person_photo);
        }
    }

	// Constructor del Adapter
    RVAdapter(List<Person> persons){
        this.persons = persons;
    }

    @Override
    public void onAttachedToRecyclerView(RecyclerView recyclerView) {
        super.onAttachedToRecyclerView(recyclerView);
        // Aquí puedes realizar configuraciones adicionales cuando el Adapter se adjunta al RecyclerView
        // Por ejemplo, configuraciones de LayoutManager, animaciones, etc.
        Log.d("MyAdapter", "Adapter adjunto al RecyclerView");
    }

	// Inflar layout de los elementos y devuelve instancia de ViewHolder
    @Override
    public PersonViewHolder onCreateViewHolder(ViewGroup viewGroup, int i) {
    View v = LayoutInflater.from(viewGroup.getContext()).inflate(R.layout.item, viewGroup, false);
        return new PersonViewHolder(v)
    }

	// Enlaza cada dato con el ViewHolder 
    @Override
    public void onBindViewHolder(PersonViewHolder personViewHolder, int i) {
        personViewHolder.personName.setText(persons.get(i).name);
        personViewHolder.personAge.setText(persons.get(i).age);
        personViewHolder.personPhoto.setImageResource(persons.get(i).photoId);
    }

	// Elementos a mostrar en el RecyclerView
    @Override
    public int getItemCount() {
        return persons.size();
    }
}
```


```java
public class RecyclerViewActivity extends Activity {

    private List<Person> persons;
    private RecyclerView rv;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.recyclerview_activity);

        rv=(RecyclerView)findViewById(R.id.rv);

        LinearLayoutManager llm = new LinearLayoutManager(this);
        rv.setLayoutManager(llm);
        rv.setHasFixedSize(true);

        initializeData();
        initializeAdapter();
    }

    private void initializeData(){
        persons = new ArrayList<>();
        persons.add(new Person("Emma Wilson", "23 years old", R.drawable.emma));
        persons.add(new Person("Lavery Maiss", "25 years old", R.drawable.lavery));
        persons.add(new Person("Lillie Watts", "35 years old", R.drawable.lillie));
    }

    private void initializeAdapter(){
        RVAdapter adapter = new RVAdapter(persons);
        rv.setAdapter(adapter);
    }
}
```

```java
public class RecyclerViewActivity extends Activity {

    private List<Person> persons;
    private RecyclerView rv;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.recyclerview_activity);

        rv=(RecyclerView)findViewById(R.id.rv);

        LinearLayoutManager llm = new LinearLayoutManager(this);
        rv.setLayoutManager(llm);
        rv.setHasFixedSize(true);

        initializeData();
        initializeAdapter();
    }

    private void initializeData(){
        persons = new ArrayList<>();
        persons.add(new Person("Emma Wilson", "23 years old", R.drawable.emma));
        persons.add(new Person("Lavery Maiss", "25 years old", R.drawable.lavery));
        persons.add(new Person("Lillie Watts", "35 years old", R.drawable.lillie));
    }

    private void initializeAdapter(){
        RVAdapter adapter = new RVAdapter(persons);
        rv.setAdapter(adapter);
    }
}
```

```java
public class CardViewActivity extends Activity {

    TextView personName;
    TextView personAge;
    ImageView personPhoto;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.cardview_activity);
        personName = (TextView)findViewById(R.id.person_name);
        personAge = (TextView)findViewById(R.id.person_age);
        personPhoto = (ImageView)findViewById(R.id.person_photo);

        personName.setText("Emma Wilson");
        personAge.setText("23 years old");
        personPhoto.setImageResource(R.drawable.emma);
    }
}
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent" android:layout_height="match_parent"
    android:padding="16dp"
    >

    <android.support.v7.widget.CardView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/cv"
        >

        <RelativeLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:padding="16dp"
            >

            <ImageView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:id="@+id/person_photo"
                android:layout_alignParentLeft="true"
                android:layout_alignParentTop="true"
                android:layout_marginRight="16dp"
                />

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:id="@+id/person_name"
                android:layout_toRightOf="@+id/person_photo"
                android:layout_alignParentTop="true"
                android:textSize="30sp"
                />

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:id="@+id/person_age"
                android:layout_toRightOf="@+id/person_photo"
                android:layout_below="@+id/person_name"
                />

        </RelativeLayout>

    </android.support.v7.widget.CardView>

</LinearLayout>
```

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent" android:layout_height="match_parent"
    android:padding="16dp"
    >

    <android.support.v7.widget.RecyclerView
        android:layout_height="match_parent"
        android:layout_width="match_parent"
        android:id="@+id/rv"
        >

    </android.support.v7.widget.RecyclerView>


</LinearLayout>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.v7.widget.CardView
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:id="@+id/cv"
    >

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:padding="16dp"
        >

        <ImageView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/person_photo"
            android:layout_alignParentLeft="true"
            android:layout_alignParentTop="true"
            android:layout_marginRight="16dp"
            />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/person_name"
            android:layout_toRightOf="@+id/person_photo"
            android:layout_alignParentTop="true"
            android:textSize="30sp"
            />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/person_age"
            android:layout_toRightOf="@+id/person_photo"
            android:layout_below="@+id/person_name"
            />

    </RelativeLayout>

</android.support.v7.widget.CardView>
```

#### 4.3.2. Eventos

Para implementar un evento dentro de cada vista, hay que crear un listener que controle el comportamiento en el `Adapter`.
Opciones:
1. Que sea el `RecyclerView` el que implemente `View.OnClickListener`. Simplifica el manejo de clics en la Activity o Fragmento pero puede hacer que el código del Adapter sea menos modular.
2. Que sea `ViewHolder` la que implemente `View.OnClickListener`. Cada ViewHolder maneja su propio clic, lo que puede mejorar la modularidad y la claridad del código.
3. Que la `Activity` implemente `View.OnClickListener` a través de un listener y el `RecyclerView` tenga que llamar al listener de la `Activity`. Utiliza una interfaz para manejar clics, lo que permite una mayor separación de responsabilidades y facilita la reutilización del Adapter en diferentes actividades o fragmentos.

**Opción 1**

En esta opción, el Adapter o el propio RecyclerView gestiona los eventos de clic directamente. Puedes definir el `OnClickListener` en el Adapter y luego asignarlo a las vistas de cada ítem en el método `onBindViewHolder`.

```java
public class MyAdapter extends RecyclerView.Adapter<MyAdapter.MyViewHolder> {

    private List<String> dataList;
    private View.OnClickListener clickListener;

    // Constructor del Adapter
    public MyAdapter(List<String> dataList, View.OnClickListener clickListener) {
        this.dataList = dataList;
        this.clickListener = clickListener;
    }

    // Clase ViewHolder
    public static class MyViewHolder extends RecyclerView.ViewHolder {
        public TextView textView;

        public MyViewHolder(View itemView) {
            super(itemView);
            textView = itemView.findViewById(R.id.textView);
        }
    }

    @Override
    public MyViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        View itemView = LayoutInflater.from(parent.getContext())
                .inflate(R.layout.item_layout, parent, false);
        return new MyViewHolder(itemView);
    }

    @Override
    public void onBindViewHolder(MyViewHolder holder, int position) {
        String data = dataList.get(position);
        holder.textView.setText(data);
        holder.itemView.setTag(position);
        holder.itemView.setOnClickListener(clickListener);
    }

    @Override
    public int getItemCount() {
        return dataList.size();
    }
}

```

```java
public class MainActivity extends AppCompatActivity implements View.OnClickListener {

    private RecyclerView recyclerView;
    private MyAdapter myAdapter;
    private List<String> dataList;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        dataList = new ArrayList<>();
        for (int i = 1; i <= 20; i++) {
            dataList.add("Item " + i);
        }

        recyclerView = findViewById(R.id.recyclerView);
        recyclerView.setLayoutManager(new LinearLayoutManager(this));
        myAdapter = new MyAdapter(dataList, this);
        recyclerView.setAdapter(myAdapter);
    }

    @Override
    public void onClick(View view) {
        int position = (int) view.getTag();
        String item = dataList.get(position);
        Toast.makeText(this, "Clicked: " + item, Toast.LENGTH_SHORT).show();
    }
}

```


**Opción 2**

```java
public class MyAdapter extends RecyclerView.Adapter<MyAdapter.MyViewHolder> {

    private List<String> dataList;

    // Constructor del Adapter
    public MyAdapter(List<String> dataList) {
        this.dataList = dataList;
    }

    // Clase ViewHolder
    public static class MyViewHolder extends RecyclerView.ViewHolder implements View.OnClickListener {
        public TextView textView;
        private List<String> dataList;

        public MyViewHolder(View itemView, List<String> dataList) {
            super(itemView);
            this.dataList = dataList;
            textView = itemView.findViewById(R.id.textView);
            itemView.setOnClickListener(this);
        }

        @Override
        public void onClick(View view) {
            int position = getAdapterPosition();
            String item = dataList.get(position);
            Toast.makeText(view.getContext(), "Clicked: " + item, Toast.LENGTH_SHORT).show();
        }
    }

    @Override
    public MyViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        View itemView = LayoutInflater.from(parent.getContext())
                .inflate(R.layout.item_layout, parent, false);
        return new MyViewHolder(itemView, dataList);
    }

    @Override
    public void onBindViewHolder(MyViewHolder holder, int position) {
        String data = dataList.get(position);
        holder.textView.setText(data);
    }

    @Override
    public int getItemCount() {
        return dataList.size();
    }
}

```

**Opción 3**
```java
public class MyAdapter extends RecyclerView.Adapter<MyAdapter.MyViewHolder> {

    private List<String> dataList;
    private OnItemClickListener onItemClickListener;

    public interface OnItemClickListener {
        void onItemClick(int position);
    }

    // Constructor del Adapter
    public MyAdapter(List<String> dataList, OnItemClickListener onItemClickListener) {
        this.dataList = dataList;
        this.onItemClickListener = onItemClickListener;
    }

    // Clase ViewHolder
    public static class MyViewHolder extends RecyclerView.ViewHolder {
        public TextView textView;

        public MyViewHolder(View itemView, OnItemClickListener listener) {
            super(itemView);
            textView = itemView.findViewById(R.id.textView);
            itemView.setOnClickListener(v -> {
                int position = getAdapterPosition();
                if (position != RecyclerView.NO_POSITION) {
                    listener.onItemClick(position);
                }
            });
        }
    }

    @Override
    public MyViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        View itemView = LayoutInflater.from(parent.getContext())
                .inflate(R.layout.item_layout, parent, false);
        return new MyViewHolder(itemView, onItemClickListener);
    }

    @Override
    public void onBindViewHolder(MyViewHolder holder, int position) {
        String data = dataList.get(position);
        holder.textView.setText(data);
    }

    @Override
    public int getItemCount() {
        return dataList.size();
    }
}

```

```java
public class MainActivity extends AppCompatActivity implements MyAdapter.OnItemClickListener {

    private RecyclerView recyclerView;
    private MyAdapter myAdapter;
    private List<String> dataList;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        dataList = new ArrayList<>();
        for (int i = 1; i <= 20; i++) {
            dataList.add("Item " + i);
        }

        recyclerView = findViewById(R.id.recyclerView);
        recyclerView.setLayoutManager(new LinearLayoutManager(this));
        myAdapter = new MyAdapter(dataList, this);
        recyclerView.setAdapter(myAdapter);
    }

    @Override
    public void onItemClick(int position) {
        String item = dataList.get(position);
        Toast.makeText(this, "Clicked: " + item, Toast.LENGTH_SHORT).show();
    }
}

```

## 5. Recursos de la interfaz de usuario

En la carpeta **res/** de los proyectos Android hay diversas subcarpetas donde se almacenan los ficheros que contienen los recursos. Cuantos más recursos alternativos existan, más posibilidades habrá de que la aplicación pueda mostrarse a un mayor número de dispositivos.

Al compilar el proyecto se genera automáticamente la clase `R.java` que contiene un ID `static int`por cada recurso definido en `res/`. Este ID permite acceder al recurso desde un fichero Java. 

Para cada recurso, hay una subclase R que se indica en esta tabla:

Recursos usados en una aplicación

| Recurso XML       | Recurso Java | Funcionalidad                                                                                                                                  |
| ----------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **res/anim/**     | R.anim       | Animaciones del proyecto.                                                                                                                      |
| **res/drawable/** | R.drawable   | Subcarpetas que almacenan los gráficos o imágenes dependiendo de la densidad de la pantalla del dispositivo (hdpi, mdpi, ldpi, etc.).          |
| **res/font/**     | R.font       | Fuentes personalizadas del proyecto (ficheros .ttf, .ttc, .otf o .xml)                                                                         |
| **res/layout/**   | R.layout     | Plantillas en formato XML de las pantallas.                                                                                                    |
| **res/menu/**     | R.menu       | Ficheros de menú de las actividades y fragments.                                                                                               |
| **res/mimap/**    | R.mipmap     | Icono de la aplicación. Se debe identificar el icono de la pantalla por cada tipo de densidad y colocar el icono en diferentes carpetas mimap. |
| **res/raw/**      | R.raw        | Recursos en formato binario (vídeos y sonido)                                                                                                  |
| **res/values/**   |              | Recursos varios (color, estilo, cadenas de caracteres)                                                                                         |
| **res/xml/**      | R.xml        | Otros ficheros XML. Se suelen guardar los ficheros que hacen referencia a las preferencias.                                                    |
**En res/values/ se almacenan**
- **strings.xml**: textos que se muestran
- **dimens.xml**: medidas en dp aplicados a atributos como margin, padding...
- **arrays.xml**: matrices de recursos 
- **styles.xml**: estilos 
- **colors.xml**: colores 

En subcarpetas para organizar los ficheros no puede usarse "res/". Sí se puede crear la carpeta "assets/" en el mismo nivel que "res/". Ahí pueden usarse nombres de archivos con mayúsculas o signos (lo que no está permitido dentro de "/res"). Esos recursos no tienen ID en el fichero `R.java` sino que son leídos por `AssetManager` con un flujo de bytes.

Hay dos tipos de recursos:
- **Recursos por defecto**: Tomados por la aplicación cuando no hay definida configuración especial y no hay definido recurso alternativo
- **Recurso alternativo**: Guardado en el lugar específico mediante un sufijo para indicar cuándo deben ser usados 
### 5.1. Según la orientación de pantalla

- Crear carpeta **/res/layout-land** Orientación horizontal (landscape). Se crea directorio igual que el original pero con el sufijo "-land"
- Crear fichero XML de la nueva plantilla alternativa. Igual que la por defecto. 
### 5.2. Según la configuración del idioma

- **/res/values/string.xml** 
Para otro idioma, añadir el sufijo del idioma correspondiente `/res/values-ca/string.xml`

```xml
<resources>
    <string name="app_name">My Application</string>
    <string name="hello_world">Hello, World!</string>
</resources>
```

```xml
<resources>
    <string name="app_name">La Meva Aplicació</string>
    <string name="hello_world">Hola, Món!</string>
</resources>
```

### 5.3. Según las características de la pantalla

Considerando tamaño y densidades de pantalla. 

/res/mipmap/ic_launcher.png  (Icono de la aplicación, adaptado para diferentes densidades)
En /res/drawable  pueden crear subcarpetas con los usfijos para que la aplicación acceda a cada una de ellas. (drawable-ldpi, drawable-mdpi, drawable-hdpi, drawable-xhdpi, drawable-xxhdpi, drawable-xxxhdpi)
También se pueden personalizar los elementos del layout añadiendole sufijo a /res/layout/ (layout-small, layout-normal, layout-arge, layout-xlarge)

### 5.4. Imágenes de una aplicación

Android Studio contiene **Image Asset** que permite crear iconos:
- Iconos de selector (Launcher icon): Representa a la aplicación en la pantalla de inicio del dispositivo, en Google Play Store...
- Iconos de pestañas y barras de acciones: Se muestran en la barra de acción, representan una acción individual. Los iconos tienen múltiples pestañas o tabs que se almacenan en res/drawable-density
- Iconos de notificaciones: Permite identificar que una notificación petenece a la aplicación res/drawable-density.

También tiene otra (**Vector Asset**) para agregar iconos de material predefinidos junto con su propio Gráfico vectorial escalable (SVG) y Adobe Photoshop (PSD) como archivos vectoriales. Imágenes vectoriales no son compatibles con inferiores a Android 4.4. (API 20). 
Esta herramienta crea recursos Vector Drawable quepueden ser soportados si se le agrega en el build.gradle la línea siguiente:

```
android {   
defaultConfig {
                vectorDrawables.useSupportLibrary = true   
                ..... 
              } 
}
```

## 6. Temas y estilos

Estilo y tema son conceptos similares al recopilar características de apariencia común a los objetos que se vayan a aplicar.

Los **estilos** se asocian a objetos de tipo `View`. Se almacenan en /res/values/ en el ficheor `style.xml`. Existen estilos predefinidos y pueden crearse otros nuevos heredando de un estilo padre...

```xml
<resources>
    <style name="EstiloNuevo" parent="@android:style/TextAppearance.Medium">
     <item name="android:textColor">#00FF00</item>
     <!-- Escribir el resto de items que se desean personalizar -->
    </style>
</resources>
```

Se aplican usando el atributo `style`

```xml
<TextView style=”@style/EstiloNuevo”
     android:text=”@string/Saludo” >
```


Los **temas** se aplican a una actividad concreta en lugar de a cada elemento . Solo se aplicarán características que soporte cada elemento. 
En el fichero de manifiesto debe editarse para que se aplique a toda la aplicación o a una actividad concreta:

```xml
<application android:theme="@style/TemaNuevo"
<activity android:theme="@style/TemaNuevo">
```

-----

Por otro lado:
res/values-night/colors.xml` (Colores nocturnos)
res/values-night/styles.xml (Estilo nocturno)
## 7. Barra de acción

El **ActionBar** es el elemento que presenta el nombre de la aplicación o actividad en la que e lusuario se encuentra, los botones de acciones disponibles y el menú de Overflow (desbordamiento) representado por el icono de tres puntos verticales. (Apareció en Android 3.0 y es nativo de Android, mostrándose de forma diferente según la versión)

Google creó el componente **ToolBar** que se encuentra en la librería de soporte y que no depende de la versión de Android. Hereda de `ViewGroup` y es más flexible que ActionBar. Puede usarse por ejemplo para añadir un título dentro de una tarjeta `CardView`

Se debe:

- **Deshabilitar la barra de acción con un `theme` `NoActionBar` en el elemento  `<application>` del fichero manifiesto:
```xml
android:theme="@android:style/Theme.AppCompat.Light.NoActionBar"
```

- Añadir el widget `Toolbar` en todos los diseños de actividades con el siguiente código:
```xml
<androidx.appcompat.widget.Toolbar
  android:id="@+id/toolbar"
  android:layout_width="match_parent"
  android:layout_height="wrap_content"
  android:background="?attr/colorPrimary"
  android:elevation="4dp"
  android:minHeight="?attr/actionBarSize"
  android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"
  app:popupTheme="@style/ThemeOverlay.AppCompat.Light" />  
```

- Identificar la barra de herramientas establecerla como barra de acción de la aplicación
```java
@Override protected void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState); 
  setContentView(R.layout.activity_main); 
  Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
  setSupportActionBar(toolbar); }
```

A veces interesará que se anime en base al desplazamiento (scroll) de la vista del contenido (ejemplo con un `RecyclerView`. Eso se consigue con la clase `CoordinatorLayout` que coordina automáticamente todos los hijos `AppBarLayour`, `RecyclerView` y el botón flotante. 
En este caso la Toolbar está dentro de un Layour especial `AppBarLayout` que es el encargado de sincronizarse con el contenido que se desplaza mediante el atributo layout_behaviour.

```xml
app:layout_behavior="@string/appbar_scrolling_view_behavior"
```

El `AppBarLayout` permite que el `Toolbar` se despliegue o contraiga al hacer scroll. Esto es útil en una pantalla con una lista o contenido desplazable.

```xml
<androidx.coordinatorlayout.widget.CoordinatorLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <com.google.android.material.appbar.AppBarLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar">

        <com.google.android.material.appbar.CollapsingToolbarLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            app:layout_scrollFlags="scroll|exitUntilCollapsed">

            <androidx.appcompat.widget.Toolbar
                android:layout_width="match_parent"
                android:layout_height="?attr/actionBarSize"
                app:layout_collapseMode="pin"/>

        </com.google.android.material.appbar.CollapsingToolbarLayout>
    </com.google.android.material.appbar.AppBarLayout>

    <androidx.recyclerview.widget.RecyclerView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layout_behavior="@string/appbar_scrolling_view_behavior" />
</androidx.coordinatorlayout.widget.CoordinatorLayout>
```

### 7.1. Creando menú principal con submenús

El **menú** representa una serie de opciones que permiten realizar acciones en una aplicación Android.

Las acciones más importantes se muestran con icono en la barra de acción, pero el resto deben estar en el **menú desbordamiento**.

El fichero estará localizado en **/res/menu** 
Por cada opción del menú debe añadirse un elemento `item` con los atributos:
 - `android:id`
 - `android:icon` o `android:title`

En la `ActionBar` considerar el atributo `app:showAsAction` que puede tomar los valores
- `never`: nunca se mostrará el botón
- `ifRoom`:  se muestra si hay sitio para ello
- `always`:  se muestra siempre
- `withText`:  se muestra también el texto en el botón

Combinadas:
`app:showAsAction<code>="ifRoom|withText"`

Se puede tener un menú con un submenú dentro de una de las opciones:

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android" >
        android:id="@+id/action_settings"
        android:title="@string/menu_settings"
        android:orderInCategory="98">
         <menu>
            <item android:id="@+id/action_modo_noche"
                  android:title="@string/menu_modo_noche" />
        </menu>
    </item>
   ...........
</menu>
```

Llamar al menú desde la clase donde se quiere que se visualice:
```java
public boolean onCreateOptionsMenu(Menu menu) {
getMenuInflater().inflate(R.menu.menu, menu);
return true;
}
```

La funcionalidad de los botones se consigue sobreescribinedo el método **onOptionItemSelected** 

```java
public boolean onOptionsItemSelected(MenuItem item) {
    switch (item.getItemId()) {
        case R.id.action_order:
            Toast.makeText(this,
                    "Has pulsado la opción ordenar alfabéticamente", Toast.LENGTH_SHORT).show();
            return true;
        case R.id.action_share:
            Toast.makeText(this,
                    "Has pulsado la opción compartir", Toast.LENGTH_SHORT).show();
            return true;
        .............................................
        default:
            return super.onOptionsItemSelected(item);
    }
}
```

## 8. Mensajes al usuario

Hay varias formas:
- **Toast**: Mensajes al usuario en pantalla y se oculta en breve espacio de tiempo
- **AlertDialog**: Información para confirmar o solicitar información. Ventana de diálogo con el mensaje y uno, dos o tres botones.
### 8.1. El Toast

Al `Toast` se le pasan tres parámetros
- Contexto de la aplicación `getApplicationContext()`
- Mensaje de texto. No duran más de 5 segundos, debe ser breve el texto.
- Duración con los valores `Toast.LENGTH_SHORT` o `Toast.LENGTH_LONG`. 
```java
Toast.makeText(getApplicationContext(),”Este es el texto a mostrar”, Toast.LENGTH_SHORT).show();
```

Por defecto aparece en la parte inferior de la pantalla. 
Con `setGravity()` se puede indicar qué posición debe ocupar. 
```java
Context context = getApplicationContext();
Toast toast = Toast.makeText(context, text, duration);
toast.setGravity(Gravity.CENTER|Gravity.RIGHT 0, 0);
toast.show();
```

### 8.2. El AlertDialog

`AlertDialog` define estilo y estructura, pero es necesario apoyarse en `DialogFragment` con los controles para construir la ventana de diálogo. Necesaria la librería `android-support-v4.jar`para que funcione en dispositivos inferiores a API 11 (Android 3.0).

Hay varios tipos:
- **Alerta**: Título (opcional), mensaje y botón de aceptar
- **Confirmación**: Título (opcional), mensaje y dos botones (Aceptar, Cancelar)
- **Selección**: Título y opciones a seleccionar
- **Personalizados**: Layout personalizado y botón de aceptar

**Pasos**
1. Crear clase que extienda de `DialogFragment` y sobreescribir `onCreateDialog()`
2. Crear objeto `AlertDialog.Builder` cuyos métodos sirven para asignar propiedades a la ventana de diálogo
	1. `setTitle()`: Título de ventana. Opcional.
	2. `setMessage()`: Texto del mensaje
	3. `setPositiveButton()`: Botón de OK
	4. `setNegativeButton()`: Botón de cancelar

```java
public class EjemploAlertDialog extends DialogFragment {
    @Override
    public Dialog onCreateDialog(Bundle savedInstanceState) {
        //Creamos el objeto AlertDialog.Builder
        AlertDialog.Builder builder =
                new AlertDialog.Builder(getActivity());
        // Asignamos las propiedades que se mostrarán.
        builder.setTitle("Importante")
            .setMessage("Debes leer este mensaje.")
               .setPositiveButton("Aceptar", 
               new DialogInterface.OnClickListener() {
                   public void onClick(DialogInterface dialog, int id) {
                            //Acciones a realizar cuando pulsamos el botón.
                    dialog.cancel();
                   }
               });     
        return builder.create();
    }
}
```

Para indicar que debe abrirse, por ejemplo al pulsar un butón se usa `getSuportFragmentManager()`

```java
boton.setOnClickListener(new View.OnClickListener() {
    public void onClick(View v) {
        FragmentManager fragmentManager = getSupportFragmentManager();
           DialogoAlerta dialogo = new DialogoAlerta();
        dialogo.show(fragmentManager, "tagAlerta");
    }
});
```
### 8.3. El SnackBar

Da un comentario breve respecto a una acción y se muestra en la parte inferior de la pantalla.
Ofrece capacidad de realizar una acción como UNDO o RETRY.
Funciona como un Toast ya que desaparece después de un tiempo de espera. Pero es posible desactivarlo cuando el usuario pulsa en otra parte de la pantalla o lo descarta desplazando el Snackbar hacia un lateral.

Se utiliza el método  `make()`

```java
public void simpleSnackbar(View view){ 
    Snackbar.make(view, getString(R.string.message), Snackbar.LENGTH_SHORT) .show(); }
```

El método `make()` admite tres parámetros:
- `view`: Raíz de la actividad
-  `R.string.message`: Mensaje del snackbar
- `Snackbar.LENGTH_LONG`: Tiempo

El encadenamiento de make() y show() se llama "method chaining", evita uso de variables intermedias. 

Se debe usar como diseño raíz un `CoordinatorLayout` en el caso de que el diseño tenga el botón `FloatingActionButton`. **Así el botón se desplaza automáticamente hacia arriba para mostrar el mensaje en la parte inferior de la pantalla y cuando desaparece el mensaje vuelve a su posición original.**

**Añadir una acción**
Es muy sencillo:
```java
public void actionSnackbar(View view){
       Snackbar.make(view, getString(R.string.hello), Snackbar.LENGTH_LONG)
               .setAction(getString(R.string.toast), new View.OnClickListener() {
                   @Override
                   public void onClick(View view) {
                       Toast.makeText(MainActivity.this, getText(R.string.action), Toast.LENGTH_SHORT).show();
                   }
               }).show();
   }
```

## 9. Creando menú contextual

El menú contextual se crea igual que el menú principal. 
Pero, si se tienen varios elementos en pantalla ¿pueden abrirse diferentes menús contextuales según el objeto sobre el que se pulse? ¿cómo se guardan los menús?

Se debe crear XML en /res/menu
```xml
<?xml version="1.0" encoding="utf-8"?><br /><menu xmlns:android="http://schemas.android.com/apk/res/android" >
	<item android:id="@+id/opCtx1" android:title="@string/opCtx1"></item>
	<item android:id="@+id/opCtx2" android:title="@string/opCtx2"></item>
</menu>
```

En el fichero Java de la clase principal se registra en el método `onCreate()` con el método `registerForContextMenu()`

```java
TextView etiqueta = (TextView)findViewById(R.id.textView2);
registerForContextMenu(etiqueta);
```

Se añade este método para mostrar el menú
```java
public void onCreateContextMenu(ContextMenu menu, View v,ContextMenuInfo menuInfo){
    super.onCreateContextMenu(menu, v, menuInfo);
 
    MenuInflater inflater = getMenuInflater();
    inflater.inflate(R.menu.mcontextualetiqueta, menu);
}
```

La funcionalidad según la pulsación se usa el método 
```java
public boolean onContextItemSelected(MenuItem item) {
 
    switch (item.getItemId()) {
        case R.id.opCtx1:
             Toast.makeText(getApplicationContext(),
                    "Opción 1 del menú contextual", Toast.LENGTH_SHORT).show();
            return true;
        case R.id.opCtx2:
             Toast.makeText(getApplicationContext(),
                    "Opción 2 del menú contextual", Toast.LENGTH_SHORT).show();
            return true;
        default:
            return super.onContextItemSelected(item);
    }
}
```

## 10. Actividades e intenciones

Con los objetos de la clase **Intent** se solicita una acción abstracta a un componente de la aplicación. Usualmente es iniciar una actividad pero también pueden iniciarse servicios y receptores de transmisión.

Los `Intent` pueden clasificarse en:
- **intents explícitos**: Se indica la clase que se quiere lanzar. 
- **intents implícitos**: Se sabe lo que se quiere realizar pero no qué clase lo hace

### 10.1. Creando nueva actividad y comunicando varias actividades

Crear una clase Java que se almacena en la carpeta **/src**. Crear como recurso una plantilla XML en **/res/layout/

Ponemos un `Button` y en su método `onClick` ponemos el método que genera el `Intent`

```java
package com.example.usuario.holamundo;

import android.content.Intent;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.view.View.OnClickListener;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity implements OnClickListener{

    protected static final int REQUESTCODE_SECOND_ACTIVITY = 10;
    private Button btSend;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        btSend=findViewById(R.id.btSend);
        btSend.setOnClickListener(this);
    }
    public void onClick(View v){
        sendMessage();
    }

    public void sendMessage(){
        Intent intent = new Intent(this,SecondActivity.class);
        startActivityForResult(intent, REQUESTCODE_SECOND_ACTIVITY);
    }
```

Se indica el propio contexto de la actividad y el nombre de la clase de Java que debe lanzarse.
Se lanza la segunda actividad mediante `startActivityForResult` (en lugar de `startActivity()` porque en este caso se quiere obtener el resultado obtenido por la segunda actividad en forma de otro `Intent`. Se pasa por parámetro identificador `REQUESTOCDE_SECOND_ACTIVITY` para saber qué actividad se ha iniciado y de la que se podrá obtener una respuesta (porque desde la actividad principal se podría llamar a varias actividades secundarias).

**Siempre comprueba que la segunda actividad esté también registrada en el manifest**

### 10.2. Pasar parámetros de la actividad principal a otra segundaria

#### Con el Intent

Los parámetros se insertan con `putExtra` dando un nombre para poder recuperarlos posteriormente. (Extras del Intent). Pueden adjuntarse enteros, flotantes, bytes, caracteres...
Luego se recupera en la actividad secundaria en el método `onCreate()` declarando un `Intent` y recuperando el parámetro dependiendo del tipo que tuviese `getExtra...()`

```java
Intent intent = new Intent(this, SecondActivity.class);
intent.putExtra("message", "Nos vemos a las 12:00");
startActivity(intent);
```


```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_second);

    Intent intent = getIntent();
    String message = intent.getStringExtra("message");

    TextView txvCaption = findViewById(R.id.txvCaption);
    txvCaption.setText("Mensaje recibido: " + message);
}
```

#### Con el Bundle

Puede crearse un objeto `Bundle` y con `putType` y `getType` almacenar y recuperar datos. Es útil para datos que se quieren pasar juntos. 

```java
// 1. Crear el objeto Bundle
Bundle bundle = new Bundle();

// 2. Añadir parámetros mediante clave-valor
bundle.putString("student", "Andrés Pandora");
bundle.putInt("studentid", 12);
bundle.putIntArray("notes", new int[]{5, 7, 2, 10, 8});

// 3. Crear e inicializar el objeto Intent
Intent intent = new Intent(this, ThirdActivity.class);

// 4. Añadir el objeto Bundle al Intent
intent.putExtras(bundle);

// 5. Iniciar la actividad
startActivity(intent);
```

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_third);

    // 1. Recoger el Intent que ha recibido la actividad al inicio
    Intent intent = getIntent();

    // 2. Recoger el objeto Bundle
    Bundle bundle = intent.getExtras();

    // 3. Obtener los parámetros del objeto Bundle
    String userName = bundle.getString("student");
    int userId = bundle.getInt("studentid");
    int[] notes = bundle.getIntArray("notes");

    // Mostrar los datos recibidos (ejemplo)
    TextView userNameTextView = findViewById(R.id.userNameTextView);
    userNameTextView.setText("Nombre: " + userName);

    TextView userIdTextView = findViewById(R.id.userIdTextView);
    userIdTextView.setText("ID: " + userId);

    TextView notesTextView = findViewById(R.id.notesTextView);
    notesTextView.setText("Notas: " + Arrays.toString(notes));
}
```

### 10.3. Obtener resultado de una actividad secundaria

Cuando la segunda actividad es iniciada con `startActivityForResult()`, esta puede devolver mediante el método:

```java 
setResult(int resultCode, Intent data)
```

El primer parámetro indica si la actividad se ha ejecutado bien o no (`RESULT_OK`, `RESULT_CANCELED`)
El segundo contiene el `Intent` a devolver... que podría tener parámetros que la primea actividad necesite.
La actividad secundaria finalizará y el control irá a la principal con `finish()`

```java
public void onClick(View v){
    Intent data = new Intent();
    data.putExtra("return", "Venimos de la segunda pantalla");
    setResult(RESULT_OK, data);
    finish();
}
```

En la actividad principal se sobrescribe el método `onActivityResult()`, que se ejecutará cuando la segunda actividad finalice: 

```java
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == REQUESTCODE_SECOND_ACTIVITY){
        if (resultCode == RESULT_OK){
            String valor = (String) data.getExtras().get("return");
            Toast toast =
                    Toast.makeText(getApplicationContext(),
                            valor, Toast.LENGTH_SHORT);

            toast.show();
        }
    }
}
```
## 11. Fragmentos

Los fragmentos surgen con la versión 3.0 de Android (API 11), debido a aparecer en el mercado diferentes dispositivos con diferentes tamaños de pantalla. El diseño de la interfaz tenía que adaptarse para aprovechar al máximo el espacio de pantalla en cualquier orientación `Landscape` y `Portrait`.

Un `Fragment` es una porción de interfaz de usuario que está dentro de una actividad (diseño propio, recurso Layout) y tiene su propio ciclo de vida aunque está ligado al ciclo de vida de la `Activity` de la que depende. Por  ej.: Actividad pausada, fragmentos lo están. Actividad destruida, fragmentos son destruidos.

Los fragmentos pueden ser
- **Estáticos**: Declarados directamente en el fichero XML o Layout de la Activity. Una vez que el fragmento está visible no puede ser eliminado ni sustituido por otro.
- **Dinámicos:** Creado en código Java y añadido dentro de un `ViewGroup`, por ejemplo, un `FrameLayout`. Será el contenedor de fragmentos que se añaden y se eliminan en tiempo de ejecución.

Las clases que herendan de `Fragment` deben implementar los métodos:
- `onCreate()`: El sistema operativo lo llama para crear el fragmento. Se deben inicializar los componentes del fragmento de forma que se conserven si el fragmento se detiene  y se reanuda.
- `onCreateView()`: Se llama para dibujar la interfaz gráfica del fragmento de forma que sea visible en la `Activity`. Se devuelve un objeto `View` resultado de inflar el `Layout` del fragmento. Puede ser nulo si el fragmento no tiene IU.
- `onPause()`: Si la actividad que lo contiene entra en pausa, se llama automáticamente a este método. Guardar los valores que se deban mostrar al usuario cuando la actividad se reanude de nuevo, mostrando la interfaz como el usuario la dejó. 

El SO es el que se encarga del control del ciclo de vida. 
Cuando llama a `onStart()` de la Activity, llama luego a `onStart()` de los fragmentos y hasta que no terminan esos `onStart()`, no finaliza el `onStart()` de la activity.

Esta secuencia de llamadas que el sistema realiza (métodos callback) deben tenerse en cuenta y no implementar operaciones largas en el tiempo que bloqueen el proceos. 

En diseños para tablets donde interesa que una parte de la interfaz quede fija es muy bueno usar fragmentos. 

![](PROGRAMACION_MULTIMEDIA_DISPOSITIVOS_MOVILES/Andalucía/resources/ud02-9.png)
### 11.1 Transacciones de fragmentos

Los fragmentos se añaden y eliminan mediante transacciones que se guardan en la pila interna que gestiona cada actividad que está en la pila de transacciones. Cuando el usuario presiona el botón atrás, el sistema operativo deshace la última transacción de fragmentos de la actividad que se encuentra en la cima de la pila de actividades.

Si hay un giro de pantalla sabemos que la Activity se destruye ¿pero qué pasa con la pila de fragmentos?: El sistema Android restaura automáticamente esa pila de fragmentos de forma que no se pierde, y si creamos un nuevo fragmento se posicionará encima de los que ya estaban guardados.

1. Definir fragmento
```java

public class ExampleFragment extends Fragment {

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        // Inflar el diseño para este fragmento
        return inflater.inflate(R.layout.fragment_example, container, false);
    }
}
```

2. Crear diseño de fragmento
```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello from ExampleFragment!" />

</LinearLayout>
```

3. Añadir fragmento a actividad
```java
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <FrameLayout
        android:id="@+id/fragment_container"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
</RelativeLayout>
```

4. Cargar fragmento en `onCreate` de la actividad

```java
// MainActivity.java
package com.example.myapp;

import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;
import androidx.fragment.app.FragmentManager;
import androidx.fragment.app.FragmentTransaction;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Añadir el fragmento solo si el estado guardado es nulo
        if (savedInstanceState == null) {
            ExampleFragment exampleFragment = new ExampleFragment();
            getSupportFragmentManager().beginTransaction()
                .add(R.id.fragment_container, exampleFragment)
                .commit();
        }
    }
}
```

En una transacción de fragmentos se puede "Editar"

5. Interacción actividad fragmento

```java
// Fragmento
// ExampleFragment.java
public void updateText(String text) {
    TextView textView = getView().findViewById(R.id.textView);
    textView.setText(text);
}


// Actividad
// MainActivity.java
ExampleFragment fragment = (ExampleFragment) getSupportFragmentManager().findFragmentById(R.id.fragment_container);
if (fragment != null) {
    fragment.updateText("New Text");
}
```


### 11.2 Comunicación con una Activity

El `Fragment` se comunica con la `Activity` que lo contiene porque envía o recibe información que necesita.

Es fácil comunicar fragmento con actividad mediante interfaces. **Definir interfaz en un fragmento y dejar que la actividad lo implemente**

1. Definir interfaz con la acción

```java
  interface ListNoteFragmentCallback { 
      void  onNoteView(Note note); 
  } 
```

2. Implementar interfaz en la actividad
```java
  public class MainActivity extends AppCompatActivity                       implements ListNoteFragment.ListNoteFragmentCallback
```

3. Adquirir instancia de interfaz desde el Fragment

```java

public void onAttach(Context context) {
   super.onAttach(context);
   try {
       callback = (ListNoteFragmentCallback) context;
   } catch (ClassCastException e) {
               throw new ClassCastException(context.toString() + " must implement 
            ListNoteFragmentCallback");
   }
} 
```

3. Invocar instancia cuando sea necesario

```java
listener = new NoteAdapter.OnItemClickListener() {
    @Override
    public void onItemClick(Note note) {
        callback.onNoteView(note);
    }
};
```
### 11.3. Pasar argumentos a un fragmento

Debemos asegurarnos que los argumentos se pasan al fragmento justo cuando se usa un método estático `newInstance()` para crear el fragmento, poniendo los parámetros que se desee en un objeto `Bundle` que estará disponible al crear una nueva instancia:

```java
public static Fragment newInstance(Bundle bundle) {
        ViewNoteFragment fragment = new ViewNoteFragment();
        if (bundle != null) {
           fragment.setArguments(bundle);
        }
        return fragment;
    }
```

Más adelante en el fragmento se puede acceder al objeto Bundle mediante el método getArguments():

```java
@Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);
        tvTitle = view.findViewById(R.id.tvTitle);
        tvContent = view.findViewById(R.id.tvContent);
        if (getArguments() != null) {
        Note note = getArguments().getParcelable(Note.TAG);
            tvTitle.setText(note.getTitle());
            tvContent.setText(note.getContent());
        }
    } 
```

Finalmente la actividad inicia el fragmento mediante el método `newInstance()` con un parámetro de tipo Bundle que contiene el objeto Note:

```java
 @Override
     public void onNoteView(Note note) {
         FragmentManager fm=getSupportFragmentManager();
         viewNoteFragment = (ViewNoteFragment) fm.findFragmentByTag(ViewNoteFragment.TAG);
         if (viewNoteFragment == null) {
             Bundle bundle= null;
             if (note!=null){
                 bundle= new Bundle();
                 bundle.putParcelable(Note.TAG,note);
             }
             viewNoteFragment = (ViewNoteFragment) viewNoteFragment.newInstance(bundle);
         }
         FragmentTransaction ft = fm.beginTransaction();
         ft.replace(R.id.fragmentcontainer, viewNoteFragment, ViewNoteFragment.TAG);
         ft.addToBackStack(null);
         ft.commit();
} 
```

**Para que un objeto de la clase Note se pueda pasar como argumento debe implementar la interfaz Parcelable,**  añadiendo implements Parcelable en la declaración de la clase.


----------------


### Paso de un fragmento a otro

**Actividad como intermediario**

```java
import android.os.Parcel;
import android.os.Parcelable;

public class DatosParcelable implements Parcelable {
    private String nombre;
    private int edad;

    // Constructor
    public DatosParcelable(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    // Métodos de getter y setter

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public int getEdad() {
        return edad;
    }

    public void setEdad(int edad) {
        this.edad = edad;
    }

    // Implementación de Parcelable

    protected DatosParcelable(Parcel in) {
        nombre = in.readString();
        edad = in.readInt();
    }

    public static final Creator<DatosParcelable> CREATOR = new Creator<DatosParcelable>() {
        @Override
        public DatosParcelable createFromParcel(Parcel in) {
            return new DatosParcelable(in);
        }

        @Override
        public DatosParcelable[] newArray(int size) {
            return new DatosParcelable[size];
        }
    };

    @Override
    public int describeContents() {
        return 0;
    }

    @Override
    public void writeToParcel(Parcel dest, int flags) {
        dest.writeString(nombre);
        dest.writeInt(edad);
    }

```

```java
// Fragmento1.java
public class Fragmento1 extends Fragment {
    public interface OnDataPassedListener {
        void onDataPassed(DatosParcelable datos);
    }

    private OnDataPassedListener listener;

    @Override
    public void onAttach(Context context) {
        super.onAttach(context);
        if (context instanceof OnDataPassedListener) {
            listener = (OnDataPassedListener) context;
        } else {
            throw new RuntimeException(context.toString()
                    + " must implement OnDataPassedListener");
        }
    }

    public void sendDataToActivity(DatosParcelable datos) {
        if (listener != null) {
            listener.onDataPassed(datos);
        }
    }
}
```

```java
// MainActivity.java
public class MainActivity extends AppCompatActivity implements Fragmento1.OnDataPassedListener {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    @Override
    public void onDataPassed(DatosParcelable datos) {
        // Llamar al método en el Fragmento 2 y pasar los datos Parcelable
        Fragmento2 fragmento2 = (Fragmento2) getSupportFragmentManager().findFragmentById(R.id.fragment2);
        if (fragmento2 != null) {
            fragmento2.receiveDataFromActivity(datos);
        }
    }
}
```

```java
// Fragmento2.java
public class Fragmento2 extends Fragment {
    public void receiveDataFromActivity(DatosParcelable datos) {
        // Manejar los datos Parcelable recibidos aquí
    }
}
```


**ViewModel**

1. **Crear**: Crea un ViewModel que contenga los datos que deseas compartir entre los fragmentos.


```java
import androidx.lifecycle.ViewModel;

public class SharedViewModel extends ViewModel {
    private String data;

    public void setData(String newData) {
        data = newData;
    }

    public String getData() {
        return data;
    }
}
```

2. **Observar**: En los fragmentos que necesiten acceder a estos datos, observa el ViewModel y actualiza la interfaz de usuario según sea necesario.

```java
import androidx.lifecycle.ViewModelProvider;
import androidx.lifecycle.ViewModelProviders;

public class Fragmento1 extends Fragment {
    private SharedViewModel viewModel;

    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        viewModel = new ViewModelProvider(requireActivity()).get(SharedViewModel.class);
        // Observar los cambios en los datos
        viewModel.getData().observe(getViewLifecycleOwner(), newData -> {
            // Actualizar la interfaz de usuario según sea necesario
        });
    }
}

import androidx.lifecycle.ViewModelProvider;
import androidx.lifecycle.ViewModelProviders;

public class Fragmento2 extends Fragment {
    private SharedViewModel viewModel;

    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        viewModel = new ViewModelProvider(requireActivity()).get(SharedViewModel.class);
        // Observar los cambios en los datos
        viewModel.getData().observe(getViewLifecycleOwner(), newData -> {
            // Actualizar la interfaz de usuario según sea necesario
        });
    }
}
```

3. **Actualizar:** Cuando necesites actualizar los datos en el ViewModel, simplemente llama al método `setData()` del ViewModel desde cualquier lugar donde tengas acceso al ViewModel.

```java
public class MainActivity extends AppCompatActivity {
    private SharedViewModel viewModel;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        viewModel = new ViewModelProvider(this).get(SharedViewModel.class);

        // Actualizar los datos en el ViewModel
        viewModel.setData("Nuevos datos desde la actividad");
    }
}
```


El ViewModel se crea la primera vez que se solicita desde una actividad o un fragmento mediante la llamada a `ViewModelProvider.get()` con la clase del ViewModel como argumento. Si la actividad ya ha sido creada previamente y el ViewModel ya está en memoria, se devolverá la misma instancia del ViewModel. Si la actividad es nueva o se ha reiniciado (por ejemplo, debido a un cambio de configuración), se creará una nueva instancia del ViewModel.

Con esta implementación, los datos en el ViewModel se comparten entre los fragmentos, y cualquier cambio en los datos se reflejará automáticamente en la interfaz de usuario de los fragmentos que observan el ViewModel. Esto ofrece una forma eficiente y coherente de compartir datos entre componentes en tu aplicación Android.

```java
public class MainActivity extends AppCompatActivity {
    private SharedViewModel viewModel;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Obtener una instancia de ViewModel
        viewModel = new ViewModelProvider(this).get(SharedViewModel.class);
    }
}
```

```java
public class MyFragment extends Fragment {
    private SharedViewModel viewModel;

    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        // Obtener una instancia de ViewModel
        viewModel = new ViewModelProvider(requireActivity()).get(SharedViewModel.class);
    }
}
```


## Librerías de diseño

Se utilizan las **librerías de soporte,** de forma que podemos proporcionar funciones más recientes a versiones anteriores de Android.  Ofrecen  clases y funciones  adicionales que no están disponibles en la API estándar del Framework del proyecto, y es una forma sencilla de dar soporte a más dispositivos.

Clases de la librería de compatibilidad o  soporte por ejemplo empiezan con `android.support.*,`. Caso de `AppCompatActivity`  (`import android.support.v7.app.AppCompatActivity;`)
Hay una nueva versión de la biblioteca de compatibilidad denominada AndroidX que contiene la biblioteca de compatibilidad existente e incluye los últimos componentes de **Jetpack**. (`import androidx.appcompat.app.AppCompatActivity;`)

No se puede trabajar con ambas librerías. Actualmente se usa AndroidX, aunque a veces se usará la librería de soporte. 

**Migrar un proyecto a AndroidX. Pasos a realizar:**
- Modificar el valor de compileSdk al menos a la versión 28 en el fichero build.gradle del módulo app.
- Tener al menos la versión com.android.tools.build:gradle:3.2.0 en el fichero build.grade del proyecto. (file -> Project Structure -> Project)
- Hecho esto, Refactor -> Refactor This -> Migrate to AndroidX

Una vez que ha finalizado la refactorización se puede comprobar que en el archivo gradle.properties se ha configurado a true los siguientes complementos:

- android.useAndroidX=true: que indica que se utilizará la biblioteca AndroidX de forma que cuando se añade una clase o un objeto View buscará en esta librería, no en la biblioteca de soporte.
- android.enableJetifier=true: este complemento migra automáticamente las bibliotecas de terceros existentes a  AndroidX.

## Terminología: Inflate

El concepto de "inflate" en el contexto de desarrollo de aplicaciones Android se refiere al proceso de convertir un archivo de diseño XML en objetos de vista en tiempo de ejecución. Esencialmente, inflar un diseño XML significa convertirlo en una representación de objetos de vista que pueden ser manipulados y visualizados en la pantalla del dispositivo.

Cuando inflas un diseño XML en Android, estás creando una jerarquía de objetos de vista que define la interfaz de usuario de tu aplicación. Esto es comúnmente utilizado en actividades, fragmentos, diálogos y otros componentes de la interfaz de usuario de Android.

El método inflate() se utiliza para llevar a cabo este proceso de inflado. Toma como argumentos el archivo de diseño XML que se va a inflar y, opcionalmente, el contenedor al que se adjuntarán las vistas infladas.

------------

- Servicios para descargar ficheros desde Internet o escuchar música sin bloquear una aplicación:[Servicios de Android](http://gpmess.com/blog/2014/08/14/utilizar-servicios-service-e-intentservice-en-android/ "Acceder a una página web sobre “Introducción a los servicios en Android.” (Se abre en una ventana nueva)")
- Intents implícitos para realizar llamadas, enviar mensajes, lanzar el navegador Web, etc.[Uso de intents implícitos](http://nbortolotti.blogspot.com.es/2011/05/utilizando-intents-implicitos-para.html "Acceder a una página web sobre “Utilizando intents implícitos.” (Se abre en una ventana nueva)"). 
- Sensores de los dispositivos móviles con los cuales una aplicación puede recibir datos del medio externo como la temperatura, la orientación, etc. [Manejo de sensores](http://www.androidcurso.com/index.php/tutoriales-android/36-unidad-5-entradas-en-android-teclado-pantalla-tactil-y-sensores/154-los-sensores "Acceder a una página web sobre “Detección y manejo de sensores.” (Se abre en una ventana nueva)")
- Conexiones de red: consulta de conexiones disponibles, comprobación del estado de la conexión, etc. [La clase ConnectivityManager](http://developer.android.com/reference/android/net/ConnectivityManager.html "Acceder a la página web oficial de Android sobre “La clase ConnectivityManager” (Se abre en una ventana nueva)")

