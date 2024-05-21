
## 1. Preferencias

Se conoce como pantalla de configuración o pantalla de preferencias a la pantalla que el usuario utiliza para introducir la información que desea a la hora de utilizar cada una de las aplicaciones.

Cuando el usuario modifica una preferencia, esta se guarda en un fichero en forma de par clave-valor.

Google recomienda diseñar las preferencias mediante la librería Preference de AndroidX.
### Diseño de la pantalla de preferencias

#### Mostrar la pantalla de preferencias

1. Se crea recurso XML en `res/xml/settings.xml.` Si indica que "android.preference.PreferenceScreen" está deprecado, debe añadirse al módulo la librería de Androix (androidx.preference)
2. La pantalla de preferencias se define por el contenedor
```xml
<PreferenceScreen>
...
</PreferenceScreen>
```

Los objetos pueden agruparse en categorías de forma que se muestre el título de categoría y se añada una línea divisoria al final de la categoría separando los grupos de preferencias. 

Ejemplo:
```xml
<PreferenceCategory android:title="@string/category_user_information">
...
</PreferenceCategory>
```


#### Tipos de preferencias

**Preference**
Muestra elemento de texto simple. Deben definirse al menos tres atributos:
- key: Valor que el usuario introduce en el fichero de preferencias. Es la misma clave que se usa para recuperar
- title: Título de la preferencia
- summary: Descripción debajo del título con tamaño de texto menor
- icon: Icono que representa a la preferencia

```xml
 android:key="preference_key"
 android:title="@string/preference_user"
 android:summary="@string/preference_user_summary"
 android:icon="@drawable/ic_action_user" >
```

**CheckBoxPreference**: El usuario puede activar o desactivar. La preferencia devuelve si está habilitado o deshabilitado. Suele estar en desuso para usar `SwitchPreferencecompat`

**SwitchPreferenceCompat**: Guarda dos estados al igual que `CheckBoxPreference` pero se muestra como un pequeño interruptor

```xml
<SwitchPreference
android:defaultValue="true"
android:key="preference_saveuser_key"
android:title="@string/preference_saveuser" />
```

**EditTextPreference**: Cuadro de diálogo donde usuario puede introducir una cadena de texto sencilla. a veces es recomendable que el valor introducido aparezca como valor resumen. (Para ello debe añadir atributo `app:useSimpleSummaryProvider="true"` dentro de la preferencia. En caso de que no esté definido aparece Not Set)

```xml
<EditTextPreference
 android:dialogTitle="@string/dialog_title_name_avatar"
 android:key="preference_name_avatar_key"
 android:title="@string/preference_name_avatar"
 app:useSimpleSummaryProvider="true"
 android:icon="@drawable/ic_action_name_avatar"/>
```


**SeekBarPreference**: Muestra un SeekBar para introducir un valor entero. Ejemplo: introducir 18 como valor inicial mediante `android:defaultValue`. Puede establecerse valor máximo con `android:max`

```xml
  <SeekBarPreference
   android:key="preference_age_key"
   android:title="@string/preference_age"
   android:defaultValue="18"/>
```

### Recuperar preferencias almacenadas

La gestión de las preferencias es transparente para el programador. Android las almacena en forma de clave-valor y quedan dentro de la aplicación.
Se utilizan las clases `androidx.preference.PreferenceManager` y `android.contentSharedPreferences`

Pueden ser recuperadas programáticamente por el desarrollador para cuando lo necesite. 

Así, no  solo es necesario en una aplicación con interfaz gráfica de preferencias; también es necesario si se quiere que la aplicación siempre esté accesible. 

```java
// Obtener instancia de SharedPreferences a partir de PreferenceManager
SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(activity_context);

// Para recuperar los valores de preferencias segun el tipo de dato se podran usar los siguientes metodos:
sharedPreferences.getString(key, default_value);
sharedPreferences.getInt(key, default_value);
sharedPreferences.getFloat(key, default_value);
sharedPreferences.getBoolean(key, default_value); // SwitchPreference

// Ejemplo
Boolean saveUser = sharedPreferences.getBoolean("preference_save_user_key", true);
```


## 2. Ficheros

La gestión de ficheros se hace como habitualmente en Java con el paquete `java.io`

Debe tenerse en cuenta dónde se ubicarán los ficheros:
- En memoria **interna** -> Memoria **interna**
- En memoria **interna** -> **Recursos** de la aplicación
- En memoria **externa** (Tarjeta de memoria)
### 2.1. Almacenamiento en memoria interna

La **memoria interna** del dispositivo es limitada y no debe sobrecargarse. Al instalar una aplicación, el sistema reserva espacio para almacenar los ficheros de datos necesarios (no confundir con la estructura de carpetas del proyecto de la aplicación.). La ruta de la memoria interna es `/data/data/paquete.aplicacion/files/`

Se pueden usar los métodos:
- `openFileOutput()`: Abrir fichero en modo escritura
- `openFileInput()`: Abrir fichero en modo lectura
- `getFilesDir()`: Recuperar ruta absoluta del directorio
- `getDir()`: Crear o abrir directorio de la aplicación
- `deleteFile()`: Eliminar fichero
- `fileList()`: Devuelve array con los ficheros internos de la aplicación
- `openRawResource()`: Lee ficheros de recursos de la carpeta `/res/raw/`

Los ficheros de la memoria interna son privados. Pero su modo de acceso puede variar con las constantes:
- `MODE_PRIVATE`: Otras aplicaciones no pueden acceder a él
- `MODE_WORLD_READABLE`: Otras aplicaciones pueden leer sobre él. (Obsoleto API 17)
- `MODE_WORLD_WRITABLE`: Otras aplicaciones pueden escribir sobre él. (Obsoleto API 17)

**Guardar una cadena de texto en memoria interna**

```java
OutputStreamWriter outputStreamWrite = new OutputStreamWriter(openFileOoutput("fichero.txt", Context.MODE_PRIVATE));
outputStreamWriter("Esto es un texto de prueba. Vaya suplicio la preparación de las POT. Ojalá llegue el 28 de mayo y acaben ya");
outputStreamWriter.close();
```

Ubicación: Explorador de archivos Android Studio (Tools - Android - Android Device Monitor - File explorer)

**Leer fichero de texto almacenado en memoria interna**

```java
BufferedReader bufferedReader = new BufferedReader(new ImputStreamReader(openFileInput("fichero.txt")));
String texto = bufferedReader.readLine();
bufferedReader.close();
```

#### 2.1.1. Almacenamiento en los recursos de la aplicación

Fichero almacenado en /res/raw/ que se quiere consultar desde la propia aplicación. 

**En la carpeta /res/raw solo hay acceso de lectura pero no de escritura**

Recuerda, la ruta de la memoria interna es `/data/data/com.example.ejemploficheros/files/`

Puede ser cualquier binario (imagen, vídeo...)
Para leerlo se puede hacer así:

```java
InputStream inputStream = getResources().openRawResource(R.raw.fich_raw);
BufferedReader bufferedReader = new BufferedReader(inputStream);
String texto = bufferedReader.readLine();
bufferedReader.close();
```

## 2.2. Almacenamiento en memoria externa

La memoria externa que se suele usar es tarjetas de memoria SD extraíbles. 
Puede corresponder a ficheros privados de la aplicación que se instala en la tarjeta o ficheros públicos compartidos por varias aplicaciones.

Debe considerarse:
- **Seguridad y permisos del usuario**: Ficheros públicos y accesibles a varias aplicaciones. Debe solicitarse permiso del usuario para acceder a la tarjeta de memoria en el archivo de manifiesto:
```xml
<uses-permission android:name=”android.permission.WRITE_EXTERNAL_STORAGE”><br /></uses-permission>
```

- **Estado de la tarjeta de memoria**: Antes de comenzar a tratar los ficheros debe conocerse el estado de la tarjeta de memoria. Esta puede no estar presente en el dispositivo o no estar bien montada. 
```java
String estado = Environment.getExternalStorageState()
```

Se devuelve una constante dependiendo del estado de la tarjeta SD:
	- MEDIA_MOUNTED: la tarjeta está montada y disponible para lectura y escritura.
	- MEDIA_MOUNTED_READ_ONLY: la tarjeta está montada en modo lectura.
	- MEDIA_UNMOUNTED: la tarjeta está insertada pero no se encuentra montada.
	- MEDIA_REMOVED: la tarjeta no está insertada.

- **Acceso al directorio de la tarjeta de memoria**: Se utilizan los métodos 
`getExternalFilesDir()`: Devuelve ruta de una carpeta determinada de la aplicación. Si se pasa como parámetro null recupera la carpeta raíz (/mnt/sdcard/Android/data/paquete.aplicacion/files/)

`getExternalStoragePublicDirectory()`: Devuelve la ruta de una carpeta pública.

Puede indicarse alguno de los subdirectorios definidos por constantes para clasificar los contenidos (como se hace en la galería multimedia)

|Constante|¿Qué almacena?|¿Dónde se almacena?|
|---|---|---|
|DIRECTORY_PICTURES|Ficheros de imágenes, fotos|Pictures/|
|DIRECTORY_MOVIES|Ficheros de películas.|Movies/|
|DIRECTORY_MUSIC|Ficheros de música.|Music/|
|DIRECTORY_RINGTONES|Ficheros de tonos.|Ringtones/|


Para **configurar memoria externa en el emulador (AVD)** debe ponerse la opción SD Card Size con tamaño de memoria adecuado. Para visualizar los ficheros se usará la misma opción que en los ficheros internos (File Explorer)

### 2.2.1. Escribiendo en memoria externa

Una vez se especifican los permisos correspondientes y se comprueba el estado de la tarjeta de memoria (si se encuentra debidamente montada), se puede escribir un fichero parecido a como se hacía en la memoria interna:

```java
String estado = Environment.getExternalStorageState();
if (estado.equals(Environment.MEDIA_MOUNTED)){

File file;

// En el espacio reservado a la aplicacion dentro de la memoria SD
file = new File(getExternalFilesDir(null), "fichero.txt");

// Para escribir en uno de los subdirectorios publicos que la SD tiene establecida
// Recuerda, estos son accesibles por cualquier aplicacion!!!!
file = new File(
         Environment.getExternalStoragePublicDirectory(
                Environment.DIRECTORY_PICTURES), "fotografia.jpg");


     OutputStreamWriter fout = new OutputStreamWriter(new FileOutputStream(file));
     fout.write("Texto de prueba almacenado en tarjeta SD.");
     fout.close();                    
}
```

### 2.2.2. Leyendo de memoria externa

Para leer, se hará igual que en escritura: Necesitamos permisos, necesitamos comprobar el estado de la tarjeta de memoria.

Ejemplo: Lectura en zona reservada:

```java
String estado = Environment.getExternalStorageState();
if (estado.equals(Environment.MEDIA_MOUNTED)){
     File file = new File(getExternalFilesDir(null), "fichero.txt");
     BufferedReader br = new BufferedReader(
                             new InputStreamReader(
                                 new FileInputStream(file)));
     String texto = br.readLine()
     br.close();
}
```

## 3. Base de datos

Android incorpora la librería SQLite que, como motor de bases de datos, es ideal para Android ya que:
- Necesita tamaño reducido y requiere pocos recursos del sistema
- Se basa en el modelo relacional
- Utiliza SQL
- Soporta transacciones
- Es de código abierto

### 3.1. Estructura de SQLite

Las clases más utilizadas son:

**SQLiteOpenHelper**: Creación y actualización de BBDD
- `onCreate()`:  Crear BBDD por primera vez
- `onUpgrade()`: Actualizar estructura de la BBDD
- `getReadableDatabase()`: Abrir BBDD en modo lectura
- `getWritableDatabase()`: Abrir BBDD en modo lectura y escritura
- `getDatabaseName()`: Recupera nombre de la BBDD
- `close()`: Cerrar BBDD

**SQLiteDatabase**: Métodos para gestionar la base de datos
- `insert()`: Insertar nuevo registro
- `update()`: Modificar registro
- `delete()`: Eliminar registro
- `execSQL()`: Ejecutar sentencia SQL que no devuelve ningún registro
- `rawQuery()`: Lanzar sentencia de consulta usando comando completo SQL y recuperar el resultado de un cursor
- `query()`: Lanzar sentencia de consulta con varios parámetros y recuperar resultado en cursor
- `isOpen()`: Comprobar si está abierta la BBDD

**SQLiteCursor**: Cursor para recorrer filas recuperadas en una sentencia SQL
- `moveToFirst()`: Posicionar cursor en primer registro
- `moveToNext()`: Posicionar cursor en siguiente registro
- `getString()`: Recuperar String
- `getInt()`: Recuperar Int
- `getFloat()`: Recuperar Float
- `getLong()`: Recuperar Long
- `getColumnCount()`: Recuperar número de columnas
### 3.2. Creación de base de datos

Debe usarse **SQLiteOpenHelper** para tener la clase auxiliar:

- Crear una clase que herede de `SQLiteOpenHelper`
- Constructor que llame a la clase padre con **contexto** `Context`, nombre **base** de datos, **`CursorFactory`**, entero de **version** de base de datos
- Se sobrescriben los métodos `onCreate(SQLiteDatabase db)` y `onUpgrade(SQLiteDatabase db, int versionActual, int nuevaVersion)`. 
En la **creación**  se ejecutará la sentencia de creación de la tabla. En el **upgradeo** se actualizará la BBDD (por ejemplo incluyendo un campo nuevo). La implementación dependerá de lo que se haya hecho en la BBDD (habría que migrar los datos a la nueva estructura...) pero podremos probar borrándola y creando de nuevo.

```java
public class MiBaseDatosHelper extends SQLiteOpenHelper {

	public MiBaseDatosHelper(Context contexto, String nombre,                           CursorFactory factory, int version) {
	    super(contexto, nombre, factory, version);
	}

	@Override
	public void onCreate(SQLiteDatabase db) {
	    db.execSQL(“CREATE TABLE miTabla (campo1 INTEGER, campo2 TEXT)”);
	}

	@Override
	public void onUpgrade(SQLiteDatabase db, int versionAnterior, int versionNueva) {
	     //Se elimina la versión anterior de la tabla
	     db.execSQL("DROP TABLE IF EXISTS miTabla");
	     //Se crea la nueva versión de la tabla
	     db.execSQL(“CREATE TABLE miTabla (campo1 INTEGER, campo2 TEXT)”);
	}

}
```

### 3.3. Operaciones sobre una base de datos

La clase auxiliar creada a partir SQLiteOpenHelper se usará cada vez que se quiera lanzar una actividad en la que se realice una operación sobre la base de datos. 

Las operaciones pueden clasificarse según si se recupera o no un resultado tras su ejecución en:
- **Inserción**, **actualización** y **eliminación** de registros -> no devuelve ningún registro, solo modifica. 
- **Selección** -> retorna registros en un cursor.

Los pasos que podrían seguirse son:
 1. Crear objeto `SQLiteOpenHelper` para abrir la BBDD pasándole el contexto (la propia actividad), nombre de la BBDD, objecto `CursorFactory` (no suele ser necesario) y el número de versión. Puede suceder:
	 1. BBDD existe y versión coincide: Se crea la conexión
	 2. BBDD existe y versión no coincide: Se lanza `onUpgrade()` y se realiza la conexión
	 3. BBDD no existe: Se lanza `onCreate()`
 2. **Abrir BBDD** en modo lectura y/o escritura, según la necesidad
 3. **Comprobar** que la BBDD **está abierta** y usar métodos para **realizar operación** sobre la misma
 4. **Cerrar la BBDD**

```java
//Creamos un objeto de la clase auxiliar.
MiBaseDatosHelper bdhelp = 
                 new MiBaseDatosHelper(this, "nombreBD", null, 1);
 
//Abrimos en modo lectura y escritura la base de datos 'MiBD' 
SQLiteDatabase bd = bdhelp.getWritableDatabase();
 
//Si la base de datos está abierta.
if(bd.isOpen())
{
     //Aquí hay que añadir el código necesario para realizar 
     //cualquier tipo de operación sobre la base de datos.
     //Veremos algunos métodos en los apartados siguientes.
 
     //Cerramos la base de datos
      bd.close();
}
```

#### 3.3.1 Inserción, actualización y eliminación de registros

**DML pero que no devuelvan ningún registro.**

**execSQL** : Recibe una sentencia SQL completa
```java
bd.execSQL(“INSERT INTO miTabla (campo1, campo2) VALUES (1, 'unTexto')” );
bd.execSQL(“UPDATE miTabla SET campo2 = 'otroTexto' WHERE campo1 = 1 ” );
bd.execSQL(“DELETE FROM miTabla WHERE campo1 = 1 ” );

// Puede realizarse paso por parametros de la siguiente forma
String[] argumentos = new String[]{"valor1","valor2"};
bd.execSQL("DELETE FROM miTabla WHERE campo2=? OR campo2=?", argumentos);
```

**insert**: Recibe nombre de la tabla, condiciones (en inserción null porque no se precisan), valores del registro (con `ContentValues` almacenados en forma de clave-valor)

```java
    //Creamos el objeto ContentValues con los valores del registro.
    ContentValues miRegistro = new ContentValues();
    miRegistro.put("campo1", 1);
    miRegistro.put("campo2", "unTexto");
    
    //Insertamos el registro.
    bd.insert("miTabla", null, miRegistro);
```

**update**: Recibe nombre de la tabla, valores (en `ContentValues`), condición (clausula WHERE, puede dejarse a null si no se necesita), argumentos de la condición. 

```java
    //Valores a actualizar.
    ContentValues miRegistro = new ContentValues();
    valores.put("campo2","otroTexto");
    
    //Actualizar el registro
    bd.update("miTabla", miRegistro, "campo1=1", null);
```

**delete**: Recibe nombre de la tabla, condición (clausula WHERE), argumentos de la condición.

```java
	//Eliminamos el registro.
	bd.delete("miTabla", "campo1=1", null);

	String[] argumentos = new String[]{"valor1","valor2"};
	bd.update("miTabla", miRegistro, "campo2=? OR campo2=?", argumentos);
```

Ejemplillos: `bd.insert("miTabla", null, miRegistro);` o `bd.delete("miTabla", null, null)`
#### 3.3.2. Recuperación o consulta de registros

**DML - Pero en recuperación de registros**

- **rawQuery**: **ejecuta directamente** sentencia SQL de la consulta que se pasa por parámetro
- **query**: **usa varios parámetros** para construir la sentencia a ejecutar. Debemos pasar el nombre de la tabla, array con nombres de los campos, condición (WHERE), argumentos (puede dejarse a null si se necesita o pasarlos como parámetros en un array), Cláusula GROUP BY (opcional), Cláusula HAVING (opcional), Cláusula ORDER BY (opcional)

La ejecución de ambas sentencias devuelve conjunto de registros `Cursor` que hereda de `SQLiteCursor` pudiendo procesar de forma individual cada fila del resultado de la consulta.

Inicialmente el cursor apunta a la posición previa de la primera fila. Debe moverse al primer registro con `moveToNext`. Después se va iterando por cada fila hasta llegar al final donde `moveToNext()` devolverá el valor false. 

**Con rawQuery**
```java
Cursor cur = bd.rawQuery("SELECT campo1, campo2 FROM miTabla", null);
```

Con **query
 
```java
String[] misCampos = new String[] {"codigo", "nombre"}; 
Cursor cur = bd.query("miTabla", misCampos, "campo1=1", null, null, null, null);
```

Una vez recuperados los objetos, usamos `moveToFirst()` y `moveToNext()`

```java
if (cur.moveToFirst()) {
     do {
              int var1 = cur.getInt(0);
              String var2 = cur.getString(1);
     } while(cur.moveToNext());
}
```


## 4. Room

#### Android Jetpack

Android Jetpack es un conjunto de librerías y herramientas para agilizar el desarrollo. Usan el paquete `androidx.*`. 

Ha **organizado** todos los componentes y los ha separado en estas cuatro categorías para entender mejor el mundo de Android:
- Interfaz de usuario
- Base
- Arquitectura
- Comportamiento

Busca **unificar** todas las librerías en un mismo paquete `androidx.*`

**Librerías equivalentes entre Support Library 28.0.0 y  las Bibliotecas de Android X**

|Support Library 28.0.0 (última versión de la biblioteca de compatibilidad.)|Bibliotecas de androidx|
|---|---|
|android.support.constraint.ConstraintLayout|androidx.constraintlayout.widget.ConstraintLayout|
|android.app.Fragment|androidx.fragment.app.Fragment|
|android.support.v4.app.ActivityCompat|androidx.core.app.ActivityCompat|

**Optimiza** las clases ya creadas (como se vio en las preferencias de usuario que pertenecen a la categorías "Comportamiento)

La aplicación puede tener varios puntos de entrada (actividades, fragmentos, servicios, proveedores de contenidos content providers) y receptores de emisión (broadcast receivers).
Las clases que forman parte de la categoría **Arquitectura** buscan simplificar la comunicación de todos los componentes permitiendo centrarse en el ciclo de vida de cada componente y así crear aplicaciones robustas, testeables y fáciles de mantener.

#### La librería Room

**Room** forma parte de la Arquitectura de componentes de Android Jetpack y permite convertir los objetos Java en datos de una tabla de SQLite de forma robusta.
Facilita las operaciones CRUD de la base de datos.

Podemos agregarla como dependencia del proyecto gradle:

```gradle
implementation "androidx.room:room-runtime:2.2.3"
annotationProcessor "androidx.room:room-compiler:2.2.3"
```

### 4.1. Componentes de la librería

Los componentes de la librería Room son:
- **Entidades**: Clases POJO de Java. Simples. Representan objeto en el mundo real. Compuestas por atributos privados y getters y setters públicos.
- **Objetos de acceso a datos o DAO**: Métodos que ofrecen acceso abstracto a la base de datos (interfaces, clases abstractas)
- **Base de datos**: Declarar la base de datos de la aplicación y definir objeto que nos permita acceder

A través de las anotaciones la librería Room genera el código de SQLite internamente. Cuando la anotación precede a la definición del componente, Room implementa el código para interactuar con la BBDD. 

Se podrían plantear en el proyecto los paquetes: `adapter`, `bd.dao`, `entity`, `iu`, `repository`

### 4.2. Crear entidades

Tabla de la base de datos y clase POJO que representa una fila de esa tabla.
Anotación `@Entity`. El nombre de la tabla coincide con la clase. Si no, se puede usar el atributo `tableName`
Cada atributo de clase se corresponde con una columna de la tabla. Por defecto es el nombre de la columna pero puede modificarse mediante la anotación `@ColumnInfo(name = "otro_nombre")`

Los nombres de tablas **no distinguen mayúsculas de minúsculas**

Otras anotaciones son:
- `@Ignore`: Se le dice a Room que ignore un campo en particular
- `@PrimaryKey(autoGenerate = true)`: Se le indica a Room que una variable es un valor que se autogenera y que no podrá repetirse. Es valor único, puede usarse para localizar un objeto concreto.
- `@NonNull`: No nulo. 
- Campos pueden ignorarse con `@Ignore`
- Si se requiere acceso muy rápido a la información de BBDD mediante búsqueda en el texto completo (FTS) se puede agregar la anotación `@Fts3` o `@Fts4`
- Para agregar índices a una entidad incluir la propiedad `indices` enumerando los nombres de las columnas que se quieran incluir en el índice o índice compuesto:

```java
@Entity(indices = {@Index("name"),
        @Index(value = {"last_name", "address"})})
public class User {
    @PrimaryKey
    public int id;

    public String firstName;
    public String address;

    @ColumnInfo(name = "last_name")
    public String lastName;

    @Ignore
    Bitmap picture;
}
```

**Restricciones**: 
- Necesita un constructor sin parámetros o un constructor con todos los campos no marcados con @Ignore: Room debe ser capaz de crear un objeto de esta clase
- Atributos `private` deben tener getter y setter 

```java
@Entity(primaryKeys = {"date", "avatar"})
public class Ranking implements Parcelable {

  public static final String TAG = "Ranking";
  @NonNull
  private String avatar;
  @NonNull
  private String date;
  private int points;
  
  public Ranking(String avatar, String date, int points) {
     this.avatar = avatar;
     this.date = date;
     this.points = points;
  }

  public String getAvatar() {
      return avatar;
  }
  public void setAvatar(String avatar) {
      this.avatar = avatar;
  }
  public String getDate() {
      return date;
  }
  public void setDate(String date) {
      this.date = date;
  }
  public int getPoints() {
      return points;
  }
  public void setPoints(int points) {
      this.points = points;   
  }

}
```
### 4.3. Crear DAO

Como se ha comentado, la DAO en Room es una clase abstracta o interfaz que define un conjunto de métodos que ofrecen acceso a la BBDD usando consultas en SQL. Estos métodos los implementa Room en tiempo de compilación y realiza ciertas comprobaciones.

Por ejemplo en `@Query`, Room verifica si hay un problema de la consulta. En ese caso muestra error de compilación en Build Output.

Se pueden hacer las siguientes consultas:
- `@Query`: Consultas a la BBDD. Si hay que filtrar en base a un parámetro que se pasa al método. Room hace coincidir el parámetro de vinculación con el parámetro del método. 
```java
@Query("SELECT * FROM ranking WHERE avatar=:avatar")
Ranking findByShortName(String avatar);
```

- `@Insert`: Inserta los parámetros con una sola transacción. Si solo se inserta un objeto este método puede devolver valor long que muestra el id de la fila o rowId insertada en BBDD. Si el parámetro es un Array o colección debe ser `long[]` o `List<Long>`
```java
@Insert(onConflict = OnConflictStrategy.IGNORE)
long insert(Ranking ranking);
```

- `@Update`: Modifica las entidades que se pasan por parámetro. Suele ser objeto que se actualiza considerando la PrimaryKey.  Puede devolver valor int con cantidad de filas actualizadas en BBDD.
```java
@Update 
void update(Ranking ranking);
```

- `@Delete`: Elimina conjunto de registros de la BBDD

```java
@Delete
void delete(Ranking ranking);
```

### 4.4. Crear Base de Datos

1. Crear clase para base de datos. Debe ser abstracta y heredar de `RoomDatabase`
2. Encima de la clase añadir anotación `@Database` y mediante el parámetro `entities` enumerar tablas y especificar versión de base de datos
3. En la clase, definir por cada DAO un método abstracto sin parámetros que devuelva la clase anotada con `@Dao`
4. Crear objecto Singleton  de la base de datos llamado `INSTANCE` que es el que usarán el resto de clases de la aplicación y accederán al objeto mediante método está tico de clase
5. Room impide acceso a la BBDD desde el hilo principal. Para ello la recomendaciones de Google usan un `ExecutorService` que ejecuta operaciones de la BBDD de forma asíncrona en un subproceso de segundo plano. Esto evita tener que crear `AsyncTask` cada vez que se quiera hacer una operación con la BBDD

```java
@Database(entities = {Ranking.class},version = 1, exportSchema = false)
public abstract class GameDatabase extends RoomDatabase
    public abstract RankingDao getRankingDao();
    private static volatile GameDatabase INSTANCE;
    private static String DATABASE_NAME="game";
    private static final int NUMBER_OF_THREADS = 4;
    public static final ExecutorService databaseWriteExecutor =
              Executors.newFixedThreadPool(NUMBER_OF_THREADS);
              
    public static void createDatabase(final Context context) {
        if (INSTANCE == null) {
            synchronized (GameDatabase.class) {
                if (INSTANCE == null) {
                    INSTANCE = Room.databaseBuilder(context.getApplicationContext(),
                            GameDatabase.class, DATABASE_NAME)
                            .build();
                }
            }
        }
    }
    
    public static GameDatabase getDatabase(){
        return INSTANCE;
   }

```

 La documentación oficial de Google en el método  `getDatabase() `se crea la base de datos si no existiera y se devuelve la instancia. Esto conlleva un problema, ya que desde cualquier parte de la aplicación que quiera acceder a nuestra base de datos hay que pasarle un objeto Context. Para solucionarlo,  se pueden crear dos métodos `onCreateDatabase()` y mantener `getDatabase()`.  
  
Para poder crear el objeto de la base de datos definimos una clase personalizada `Application` y en el método `onCreate()` llamamos al método de creación de la base de datos:

```java
public class GameApplication extends Application {

public static final String CHANNEL_ID = "1" ;
    @Override
    public void onCreate() {
        super.onCreate();
        GameDatabase.onCreateDatabase(this);
    }
}
```


Eso sí, añadirse atributo `android:name` al nodo `<application>` para indicar que la clase que hereda de `Application` corresponde con el objeto que automáticamente se crea cuando se ejecuta la aplicación. 

```xml
<application
<strong>android:name=".iu.GameApplication"</strong>
................
```
### 4.5. Clase Repository: Acceder a Room desde la app

El acceso a la base de datos desde la aplicación se hace con el patrón **Repository**: Añade una capa en la aplicación con la misión de mover información entre objetos de la aplicación (POJO) y el sistema de almacenamiento (SQLite, sistema de archivos, servidor remoto...)

(Patrón: Solución que resuelve problemas comunes en el desarrollo de software y que después de comprobar su efectividad se convierte en solución estándar)

La clase es la responsable de interactuar con la base de datos de `Room` en nombre de la vista y debe proporcionar métodos que utilicen el DAO para insertar, eliminar, consultar registros del ranking. Estas operaciones de BBDD deben realizarse en subprocesos separados del subproceso principal usando la clase `AsyncTask`

```java
    private RankingRepository() {
        rankingDao = GameDatabase.getDatabase().getRankingDao();
    }
    public static RankingRepository getInstance() {
        if (instance == null)
            instance = new RankingRepository();
        return instance;
}
```

Cualquier componente (actividades, fragmentos) puede llamar a cualquier método de la clase repositorio (y son asíncronos). El repositorio avisa a la actividad de que ya se tienen los datos o que ya se ha realizado la acción.

Se declara una interfaz de forma que toda clase que quiera respuesta del  repositorio debe implementar la interfaz 

```java
public interface RankingRepositoryCallback {
        void onSuccess(List<Ranking> list);
        void onSuccess();
    }
}
```

Ejemplo, al eliminar un ranking el método recibe por parámetro la clase que implementa `RankingRepositoryCallback` y cuando se elimina el ranking se llama al método `onSuccess()` que ejecutará las acciones pertinentes. 

```java
 public void delete(final Ranking ranking, final RankingRepositoryCallback callback) {
         if (ranking != null) {
             new AsyncTask<Void, Void, Void>() {
                 @Override
                 protected Void doInBackground(Void... voids) {
                     rankingDao.delete(ranking);
                     callback.onSuccess();
                     return null;
                 }
             }.execute();
         }
     } 
```
## 5. Proveedores de contenidos

Los datos pueden almacenarse en un dispositivo móvil (ficheros, base de datos). 
¿Cómo hacer que estos datos sean accesibles desde otras aplicaciones? Mediante los **proveedores de contenidos** (**Content Provider**) que se encargan de compartir los datos entre varias aplicaciones, accediendo mediante uso de URI (cadena de caracteres que identifica de forma única a un recurso)

La URI está compuesta del prefijo (`http://` internet, `smsto:` envío de mensajes, `mailto:` envío de correo, `content://` acceder a proveedores de contenido)

Sobre los datos de proveedores de contenido puede hacerse cualquier operación de inserción, actualización, borrado, consulta. 

Debe solicitarse el permiso en el fichero de manifiesto para operaciones de lectura y de escritura. Por ejemplo, para acceder al proveedor de contenido Browser para la tabla del historial de navegación: 

```xml
<uses-permission android:name=”com.android.browser.permission.READ_HISTORY_BOOKMARKS”/>
<uses-permission android:name=”com.android.browser.permission.WRITE_HISTORY_BOOKMARKS”/>
```

Proveedores de contenido: Registro de llamadas, lista de contactos, páginas visitadas...
Además, veamos cómo crear un proveedor de contenidos para una aplicación propia. 

**Proveedores de contenido de Android:** https://developer.android.com/reference/android/provider/package-summary

### 5.1. Uso de proveedores de contenidos

Cada URI indica el recurso al que se desea acceder: Debe indicarse el prefijo (`content://`), el proveedor o aplicación a la que se desea acceder y la tabla a la que se hace referencia.

Ej.: Tabla de lista de favoritos del navegador ( `content://browser/bookmarks` o la constante preestablecida `Browser.BOOKMARKS_URI` que da Android)

**Ejemplo** Recuperar la lista de favoritos

- Se solicitan permisos adecuados en el manifiesto (solo el de lectura)
- Se crea instancia de la URI para acceder al recurso Browser y la tabla correspondiente usando la constante `BOOKMARKS_URI`
- Se crea referencia a `ContentResolver` mediante `getContentResolver()` para hacer operaciones sobre el proveedor de contenidos.
- Se accede a BookmarkColumns, con columnas que deben indicarse en la consulta. Debe crearse un array indicando las dos columnas que se quieren obtener. (Consultar columnas y tablas de cada proveedor en documentación oficial de Android)
- Después, recorrer el cursor para recoger los valores de las dos columnas (en este caso podemos indicar el índice que ocupa cada columna en la tabla, accediendo al campo de cada registro y recuperando su valor. 

```java
Uri miUri =  Browser.BOOKMARKS_URI;
 
ContentResolver contRes = getContentResolver();
 
String[] columnas = new String[] {
              Browser.BookmarkColumns.URL,
              Browser.BookmarkColumns.VISITS };
 
Cursor cur = contRes.query(miUri,
                    columnas,      
                    null,       
                    null,       
                    null);  

int columnaURL = cur.getColumnIndex(Browser.BookmarkColumns.URL);
int columnaVisits = cur.getColumnIndex(Browser.BookmarkColumns.VISITS);

cur.getString(columnaURL);
cur.getString(columnaVisits);
```


**Otro ejemplo: Recuperar contactos en agenda**

**PERMISO MANIFIESTO**

```xml
<uses-permission android:name="android.permission.READ_CONTACTS"/>
```

**LAYOUT**

```xml
<ScrollView 
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/contactos"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

</ScrollView>
```

**ACTIVITY**
```java
public class MainActivity extends Activity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
        TextView texto = (TextView) findViewById(R.id.contactos);
        
        Cursor c = managedQuery(ContactsContract.Contacts.CONTENT_URI, 
        new String[] {ContactsContract.Contacts.DISPLAY_NAME}, 
        ContactsContract.Contacts.IN_VISIBLE_GROUP, 
        null,
        ContactsContract.Contacts.DISPLAY_NAME);

        while (c.moveToNext()) {
            String contactos = c.getString(c
                .getColumnIndex(ContactsContract.Data.DISPLAY_NAME));
            texto.append(contactos);
            texto.append("\n");
        }
    }
}
```

### 5.2. Creando un proveedor de contenidos

- Identificar el tipo de información que se va a compartir y dónde está almacenada (fichero, base de datos)
- Crear clase que extienda de `ContentProvider` e implementar métodos abstractos con los que otras aplicaciones puedan acceder a los datos

> **onCreate**: llamado al iniciar el Content Provider
> **getType:** devuelve el tipo MIME de los datos del Content Provider (MIME se podría definir como una serie de convenciones o especificaciones dirigidas al intercambio de todo tipo de archivos (texto, audio, vídeo, ...) a través de Internet de una forma transparente para el usuario) 
> **insert**: inserta nuevos datos en el Content Provider
> **update**: actualiza datos existentes en el Content Provider
> **delete**: borra datos del Content Provider
> **query**: devuelve los datos a la persona que los consulte


- Registrar el `ContentProvider` en el fichero de manifiesto. 

---

**a. Identificar la URI**
Estructura de la URI: `<prefijo>://<autoridad>/<datos>/<id>`

Como prefijo en este caso se usa "content" ya que estamos tratando con un Content Provider. En la autoridad especificaremos el identificador del Content Provider similar al nombre de un paquete de una aplicación, en este caso usaremos "mi.content.provider.contactos". En los datos se indica que datos se quieren compartir, en el ejemplo vamos a compartir una tabla de SQLite llamada "contactos". Y la id es opcional, indicaríamos el registro a compartir. Por lo tanto nuestra URI y la que usaremos en el ejemplo quedará de la siguiente manera:


`content://mi.content.provider.contactos/contactos`

**b. Crear base de datos SQLite**

**c. Clase `ContentProvider`**

```java
public class MyContentProvider extends ContentProvider {
	// Instancia a la base de datos
    private MiBaseDatos MBD;
    // Objecto de las consultas CRUD
    SQLiteDatabase SQLDB;
    // Identificador del ContentProvider
    private static final String NOMBRE_CP = "mi.content.provider.contactos";

    private static final int CONTACTOS = 1;
    private static final int CONTACTOS_ID = 2;
    // Almacenar direcciones URI que se necesiten en el proyecto (metodo addURI que pide como parametro autoridad, ruta de datos e identificador siempre en positivo)
    private static final UriMatcher uriMatcher = new UriMatcher(UriMatcher.NO_MATCH);

    static{
        uriMatcher.addURI(NOMBRE_CP, "contactos", CONTACTOS);
        uriMatcher.addURI(NOMBRE_CP, "contactos/#", CONTACTOS_ID);
    });


	// Iniciar base de datos
  public boolean onCreate() {
        MBD = new MiBaseDatos(getContext());
        return true;
  }

	// Insertar registros
	/*
		La variable "registro" la usaremos para comprobar si se inserto bien el registro, gracias al método insert que nos devuelve la id del registro insertado en caso de que lo haya hecho bien.  
	  
	Encapsulamos todo en un bloque try-catch para tratar la excepción "IllegalArgumentExcepcion" que se produce cuando se llama a un método con un argumento que no es razonable de tratar. Dentro comprobamos el argumento "uri" y si es igual a nuestra uriMatcher "CONTACTOS" ponemos nuestra base de datos en modo escritura e insertamos el registro en nuestra tabla "contactos" usando el argumento values.  
	  
	El método insert devuelve la uri del nuevo registro.*/
	public Uri insert(Uri uri, ContentValues values) {
	    long registro = 0;
	    try {
	        if (uriMatcher.match(uri) == CONTACTOS) {
	            SQLDB = MBD.getWritableDatabase();
	            registro = SQLDB.insert("contactos", null, values);
	        }
	    } catch (IllegalArgumentException e) {
	        Log.e("ERROR", "Argumento no admitido: " + e.toString());
	    }
	  
	    // Comprobar si se inserto bien el registro
	    if (registro > 0) {
	        Log.e("INSERT", "Registro creado correctamente");
	    } else {
	        Log.e("Error", "Al insertar registro: " + registro);
	    }
	  
	    return Uri.parse("contactos/" + registro);
	}


/* Método muy similar al anterior, pero en este caso comprobamos que la uri sea igual a nuestra usriMatcher "CONTACTOS_ID". En caso de que sea así almacenamos el registro a actualizar en la variable "id" y para ello usamos el método "getLastPathSegment()" que nos devuelve el ultimo segmento de la uri decodificado.*/
	public int update(Uri uri, ContentValues values, String selection,
	        String[] selectionArgs) {
	  
	    String id = "";
	    try {
	        if (uriMatcher.match(uri) == CONTACTOS_ID) {
	            id = uri.getLastPathSegment();
	            SQLDB = MBD.getWritableDatabase();
	            SQLDB.update("contactos", values, "_id=" + id, selectionArgs);
	        }
	    } catch (IllegalArgumentException e) {
	        Log.e("ERROR", "Argumento no admitido: " + e.toString());
	    }
	  
	    return Integer.parseInt(id);
	}

	public int delete(Uri uri, String selection, String[] selectionArgs) {
	    int registro = 0;
	    try {
	        if (uriMatcher.match(uri) == CONTACTOS_ID) {
	            String id = "_id=" + uri.getLastPathSegment();
	            SQLDB = MBD.getWritableDatabase();
	            registro = SQLDB.delete("contactos", id, null);
	        }
	    } catch (IllegalArgumentException e) {
	        Log.e("ERROR", "Argumento no admitido: " + e.toString());
	    }
	
	    return registro;
	}

/*En este método vamos a usar nuestras dos uriMatcher, una para el caso de consultar un registro y la otra para el caso de querer consultar todos los registros.  
  
En este caso ponemos nuestra base de datos en modo lectura y cargamos las consultas en un cursor ya que este método devuelve un cursor.*/
	public Cursor query(Uri uri, String[] projection, String selection,
	        String[] selectionArgs, String sortOrder) {
	    
	    Cursor c = null;
	    try {
	        switch (uriMatcher.match(uri)) {
	        case CONTACTOS_ID:
	            String id = "_id=" + uri.getLastPathSegment();
	            SQLDB = MBD.getReadableDatabase();
	            c = SQLDB.query("contactos", projection, id, selectionArgs, 
	                    null, null, null, sortOrder);
	            break;
	        case CONTACTOS:
	            SQLDB = MBD.getReadableDatabase();
	            c = SQLDB.query("contactos", projection,   null, selectionArgs, 
	                    null, null, null, sortOrder);
	            break;
	        }
	    } catch (IllegalArgumentException e) {
	        Log.e("ERROR", "Argumento no admitido: " + e.toString());
	    }
	
	    return c;
	}
}
```


**d. Registrarlo en el manifiesto**
```xml
 <provider
        android:name=".MiContentProvider"
        android:authorities="mi.content.provider.contactos" >
    </provider>
```


----


**Usar el ContentProvider**

```java
public class MainActivity extends Activity {
 
    private static final Uri URI_CP = Uri.parse(
            "content://mi.content.provider.contactos/contactos");
    
    private Uri uri;
    private Cursor c;
 
    private int id;
    private String nombre;
    private int telefono;
    private String email;
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
        ContentResolver CR = getContentResolver();
        
        // Insertamos 4 registros
        CR.insert(URI_CP, setVALORES(1, "Pedro", 111111111, "pedro@DB.es"));
        CR.insert(URI_CP, setVALORES(2, "Sandra", 222222222, "sandra@DB.es"));
        uri = CR.insert(URI_CP, setVALORES(3, "Mar", 333333333, "mar@DB.es"));
        Log.d("REGISTRO INSERTADO", uri.toString());
        uri = CR.insert(URI_CP, setVALORES(4, "Dani", 444444444, "dani@DB.es"));
        Log.d("REGISTRO INSERTADO", uri.toString());
        
        
        // Recuperamos todos los registros de la tabla
        String[] valores_recuperar = {"_id", "nombre", "telefono", "email"};
        c = CR.query(URI_CP, valores_recuperar, null, null, null);
        c.moveToFirst();
        do {
            id = c.getInt(0);
            nombre = c.getString(1);
            telefono = c.getInt(2);
            email = c.getString(3);
            Log.d("QUERY", "" +id+ ", " +nombre+ ", " +telefono+ ", " +email);
        } while (c.moveToNext());
        
        
        // Actualizamos un registro de la tabla
        uri = Uri.parse("content://mi.content.provider.contactos/contactos/3");
        CR.update(uri, setVALORES(3, "PPPPP", 121212121, "xxxx@xxxx.es"), 
                null, null);
        // Y lo mostramos en el log
        c = CR.query(uri, valores_recuperar, null, null, null);
        c.moveToFirst();
        id = c.getInt(0);
        nombre = c.getString(1);
        telefono = c.getInt(2);
        email = c.getString(3);
        Log.d("QUERY", "" +id+ ", " +nombre+ ", " +telefono+ ", " +email);

        
        // Borramos un registro
        uri = Uri.parse("content://mi.content.provider.contactos/contactos/4");
        CR.delete(uri, null, null);
        
    }

    private ContentValues setVALORES(int id, String nom, int tlf, String email) {
        ContentValues valores = new ContentValues();
        valores.put("_id", id);
        valores.put("nombre", nom);
        valores.put("telefono", tlf);
        valores.put("email", email);
        return valores;
    }
}
```

>Las variables que estamos usando son "URI_CP" que sera la dirección donde esta ubicado el content provider, "uri" la usaremos para manejar las consultar a través de su id, "c" el cursor donde almacenaremos los datos y 4 variables donde almacenaremos cada valor de un registro.  
  >
>Ya en el onCreate creamos un objeto "ContentResolver" que sera el encargado de acceder a un content provider y con el método "getContentResolver" conseguimos la instancia de un Content Resolver.  
  >
>Para insertar registros usamos el método "insert(url, values)" que nos pide como parámetro la dirección del content resolver "url" y un ContentValues los valores a insertar"values". Para insertar los valores hemos creado un método auxiliar "setVALORES(id, nom, tlf, email)" que nos facilitara las cosas ya que poniendo como parámetro los datos a insertar, este nos devuelve un ContentValues con los datos del registro. El método "insert" nos devuelve la id del registro a insertar, he puesto dos ejemplos para que veamos su uso en el log.  
  >
Para consultar todos los registros hacemos uso del método "query(url, projection, selection, selectionArgs, sortOrder)" pasándole la dirección uri del Content Provider. En el articulo base de datos se explica mas detalladamente esta función de consulta.  
  >
Actualizamos un registro con el metodo "update(url, values, where, selectionArgs)" pasándole una uri personalizada con el registro a actualizar, en este caso el numero 3.  
  >
Y para concluir el articulo borramos un registro con el método "delete(url, where, selectionArgs)" pasandole una uri con la id del registro que vamos a borrar.

