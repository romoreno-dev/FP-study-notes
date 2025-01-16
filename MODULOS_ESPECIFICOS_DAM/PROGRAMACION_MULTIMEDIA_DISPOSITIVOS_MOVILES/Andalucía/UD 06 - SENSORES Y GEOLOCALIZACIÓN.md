## 1. Métodos de entrada

**Método de entrada**: Parte del sistema operativo o de un programa que permite al usuario introducir caracteres y símbolos en una aplicación. 

Comenzó con el teclado. El más usado en los ordenadores es el sistema QWERTY (heredado de las máquinas de escribir; creado con finalidad de separar las teclas que aparecen con más frecuencia incrementando velocidad de escritura).

En el mundo móvil, inicialmente el **teclado físico alfanumérico**. Se podía nescribir mensajes a golpe de click (cada tecla contenía varios caracteres alfabéticos. Posteriormente, dispositivos con **teclado físico QWERTY**: Móvil plegable y el teclado se desliza por la parte trasera cambinado la orientación de vertical a horizontal. También teclado físico en la parte inferior de la pantalla, con un frontal compartido por la pantalla y el teclado. (T-Mobile G1; Blackberry). Finalmente, **pantallas táctiles**, nueva experiencia pulsando la pantalla o haciendo uso de gestos (Gestures) ejecutando con los dedos distintas acciones. (Surgimiento de los teclados virtuales QWERTY, inciialmente complicada por tamaño de los teclados insuficiente pero actualmente con la evolución de las pantallas táctiles son perfectamente funcionales). Hay aplicaciones específicas para la entrada de datos como `Google Keyboard` que permite soporte de múltiples idiomas, dictado por voz, predicción de palabras, introducción de caracteres por gestos...
### 1.1. Escuchador de eventos

El escuchador intercepta los **eventos**. Estos ocurren cuando el usuario interacciona con la aplicación. Se lanza desde un objeto de vista específico y se espera que un objecto de escucha (`EventListener`) asociado al componente realice una acción determinada.

Los **listeners** responden a la interacción del usuario sobre un objeto `View` cuando este es registrado o asociado a dicho objeto. 
La `View` puede registrar varios escuchadores, llamándose al método oportunido dependiendo del evento.

| **Método de la interfaz**                                                             | Descripción                                                                               | **Interfaz**                       |
| ------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ---------------------------------- |
| `onClick(View v)`                                                                     | Cuando el usuario pulsa sobre el objeto vista                                             | `View.OnClickListener`             |
| `onLongClick(View view)`                                                              | Cuando hace click en una vista y la mantiene presionada más de un segundo                 | `View.OnLongClickListener`         |
| `onFocusChange(View v, boolean hasFocus)`                                             | Cuando el elemento tiene el foco o sale de él                                             | `View.OnFocusChangeListener`       |
| `onKey(View v, int keyCode, KeyEvent event)`                                          | Cuando el usuario presiona o suelta una tecla de hjardware sobre un elemento              | `View.OnKeyListener`               |
| `onTouch(View v, MotionEvent event)`                                                  | Cuando realiza una acción táctil (presionar, soltar, gesto) en los límites de un elemento | `View.OnTouchListener`             |
| `onCreateContextMenu(ContextMenu menu, View v, ContextMenu.ContextMenuInfo menuInfo)` | Cuando se crea un menú contextual ("click largo")                                         | `View.OnCreateContextMenuListener` |

Los métodos pueden recibir dos argumentos:
- `View`, vista donde se produce el vento
- `Event`, información sobre el evento que ha ocurrido
Es posible invocar objetos de cada uno de ellos para obtener información (id de la vista con `getId()` o tecla pulsada en `KeyEvent` mediante `getKeyCode()`).

Algunos tienen como tipo de retorno un valor booleano para indicar al sistema si se usó el evento. El evento finaliza al devolver `true`. En caso de devolver `false` se propagará el vento a otros listeners. 

```java
// OnCLickListener
button.setOnClickListener(new View.OnClickListener() {
     @Override
     public void onClick(View v) {
     // Código a ejecutar en el hilo principal
     }
});

// OnLongClickListener
textview.setOnLongClickListener(new View.OnLongClickListener() {
    @Override
    public boolean onLongClick(View v) {
            // Código a ejecutar en el hilo principal
        }
});

// OnFocusChangeListener
edittext.setOnFocusChangeListener(new OnFocusChangeListener() {

    @Override
    public void onFocusChange(View v, boolean hasFocus) {
        // Código a ejecutar en el hilo principal
    }
});

// OnKeyListener
linearlayout.setOnKeyListener(new OnKeyListener() {
        @Override
        public boolean onKey(View v, int keyCode, KeyEvent event) {
            if (keyCode == KeyEvent.KEYCODE_BACK) {
                return true;
            } else {
                return false;
            }
        }
    });

// On TouchListener
imageButton.setOnTouchListener(new OnTouchListener() {
    @Override
    public boolean onTouch(View v, MotionEvent event) {
        if(event.getAction() == MotionEvent.ACTION_UP){
            // Código a ejecutar en el hilo principal 
            return true;
        }
        return false;
    }
});
```

### 1.2. Controlador de eventos

Como se ha visto, se puede crear una clase anónima interna seguido de la clase a ampliar o la interfaz a implementar.

```java
new View.OnClickListener() {
     @Override
     public void onClick(View v) {
     // Código a ejecutar en el hilo principal
     }
}
```

Pero también es posible crear una instancia de una interfaz `EventListener`  y, en la clase `Activity` o `Fragment` implementar la interfaz:

```java
public class MainActivity extends Activity implements OnClickListener{
   @Override
   protected void onCreate(Bundle savedValues) {
      Button b = (Button)findViewById(R.id.boton);
      b.setOnClickListener(this);
   }
   @Override
   public void onClick(View v) {
      //Acciones a realizar
   }
   ....
}
```

### 1.3. Teclado

Los dispositivos Android actuales tienen un teclado software (Soft Keyboard) en la pantalla conocido como método de entrada táctil (IME). Aparece al pulsar sobre un cambo de texto en la interfaz gráfica o cuando recibe el foco, permitiendo al usuario introducir texto. 

**SOLAMENTE** cuando se tiene un teclado hardware conectado al dispositivo o un dispositivo con controles de juegos o joystiks es posible controlar eventos de teclado con la clase `KeyEvent`, en ese caso el tecvlado software no aparecerá en pantalla. 

Cuando hay una actividad en primer plano con teclado software NO activan la familia de eventos `onKeyDown()` por lo que no se debe desarrollar una aplicación que requiera que se presionen teclas concretas. No hay forma de detectar de forma fiable las pulsaciones de teclas.

**Teclado físico**
Se puede controlar la pulsación de cualquier tecla o la combinación de varias. 
`onKeyUp()` se activa una vez al pulsar. Si el usuario mantiene pulsado `onKeyDown()` se activa varias veces. 
Las clases `Activity` y `View` implementan la interfaz `KeyEvent.Callback` por lo que deben sobrescribirse los métodos de devolución de llamada:

```java
   @Override
    public boolean onKeyUp(int keyCode, KeyEvent event) {
        switch (keyCode) {
            case KeyEvent.KEYCODE_D:
                //Realizar acción
                return true;
            case KeyEvent.KEYCODE_F:
                //Realizar acción;
                return true;
            case KeyEvent.KEYCODE_J:
                //Realizar acción
                return true;
            case KeyEvent.KEYCODE_K:
                //Realizar acción
                return true;
            default:
                return super.onKeyUp(keyCode, event);
        }
    }
}
```

**Teclado software**
Una posible opción es usar el listener `TextWatcher` que se activa cuando cambian los datos. Sin embargo, si se quiere usar para controlar que se ha pulsado una tecla que no ha modificado el texto no es posible usarlo. Debe usarse la interfaz `OnEditorActionListener()` que puede capturar el evento dentro del método de entrada y a continuación se pregunta por la tecla pulsada:

```java
edName.setOnEditorActionListener(new TextView.OnEditorActionListener() {
            @Override
            public boolean onEditorAction(TextView v, int actionId, KeyEvent event) {
                if (actionId == EditorInfo.IME_ACTION_SEND  || EditorInfo.IME_ACTION_UNSPECIFIED==actionId) {
                    Toast.makeText(MainActivity.this,"Se ha pulsado la tecla SEND",Toast.LENGTH_SHORT).show();
                    return true;
                }
                return false;
            }
        });
```

### 1.4. Pantalla táctil

Puede detectarse el contacto o múltiples puntos de contacto con la superficie, detectando cuando el usuario interacciona con la pantalla, ya que llama al evento `onTouchEvent(MotionEvent)` de la interfaz `onTouchListener`. 

El objeto `MotionEvent` contiene:
- **Acción realizada** ( `getAction()`). Con los tipos
	- `ACTION_DOWN`: Se presiona la pantalla y no se mueve el puntero hacia ningún lado
	- `ACTION_MOVE`: Primera pulsación en la pantalla y se mueve el puntero por ella generándose `ACTION_DOWN` y `ACTION_MOVE`
	- `ACTION_UP`: Se levanta el dedo de la pantalla (anteriormente se dio `ACTION_DOWN`)
	- `ACTION_CANCEL`: Se cancela el gesto y no se recibe ningún punto más
	- `ACTON_OUTSIDE`: Evento fuera de los límites normales de un elemento de la UI

**Todos los eventos `Touch` comienzan con `ACTION_DOWN` y terminan con `ACTION_UP`** 

- **Coordenadas** (`getX()`, `getY()`) : Posición del componente que se ha tocado o desplazado.
- **Tiempo** (`getEventTime()`): Tiempo en milisegundos desde que el usuario presionó por primera vez una cadena de eventos táctiles.
- **Presión** (`getPressure(int)`): Valor entre 0 y 1 de la presión realizada sobre la pantalla. 
- **Tamaño de la pulsación** `getSize(int)`: Aproximación del área de la pantalla que se presiona en valor escalado entre 0 y 1.

Si en la jerarquía de vistas hay una interesada en un gesto en curso, debe sobreescribirse el método `dispatchTouchEvent()`:

```java
@Override
    public boolean dispatchTouchEvent(MotionEvent ev) {
        switch (ev.getAction() & MotionEvent.ACTION_MASK) {
            case MotionEvent.ACTION_POINTER_DOWN:
                break;
            case MotionEvent.ACTION_POINTER_UP:
                break;
            case MotionEvent.ACTION_UP:
                break;
            case MotionEvent.ACTION_DOWN:
                break;
        }
            return super.dispatchTouchEvent(ev);
    }
}
```

El método `dispatchTouchEvent` es un controlador que decide cómo enrutar los eventos táctiles. Las llamadas que se realizan en una jerarquía de vistas con los eventos `Touch`:
- Cuando pulsa la pantalla el evento se puede interceptar mediante `Activity.dispatchTouchEvent()`. Si el método devuelve `false`, se entrega a la vista root o `ViewGroup` y, si no es interceptado mediante `onInterceptTouchEvent()` pasa a todas las vistas secundarias que puedan manejar el evento mediante `onTochEvent()`
- Si la vista principal (`ViewGroup`) consume el elemento a través de `onInterceptTouchEvent()`, es decir, devuelve `true` se detiene su transmisión hacia abajo y se llama al `onTouchEvent()` del elemento superior. El método `onInterceptTouchEvent()` permite a un elemento superior ver cualquier evento táctil antes de que lo hagan sus elementos secundarios. También puede devolver `false` y ocuparse de inspeccionar qué sucede.
- Si el evento no se ha detenido durante la transferencia de arriba a abajo y la vista inferior no lo consume, se invertirá hacia arriba. Entonces `ViewGroup` puede consumir el evento y si no lo se consume pasará a `onTouchEvent()` de `Activity`
- `onTouchListener()` tiene prioridad sobre `onTouchEvent()` para consumir eventos
- Si un `ViewGroup` o cualquiera de sus elementos secundarios no devuelven verdadero en `onTouchEvent()`, `dispatchTouchEvent()` y `onInterceptTouchEvent()`, solo se llamaran para `ACTION_DOWN`. Sin un `true` de `onTouchEvent` la vista principal asume que su vista no necesita `MotionEvents`.
#### Gestures

Los trazos que el usuario hace al dibujar en la pantalla táctil se conocen como gesto o `Gestures`. 
Son una secuencia de puntos de contacto con la pantalla o `MotionEvents` que contienen información de la acción realizada, dónde tuvo lugar el toque, la presión.
El sistema puede interpretar estos datos y ver si cumple  con el patrón de gestos que admite una aplicación.

Para administrar y responder a los gestos, Android proporciona el namespace `Android.Gestures`.

El sistema de gestos se integró en Android 9 Pie con la barra de navegación pudiendo acceder a la pantalla de inicio, al cajón de aplicaciones, a la vista de aplicaciones recientes, cambiar a una aplicación anterior con un gesto...

Los gestos simplifican la interfaz de usuario evitando integrar un botón para cada acción. 

Dos opciones:
- `Gesture Builder`: Permite añadir gestos personalizados a una librería de forma que posteriormente la aplicación pueda reconocer uno de los gestos guardados y realizar una acción personalizada. 
- Detectar gestos comunes `onDown()`, `onLongPress()`, `onFling()` en objetos `Activity` o `View`

#### Creación y uso de una biblioteca de gestos

Se crea una vista transparente encargada de detectar los gestos:

```xml
<android.gesture.GestureOverlayView
	android:id="@+id/gestures_overlay"
	android:layout_width="match_parent"
	android:layout_height="0dp"
	android:layout_weight="1"
	android:gestureStrokeType="multiple" />
```

Se crea la clase `GestureLibrary` que gestiona el archivo que contiene todos los gestos que la aplicación puede detectar y que han sido creados mediante Gesture Builder. Busca coincidencia con el gesto realizado por el usuario, calculando una puntuación de predicción para el gesto (puntuación de predicción de 1,.0 o más es una buena coincidencia).

```java
private GestureLibrary library;
...
@Override
protected void onCreate(Bundle savedInstanceState) {
   super.onCreate(savedInstanceState);    
   library=GestureLibraries.fromRawResource(this,R.raw.gestures);
    ...
}
```

`GesturePerformedListener`: Listener necesario que debe registrarse en `GestureOverlayView`. Al detectar un gesto, llama al método callback `onGesturePerformed()` y se pasa como argumentos una referencia a `GestureOverlayView` en el que se detectó el gesto y el objeto `Gesture` con información sobre el gesto. 

```java
public void onGesturePerformed(GestureOverlayView overlay, Gesture gesture) {
        ArrayList<Prediction> predictions = library.recognize(gesture);
        if (predictions.size() > 0 && predictions.get(0).score> 1.0) {
            String action = predictions.get(0).name;
            Toast.makeText(this, action, Toast.LENGTH_SHORT).show();
        }
    }
```

#### Uso de gestos táctiles

El gesto está formado por varios contactos con la pantalla (punteros) y que pueden darse al mismo tiempo. Puede hacerse uso de métodos de la clase `MotionEvent` para acceder al conjunto de punteros como:
- `getPointerCount()`: Número de punteros del gesto
- `getActionIndex()`: Índice del puntero. `MotionEvent` almacena cada puntero en un array, siendo el índice la posición del puntero en ese array. El índice puede cambiar de un evento al siguiente ya que el gesto consta de movimientos sucesivos. En ese caso se usará `findPointerIndex()` para obtener el índice del puntero de un ID determinado. 

En el evento multitáctil se desencadenan estos eventos táctiles: `ACTION_DOWN`, `ACTION_MOVE`, `ACTION_UP` (ya descritos) y:
- `ACTION_POINTER_DOWN`: Nuevo contacto con la pantalla o puntero y además no es el primero. Información en el índice `getActionIndex()`
- `ACTION_POINTER_UP`: Se deja de presionar un puntero y  además no es el último. 

**Multitáctil**
```java

OpenClipart-Vectors (Licencia Pixabay)
private int mActivePointerId;

public boolean onTouchEvent(MotionEvent event) {
     ...
     // Get the pointer ID
     mActivePointerId = event.getPointerId(0);

     // ... Many touch events later...

     // Use the pointer ID to find the index of the active pointer
     // and fetch its position
     int pointerIndex = event.findPointerIndex(mActivePointerId);
     // Get the pointer's current position
     float x = event.getX(pointerIndex);
     float y = event.getY(pointerIndex);
        ...
 }
```

**GestureDetector**
Android proporciona `GestureDetector` para consumir `MotionEvents` y crear eventos de gestos de mayor nivel para los oyentes. Se usa para detectar gestos táctiles básicos (desplazar, lanzar, tocar dos veces). 
- `GestureDetector`: Desplazar, lanzar, tocar dos veces
- `ScaleGestureDetector`: Procesar el gesto de dos dedos en forma de pinza y realizar cambio de escala según el gesto.

¿Cómo funcionaría? Dentro del método `onTouch()` de la `Activity` se llamaría a su método `onTouchEvent(MotionEvent)` que devolverá true si maneja el evento y false si no. Se utiliza el escuchador `OnGestureListener` o bien `SimpleOnGestureListener` si no se quieren implementar todos sus métodos.

```java
    public class MainActivity extends Activity implements
            GestureDetector.OnGestureListener,
            GestureDetector.OnDoubleTapListener{

        private static final String DEBUG_TAG = "Gestures";
        private GestureDetectorCompat mDetector;

        // Called when the activity is first created.
        @Override
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            // Instantiate the gesture detector with the
            // application context and an implementation of
            // GestureDetector.OnGestureListener
            mDetector = new GestureDetectorCompat(this,this);
            // Set the gesture detector as the double tap
            // listener.
            mDetector.setOnDoubleTapListener(this);
        }

        @Override
        public boolean onTouchEvent(MotionEvent event){
            if (this.mDetector.onTouchEvent(event)) {
                return true;
            }
            return super.onTouchEvent(event);
        }

        @Override
        public boolean onDown(MotionEvent event) {
            Log.d(DEBUG_TAG,"onDown: " + event.toString());
            return true;
        }

        @Override
        public boolean onFling(MotionEvent event1, MotionEvent event2,
                float velocityX, float velocityY) {
            Log.d(DEBUG_TAG, "onFling: " + event1.toString() + event2.toString());
            return true;
        }

        @Override
        public void onLongPress(MotionEvent event) {
            Log.d(DEBUG_TAG, "onLongPress: " + event.toString());
        }

        @Override
        public boolean onScroll(MotionEvent event1, MotionEvent event2, float distanceX,
                float distanceY) {
            Log.d(DEBUG_TAG, "onScroll: " + event1.toString() + event2.toString());
            return true;
        }

        @Override
        public void onShowPress(MotionEvent event) {
            Log.d(DEBUG_TAG, "onShowPress: " + event.toString());
        }

        @Override
        public boolean onSingleTapUp(MotionEvent event) {
            Log.d(DEBUG_TAG, "onSingleTapUp: " + event.toString());
            return true;
        }

        @Override
        public boolean onDoubleTap(MotionEvent event) {
            Log.d(DEBUG_TAG, "onDoubleTap: " + event.toString());
            return true;
        }

        @Override
        public boolean onDoubleTapEvent(MotionEvent event) {
            Log.d(DEBUG_TAG, "onDoubleTapEvent: " + event.toString());
            return true;
        }

        @Override
        public boolean onSingleTapConfirmed(MotionEvent event) {
            Log.d(DEBUG_TAG, "onSingleTapConfirmed: " + event.toString());
            return true;
        }
    }
```

La clase `GestureDetector` detecta los siguientes gestos:
- `onSingleTapUp`: Toque a la pantalla. Pulsar y levantar el dedo. Evento tras leventar el dedo
- `onDoubleTap`: Doble toque
- `onSingleTapConfirmed`: Solo un toque y no hay segundo
- `onLongPress`: Pulsación larga en la pantalla
- `onScroll`: Arrastrar el dedo para realizar scroll. Argumento: Distancia que se ha arrastrado en eje X e Y
- `onFling`: Lanzamiento. Pulsar, arrastrar y soltar. Argumento: Velocidad en px del lanzamiento en el eje X e Y. 

### 1.5. Sensores en Android

El **sensor** es un dispositivo capaz de detectar una magnitud física o química (temperatura, intensidad lumínica, distancia, aceleración, inclinación, desplazamiento, presión, fuerza, torsión, humedad, movimiento...)

Quitando la memoria y el procesador, los sensores que incluyen los teléfonos inteligentes establecen las prestaciones que engloban a un dispositivo en gamas baja, media o alta. 

Los sensores diferencian a un móvil de un portátil. Las funciones importantes de un móvil están asociadas a un sensor (ajustar brillo de pantalla, girar imagen, identificar huella digital...)

La cámara, el micrófono y el GPS son sensores pero usan clases diferentes para su uso dentro de Android. Para el resto de sensores Android usa el mismo marco de trabajo en el que se puede:
- Comprobar si el sensor está disponible
- Determinar las capacidades del sensor
- Adquirir datos del sensor y tasa de rastreo
- Registrar y eliminar eventos de escucha de los sensores que monitorean los cambios del sensor.

Podemos englobarlos en tres categorías:
- De **movimiento**: Miden fuerzas de aceleración y rotación en los tres ejes. Acelerómetros, sensores de gravedad, giroscopios, sensores del vector de rotación
- **Ambientales**: Miden parámetros como temperatura, presión, iluminación, humedad. Barómetros, fotómetros, termómetros
- De **posición**: Miden posición física de un dispositivo. Sensores de orientación y magnetómetro. 

#### Marco de trabajo de sensores

Se usarán las clases:

- `Sensor`: Representa a cualquier sensor y contiene métodos para conocer sus capacidades. Tiene constantes de los sensores que se pueden solicitar. 

| Sensor                       | Descripción                                                                                                                                                                                                         |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **TYPE_ACCELEROMETER**       | Mide en m/s2 la fuerza de aceleración                                                                                                                                                                               |
| **TYPE_AMBIENT_TEMPERATURE** | Mide la temperatura ambiente de la habitación en grados Celsius (°C).                                                                                                                                               |
| **TYPE_GRAVITY**             | Mide en m/s2 la fuerza de gravedad que se aplica a un dispositivo en los tres ejes físicos (x, y, z).                                                                                                               |
| **TYPE_GYROSCOPE**           | Mide la velocidad de rotación de un dispositivo en rad/s alrededor de cada uno de los tres ejes físicos (x, y, z).                                                                                                  |
| **TYPE_LIGHT**               | Mide el nivel de luz ambiental (iluminación) en lx.                                                                                                                                                                 |
| **TYPE_LINEAR_ACCELERATION** | Mide en m/s2 la fuerza de aceleración que se aplica a un dispositivo en los tres ejes físicos (x, y, z), excluyendo la fuerza de gravedad.                                                                          |
| **TYPE_MAGNETIC_FIELD**      | Mide el campo geomagnético ambiental de los tres ejes físicos (x, y, z) en μT.                                                                                                                                      |
| **TYPE_ORIENTATION**         | Mide los grados de rotación de un dispositivo alrededor de los tres ejes físicos (x, y, z).                                                                                                                         |
| **TYPE_PRESSURE**            | Mide la presión del aire del ambiente en hPa o mbar.                                                                                                                                                                |
| **TYPE_PROXIMITY**           | Mide en cm la proximidad de un objeto con respecto a la pantalla de visualización de un dispositivo. Por lo general, este sensor se usa para determinar si una persona está sosteniendo un teléfono cerca del oído. |
| **TYPE_RELATIVE_HUMIDITY**   | Mide en valor de porcentaje (%) la humedad relativa del ambiente.                                                                                                                                                   |
| **TYPE_ROTATION_VECTOR**     | Mide la orientación de un dispositivo proporcionando los tres elementos del vector de rotación del dispositivo.                                                                                                     |
| **TYPE_TEMPERATURE**         | Mide la temperatura del dispositivo en grados Celsius (°C).                                                                                                                                                         |
| **TYPE_STEP_DETECTOR**       | Detector de pasos                                                                                                                                                                                                   |
| **TYPE_STEP_COUNTER**        | Contador de pasos                                                                                                                                                                                                   |
| **TYPE_HEART_RATE**          | Frecuencia cardiaca                                                                                                                                                                                                 |

Debe conocerse si un sensor es soportado por una API de Android:
https://developer.android.com/develop/sensors-and-location/sensors/sensors_overview?hl=es#disponibilidad-del-sensor

- `SensorManager`: Instancia del servicio del sensor llamado a `Context.getSystemService()` con el argumento `SENSOR_SERVICE`. Proporciona métodos para acceder a los sensores, recibir datos, registrar y cancelar el registro de escuchadores, adquirir información de orientación... Proporciona constantes que informan de la exactitud del sensor, definir velocidades de adquisición de datos, calibrar...
- `SensorEventListener`: Métodos que son llamados cuando cambian los valores del sensor o la exactitud del mismo
- `SensorEvent`: Información sobre un evento del sensor. Datos sin procesar del sensor, tipo de sensor que lo generó, exactitud de datos, marca de tiempo.

En la clase `Sensor` podemos destacar los siguientes métodos públicos:

- public float **getMaximumRange**(): indica el rango máximo de unidades del sensor.
- public float **getMinDelay**(): tiempo mínimo en microsegundos entre dos eventos.
- public string **getName**(): nombre del sensor.
- public float **getPower**(): potencia del sensor mientras esta siendo usada en mA.
- public float **getResolution**(): resolución en las unidades del sensor.
- public int **getType**(): tipo genérico del sensor.
- public String **getVendor**(): fabricante del sensor.
- public int **getVersion**(): versión del sensor.

Para sensores de movimiento o posición debe considerarse el **sistema de referencia**. Por defecto, está definido en relación con la pantalla del dispositivo. 
Otros sensores usan el sistema de referencia relativo al mundo, datos que representan el movimiento del sispositivo en relación con la tierra. 

Es importante desactivar los sensores que no se necesitan cuando la actividad está en pausa, ya que el sistema no lo hace cuando la pantalla se apaga y consumen batería. 

#### Identificación de sensores y eventos

**Veamos qué sensores tiene disponible el móvil mediante `SensorManager.getSensorList(int)`**

```java
   private TextView tvSensor;
    private SensorManager sensorManager;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        tvSensor = (TextView) findViewById(R.id.tvSensor);
        sensorManager = (SensorManager)
                getSystemService(SENSOR_SERVICE);
        List<Sensor> listSensor = sensorManager.
                getSensorList(Sensor.TYPE_ALL);
        for (Sensor sensor : listSensor) {
            tvSensor.append(sensor.getName() + "\n");
        }
    }
```

**Obtengamos datos de un sensor concreto haciendo un listener `SensorEventListener`**
Se implementarán los métodos
- `onAccuracyChanged(Sensor sensor, int accuracy)`: Cuando la exactitud del sensor cambia
- `onSensorChanged(SensorEvent event)`: Cuando los valores de los sensores han cambiado

```java
    @Override
    public void onSensorChanged(SensorEvent event) {
        switch (event.sensor.getType()) {
            case Sensor.TYPE_ACCELEROMETER:
                mAccelerometerData = event.values.clone();
                for (int i = 0; i < 3; i++)
                    tvSensor.append("Accelerometer: " + i + ": " + event.values[i] + "\n");

                break;
            case Sensor.TYPE_MAGNETIC_FIELD:
                mMagnetometerData = event.values.clone();
                for (int i = 0; i < 3; i++)
                    tvSensor.append("Magnetometer: " + i + ": " + event.values[i] + "\n");
                break;
            default:
                mOtherData = event.values.clone();
                for (int i = 0; i < event.values.length; i++)
                    tvSensor.append("Other: " + i + ": " + event.values[i] + "\n");
        }

    }
```


Por cada sensor, debe registrarse su listener:
```java
    listSensor = sensorManager.getSensorList(Sensor.TYPE_ACCELEROMETER);
        if (!listSensor.isEmpty()) {
            Sensor acelerometroSensor = listSensor.get(0);
            sensorManager.registerListener(this, acelerometroSensor,
                    SensorManager.SENSOR_DELAY_UI);
        }
        listSensor = sensorManager.getSensorList(Sensor.TYPE_MAGNETIC_FIELD);
        if (!listSensor.isEmpty()) {
            Sensor magneticSensor = listSensor.get(0);
            sensorManager.registerListener(this, magneticSensor,
                    SensorManager.SENSOR_DELAY_UI);
        }
        listSensor = sensorManager.getSensorList(Sensor.TYPE_PROXIMITY);
        if (!listSensor.isEmpty()) {
            Sensor proximidadSensor = listSensor.get(0);
            sensorManager.registerListener(this, proximidadSensor,
                    SensorManager.SENSOR_DELAY_UI);
        }
```

Se debe cancelar el registro de los objetos de escucha del sensor cuando se deje de usar o cuando se pause la actividad:
```java
    @Override
    protected void onPause() {
        super.onPause();
        sensorManager.unregisterListener(this);
    }
```

#### Sensores de movimiento

Los sensores de movimiento permiten monitorizar el movimiento del dispositivo (inclinación, sacudida, rotación, balanceo). 
Ejemplos de uso: La galería de fotos detecta la orientación para visualizar las imágenes; Aplicaciones de senderismo hacen uso de la brújula indicando el norte a los usuarios; Aplicaciones de realidad aumentada usan sensores de orientación y cámara mostrando objetos digitales creados por ordenador sobre objetos reales. 

Hay una **arquitectura diferente** según el tipo de sensor:
- **Basados en hardware o en software**: Sensores vectoriales de rotación, gravedad, aceleración lineal, movimiento significativo, contador y detector de pasos... Su inclusión depende del fabricante porque suelen basarse en un hardware específico para obtener los datos. Por ejemplo el sensor de orientación devuelve la posición del teléfono (vertical, horizontal izquierda, horizontal derecha) usando el giroscopio.
- **Basados en hardware**: Sensores del acelerómetro y del giroscopio.

**Ejemplo: Usar el sensor acelerómetro para medir la fuerza de aceleración en m/s2 en un dispositivo en los tres ejes físicos (x, y, z) incluida la fuerza de gravedad**.

1. Implementar `SensorEventListener`
2. Registrar el `SensorEventListener` para el acelerómetro. Por ejemplo en el método `onResume()`, para que se active cuando esté en primer plano
3. Desregistrar el `SensorEventListener` cuando la actividad esté pausada.

 Se debe establecer **un valor de umbral** de forma que, si el movimiento es inferior a este umbral será considerado como ruido y no se tendrá en cuenta. Su valor se establece en la constante SHAKE THRESHOLD GRAVITY y puede ser un valor superior a 1 e inferior a 2 según la sensibilidad. Este valor es un múltiplo de la gravedad de la Tierra de ahí que en cada dirección se calcula la aceleración en base a la gravedad que se encuentra en la Tierra establecido en SensorManager.GRAVITY_EARTH.

```java
public class MainActivity extends Activity implements SensorEventListener {

    private SensorManager sensorManager;
    private Sensor accelerometer;
    private TextView xValue, yValue, zValue;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        xValue = findViewById(R.id.xValue);
        yValue = findViewById(R.id.yValue);
        zValue = findViewById(R.id.zValue);

        sensorManager = (SensorManager) getSystemService(SENSOR_SERVICE);
        if (sensorManager != null) {
            accelerometer = sensorManager.getDefaultSensor(Sensor.TYPE_ACCELEROMETER);
            if (accelerometer == null) {
                // Manejar el caso en que el acelerómetro no está disponible
                xValue.setText("Acelerómetro no disponible");
            }
        }
    }

    @Override
    protected void onResume() {
        super.onResume();
        if (accelerometer != null) {
            sensorManager.registerListener(this, accelerometer, SensorManager.SENSOR_DELAY_NORMAL);
        }
    }

    @Override
    protected void onPause() {
        super.onPause();
        if (accelerometer != null) {
            sensorManager.unregisterListener(this);
        }
    }

    @Override
    public void onSensorChanged(SensorEvent event) {
        if (event.sensor.getType() == Sensor.TYPE_ACCELEROMETER) {
            float x = event.values[0];
            float y = event.values[1];
            float z = event.values[2];

            xValue.setText("X: " + x + " m/s²");
            yValue.setText("Y: " + y + " m/s²");
            zValue.setText("Z: " + z + " m/s²");
            Log.d(LOG_TAG, "x:"+xValue +";y:"+yValue+";z:"+zValue);
    
		    float gX = x / SensorManager.GRAVITY_EARTH;
		    float gY = y / SensorManager.GRAVITY_EARTH;
		    float gZ = z / SensorManager.GRAVITY_EARTH;
		
		    double gForce = Math.sqrt(gX * gX + gY * gY + gZ * gZ);
		
		    if (gForce > SHAKE_THRESHOLD_GRAVITY) {
		      logD("Se ha realizado un movimiento");
		    }
        }
    }

    @Override
    public void onAccuracyChanged(Sensor sensor, int accuracy) {
        // No es necesario manejar los cambios de precisión en este ejemplo
    }
}
```

Más sensores de movimiento... https://developer.android.com/develop/sensors-and-location/sensors/sensors_motion?hl=es-419

## 2. Posición y geolocalización

La posición de un objeto a nivel mundial se obtiene mediante un conjunto de 27 satélites que se encuentran en órbita, 3 de los cuales funcionan como refuerzo, cubriendo todo el planeta.
El móvil tiene un receptor GPS que se conecta al menos con tres de los satélites más cercanos, calculando su posición en base al tiempo que tarde en llegar cada señal de cada satélite (triangulación). Basta con tres, pero suele usarse también un cuarto para determinar la altitud (distancia vertical).

El sensor GPS consume batería y necesita estar en un entorno abierto. Cuando no es posible, se usa la red de comunicaciones móviles (GSM) con millones de torres y antena que dan cobertura para llamar desde los teléfonos. El dispositivo puede calcular su posición usando tres torres de telefonía y en base al tiempo que tarda la señal en el ir a la torre y la fuerza de la señal (Sistema de posicionamiento global asistido A-PGS).

Google Maps: Consigue posición media A-PGS mostrando la posición con un círculo azul en un radio de 20 metros. Si no puede determinar aparece un círculo azul claro alrededor del punto azul, que desaparece al actualizarse la posición a través de los satélites GPS:

### 2.1. Proveedor de localización

1.**Con `android.location.LocationManager`** se puede acceder a los servicios de ubicación del sistema Android.
Hay tres tipos de proveedores:
- **GPS**: Se necesita el permiso `ACCESS_FINE_LOCATION` y se usa la constante `GPS_PROVIDER` de `LocationManager`
- **Red** (A-PGS, wifi, GSM): Recoge ubicación mediante acceso a una red o puntos de acceso Wifi. Se necesita cualquiera de los permisos `ACCESS_COARSE_LOCATION` o `ACCESS_FINE_LOCATION`. Se usa la constante `NETWORK_PROVIDER` de `LocationManager` 
- **Pasivo**: Actualizaciones de ubicación lanzadas por otras aplicaciones. No quiere hacer nueva petición de lectura. Constante `PASSIVE_PROVIDER` de `LocationManager`

El servicio puede obtenerse metiante el método `getSystemService()`: 

```java
LocationManager locationManager =(LocationManager) this.getSystemService(Context.LOCATION_SERVICE);
```

La lista de proveedores puede obtenerse mediante `getAllProviders()` (precisión, coste, consumo, altitud, velocidad...)

```java
List listProvider = locationManager.getAllProviders();
LocationProvider provider = locationManager.getProvider(listProvider.get(0));
int precision = provider.getAccuracy();
boolean supportsAltitude = provider.supportsAltitude();
int requirement = provider.getPowerRequirement();
```

2.**Con Google Play** aparece el proveedor de ubicación fusionada (Fused Location Provider) que usa GPS según la precisión o el intervalo de actualización pero fusiona la información de ubicación en base a otros proveedores de red, sensores, historia lde ubicaciones... Puede usarse la clase `FusedLocationProviderClient`.

El proveedor permite a través de los servicios de Google notificar al usuario cuando entra o sale de un área (geovallado), calcular posición en base a otros objetivos, usar sensores del dispositivo para saber si camina, anda, conduce un automóvil... 

No es necesario tener activada la ubicación para que Google obtenga información. Puede hacerlo a través de aplicaciones como Google Location Track. 

### 2.2. Opciones de ubicación

Criterios para seleccionar un proveedor de ubicación mediante `android.location.Criteria` (precisión, uso de energía, capacidad de informar de altitud, velocidad, rumbo, costo monetario..): 
```java
public  String getProviderName() {
    LocationManager locationManager =(LocationManager)this.getSystemService(Context.LOCATION_SERVICE);
    Criteria criteria = new Criteria();
    criteria.setPowerRequirement(Criteria.POWER_LOW);
    criteria.setAccuracy(Criteria.ACCURACY_FINE);
    criteria.setSpeedRequired(true);
    criteria.setAltitudeRequired(false);
    criteria.setBearingRequired(false);
    criteria.setCostAllowed(false);
    return locationManager.getBestProvider(criteria, true);
}
```

Se puede establecer mediante `LocationRequest` los requerimientos a la hora de obtener ubicación:
- Periodicidad de actualizaciones `setInterval(long millis)`. Preferencia. Puede ser más o menos según conectividad o batería
- Periodicidad máxima de actualizaciones `setFasterInverval(long millis)`
- Prioridad `setPriority()`
	- PRIORITY_BALANCED_POWER_ACCURACY: los datos recibidos tendrán una precisión de unos 100 metros. En este modo el dispositivo tendrá un consumo de energía aceptable al utilizar normalmente la señal Wifi y de datos móviles para determinar la ubicación.
	- PRIORITY_HIGH_ACCURACY: se usa normalmente la señal GPS y se recibirá la ubicación más precisa
	- PRIORITY_LOW_POWER: se usa a nivel de ciudad y equivale a una preción de unos 10 kilómetros, pero el consumo de energía será menor para obtener la ubicación.
	- PRIORITY_NO_POWER: en este caso nuestra aplicación sólo recibirá datos si están disponibles porque alguna otra aplicación los haya solicitado. Es decir, nuestra aplicación no tendrá un impacto directo en el consumo de energía solicitando nuevas ubicaciones, pero si éstas están disponibles las utilizará.

```java
protected void createLocationRequest() {
    LocationRequest locationRequest = LocationRequest.create();
    locationRequest.setInterval(10000);
    locationRequest.setFastestInterval(5000);
    locationRequest.setPriority(LocationRequest.PRIORITY_HIGH_ACCURACY);
}
```
### 2.3. Permisos de ubicación

La ubicación puede solicitarse en dos situaciones diferentes:
- **Ubicación en primer plano:** Actividad es visible y solicita ubicación. O aplicación ejecuta servicio en primer plano y se notifica al usuario mediante notificación que no puede cancelar a no ser que el servicio finalice: Está consumiendo recursos del sistema. 
- **Ubicación en segundo plano**: Aplicación accede a ubicación de una forma diferente a la del primer plano. Es necesario el permiso `ACCESS_BACKGROUND_LOCATION` en el manifiesto (Antes de Android 10 se daba de forma automática con el acceso en primer plano)

Según el proveedor de primer plano debe declararse alguno de los permisos: `ACCESS_COARSE_LOCATION` (precisión de hasta una manzana), `ACCESS_FINE_LOCATION` (ubicación más precisa).  El más preciso ya implica la declaración.

Ejemplo del permiso en el manifest:
`<uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION"/>`

Ejemplo de solicitud del permiso (Como solicitar permisos en tiempo de ejecución: https://developer.android.com/training/permissions/requesting?hl=es-419)

```java
private static final int PERMISSIONS_READ_FINE_LOCATION = 100;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        if (ContextCompat.checkSelfPermission(MainActivity.this,
                Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
            if (ActivityCompat.shouldShowRequestPermissionRationale(MainActivity.this,
                    Manifest.permission.ACCESS_FINE_LOCATION)) {
                ActivityCompat.requestPermissions(MainActivity.this,
                        new String[]{Manifest.permission.ACCESS_FINE_LOCATION}, PERMISSIONS_READ_FINE_LOCATION);
            }else{
                ActivityCompat.requestPermissions(MainActivity.this,
                        new String[]{Manifest.permission.ACCESS_FINE_LOCATION}, PERMISSIONS_READ_FINE_LOCATION);
            }
        }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode,
                                           String permissions[], int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        switch (requestCode) {
            case PERMISSIONS_READ_FINE_LOCATION: {
                // If request is cancelled, the result arrays are empty.
                if (grantResults.length > 0
                        && grantResults[0] == PackageManager.PERMISSION_GRANTED) {

                    Toast.makeText(this, "Permission Granted", Toast.LENGTH_SHORT).show();

                } else {

                    Toast.makeText(this, "Permission Denied", Toast.LENGTH_SHORT).show();
                }
                return;
            }

            // Otros 'case': para comprobar otros tipos de permisos que se han solicitado
       }
}
```

### 2.4. Localización por GPS

La ubicación del dispositivo GPS mediante `LocationManager` y `LocationListener` que tiene una serie de métodos asociados a los eventos que pueden recibirse del proveedor:
- **onLocationChanged**(location): este método se invoca cuando se recibe una actualización de la posición
- **onProviderDisabled**(provider): este método se invoca cuando el proveedor se deshabilita
- **onProviderEnabled**(provider): este método se invoca cuando el proveedor se habilita
- **onStatusChanged**(provider, status, extras): este método se invoca cuando el proveedor cambia su estado, que puede variar entre `OUT_OF_SERVICE`, `TEMPORARILY_UNAVAILABLE`, `AVAILABLE`.

A continuación se comprobará si el GPS que será nuestro proveedor de localización o LocationProvider está habilitado. Si el proveedor de ubicación está deshabilitado, puede ofrecer al usuario la oportunidad de habilitarlo en **Configuración** activando un Intent con la acción ACTION_LOCATION_SOURCE_SETTINGS.

```java
@Override
    protected void onStart() {
        super.onStart();

        // Esta verificación debe realizarse durante onStart () porque el sistema llama
        // este método cuando el usuario regresa a la actividad, lo que asegura el deseado
        // El proveedor de ubicación se habilita cada vez que la actividad se reanuda desde el estado detenido.
        LocationManager locationManager =
                (LocationManager) getSystemService(Context.LOCATION_SERVICE);
        final boolean gpsEnabled = locationManager.isProviderEnabled(LocationManager.GPS_PROVIDER);

        if (!gpsEnabled) {
           // Cree un diálogo de alerta aquí que solicite que el usuario habilite
           // los servicios de ubicación, luego, cuando el usuario hace clic en el botón "Aceptar",
           enableLocationSettings();
        }
    }

    private void enableLocationSettings() {
        Intent settingsIntent = new Intent(Settings.ACTION_LOCATION_SOURCE_SETTINGS);
        startActivity(settingsIntent);
    }
```

Cómo solicitar la posición:

- `getLastKnownLocation()` devuelve la última posición conocida en un objeto `Location` que contiene la **latitud** y **longitud** de la última posición conocida, en el caso que la ubicación no estuviera activada devuelve null. Se puede mirar la marca de tiempo para ver si esta posición fuera válida para nuestra aplicación, en caso contrario hay que realizar una nueva petición.

- `requestLocationUpdates():` este método enviará actualizaciones de la ubicación según los parámetros establecidos en la llamada: el nombre del proveedor, el intervalo de tiempo entre cada actualización, distancia en metros entre localizaciones actualizadas, y la variable de tipo LocationListener que actualizará la localización en caso de producirse nuevos cambios: si el sistema se encuentra en modo avión, en un túnel o bien no puede alcanzar satélites para GPS, etc. No se realizará la llamada pero no devolverá nunca un valor null. Debe usarse siempre que necesite seguir recibiendo actualizaciones de ubicación.

- `requestSingleUpdate()`: es similar a `requestLocationUpdates()`, excepto que solo llamará una vez y luego desactivará el rastreo de ubicación nuevamente. Debe usarse cuando se desea la ubicación en este momento y no le importan las actualizaciones.

```java
 
 //Minimo tiempo para updates en Milisegundos
    private static final long MIN_TIEMPO_ENTRE_UPDATES = 1000 * 60 * 1; // 1 minuto
    //Minima distancia para updates en metros.
    private static final float MIN_CAMBIO_DISTANCIA_PARA_UPDATES = 2; // 2 metros
 //...
 locationManager.requestLocationUpdates(LocationManager.GPS_PROVIDER, MIN_TIEMPO_ENTRE_UPDATES, MIN_CAMBIO_DISTANCIA_PARA_UPDATES, this);
```

### 2.5. Google Cloud Platform

Una aplicación que usa mapas utiliza la API de Google Maps que está dentro de los servicios de Google Play. Estos están preinstalados en todos los dispositivos móviles de Android y permite a los desarrolladores usar las API y servicios de Google (buscador, traductor, mapas..).

Estos servicios se actualizan a través de Google Play y evolucionan para que el dispositivo no quede desactualizado.

Se ofrecen a través de **Google Cloud Platform (GCP)** plataforma en la nube donde Google ha reunido todos sus productos relacionados con la tecnología de la información.

Para conectarse, es necesario generar una API key que se usa para identificar y autenticar la llamada a la API. Para ello se debe **crear el proyecto** o **seleccionar un proyecto**, seleccionar la opción Credenciales > Crear Credenciales > Clave de API. Es importante seleccionar la opción Restringir clave. En el caso de las aplicaciones Android mediante una huella digital del certificado de lanzamiento. 

### 2.6. Google Maps

Las APIs que forman parte de Google Maps Platform se dividen en Maps, Routes y Places. 
Debe habilitarse el SDK de Maps para Android en Google Cloud Platform. 

Deben añadirse las librerías necesarias para la geolocalización en `build.gradle`
```gradle
apply plugin:'com.android.application'
...
dependencies {
     implementation 'com.google.android.gms:play-services-maps:17.0.1'
}
```

Debe añadirse en `AndroidManifest.xml` dos elementos nuevos dentro de `<aplication>`:

La versión de Google Play Services:
```xml
<meta-data
    android:name="com.google.android.gms.version"
    android:value="@integer/google_play_services_version" />
}
```

La API key:
```xml
<meta-data
    android:name="com.google.android.geo.API_KEY"
    android:value="YOUR_KEY_HERE" />
```

Uso de OpenGL ES version 2:
```xml
<meta-data
    android:name="com.google.android.geo.API_KEY"
    android:value="YOUR_KEY_HERE" />
```

#### Marco de trabajo

La clase `GoogleMap` modela un objeto mapa que se ha insertado en la interfaz gráfica mediante un fragmento `MapFragment` o `SupportMapFragment`.
El mapa es similar a los de Google Maps pero:
- No admiten contenido personalizado como iconos inteligentes
- No todos los iconos del mapa permiten el evento click (como las estaciones de transporte público)

La clase permite eventos que controlan los gestos del usuario, responden a la pulsación de teclas y gestos táctiles.
Para manejar pulsaciones puede implementarse `OnMapClickListener` con el método callback `onMapClick`. También `OnMapLongClickListener`....

La API de Google Maps requiere actualmente que se llama a `mapFragment.getMapAsync(this)` y la clase que contiene el mapa debe implementar `OnMapReadyCallBack` para que se ejecute `onMapReady` que trae el objeto de tipo Google Maps para pintar marcadores mover cámara. 

La visualización del usuario se gestiona mediante una **cámara**. Cuando se actualiza la posición en el mapa no se mueve el mapa sino que se cambia la posición de la cámara mediante `GoogleMap.moveCamera(CameraUpdate)`. `CameraUpdate` se obtiene a partir de `CameraUpdateFactory` al que se le pasan las nuevas coordenadas y el zoom deseado (obetivo, rumbo, inclinación y zoom)

En la visualización existen una serie de **controles** (zoom, brújula, ubicación) que se puede activar o desactivar mediante la clase `UiSettings` obtenida con `GoogleMap.getUiSettings`.

En la ubicación al usuario se suelen usar **marcadores**, clase `Marker` que puede ser personalizada con un título, cambiando el color, la imagen con `MarkerOptions`. Se puede añadir información con ventas de información con los método `title()` y `snippet()`. Se usa la clase `LatLng` que contiene latitud y longitud aunque también puede usarse la clase `Location` con más información como rumbo, velocidad, marca de tiempo...

```java
private final LatLng PERTH = new LatLng(-31.952854, 115.857342);
private Marker markerPerth;<br />// ...
    /** Este método se llama cuando el mapa está listo */
    @Override
    public void onMapReady(GoogleMap map) {
        markerPerth = map.addMarker(new MarkerOptions()
            .position(PERTH)
            .snippet("PETH ubication")
            .title("Perth"));
        markerPerth.setTag(0);
    }
```

#### Primer proyecto

1. Usemos un fragmento dentro de una actividad que mostrará la ubicación del dispositivo. Este fragmento será del tipo `SupporMapFragment`
```xml
<fragment android:layout_width="match_parent"
android:layout_height="match_parent"
android:id="@+id/map"
tools:context=".MapsActivity"
android:name="com.google.android.gms.maps.SupportMapFragment" />
```

2. Se solicita al servicio de ubicación que actualice su posición usando `LocationService`, se añade esta línea en el `onCreate()` de la aplicación
```java
fusedLocationClient = LocationServices.getFusedLocationProviderClient(this);
```

Este cliente es el que se usa para conocer la última localización con el método `getLastLocation()` que devuelve una tarea o `Task`

```java
    @SuppressLint("MissingPermission")
    public void getLastLocation() {
        // Get last known recent location using new Google Play Services SDK (v11+)
        fusedLocationClient.getLastLocation()
                .addOnSuccessListener(new OnSuccessListener<Location>() {
                    @Override
                    public void onSuccess(Location location) {
                        // GPS location can be null if GPS is switched off
                        if (location != null) {
                            onLocationChanged(location);
                        }
                    }
                })
                .addOnFailureListener(new OnFailureListener() {
                    @Override
                    public void onFailure(@NonNull Exception e) {
                        Log.d("MapDemoActivity", "Error trying to get last GPS location");
                        e.printStackTrace();
                    }
                });
    }
```

Si la aplicación necesita actualizar la ubicación en un periodo de tiempo establecido se usa `requestLocationUpdates()` al que se le pasa el `LocationRequest` y que contiene los parámetros de calidad de servicio.

Ejemplo: PRIORITY_HIGH_ACCURACY, 10 segundos. Apropiado para mapas con ubicación en tiempo real: 

```java
    private long UPDATE_INTERVAL = 10 * 1000;  /* 10 secs */
    private long FASTEST_INTERVAL = 2000; /* 2 sec */
    //....
    @SuppressLint("MissingPermission")
    protected void startLocationUpdates() {

        // Create the location request to start receiving updates
        LocationRequest locationRequest = LocationRequest.create();
        locationRequest.setPriority(LocationRequest.PRIORITY_HIGH_ACCURACY);
        locationRequest.setInterval(UPDATE_INTERVAL);
        locationRequest.setFastestInterval(FASTEST_INTERVAL);

        // Create LocationSettingsRequest object using location request
        LocationSettingsRequest.Builder builder = new LocationSettingsRequest.Builder();
        builder.addLocationRequest(locationRequest);
        LocationSettingsRequest locationSettingsRequest = builder.build();

        // Check whether location settings are satisfied
        SettingsClient settingsClient = LocationServices.getSettingsClient(this);
        settingsClient.checkLocationSettings(locationSettingsRequest);

        // new Google API SDK v11 uses getFusedLocationProviderClient(this)
        fusedLocationClient.requestLocationUpdates(locationRequest, new LocationCallback() {
                    @Override
                    public void onLocationResult(LocationResult locationResult) {
                        // do work here
                        onLocationChanged(locationResult.getLastLocation());
                    }
                },
                Looper.myLooper());

    }
```

3. Al recibir la nueva localización se modifica el mapa moviendo la cámara:

```java
public void onLocationChanged(Location location) {
        // New location has now been determined
        String msg = "Updated Location: " +
                Double.toString(location.getLatitude()) + "," +
                Double.toString(location.getLongitude());
        Toast.makeText(this, msg, Toast.LENGTH_SHORT).show();
        // You can now create a LatLng Object for use with maps
        LatLng latLng = new LatLng(location.getLatitude(), location.getLongitude());
        gMap.moveCamera(CameraUpdateFactory.newLatLngZoom(latLng, 16.0f));
    }
```

Antes de habilitarla capa, se debe solicitar el permiso de ubicación del usuario:
```java
@SuppressLint("MissingPermission")
    @Override
    public void onMapReady(GoogleMap googleMap) {
        gMap = googleMap;
        if (checkPermissions())
            googleMap.setMyLocationEnabled(true);
    }
```

#### Personalización de un mapa

Puede usarse un objeto `MapView` que representa al mapa en una sección rectangular. Es necesario llamar desde el ciclo de vida a los diferentes métodos (`onCreate()`, `onStart()`, `onResume()`)

Hay varias representaciones de un mapa que se asignan mediante una llamada al método `setMapType()`, pasando como parámetro:

- GoogleMap.**MAP_TYPE_NORMAL**: es el mapa de ruta típico donde se muestra elementos naturales como un río, etiquetas de rutas y otros elementos.
- GoogleMap.**MAP_TYPE_SATELLIT**: muestra imágenes de satélite.
- GoogleMap.**MAP_TYPE_HYBRID**: muestra rutas e imágenes de satélite a la vez.
- GoogleMap.**MAP_TYPE_TERRAIN**: es un mapa topográfico.

En objeto `SupportMapFragment` o `MapView` se puede cambiar el estado inicial de un mapa de forma programática si se pasa un objeto `GoogleMapsOptions`

```java
GoogleMap googleMap = ((SupportMapFragment)getSupportFragmentManager().findFragmentById(R.id.map_fragment)).getMap();
googleMap.setMapType(GoogleMap.MAP_TYPE_SATELLITE);
googleMap.getUiSettings().setMyLocationButtonEnabled(true);
```

Para cambiar la cámara de un mapa se puede usar la clase `CameraUpdateFactory` con métodos para crear `CameraUpdate`

```java
GoogleMap map = ...;
 map.animateCamera(CameraUpdateFactory.zoomIn());
```
