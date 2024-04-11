1
## 5. La primera aplicación en Android

- Pinchar en **Start a new Android Studio Project**
- Seleccionar **Phone and Tablet** y partir de una **Empty Activity**
- Configurar **nombre de aplicación (Name)**, **nombre de la compañía (Package Name)** (para garantizar que la aplicación es única tanto en Google Play como en la ruta de instalación de la aplicación en el dispositivo), **localización del proyecto (Save Location)** y **versión mínima (Minimum SDK)** (indicar el valor mínimo de la API requerida para ejecutar la aplicación; es importante al crear dispositivo virtual ya que la versión de ese dispositivo debe ser igual o superior a este valor. Hay asistente **Help me choose** con el porcentaje de dispositivos que la usan)

Al ver el listado de archivos del proyecto en el **Panel Project**, este podría variar en función de la **perspectiva** seleccionada (Por defecto "Vista Android". La vista real es **Vista Project**).

### Organización de los ficheros 

Existe un único módulo `app` que contiene los ficheros.
- `/libs` Librerías del proyecto (Ficheros JAR)
- `/build` Ficheros generados al compilar
- `/src/main/java` Ficheros fuente `.java`  (Viene la `MainActivity.java`)
- `/src/main/res`  Recursos de la aplicación (imágenes, vídeos,, textos...)
	- `/drawable`  Imágenes y elementos gráficos (divididos en resolución y densidad)
	- `/mipmap`  Iconos (divididos en resolución y densidad)
	- `/layout` Ficheros XML. Interfaces gráficas
	- `/values`  Ficheros XML de textos, estilos, colores
	- `/menu` Menús de la aplicación
* `/src/main/AndroidManifest.xml`  Aspectos más importantes de la aplicación: Nombre, versión, icono, pantallas, mensajes
* `build.gradle` Información para compilar el proyecto

Los ficheros de `app/src/main/res/layout` definen el diseño (layout) de los componentes de tipo view que contiene la aplicación.

La pantalla puede verse de forma gráfica (Design), el código generado (Text o Code) y las dos (Split).
Por defecto, morado (espacio de nombres declarados en el nodo raíz, azul atributo, verde valor del atributo)

### El primer layout (activity_main.xml)

En el ejemplo inicial podemos ver un nodo `ConstraintLayout` con un componente de tipo `View` (un `TextView`) con un texto que dice "Hello World!"

```xml
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

Podríamos centrar el texto con:
`android:gravity="center"`

Podríamos centrar el `TextView` con:
```xml
android:layout_centerHorizontal="true"
android:layout_centerVertical="true"
```


### La primera clase (MainActivity.java)

```java
package com.example.helloworld
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
    
}
```

La clase se encarga de que se cargue la pantalla principal del código anterior.
- Es una Actividad (pantalla) porque hereda de `AppCompatActivity`
- Se sobreescribe el método `onCreate()` para iniciar la aplicación, llamando al método de carga del layout del XML  ( `setContentView` ),  indicándole se visualice a través de la constante entera ubicada en la clase estática `R.layout` que referencia a todos los ficheros XML de `/res/layout`


### El fichero de manifiesto

Veamos un ejemplo:

```java
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.helloworld">
    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
 
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```

En el nodo `manifest` se referencia al espacio de nombres de Android y se indica el nombre del paquete de la aplicación.

En el nodo `application` se especifican los componentes y características de configuración

En el ejemplo, dentro de ese nodo solo está el nodo `activity` con el `android:name` que referencia al nombre de la clase principal que carga la actividad. 
Todas las activities estarán registradas en el Manifest.
La que tenga la etiqueta `intent-filter` se indica que la actividad es principal y ejecutable. 


## 6. Componentes de una aplicación en Android

Los componentes deben definirse siempre en el manifiesto dentro de la etiqueta `application` con su etiqueta correspondiente. 

- **Activity** (`activity`): Componente principal de la interfaz gráfica (similar a ventana) 
- **Service** (`service`):  Componente en segundo plano (similar a servicios del sistema: envían notfiicaciones, muestran activities, analizan datos..)
- **Content Provider** (`provider`):  Componente que comparte datos entre aplicaciones Android
- **Broadcast Receiver**  (`receiver`): Componente que detecta y reacciona a eventos (ya sea del sistema (batería baja, SD, SMS...) o de otras aplicaciones)

- **Intent**: Comunicación entre componentes mediante mensajes o peticiones. Por ejemplo abrir una actividad desde la inicial, enviar mensaje, broadcast, servicio, aplicación...
- **Widget**: Referencia a objeto `View` en la interfaz de usuario
- **View**: Componente básico con el que se construye la interfaz gráfica de la aplicación. (Cuadros de texto, botones, listas...)
- **Layout**: Agrupa y organiza los componentes de tipo `View` que forman la `Activity`. Un layout puede contener a otros layouts y los hay de distintos tipos. 

## 7. Despliegue de aplicaciones Android

Los IDE disponen de emuladores para probar las aplicaciones antes de instalarlas en el dispositivo para el que se programan. En el caso de Android Studio, es AVD Manager.

Debe probarse la app con diferentes niveles de API de Android para garantizar que se ejecuta correctamente. Primero con el emulador (paso a paso, breakpoints, observación de variables) y después con un dispositivo real.

Debe crearse emulador y luego seleccionar el módulo app y el dispotivio que se quiere ejecutar. (emuladores suelen ser lentos aunque algunos procesadores instalan acelerador de software al instalar Android Studio). También está la opción de Genymotion (con Virtualbox)

Para desplegar en dipositivo real hay que instalar el paquete **Google USB Driver** en el **SDK Manager** y tener activado el modo **Depuración de USB** en el dispositivo. También instalar los drivers del fabricante si los requiere. Una vez listo, puede lanzarse la app en el dispositivo.

## 8. Ciclo de vida de una actividad

Se inicia la actividad principal y esta invoca a otra actividad mientras el usuario interacciona con la aplicación.
El sistema operativo llama de forma automática a los métodos del ciclo de vida de las actividades y estos devuelven el resultado al sistema (son métodos `callback`)

Las actividades que dejamos de ver no se destruyen, se guardan en un pila de actividades en el mismo orden en el que han sido abiertas. Cuando el usuario pulsa el botón de "Atrás", la actividad finaliza y se quita de la pila. Cuando la actividad principal finalice, se elimina toda la información de la aplicación. También se elimina cuando hay un cambio de configuración en el dispositivo (como el idioma; caso en el que se llamará a `onPause()`, `onStop()`  y `onDestroy()` y se creará nueva instancia con `onCreate()`, `onStart()`, `onResume()`
Si hay muchas actividades, (muchas aplicaciones en ejecución), el sistema puede destruir actividades detenidas para liberar memoria. 

Una actividad puede pasar por los **estados**:
- **Activa**: Actividad visible y puede ser usada por el usuario
- **Pausada**: Actividad visible pero ha perdido el foco por otra actividad (ventanas de diálogo y avisos; puede verse la anterior porque la nueva actividad no suele ocupar toda la pantalla)
- **Parada**: Actividad deja de estar visible. Conveniente guardar el estado por si el usuario vuelve a ella. 

Los **métodos** que gestionan el ciclo de vida son:
- `onCreate()`: La actividad es creada. Se inicializa la interfaz gráfica y los datos. El método debe ser sobreescrito. Se recibe como parámetro una instancia de la clase `Bundle` para restaurar la actividad de su estado anterior. La primera vez este parámetro es nulo. 
- `onStart()`:  Actividad preparada para ser visualizada. (No tiene por qué mostrarse al usuario)
- `onResume()`:  Actividad en parte superior de la pila y es visible al usuario. Puede interactuarse con ella.
- `onPause()`: Actividad pasa a segundo plano porque otra actividad toma el foco. Debe guardarse el estado. 
- `onStop()`: Actividad deja de estar visible por completo. Si no hay memoria podría destruirse sin pasar por aquí.
- `onRestart()`:  Actividad vuelve a visualizarse después de haber sido parada y sin haber llegado a destruirse.
- `onDestroy()`:  Actividad se destruye completamente para liberar la memoria utilizada.

Métodos que abarcan todo el ciclo: `onCreate()` y `onDestroy()`
Actividad visible al usuario desde `onStart()`  hasta `onStop()` (aunque podría no tener foco)
Actividad visible y con foco desde `onResume()` hasta `onPause()`

![](resources/ud01-1.png)