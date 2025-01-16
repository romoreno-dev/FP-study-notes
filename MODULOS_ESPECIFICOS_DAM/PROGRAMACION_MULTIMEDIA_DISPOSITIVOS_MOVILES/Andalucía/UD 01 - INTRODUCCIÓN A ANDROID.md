## 1. Introducción

Se llama **dispositivo móvil** a un aparato pequeño y de poco **peso**, con pantalla y teclado (generalmente táctil), con pequeñas capacidades de procesamiento, memoria limitada y conexión (permanente o no) a una red. Diseñados para cumplir funciones como llamadas telefónicas, agendas, **GPS**pu, acceso al correo, música, navegar... y otras más generales. 

Los móviles se clasifican en:
- Smartphones (Teléfonos inteligentes)
- PDA (Personal Digital Assistant)  o PocketPC (PC de bolsillo), en desuso
- Handhelds (PC de mano)
- Internet tables (entre las PDA y los PCs)
- Ultramóviles (pequeñas tablets PC con teclado físico). 
- Phablets (Dispositivos móviles de tamaño próximo a las tablets)
- Weareables (Relojes con funciones mobile)

Los móviles tenían limitaciones técnicas (actualmente muchas han desaparecido, sobre todo en teléfonos de gama alta) como:
- Suministro de energía limitado (dependientes de batería)
- Procesadores con capacidad de cómputo reducida. Baja frecuencia de reloj para ahorrar energía. Sin capacidad algunos para cálculos en punto flotante.
- Poca memoria principal (RAM)
- Almacenamiento de datos persistente reducido (pequeña memoria flasg interna, SD...)
- Conexión a red de forma intermitente, ancho de banda limitado
- Pantalla de dimensiones reducidas
- Teclados demasiado pequeños

Como ventajas:
- Movilidad
- Poco peso
- Pequeño tamaño
- Facilidad de transporte
- Conectividad a redes de comunicaciones (3G, $g, $G+, mensajería SMS y MMS, voz, Internet, Bluetooth, infrarrojos, radiofrecuencia...)

## 2. Tecnologías disponibles

**Hardware**: Principales fabricantes de smartphones son Samsung, Huawei, Appler, Xiaomi, Oppo, Vivo, LG...  Principales fabricantes de tablets: Appler, Samsung (Samsung Galaxy xxx y Note), Huawei, Amazon...   
A la hora del hardware se considera gama media en 2019:
- Pantalla FullHD
- Procesador potente (Kirin 710, Snapdragon 710)
- Doble cámara (incluso tres)
- Gran batería y carga rápida (mínimo 4000 mAh)
- Gran diseño abandonando el policarbonato por un plástico pulido que aparente ser cristal

**Sistemas operativos**: Basados en Windows, Linux, MacOS X. Otros desarrollados específicamente para este tipo de dispositivo: Android, iOS, Windows Phone.
A la hora de los sistemas operativos:
- Android: Desarrollado por Android Inc., compraod en 2005 por Google, basado en el núcleo de Linux. El primer fabricante que lo incorporó fue HTC. En la mayoría de dispositivos.
- iOS: Por Apple para iPhone primero y para iPod Touch y iPad después
- Windows Phone (antes Windows Mobile). Desarrollado por Microsoft para smatphones y otros dispositivos móviles.
- Blackberry OS: Por Research in Motion (RIM) para Blackberry. En desuso
- Symbian OS (Nokia), HP webOS (HP), Palm Os (PDA), Maemo OS (Nokia para smartphones, PDA y tablets), Bada (Samsung)

**Plataformas de desarrollo**: Android Studio, Visual Studio, Code Warrior, Eclipse, Netbeans   
**Lenguajes de programación**: Korlin, Java, C# , C   
Ranking: 1 Android - 2 iOS - 3 BB. Symbian ha bajado mucho (2018)

Entre las plataformas de desarrollo para móviles más populares suele encontrarse las que los propios autores de los sistemas operativos ofrecen:
- Android: Proporciona Android SDK para programar aplicaciones en Java en su sistema operativo. IDE más usado Android Studio; Eclipse con plugin ADT (Android Development)
- iOS: SDK se puede descargar gratis, pero para firmar el software debe usarse en programa de desarrollo no gratuito. Lenguaje de programación Objective-C   Swift. 
- Windows Phone: Silverlight, XNA, .NET Compact Framework de Microsoft. Usando Visual Studio 2010 Express .Expression Blend para Windows Phone.
- Java ME: Herramientas (Bibliotecas, compiladores, IDE) que son subconjunto de Java orientados al desarrollo en dispositivos móviles. Necesario máquina virtual para ejecutar como sucedía con Symbian (en modo nativo en con Java ME)
- Android Studio. Lo dicho.

#### Android

- 2005 - **Android Inc.** se dedicaba a desarrollar aplicaciones para dispositivos móviles, es comprada por Google en 2005 y desarrollan una máquina virtual Java para móviles llamada **Dalvik VM.**
- 2007 - se crea consorcio (formado por Google, Intel, Motorola, Samsung, Ericson) para difundir la plataforma.  
- 2008 - Se lanza primera versión de Android SDK y aparece el primer móvil con este sistema operativo. Se libera el código fuente con licencia Apache. Aparece Android Market.   
- 2009 - Se incorpora nueva versión de Android con teclado en pantalla  
- 2010 - Android una de las plataformas más usadas    
- 2011 - Versiones para tabletas     
- 2012 Google reemplaza el Android Market por Google Play Store (aplicaciones y contenidos)

Las plataformas de Android se identifican por:
- Nombre comercial: De postres ordenados alfabéticamente
- Versión: Números separados por operador punto (majorVersion.minorVersion)
- Nivel de API: Números enteros comenzando por el 1

Un buen consejo es programar para que las aplicaciones funcionen en la mayor cantidad de dispositivos posibles. 

| Nombre (Postre)    | Versión     | SDK     | Año de lanzamiento | Usaría Java (No es 100% seguro)      |
| ------------------ | ----------- | ------- | ------------------ | ------------------------------------ |
| Android 1.0        | 1.0         | 1       | 2008               | 5                                    |
| Android 1.1        | 1.1         | 2       | 2009               | 5                                    |
| Cupcake            | 1.5         | 3       | 2009               | 5                                    |
| Donut              | 1.6         | 4       | 2009               | 5                                    |
| Eclair             | 2.0 - 2.1   | 5 - 7   | 2009 - 2010        | 5                                    |
| Froyo              | 2.2 - 2.2.3 | 8       | 2010               | 5                                    |
| Gingerbread        | 2.3 - 2.3.7 | 9 - 10  | 2010 - 2011        | 6                                    |
| Honeycomb          | 3.0 - 3.2.6 | 11 - 13 | 2011               | 6                                    |
| Ice Cream Sandwich | 4.0 - 4.0.4 | 14 - 15 | 2011               | 6                                    |
| Jelly Bean         | 4.1 - 4.3.1 | 16 - 18 | 2012 - 2013        | 6(Podría usarse Kotlin)              |
| KitKat             | 4.4 - 4.4.4 | 19 - 20 | 2013               | 6                                    |
| Lollipop           | 5.0 - 5.1.1 | 21 - 22 | 2014 - 2015        | 7                                    |
| Marshmallow        | 6.0 - 6.0.1 | 23      | 2015               | 7                                    |
| Nougat             | 7.0 - 7.1.2 | 24 - 25 | 2016 - 2017        | 7                                    |
| Oreo               | 8.0 - 8.1   | 26 - 27 | 2017 - 2018        | 8                                    |
| Pie                | 9.0         | 28      | 2018               | 8 (Comienza soporte oficial  Kotlin) |
| Android 10         | 10.0        | 29      | 2019               | 8                                    |
| Android 11         | 11.0        | 30      | 2020               | 8                                    |
| Android 12         | 12.0        | 31      | 2021               | 8                                    |
| Android 12L        | 12.1        | 32      | 2021               | 8                                    |
| Android 13         | 13          | 33      | 2022               | 11                                   |
| Android 14         | 14          | 34      | 2023               | 17                                   |
| Android 15         | 15 DP2      | V DP2   | 2024               | ¿17?                                 |
## 3. Arquitectura del sistema Android

- **Núcleo de Android** (capa más interna): Linux. Gestión de memoria y de procesos, servicios, pila de red y controladores de dispositivos. Depende del hardware. 
- **Librerías nativas**: Bibliotecas C/C++ para implementar aplicaciones como bibliotecas de gráficos (**Surface Manager**), de medios (**Media Framework**), motor de base de datos (**SQL Lite**), navegador Android (**WebKit**)
- **Runtime de Android**. La máquina virtual. La primera era Dalvik (adaptación de la JVM de menor peso). Cuando Java pasa a Oracle surgen problemas legales por el uso de la JVM por Dalvik. Android 4.4 KitKat lanza ART (Android Runtime) como alternativa a Dalvik y es el sustituto desde Android Lollipop (5). También están las librerías disponibles en Java (Core libraries)
- **Entorno de aplicación** Herramientas para desarrollo de aplicaciones Android. Mismos API del framework usados por las aplicaciones del dispositivo o las creadas por el propio desarrollador. Ejemplos:
	- Activity Manager: Ciclo de vida de actividades
	- Window Manager: Ventanas de aplicaciones (Surface Manager)
	- Telephone Manager: Funciones del teléfono
	- Views: Elementos para interfaces de usuario
	- Content Provider: Datos entre aplicaciones Android y funciones del teléfono
	- Notification Manager: Eventos sucedidos durante la ejecución
* **Capa de aplicaciones**. Se encuentran instaladas todas las aplicaciones Android que correrán en (Dalvik / ART usando servicios, API y librerías. 

![](PROGRAMACION_MULTIMEDIA_DISPOSITIVOS_MOVILES/Andalucía/resources/ud01-2.png)

Por citar algunas funcionalidades Android:
- Creación de aplicaciones se usuario usando aplicaciones interactivas
- Gestión de datos
- Procesamiento y reproducción de objetos multimedia
- Envío y recepción de mensajes de texto y multimedia, mensajes tipo push, servicios en segundo plano con hilos, sensores de dispositivos móviles, Wi-Fi y bluetooth, HTTP HTTPS
## 4. Entornos de desarrollo para aplicaciones Android

Google pensó en Java para programar Android porque es fácil, extendido, independiente de la plataforma, con retrocompatibilidad hacia atrás. Solo se necesita una JVM y puede ejecutarse en cualquier sistema operativo que la soporte. 

Android Studio solo incluye algunas funcionalidades de Java 8, lo cual limita las aplicaciones. 
En 2017, Google anuncia que Kotlin pasa a ser lenguaje oficial en Android y le da soporte. Es 100% compatible con Java, el código de ambos puede convivir en un mismo proyecto y las librerías de Java ser usadas en Kotlin.

Debe tenerse JDK 7 para Android Lollipop o superior. 

La instalación del kit de desarrollo incluye:
- API para desarrollo de las aplicaciones (clases)
- Herramienta para depuración
- Emulador para ejecutar aplicación en dispositivo virtual. 

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

![](PROGRAMACION_MULTIMEDIA_DISPOSITIVOS_MOVILES/Andalucía/resources/ud01-1.png)