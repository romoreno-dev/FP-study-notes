
## Acceso a datos

### Ficheros

Uso de ficheros en la actualidad


## Bases de datos

Introducción
Bases de datos relacionales
Bases de datos orientadas a objetos
Comparativa
Bases de datos objeto-relacionales
Acceso a bases de datos mediante conectores
Mapeo objeto relacional (ORM)
Bases de datos XML

Desarrollo de componentes

## Introducción al Manejo de ficheros. Clases asociadas a las operaciones de gestión de ficheros y directorios

Los **datos persistentes** persisten más allá de la ejecución de la aplicación que los trata. Los ordenadores almacenan sus datos dentro de ficheros en unidades de almacenamiento secundario (discos duros, discos ópticos...).

Se conoce como **flujo de Entrada/Salida** a las operaciones que son un flujo de información del programa con el exterior.

En Java, las operaciones de entrada salida se pueden realizar mediante el paquete estándar `java.io` que incorpora interfaces, clases y excepciones para este fin permitiendo:
- Lectura de entradas desde un flujo de datos
- Escritura de entradas a un flujo de datos
- Operar con ficheros en el sistema de ficheros local
- Gestionar la serialización de objetos

![](ud01-1.png)

### Clase `File`

- Representación abstracta de ficheros y directorios
- Permite examinarlos y manipularlos, independientemente de la plataforma. Examinar el nombre, descomponerlo en su rama de directorios, crear el fichero si no existe...
- Sus instancias representan **nombres de archivo**, no los archivos en sí mismos
- Es posible que no exista archivo a ese nombre, por lo que deberán controlarse las _excepciones_

- Lo recomendable a la hora de indicar las rutas es usar `File.separator`, válido para todas las plataformas.
##### Algunos métodos estáticos 
- `createTempFile(prefix, suffix)`: Crea nuevo fichero con nombre único. En este caso crea una fichero temporal y devuelve un objeto `File` que apunta a él. Permite asegurarnos de tener un nombre de archivo no repetido.
-  `listRoots()`: Lista los nombres de archivo (`File`) de la raíz del sistema de archivos.

##### Algunos métodos de instancia

- `renameTo(File dst)` : **Renombrar** el archivo. Objeto `File` dejará de referirse al renombrado porque el `String` con el nombre del archivo del objecto `File` no cambia.
- `delete()` : Borra el archivo
- `deleteOnExit()`: Borra al finalizar la ejecución de la JVM
- `setLastModified(long time)`: Establecer fecha y hora de modificación 
- `mkdir()`: Crear un directorio
- `mkdirs()`: Crea los directorios superiores
- `list()`, `listFiles()`: Lista directorios. Uno devuelve un `String[]`, el otro un `File[]`
- `exists()`: Saber si un fechero existe o no
- `createNewFile()`: Crea fichero vacío con el nombre del `File` si y solo sí no existe. Devuelve `boolean` true si no existía y fue creado, false si ya existía.  (Excepciones `IOException`, `SecurityException`)
- `isDirectory()`: Para saber si el elemento es un directorio


##### Interfaz `FilenameFilter`

Permite filtrar ficheros por un determinado criterio (fecha, tamaño...).
La clase que la implementa debe implementar su método `boolean accept(File dir, String name)`

Ejemplo:

Dado el directorio:
```java
File directory = new File("ruta/a/tu/directorio"); 
```

Es posible filtrar por determinada extensión:

```java
//------------------JAVA 7 -------------------------
// Filtro para archivos con extensión .txt 
FilenameFilter textFileFilter = new FilenameFilter() { 
	@Override
	public boolean accept(File dir, String name) { 
		return name.endsWith(".txt"); 
	} 
}; 
String[] files = directory.list(textFileFilter);

//------------------JAVA 8 -------------------------

String[] files = directory.list((file, name) -> name.endsWith(".txt"));

```

O por nombre: 

```java
//------------------JAVA 7 -------------------------
// Filtro para archivos con extensión .txt 
FilenameFilter textFileFilter = new FilenameFilter() { 
	@Override
	public boolean accept(File dir, String name) { 
		return name.endsWith(".txt"); 
	} 
}; 
String[] files = directory.list(textFileFilter);

//------------------JAVA 8 -------------------------

String[] files = directory.list((file, name) -> name.endsWith(".txt"));
```

##### Creación de fichero

```java
try {
	File file = new File("C:\Usuarios\romoreno-dev\Documentos\prueba.txt");
	if (file.createNewFile()) {
		System.out.println("Fichero creado");
	} else {
		System.out.println("Fichero no creado (ya existe)");
	}
} catch (Exception e) {
	e.getMessage();
}
```

##### Creación de directorio

```java
try {
	boolean exist new File("ruta/a/tu/directorio").mkdirs();
	if (exist) {
		System.out.println("Directorios creados");
	} else {
		System.out.println("Directorios no creados");
	}
} catch (Exception e) {
	e.getMessage();
}
```


##### Borrado de ficheros

Para borrar un directorio, debe borrarse primero cada uno de directorios y ficheros que contenga. Se pueden ir recorriendo recursivamente para ir borrando todos los ficheros.

```java
    public static boolean deleteDirectory(File directory) {
        if (!directory.exists()) {
            return false; // El directorio no existe
        }

        if (directory.isDirectory()) {
            // Listar todos los archivos y subdirectorios
            File[] files = directory.listFiles();
            if (files != null) {
                // Recorrer y eliminar cada archivo y subdirectorio
                for (File file : files) {
                    if (file.isDirectory()) {
                        // Llamar recursivamente para eliminar subdirectorios
                        deleteDirectory(file);
                    } else {
                        // Eliminar archivo
                        file.delete();
                    }
                }
            }
        }

        // Eliminar el directorio después de que su contenido haya sido eliminado
        return directory.delete();
    }
```

### Flujos

### Flujos basados en bytes

### Flujos basados en caracteres

### Formas de acceso a un fichero

### Operaciones básicas sobre ficheros de acceso secuencial

### Operaciones básicas sobre ficheros de acceso aleatorio

## Ficheros XML. Analizadores sintáticos (parser) y vinculación (binding)

### Conceptos previos y definiciones

### Introducción JAXB

### Funcionamiento JAXB

## Librerías para conversión de XML a otros formatos

### JasperReport



