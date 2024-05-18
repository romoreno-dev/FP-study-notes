
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

## 2. Ficheros

### 2.1. Almacenamiento en memoria interna

#### 2.1.1. Almacenamiento en los recursos de la aplicación

## 2.2. Almacenamiento en memoria externa

### 2.2.1. Escribiendo en memoria externa

### 2.2.2. Leyendo de memoria externa


## 3. Base de datos

### 3.1. Estructura de SQLite

### 3.2. Creación de base de datos

### 3.3. Operaciones sobre una base de datos

#### 3.3.1 Inserción, actualización y eliminación de registros

#### 3.3.2. Recuperación o consulta de registros

## 4. Room

### 4.1. Componentes de la librería

### 4.2. Crear entidades

### 4.3. Crear DAO

### 4.4. Crear Base de Datos

### 4.5. Clase Repository: Acceder a Room desde la app

## 5. Proveedores de contenidos

### 5.1. Uso de proveedores de contenidos

### 5.2. Creando un proveedor de contenidos

