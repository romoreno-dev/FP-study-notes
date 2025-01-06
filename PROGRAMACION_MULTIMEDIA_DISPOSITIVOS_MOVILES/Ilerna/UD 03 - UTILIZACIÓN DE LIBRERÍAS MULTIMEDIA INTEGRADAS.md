
## 1. Conceptos sobre aplicaciones multimedia

Las aplicaciones multimedia son de las más utilizadas y descargadas en las tiendas. 
El protocolo que permite enviar audio y vídeo a través de Internet y mediante el que funcionan aplicaciones que envían audio y vídeo en tiempo real es el protocolo RTP. 

En el desarrollo de apps multimedia se deben considerar:
- Resoluciones y tamaños de pantalla
- Tipos de procesadores
- Capacidades de memoria
- Códecs soportados
- Uso de periféricos (teclados, joystick, auriculares Bluetooth o con cable, micrófono, cámaras)

Los sistemas operativos móviles tratan de estandarizar mediante las librerías multimedia, sus clases e interfaces, todas las diferentes funcionalidades del hardware ocultando las diferencias entre terminales para que el desarrollador pueda centrarse en codificar mecanismos que mantengan la estabilidad de la app ante diferencias de hardware. 

Dado el rápido avance del hardware y el software será  frecuente encontrarse con clases o interfaces que se han ido quedando obsoletas o que solo funcionarán para una versión moderna del sistema operativo. Ej.: Paquetes `Camera`, `Camera2` y `CameraX`.

Manejar el hardware de la cámara a bajo nivel o la reproducción de vídeo, no es una tarea sencilla pese a que se provean facilidades. También requiere de recursos como memoria y tiempo de CPU, memoria de los terminales, uso de protocolos de compresión, fuente de los datos multimedia y como acceder a ellos de la forma más eficiente,...

## 2. Arquitectura del API utilizado

### 2.1. Arquitectura de aplicaciones de audio y video. Soluciones que requieran implementar algo sencillo

Por ejemplo, debe considerarse que en una aplicación reproductora de audio el usuario puede estar haciendo otras cosas y lanzar comandos en un momento dado mediante la activación de la `Activity` o el uso de botones de notificación. Sin embargo, cuando está usando una aplicación reproductora de vídeo será muy habitual que la app tenga una vista enlazada al reproductor y se ejecute en primer plano. 
Igualmente con aplicaciones grabadoras de vídeo o de sonido, según las necesidades a cubrir. 

**Arquitectura de una app de audio**
Arquitectura cliente-servidor con;:
- **Módulo de control: (cliente)** Que mediante una interfaz gráfica permite al usuario lanzar comandos (play, pause, siguiente pista, pista anterior)
- **Servicio corriendo en background (servidor):** Responsable de reproducir cada pista de audio según las acciones indicadas en el módulo de control.
Con ciertas clases de Android se podrá conseguir que el sistema funcione con más de un cliente (por ejemplo, que la pista actual que se reproduce en el servidor mediante los controles de la app también pueda ser controlada desde otros dispositivos. Se proveen las clases `MediaBrowser` y `MediaBrowserService`. En caso de no necesitar que módulos de terceros accedan al sistema se puede usar un servicio más sencillo que herede de `Service`. 

**Arquitectura de una app de vídeo**
Aquí no será necesario separar los controles del propio reproductor. Este estará enlazado a una ventana en la que se volcarán las imágenes de vídeo.
Aún así se diferenciará en el código dos partes:
- la interfaz gráfica
- el control del media (carga, codificación,...) 
La parte gráfica tiene diferentes posibilidades como un elemento `VideoView` y cargarlo usando un `MediaController` para que el usuario controle la reproducción a su gusto.

```xml
<VideoView
android:id=”@+id/videoView”
android:layout_width=”match_parent”
android:layout_height=”match_parent” />
```


```kotlin
// Recuperar el componente VideoView del layout
val videoView = findViewById<VideoView>(R.id.videoView)
// Opción 1: setVideoPath - Archivo en disco (Nota: android.permission.WRITE_EXTERNAL_STORAGE)
val clip = File(Environment.getExternalStorageDirectory(), “test.mp4”)
videoView.setVideoPath(clip.path);

// Opción 2: setVideoURI - Archivo en directorio res/raw (Nota: no debemos escribir la extensión)
videoView.setVideoURI(Uri.parse(“android.resource://$packageName/raw/test”))

// Opción 3: setVideoPath - Archivo en Internet (Nota: android.permission.INTERNET)
videoView.setVideoPath(“http://videocdn.bodybuilding.com/video/
mp4/62000/62792m.mp4”)

// Instanciar MediaController en la Activity indicandole el VideoView
val mediaController = MediaController(this)
mediaController.setMediaPlayer(videoView)

// Indicarle al VideoView el MediaController e iniciar
videoView.setMediaController(mediaController)
videoView.requestFocus()
videoView.start()
```


**Arquitectura de una app captadora de audio o de vídeo**

Para captar audio o vídeo debe considerarse si se van a usar otras aplicaciones como interfaz hacia el hardware o si se usará directamente la cámara o el micro. 
Puede convenir llamar directamente a la grabadora instalada por defecto en el móvil.
Por ejemplo: Aquí se usará una app preinstalada en el sistema como grabadora de vídeo y se le solicitará que grabe uno. 

**Uso de FileProvider**: Mediante `FileProvider` se permite compartir archivos de forma segura entre diferentes apps.
Este debe definirse en el `manifest`: 
```xml
<provider
android:name=”androidx.core.content.FileProvider”
android:authorities=”${applicationId}.provider”
android:exported=”false”
android:grantUriPermissions=”true”>
	<meta-data
	android:name=”android.support.FILE_PROVIDER_PATHS”
	android:resource=”@xml/provider_paths”/>
</provider>
```

Se hace referencia al documento XML que definirá las rutas. En `res/xml/provider_path_xml`:
```xml
<?xml version=”1.0” encoding=”utf-8”?>
<paths>
<files-path name=”v” path=”videos” />
</paths>
```

**Captadora de vídeo**
Ahora puede llamarse a una aplicación que responda a una acción `MediaStore.ACTION_VIDEO_CAPTURE` (captar vídeo) y a otra que responda a la acción `Intent.ACTION_VIEW` (ver vídeo)

```kotlin
private fun grabar() {
		val output = File(File(filesDir, VIDEOS), FILENAME)
		if(output.exists())
			output.delete()
		else
			output.parentFile?.mkdirs()
		outputUri = FileProvider.getUriForFile(this, AUTHORITY, output)
		// Se crea el intent pidiendole que responda a esa accion y pasandole la URL y la calidad del vídeo
		val intent = Intent(MediaStore.ACTION_VIDEO_CAPTURE)
		intent.putExtra(MediaStore.EXTRA_OUTPUT, outputUri)
		intent.putExtra(MediaStore.EXTRA_VIDEO_QUALITY, 1)
		intent.addFlags(Intent.FLAG_GRANT_WRITE_URI_PERMISSION
		or Intent.FLAG_GRANT_READ_URI_PERMISSION)
	// Se inicia Activity pidiendole que espere un resultado en onActivityResult
		startActivityForResult(intent, REQUEST_ID)
	}

override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
		if (requestCode == REQUEST_ID && resultCode == RESULT_OK) {
		// Se crea intent para llamar a la app por defecto para mostrar video
		val view = Intent(Intent.ACTION_VIEW)
		.setDataAndType(outputUri, “video/mp4”)
		.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION)
		startActivity(view)
		finish()
	} 
}
```

**Captadora de audio** 

Una aplicación captadora de audio será similar:
```kotlin
class Actividad : Activity() {
	override fun onCreate(savedInstanceState: Bundle?) {
		super.onCreate(savedInstanceState)
		val intent = Intent(MediaStore.Audio.Media.RECORD_SOUND_ACTION)
		startActivityForResult(intent, REQUEST_ID)
	}
	override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?)
	{
		if (requestCode == REQUEST_ID && resultCode == RESULT_OK) {
		Toast.makeText(this, “Grabación terminada”, Toast.LENGTH_LONG).
		show()
	}
	finish()
}
	companion object {
		private const val REQUEST_ID = 1337
	}
}
```

### 2.2. Arquitectura del sistema Android

- **1º Nivel: El framework de aplicación** es el nivel más alto (**SDK**, con el que los desarrolladores se comunican). 
- **2º Nivel: El IPC**,  que sirve para acceder a los servicios de Android con mayor facilidad.
- **3º Nivel**: **Servicios**. Hay dos tipos de servicios:
	- System server** (servicios del sistema)
	- Media server** (servicios de los media). Aquí se encuentra la cámara, el `MediaPlayer`...

- **4º Nivel**: El **HAL** (Hardware Abstraction Layer) es una definición estándar de las llamadas al hardware que los fabricantes de móviles deben cumplir para que Android funcione en ellos

- **5º Nivel: Linux Kernel** (núcleo de Linux). Es el código central de todo el sistema operativo. Aquí se encuentran los drivers que controlan la cámara, la pantalla, el micrófono y el sonido.

Cuando desde la app se pregunta al sistema sobre un códec, es posible que se haga todo este recorrido hacia el interior de sistema antes de dar una respuesta.

![](resources/UD03_1.png)
## 3. Descripción e instalación de librerías multimedia

Se puede **reproducir audio y vídeo** desde:
- Fichero almacenado en el dispositivo
- Recurso incrustado en el paquete de la aplicación (APK) en `/res/raw`
- Desde stream al que uno e conecta a través de internet
Se puede **grabar audio y vídeo** cuando se concedan los permisos necesarios.

## 3.1. Permisos necesarios para multimedia

Deben ser declarados en el manifest:

- **CAMERA**: Permite acceder a la cámara del dispositivo para capturar fotos o vídeos
- **RECORD_AUDIO**: Permite acceder al micrófono del dispositivo para grabar audio
- **WRITE_EXTERNAL_STORAGE** y **READ_EXTERNAL_STORAGE**: Permite acceder al almacenamiento externo del dispositivo para guardar y leer archivos multimedia
- **INTERNET**: Permiso para acceder a la red
- **SEND_SMS**: Permite enviar mensajes mediante SMS
- **FLASH_LIGHT**: Uso de flash
- **ACCESS_FINE_LOCATION**: Uso de GPS. Ubicación más precisa.
- **ACCESS_COARSE_LOCATION**: Uso de GPS. Ubicación menos precisa. 

Estructura en el `manifest`: 
```xml
<uses-permission android:name="android.permission.PERMISO_SOLICITADO" />
```

**Solicitar en tiempo de ejecución**
A partir de Android 6.0 (API 23), además de ser declaradas, deben solicitarse en tiempo de ejecución los permisos de funciones sensibles.

![](UD03_4.png)

![](UD03_5.png)


La mayoría de las clases de librerías multimedia se encuentran en el paquete `android.media.*`

- `MediaPlayer`: La clase **MediaPlayer** permitirá en buena parte la reproducción de Audio y Video de forma sencilla y eficaz desde ficheros o streams. Su única desventaja es a la hora de reproducir audio o vídeo en streaming (para eso mejor `Exoplayer`). Permite control básico de la reproducción con reproducir, pausar, detener, buscar y ajustar el volumen. Útil para aplicaciones que no requieran control extremadamente preciso o de baja patencia (aplicaciones de música, vídeo o podcast)

Sin embargo, hay otras clases más sencillas y eficientes para ciertos casos concretos en la reproducción de audio que también conviene conocer:
- `SoundPool`: Puede **solapar varias fuentes de sonido dando prioridad a cada fuente** con propiedades para lanzarlas al **mismo tiempo**, decidiendo cuál se reproduce y cuál no o incluso **mezclarlos**. Imprescindible en el desarrollo de videojuegos (necesarios varios sonidos a la vez). Maneja y reproduce una colección de recursos de audio. Podría incluso indicársele que utilice solo dos canales por ejemplo para que solo dos de los múltiples sonidos sean mezclados, reduciendo rendimiento.  Permite cargar clips de audio desde la carpeta de recursos o desde un archivo del discos. Usa los servicios de decodificación de `MediaPlayer` para convertir los clips de audio en el formato básico PCM de 16 bits y cargarlos en memoria. La reproducción de sonidos será más veloz, pues solo serán decodificados una vez. Es adecuado si el número de clips de audio y su longitud no es excesiva (o podría necesitarse demasiada memoria)

- `AudioTrack`: Clase de bajo nivel. Eficiente para **reproducir fuentes de audio que ya han sido decodificadas** en PCM (Pulse Code Modulation). Controla la carga y reprodución un buffer de audio PCM directamente por hardware. Adecuado para baja latencia. Reproducción de sonidos más largos o generación de audios en tiempo real. Aplicaciones con control más preciso sobre la reproducción del audio (reproducción de música, editores de audio, síntesis de sonido). Ej.: Un MP3 mejor que usemos `MediaPlayer` pero si la velocidad es importante y solo tenemos unos pocos sonidos decodificados en PCM mejor usar `AudioTrack`.  En modo streaming acepta escrituras continuas de bytes que lanza a la capa nativa para su reproducción (útil cuando los clics son demasiado grandes o porque los datos llegan desde streaming). El modo estático es útil cuando se trabaja con sonidos cortos y de poco tamaño (rápido y eficiente; prefiero en juegos y pequeños sonidos relacionados con la interacción)

- `ToneGenerator`: Reproducir **sonidos básicos y sencillos** como un par de frecuencias en forma de pitido. Generar tonos de audio de frecuencia constante comotonos DTMF (Dual-Tone Multi-Frequency). Forma más sencilla de reproducir sonidos sin almacenar datos en memoria. El generador utilizará su circuitería para generar impulsos de frecuencias programadas. Útil para marcadores de teléfono, aplicaciones de prueba de audio o aplicaciones de música.

Para la reproducción de vídeo no hay grandes alternativas dentro del SDK. Comentamos la siguiente fuera del SDK: 
- `ExoPlayer`: Reproductor de vídeo. No pertenece al SDK de Android pero está integrada en el sistema y es fácil de usar en los proyectos. Tiene funciones de alto nivel para configurar y ajustar todos los parámetros de la reproducción. Además tiene funcionalidades (potencia extra, aunque podría perjudicar batería) que no tiene `MediaPlayer` (steaming de vídeo y audio: Soporta Dynamic Adaptative Streaming sobre HTTP -DASH-, Smooth, SmoothStreaming, Common Encryption. Son tecnologías imprescindibles para el funcionamiento de canales de streaming.)

> Para usar ExoPlayer debe incluirse:

```gradle
// Incluir todas las funcionalidades de ExoPlayer
implementation ‘com.google.android.exoplayer:exoplayer:2.10.4’
// O solo algunas de ellas
implementation ‘com.google.android.exoplayer:exoplayer-core:2.11.5’
implementation ‘com.google.android.exoplayer:exoplayer-ui:2.11.5’
```

----------

- `MediaControler`: Visualizar controles estándar para `MediaPlayer` (pausa, stop,...)
- `AsyncPlayer`: Reproduce lista de audios desde un thread secundario
- `VolumeShaper`: Permite añadir atenuaciones al inicio, al final o en transiciones de audios. 

----------

- `MediaRecorder`: Captación de audio y vídeo según las fuentes que se configuren. Permite configurar formato y longitud de los archivos de salida. Cuando se use con `Camera2` permite grabar clips de vídeo y almacenarlos en el formato deseado.

- `Camera2`: Segunda versión de una clase para control de la cámara del dispositivo. Control de los parámetros de toma de imágenes y de vídeo desde hardware.
- `CameraX`: Forma fácil de acceder a `Camera2`. Biblioteca de compatibilidad para acceder a estas funcionalidades pero con una programación más sencilla basada en casos de uso. 

- `MediaCoder`: Permite acceder a los códecs del sistema
- `Surface`: Usado como un buffer de vídeo para clases como `MediaRecorder` o `SurfaceTexture`. Controlado por un productor de vídeo como `MediaPlayer`
- `MediaMuxer`: Permite la mezcla de streams de vídeo y audio. Soporta codificación de salida MP4, Webm y 3GP.

| Métodos                                                     | Descripción                                         |
| ----------------------------------------------------------- | --------------------------------------------------- |
| `public void setDataSource(String path)`                    | Define la ruta del recurso que se usará             |
| `public void prepare()`                                     | Prepara el reproductor de forma sincronizada        |
| `public void start()`                                       | Comienza o continúa la reproducción                 |
| `public void stop()`                                        | Detiene la reproducción                             |
| `public void pause()`<br>                                   | Pausa la reproducción                               |
| `public boolean isPlaying()`                                | Comprueba si se está reproduciendo                  |
| `public void seekTo(int millis)`                            | Avanza una determina posición                       |
| `public void setLooping(boolean looping)`                   | Reproducción continua                               |
| `public boolean isLooping()`                                | Comprueba si está activada la reproducción continua |
| `public void selectTrack(int index)`                        | Elige una pista determinada                         |
| `public int getCurrentPosition()`                           | Devuelve la posición actual de reproducción         |
| `public int getDuration()`                                  | Devuelve la duración el archivo                     |
| `public void setVolume(float leftVolume,float rightVolume)` | Ajusta el volumen de reproducción                   |

## 4. Fuentes de datos multimedia. Clases.

### 4.1. Formatos de Audio y Vídeo

El sistema Android da soporte para algunos formatos de audio y vídeo (posee códecs instalados por defecto). Debe buscarse utilizar estos si se quiere que la app funcione en todos los dispositivos disponibles. Si se quiere centrarse solo en ciertas marcas y modelos pueden usarse códecs que solo estén disponibles en ese terminal.

A partir de Android 10 (API 29) hay algunos métodos interesantes en `MediaCodecInfo` para ayudarse en esta información:

| Métodos                 | Descripción                                                                                                                  |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `isSoftwareOnly`        | Si el códec es puramente virtual (sin ayuda del hardware para la conversión). Velocidad y rendimiento pueden ser inferiores. |
| `isHardwareAccelerated` | Lo contrario. Su usa hardware y es más veloz.                                                                                |
| `isVendor`              | Si el códec es del fabricante o si es estándar de Android.                                                                   |
![](resources/UD03_2.png)

![](resources/UD03_3.png)

### 4.2. Hardware

El paquete `android.hardware` da al desarrollador las clases necesarias para manejar el hardware del dispositivo.
- `Camera2` o, si se ha actualizado, `CameraX`. 
Como no todos los dispositivos dispondrán de las características de hardware soportado por Android, en el manifest debe declararse cuáles son indispensables para el funcionamiento.

**Uso no fundamental**
```xml
<uses-feature android:name=”android.hardware.camera.any” android:
required=”false” />
```

**Uso fundamental**
```xml
<uses-feature android:name=”android.hardware.camera.any” android:
required=”true” />
```

Otros usos:
- **android.hardware.camera**: Cámera trasera del terminal
- **android.hardware.camera.any**: Cámera trasera o frontal, indistintamente
- **android.hardware.camera.autofocus**: Autoenfoque de cámara
- **android.hardware.camera.external**: Cámara externa
- **android.hardware.camera.flash**: flash de la cámara.
- **android.hardware.camera.front**: cámara frontal del dispositivo.
- **android.hardware.audio.low_latency**: aceleración del procesamiento de audio
- **android.hardware.audio.output:** función de salida de audio por altavoces, jack de audio, Bluetooth o cualquier otro mecanismo que permita la función.
- **android.hardware.audio.pro**: funcionalidades de audio de alto nivel.
- **android.hardware.audio.microphone**: micro / grabación de audio.
- **android.hardware.gamepad**: gamepad.

Para alta eficiencia es posible comunicarse de forma directa con el uso del **NDK (Native Development Kit)**. Conjunto de herramientas y librerías que permiten acceder a los niveles más bajos del sistema. Necesario programar en C y C++.
### 4.3. Fuentes de datos

- **Capturar vídeo**: Hardware de la cámara o app intermedia
- **Reproducir vídeo**: `app/src/main/res/raw`  (se les asignará un identificador sin necesidad de tener que abrir y leer el fichero pero sus recursos están limitados en tamaño si no van comprimidos) o `app/src/main/assets` (no tiene identificador pero puede crearse un árbol de directorios libremente)

Ya se vio un ejemplo al comienzo del tema sobre uso de `VideoView` y `MediaPlayer`.
Baste recordar que:
- `setVideoPath`: Permite indicar archivo en almacenamiento externo (`File(Environment.getExternalStorageDirectory(), namefile)`) o archivo en internet (introduciendo la url directamente
- `setVideoUri`: Permite indicar URI de recurso. Con `Uri.parse("android.resource://$packageName/raw/test")`

## 5. Datos basados en el tiempo

En aplicaciones de control en tiempo real como las de reproducción multimedia, el tiempo de procesamiento tiene un máximo que no puede superarse. El proceso ha de ser suficientemente rápido o se perderán datos y se carecerá de la calidad suficiente. 
Los procesos que llevan a cabo las librerías multimedia tienen en cuenta esos aspectos. 
Si no fuese suficiente, siempre se puede recurrir al NDK.

El tiempo también significa tamaño (según la velocidad de muestreo, así aumentará nuestro archivo de audio); por lo que debe tenerse en cuenta el tamaño de disco disponible. Y se pueden establecer límites y de tiempo y/o tamaño resultante en la captación. 
### 5.1. Una app grabadora de audio

**1. Añadir permisos y uso del hardware**
```xml
<uses-permission android:name=”android.permission.RECORD_AUDIO”/>
<uses-permission android:name=”android.permission.WRITE_EXTERNAL_STORAGE”/>
<uses-feature android:name=”android.hardware.microphone” android:required=”true”/>
```

**2. Botones para comenzar y detener la grabación y otro para reproducir el archivo de audio**

```xml
<?xml version=”1.0” encoding=”utf-8”?>
<androidx.constraintlayout.widget.ConstraintLayout
xmlns:android=”http://schemas.android.com/apk/res/android”
xmlns:app=”http://schemas.android.com/apk/res-auto”
xmlns:tools=”http://schemas.android.com/tools”
android:layout_width=”match_parent”
android:layout_height=”match_parent”
tools:context=”.MainActivity”>
<TextView
android:id=”@+id/textView”
android:layout_width=”wrap_content”
android:layout_height=”wrap_content”
android:text=”Hello World!”
app:layout_constraintBottom_toBottomOf=”parent”
app:layout_constraintLeft_toLeftOf=”parent”
app:layout_constraintRight_toRightOf=”parent”
app:layout_constraintTop_toTopOf=”parent” />
<Button
android:id=”@+id/btnGrabar”
android:layout_width=”wrap_content”
android:layout_height=”wrap_content”
android:layout_marginTop=”32dp”
android:text=”Grabar”
app:layout_constraintEnd_toEndOf=”parent”
app:layout_constraintStart_toStartOf=”parent”
app:layout_constraintTop_toTopOf=”parent” />
<Button
android:id=”@+id/btnReproducir”
android:layout_width=”wrap_content”
android:layout_height=”wrap_content”
android:layout_marginTop=”24dp”
android:text=”reproducir”
app:layout_constraintEnd_toEndOf=”parent”
app:layout_constraintStart_toStartOf=”parent”
app:layout_constraintTop_toBottomOf=”@+id/btnGrabar” />
</androidx.constraintlayout.widget.ConstraintLayout>
```

**3. Código de la aplicación**

```kotlin
private var isGrabando = false
private lateinit var grabadora: MediaRecorder

override fun onCreate(savedInstanceState: Bundle?) {
	super.onCreate(savedInstanceState)
	setContentView(R.layout.activity_main)
	btnGrabar.setOnClickListener {
		onGrabar()
	}
	btnReproducir.isEnabled = false
	btnReproducir.setOnClickListener {
		onReproducir()
	}
}

/**
	METODO PARA EL BOTON DE GRABAR/PARAR
*/
private fun onGrabar() {
	if(isGrabando) {
		isGrabando = false
		btnGrabar.text = “Grabar”
		stopGrabacion()
	}
	else {
		isGrabando = true
		btnGrabar.text = “Detener”
		startGrabacion()
	}
}

/**
	METODO PARA EL BOTON DE REPRODUCIR
*/
override fun onReproducir() {
	// Se crea un MediaPlayer sobre el archivo de salida
	val file = getArchivoSalida()
	val reproductor = MediaPlayer()
	reproductor.setDataSource(file?.path)
	reproductor.prepare()
	reproductor.start()
}

/**
	AL INICIAR LA ACTIVIDAD
*/
override fun onStart() {
	super.onStart()
	// Pedir permisos en tiempo de ejecucion
	// (en versiones en las que es necesario)
	if(Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
		requestPermissions(arrayOf(
		Manifest.permission.RECORD_AUDIO,
		Manifest.permission.WRITE_EXTERNAL_STORAGE),
		6969)
	}
	// Instanciar el MediaRecorder, indicando duracion maxima,
	// tamaño del fichero, mensaje de error
	// informacion de tamaño maximo,... 
	grabadora = MediaRecorder()
	grabadora.setMaxDuration(15000)//15 segundos max
	grabadora.setMaxFileSize(1024*1024)//1 Mb max
	grabadora.setOnErrorListener { mr: MediaRecorder, what: Int, extra:
		Int ->
		showMensaje(“Error: Error en $mr, ocurrió $what con $extra”)
		onGrabar()
	}
	grabadora.setOnInfoListener { mr: MediaRecorder, what: Int, extra:
		Int ->
		when(what) {
			MediaRecorder.MEDIA_RECORDER_INFO_MAX_DURATION_REACHED -> {
				showMensaje(“Se alcanzó la duración máxima!”)
				onGrabar()
			}
			MediaRecorder.MEDIA_RECORDER_INFO_MAX_FILESIZE_REACHED -> {
				showMensaje(“Se alcanzó el tamaño máximo!”)
				onGrabar()
			}
		}
	}
}

/**
	AL PARAR ACTIVIDAD
*/
override fun onStop() {
	// Se libera el MediaRecorder
	grabadora.release()
	super.onStop()
}

/**
	METODO PARA INICIAR GRABACIOON
*/
private fun startGrabacion() {
	val recording = getArchivoSalida()
	// Se elimina el fichero si ya existe
	if(recording?.exists() == true) {
		recording.delete()
	}
	// Se configuran los parametros de grabacion en el MediaRecorder
		grabadora.setOutputFile(getArchivoSalida()?.path)
		grabadora.setAudioSource(MediaRecorder.AudioSource.MIC)
		grabadora.setOutputFormat(MediaRecorder.OutputFormat.AMR_NB)
		grabadora.setAudioEncoder(MediaRecorder.AudioEncoder.AMR_NB)
		grabadora.setAudioChannels(2)
	try {
		//Se prepara y se inicia la grabacion
		grabadora.prepare()
		grabadora.start()
	}
	catch(e: Exception) {
		showMensaje(“Error preparando la grabadora “+e.message)
	}
}

/**
	METODO PARA PARAR GRABACION
*/
private fun stopGrabacion() {
	// Se detiene la grabacion
	try {
		grabadora.stop()
	} catch(e: java.lang.Exception) {
		showMensaje(“Error al detener la grabación “+e.message)
	}
	grabadora.reset()
	val recording = getArchivoSalida()
	if(recording?.exists()==true && recording.length() > 0) {
		btnReproducir.isEnabled = true
		showMensaje(“Grabación finalizada”)
	} else {
		showMensaje(“Error en la grabación”)
	}
}

/**
	SE CREA EL ARCHIVO DE SALIDA
*/
private fun getArchivoSalida(): File? {
	return File(getExternalFilesDir(null), archivo)
}

/**
	SE MUESTRA MENSAJE
*/
private fun showMensaje(msg: String, e: Exception? = null) {
	Log.e(tag, msg, e)
	Toast.makeText(this, msg, Toast.LENGTH_LONG).show()
	textView.text = msg
}

companion object {
	private const val tag = “Activity”
	private const val archivo = “grabacion.3gp”
}

```

## 6. Clips de audio. Secuencias MIDI. Clips de video. Y otros.

### 6.1. Clips de audio y vídeo

**Código para reproducir tanto audio como vídeo**

```kotlin
import android.media.MediaPlayer
import android.net.Uri
import android.os.Bundle
import android.widget.MediaController
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {

    private lateinit var mp: MediaPlayer

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // Audio
        initAudio()

        // Video
        initVideo()
    }

    ///////////////////////////////////////////////////////////////////////////
    ///////////
    /// AUDIO
    private fun initAudio() {
        mp = MediaPlayer.create(this, R.raw.audio_midi)
        // mp = MediaPlayer.create(this, R.raw.audio_ogg)

        mp.setOnCompletionListener { 
            stopAudio()
            Toast.makeText(this, getString(R.string.audio_finish), Toast.LENGTH_LONG).show()
        }

        btnPlayAudio.setOnClickListener {
            if (mp.isPlaying)
                pauseAudio()
            else
                playAudio()
        }

        btnStopAudio.setOnClickListener {
            stopAudio()
        }

        btnPlayAudio.text = getString(R.string.play)
        btnStopAudio.isEnabled = false
    }

    private fun playAudio() {
        mp.start()
        btnPlayAudio.text = getString(R.string.pause)
        btnStopAudio.isEnabled = true
    }

    private fun stopAudio() {
        mp.stop()
        mp.prepare()
        mp.seekTo(0)
        btnPlayAudio.text = getString(R.string.play)
        btnStopAudio.isEnabled = false
    }

    private fun pauseAudio() {
        mp.pause()
        btnPlayAudio.text = getString(R.string.play)
    }

    ///////////////////////////////////////////////////////////////////////////
    ///////////
    /// VIDEO
    private fun initVideo() {
        videoView.setOnCompletionListener {
            stopVideo()
            Toast.makeText(this, getString(R.string.video_finish), Toast.LENGTH_LONG).show()
        }

        btnPlayVideo.setOnClickListener {
            when {
                videoView.isPlaying -> pauseVideo()
                videoView.currentPosition != 0 -> resumeVideo()
                else -> playVideo()
            }
        }

        btnStopVideo.setOnClickListener {
            stopVideo()
        }

        btnPlayVideo.text = getString(R.string.play)
        btnStopVideo.isEnabled = false
    }

    private fun playVideo() {
        // Archivo en directorio res/raw (Nota: no debemos escribir la extensión)
        // videoView.setVideoURI(Uri.parse("android.resource://$packageName/raw/video_mp4"))
        // videoView.setVideoURI(Uri.parse("android.resource://$packageName/raw/video_ogv"))
        videoView.setVideoURI(Uri.parse("android.resource://$packageName/raw/video_3gp"))

        val mediaController = MediaController(this)
        mediaController.setMediaPlayer(videoView)
        videoView.setMediaController(mediaController)
        videoView.requestFocus()
        videoView.start()

        btnPlayVideo.text = getString(R.string.pause)
        btnStopVideo.isEnabled = true
    }

    private fun resumeVideo() {
        videoView.start()
        btnPlayVideo.text = getString(R.string.pause)
    }

    private fun pauseVideo() {
        videoView.pause()
        btnPlayVideo.text = getString(R.string.play)
    }

    private fun stopVideo() {
        videoView.stopPlayback()
        btnPlayVideo.text = getString(R.string.play)
        btnStopVideo.isEnabled = false
    }
}

```

**Uso de SoundPool**

```kotlin
import android.media.AudioManager
import android.media.SoundPool
import android.widget.Button
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {

    private lateinit var audioManager: AudioManager
    private lateinit var soundPool: SoundPool

    data class Sonido(val id: Int, var boton: Button? = null, var cargado: Boolean = false)

    private val sonidos = HashMap<Int, Sonido>()
    private val sonidosRes = arrayListOf(
        R.raw.animal_bark_and_growl,
        R.raw.animal_hiss_and_rattle,
        R.raw.crow_call,
        R.raw.distant_dog_barking,
        R.raw.dog_barking,
        R.raw.dog_growling,
        R.raw.dog_snarling,
        R.raw.mouse_squeaking
    )

    private lateinit var botonesRes: ArrayList<Button>
    private var actVolume = 0f
    private var maxVolume = 0f
    private var volume = 0f

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        botonesRes = arrayListOf(
            button1, button2, button3, button4,
            button5, button6, button7, button8
        )

        txtCanales.doOnTextChanged { _, _, _, _ ->
            val canales = getCanalesFromUI()
            if (canales != null) {
                soundPool.release()
                initAudio(canales)
            }
        }
    }

    override fun onResume() {
        super.onResume()
        initAudio(getCanalesFromUI() ?: 8)
    }

    override fun onPause() {
        soundPool.release()
        super.onPause()
    }

    private fun getCanalesFromUI(): Int? = txtCanales.text.toString().toIntOrNull()

    private fun deshabilitarBotones() {
        button1.isEnabled = false
        button2.isEnabled = false
        button3.isEnabled = false
        button4.isEnabled = false
        button5.isEnabled = false
        button6.isEnabled = false
        button7.isEnabled = false
        button8.isEnabled = false
    }

    private fun initAudio(canales: Int) {
        deshabilitarBotones()

        audioManager = getSystemService(Context.AUDIO_SERVICE) as AudioManager
        actVolume = audioManager.getStreamVolume(AudioManager.STREAM_MUSIC).toFloat()
        maxVolume = audioManager.getStreamMaxVolume(AudioManager.STREAM_MUSIC).toFloat()
        volume = actVolume / maxVolume
        volumeControlStream = AudioManager.STREAM_MUSIC

        val audioAttr = AudioAttributes.Builder()
            .setLegacyStreamType(AudioManager.STREAM_MUSIC)
            .build()

        soundPool = SoundPool.Builder()
            .setMaxStreams(canales)
            .setAudioAttributes(audioAttr)
            .build()

        soundPool.setOnLoadCompleteListener { _, sampleId, status ->
            sonidos[sampleId]?.cargado = status == 0
            sonidos[sampleId]?.boton?.isEnabled = status == 0
        }

        for ((boton, idRes) in sonidosRes.withIndex()) {
            val id = soundPool.load(this, idRes, 1)
            sonidos[id] = Sonido(id, botonesRes[boton])
        }
    }

    fun onClick(view: View?) {
        val i = view?.tag as String
        val sonido = sonidos[sonidos.keys.elementAt(i.toInt() - 1)]
        if (sonido != null) {
            if (swtBucle.isChecked)
                playLoop(sonido)
            else
                play(sonido)
        }
    }

    private fun play(sonido: Sonido) {
        if (sonido.cargado) {
            soundPool.play(sonido.id, volume, volume, 1, 0, 1f)
        }
    }

    private fun playLoop(sonido: Sonido) {
        if (sonido.cargado) {
            soundPool.play(sonido.id, volume, volume, 1, -1, 1f)
        }
    }

    fun pause(sonido: Sonido) {
        soundPool.pause(sonido.id)
    }

    fun stopSound(sonido: Sonido) {
        soundPool.stop(sonido.id)
    }
}

```

**Uso de ExoPlayer**

`implementation ‘com.google.android.exoplayer:exoplayer:2.10.4’`

```kotlin
import android.net.Uri
import com.google.android.exoplayer2.ExoPlayerFactory
import com.google.android.exoplayer2.SimpleExoPlayer
import com.google.android.exoplayer2.source.MediaSource
import com.google.android.exoplayer2.source.ProgressiveMediaSource
import com.google.android.exoplayer2.upstream.DefaultDataSourceFactory
import com.google.android.exoplayer2.util.Util

class RadioPlayerActivity : Activity() {

    private lateinit var exoPlayer: SimpleExoPlayer
    private lateinit var ms: MediaSource
    private lateinit var dsf: DefaultDataSourceFactory

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_exoplayer)

        exoPlayer = ExoPlayerFactory.newSimpleInstance(this)
        dsf = DefaultDataSourceFactory(this, Util.getUserAgent(this, "ExoPlayer"))

        val radio1 = "http://playerservices.streamtheworld.com/api/livestream-redirect/LOS40.mp3"
        val radio2 = "http://us3.internet-radio.com:8342/listen.pls&t=.pls"

        // Crea la fuente de medios para el primer enlace de radio
        ms = ProgressiveMediaSource.Factory(dsf).createMediaSource(Uri.parse(radio1))

        with(exoPlayer) {
            prepare(ms)

            btnPlay.setOnClickListener {
                playWhenReady = true
            }

            btnStop.setOnClickListener {
                playWhenReady = false
            }
        }
    }

    override fun onDestroy() {
        exoPlayer.playWhenReady = false
        super.onDestroy()
    }
}

```
### 6.2. MIDI

El sistema Android tiene capacidad para controlar dispositivos MIDI conectados a él mediante USB o Bluetooth. 
Así el dispositivo Android puede conectarse a dispositivo hardware o software MIDI para controlar o recibir comandos MIDI. Por ejemplo se podría recibir datos de un teclado MIDI conectado a la app para generar los sonidos o desarrollar una app que mostrarse un teclado y enviase los comandos MIDI a un dispositivo. 

El SDK de Android dispone de `android.media.midi` para enumerar los dispositivos y conectarse a ellos. a partir de Android API 29 también se puede usar la API nativa de MIDI (aunque es necesario el uso del lenguaje C)

## 7. Protocolo de transmisión en tiempo real RTP

El **Realtime Transport Protocol (RTP)** permite enviar y recibir audio y vídeo a través de Internet. Puede usarse para llamadas telefónicas de VozIP, para escuchar música de radios digitales, ver contenidos de vídeo como Netflix,...

No garantiza entrega de paquetes ni controla flujo de datos. Se usa RTP junto con RTCP permitiendo experiencia multimedia interactiva y tiempo real en Internet. 

El **RTP Control Protocol (RTPC)** se encarga del control de flujo y calidad del servicio ayudando a la sincronización de los diferentes streams.

El protocolo RTP lleva en su interior el payload, es decir, los datos de audio o vídeo que tienen que llegar en tiempo de modo que el cliente no perciba saltos o retardos en la reproducción. Los paquetes RTP llevan timestamps y números de secuencia y cuentan con mecanismos para detectar la pérdida de paquetes de datos y otros problemas que se dan sobre todo cuando se utiliza el protocolo UDP. 

**Herramientas de digital right management (DMR) como Widevine** se aplican a los streams para encriptar e impedir la copia de los datos involucrados. La clase `` `` es compatible con la reproducción de contenido protegido por DRM a partir de Android 8 (API 26) aunque también se disponen de otras clases como `MediaDrm`

Ya se ha hablado de `ExoPlayer` un potente reproductor que se puede incrustar en la app, permitiendo diversos niveles de complejidad. 

### 7.1. Control y mono

La clase `VolumeShaper` permite insertar atenuaciones de volumen al comienzo, al final o de transición entre clips de audio. Se pueden crear instanciar de `VolumeShaper` desde objetos `MediaPlayer` o `AudioTrack` y configurar con él las atenuaciones que deseemos mediante los parámetros que definen la curva de sonido. 
Control preciso y suave sobre las transiciones de volumen, mejorando la calidad del audio en aplicaciones como juegos, música o vídeo. 

Otras formas de control de media interesantes en la actualiza es el enrutado de audio o vídeo hacia dispositivos externos. Esto se puede hacer con la interfaz `MediaRouter` cuando nos conectamos a dispositivos externos. Estos dispositivos responderán con `MediaRouterProvider` que permitirán conectarnos a esos dispositivos y enviar comandos de control de la reproducción (Caso de los dispositivos Google Cast).

Android también permite manejar el control de volumen de audio, con `setVolumeControlStream` permite especificar el canal en el que se reproducirán los clips. Se pueden estudiar los canales que permite Android para controlar por separado el volumen de las notificaciones, la música, los tonos de llamada. Así cuando el usuario modifique el volumen, este solo afectará al canal que se haya elegido.

También se pueden evitar cambios drásticos de sonido al desconectar los auriculares inalámbricos. Se podría pausar el audio o dejar que siga sonando. El sistema avisará mediante un intent con la acción de tipo `ACTION_AUDIO_BECOMING_NOISY`. En la app habrá que crear un `BroadcastReceiver` que admita esta acción y actúe en consecuencia. 

También está la posibilidad de elegir reproducción mono o estéreo mediante las constantes de `AudioFormat`: `AudioFormat.CHANNEL_OUT_MONO` y `AudioFormat.CHANNEL_OUT_STREO`  en `setChannelMask` al crear un `AudioTrack`

```kotlin
val minBufferSize = AudioTrack.getMinBufferSize(16000,
AudioFormat.CHANNEL_OUT_STEREO, AudioFormat.ENCODING_PCM_16BIT)
val track = AudioTrack.Builder().setAudioFormat(
AudioFormat.Builder()
	.setChannelMask(AudioFormat.CHANNEL_OUT_STEREO)
	.setEncoding(AudioFormat.ENCODING_PCM_16BIT)
	.setSampleRate(44100)
	.build())
	.setTransferMode(AudioTrack.MODE_STREAM)
	.setBufferSizeInBytes(minBufferSize)
	.build()
track.play()
```

**Ejemplo: Evitar sonidos altos**

```kotlin
private val intentFilter = IntentFilter(AudioManager.ACTION_AUDIO_BECOMING_
NOISY)
private val myNoisyAudioStreamReceiver = BecomingNoisyReceiver()
private val callback = object : MediaSession.Callback() {
	override fun onPlay() {
		registerReceiver(myNoisyAudioStreamReceiver, intentFilter)
}
	override fun onStop() {
		unregisterReceiver(myNoisyAudioStreamReceiver)
	}
}
private class BecomingNoisyReceiver : BroadcastReceiver() {
	override fun onReceive(context: Context, intent: Intent) {
		if (intent.action == AudioManager.ACTION_AUDIO_BECOMING_NOISY) {
			// Aquí pausamos el playback, o la acción que creamos oportuna
			Log.e(tag, “BecomingNoisyReceiver:onReceive:”)
		}
	}
}
```


## 8. Servicios multimedia en Android Studio

- **Audio Flinger:** Es el servidor de audio de Android, encargado de gestionar y
controlar la mezcla y enrutamiento de audio. Audio Flinger permite la reproducción y
grabación de audio, aplicando efectos y ajustando niveles de volumen en función de
la fuente y el destino del sonido.
- **Camera Service**: Este servicio gestiona y controla el acceso a las cámaras del
dispositivo Android. Camera Service permite a las aplicaciones capturar imágenes y
video, cambiar configuraciones de la cámara, y acceder a características avanzadas
como enfoque automático, flash y estabilización de imagen.
- **MediaPlayer Service:** Facilita la reproducción de audio y video desde diversas
fuentes, como archivos locales, recursos en la aplicación o streams en línea.
MediaPlayer Service proporciona control básico de reproducción, como reproducir,
pausar, detener, buscar y ajustar el volumen.
- **MediaCodec Service**: Este servicio ofrece una interfaz para codificar y decodificar
contenido multimedia en Android. MediaCodec Service permite la compresión y
descompresión de audio y video en diferentes formatos, lo que facilita la
reproducción, grabación y transmisión de contenido multimedia en aplicaciones
Android.
- **MediaDrm Service**: Es un servicio que gestiona la protección y gestión de derechos
digitales (DRM) en dispositivos Android. MediaDrm Service permite a las
aplicaciones reproducir contenido protegido con DRM, como videos y música con
derechos de autor, garantizando la seguridad y el cumplimiento de las restricciones
de licencia.