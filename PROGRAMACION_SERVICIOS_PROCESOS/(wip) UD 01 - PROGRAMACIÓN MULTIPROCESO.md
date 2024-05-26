
## 1. Recordatorio de Java

Recordemos que existe:
- El **lenguaje de programación Java**: Lenguaje de alto nivel, orientado a objetos. Sus programas son tanto compilados como interpretados. La compilación traduce el código Java a un lenguaje intermedio (Java bytecode). Este es analizado y ejecutado (interpretado) por la JXM, traductor entre el bytecode, el sistema operativo subyacente y el hardware. 
- La **plataforma Java**: Plataforma software ejecutada sobre varias plataformas de hardware. Formada por JVM  + API Java. La API Java abarca objetos básicos, conexión en red, seguridad, manipulación de XML y servicios web. Está agrupada en bibliotecas (paquetes) de clases e interfaces. Versiones: 
	- Java SE (Standard Edition). Aplicaciones Java en desktops, servidores, empotrados, tiempo real
	- Java EE (Enterprise Edition). Aplicaciones Java para servidor portables, robustas, escalables, seguras
	- Java ME (Micro Edition). Dispositivos móviles y empotrados

Será necesario un IDE para desarrollar las aplicaciones. Y en este cortijo, se usa Netbeans como IDE.
## 2. Introducción: Aplicaciones, Ejecutables y Procesos

-**Aplicación**. Programa informático. Diseñado como herramienta para resolver un problema específico del usuario. No confundir con los sistemas operativos o las herramientas para el desarrollo de software. Al instalarla en el equipo se puede observar que está formada por varios ejecutables y bibliotecas. Siempre que se lance la ejecución de una aplicación, se creará al menos un proceso nuevo en el sistema.

Un programa es el conjunto de instrucciones que ejecutadas en un ordenador realizarán una tarea o ayudarán al usuario a realizarla. El desarrollador crea un programa escribiendo su código fuente y con la ayuda de un compilador obtiene su código binario o interpretado. El código binario o interpretado se guarda en un archivo que es un ejecutable o binario.

-**Ejecutable**. Archivo que contiene código binario o interpretado que será ejecutado en un ordenador.

-**Proceso**. Es un programa en ejecución. En un sistema operativo supone una unidad de trabajo completa, siendo el Sistema Operativo el que gestiona los procesos que se encuentren en ejecución en el equipo. El proceso existe mientras que se ejecuta la aplicación (esta puede suponer el inicio de varios procesos.

¡IMPORTANTE! El ejecutable es un fichero. El proceso es una entidad activa: el contenido del ejecutable ejecutándose. 

### 2.1. Ejecutables. Tipos

Según el tipo de código que contenga un ejecutable se puede clasificar en:
- **Binario**: Formado por un conjunto de instrucciones ejecutadas por el procesador del ordenador. Se obtiene al compilar el código fuente de un programa y enlazar el código objeto. Solo se ejecutará en la plataforma compatible con aquella para la que ha sido compilado.

- **Interpretados**: Se trata como ejecutable pero no es código binario sino otro tipo (bytecode). Formado por códigos de operación que tomará el intérprete (en el caso de Java el intérprete es la máquina virtual o JRE). El intérprete los traduce al lenguaje máquina que ejecutará el procesador. El código interpretado es más susceptible de ser multiplataforma o independiente de la máquina física. 

- **Scripts**: Contiene instrucciones que serán ejecutadas una detrás de otra por el intérprete. Estos no son compilados. Pueden abrirse y ver el código que contienen con un editor de texto plano. Los intérpretes de estos lenguajes se conocen con el nombre de **motores**. Ej.: Javascript, PHP, JSP, ASP, Python, .BAT en MS-DOS, Powershell, Bash scripts...

- **Bibliotecas (librerías)**: Funciones que permiten dar modularidad y reusabilidad a los programas. Su contenido es código ejecutable, aunque ese código es ejecutado por todos los programas que invocan las funciones que contienen. 
  Las funciones de una librería suelen ser reutilizables y útiles, evitando la reescritura de código. Es el caso de las bibliotecas estándar de C, los paquetes compilados DLL en Windows, las APIs y la J2EE de Java, las bibliotecas de .NET...

El fichero ejecutable en Windows se identificaría como `.exe` (o .bat, .com, .dll para librerías dinámicas... ocultando las extensiones de los archivos conocidos por el usuario) y en Linux como aquel fichero con permiso de ejecución activo.

#### Cómo se ven los ficheros
Los **ficheros ejecutables** pueden verse con editores hexadecimales. Así se ve el contenido en formato binario de cada uno de los bytes de un fichero, un intento de su traducción a ASCII y su desplazamiento a partir del primer byte del fichero. 
Editores: HxD en Windows, Bless Hex Editor en Ubuntu.

![[Pasted image 20240525184538.png]]
Puede incluir literales (3) de las cadenas de textos incluidas en el ejecutable.

El **fichero interpretado** (por ejemplo un .jar). Podría verse la codificación en binario de las instrucciones ejecutables interpretadas, compatibles y compiladas para la máquina virtual de Java. 
Pueden verse literales. Existe un número mágico (con el que comienzan todas las instrucciones bytecode en Java) que es "CAFEBABE".  (Buscar CAFEBABE con tipos de valores hexadecimales, habrá uno por instrucción)

La **librería** (por  ejemplo los DDL) son instrucciones ejecutables en código máquina como en un fichero binario. 

Observa que ficheros binarios y librerías tienen sus primeros bytes exactamente iguales...

En el **script** se ven las instrucciones en lenguaje de alto nivel que serán ejecutadas una tras otra.  

## 3. Gestión de procesos

Actualmente los Sistemas Operativos son **multitarea** permitiendo que varios procesos puedan ejecutarse al mismo tiempo haciendo que todos compartan el núcleo o núcleos del procesador. 
Lo comparten mediante la gestión de procesos que decide qué proceso ocupa el procesador en un momento dado, alternándolos.

**Tipos de procesos del sistema**:
- **Por lotes**: Tareas de las que el usuario solo está interesado en el resultado final. El usuario introduce las tareas y los datos iniciales, deja que se realice todo el proceso y recoge los resultados.

- **Interactivos**: El proceso interactúa continuamente con el usuario y actúa de acuerdo a las acciones que este realiza o a los datos que suministra. 

- **Tiempo real:** Tiempo de respuesta es crítico. Debe reaccionar ante eventos en un tiempo máximo que sea correcto y aceptable. 

### 3.1. Gestión de procesos. Introducción

El microprocesador puede ejecutar miles de millones de instrucciones básicas en un segundo (Ej.: i7 3,4 GHz). El usuario aprecia que solo ejecuta la aplicación que él utiliza, pero realmente el microprocesador ejecuta instrucciones y da sus resultados sin saber si corresponden a uno u otro proceso.

El Sistema Operativo decide qué proceso puede entrar ejecutarse o si debe esperar. 

Los nuevos microcontroladores, con varios núcleos, pueden casi totalmente, dedicar una CPU (Central Processing Unit) a la ejecución de uno de los procesos activos en el sistema. (Esta información no interesa demasiado pero bueno)

### 3.2. Estados de un proceso

Puede haber diferentes estados en el **ciclo de vida de un proceso**
1. **Nuevo**: Proceso nuevo, creado
2. **Listo o preparado**: Proceso esperando la CPU para ejecutar sus instrucciones
3. **En ejecución**: Proceso que actualmente está ejecutándose en la CPU
4. **Bloqueado**: Esperando la respuesta de algún proceso para continuar su ejecución (ej. operación de entrada salida)
5. **Suspendido**: Proceso que ha sido llevado a la memoria virtual para liberarla RAM
6. **Terminado**: Proceso que ha terminado, no necesita más de la CPU

El sistema operativo gestiona los cambios en el estado de los procesos.
Estos pueden comunicarse entre sí o ser independientes. Si se comunican, necesitan sincronizarse  y establecer mecanismos de comunicación.

---

1. Procesos nuevos entran en la cola de procesos activos en el sistema
2. Procesos van avanzando posiciones en cola de procesos activos hasta que les toca el turno para que el SO les de uso de CPU
3. SO da uso de CPU a cada proceso durante un tiempo determinado y equitativo (quantum), cuando se consume el quantum es pausado y enviado al final de la cola
4. Si elproceso finaliza sale del gestor de procesos. 

----
Todo **proceso en ejecución tiene que estar cargado** en la **RAM** fisica del equipo o memoria principal así como todos los **datos** que necesite


### 3.3. El cargador  y el planificador

#### Cargador
Es el encargado de crear los los procesos. Cuando se inicia un proceso el cargador realiza las siguientes tareas.
1. Carga el proceso en memoria principal. Reserva espacio en RAM para el proceso. En el espacio copia las instrucciones del fichero ejecutable, las constantes y deja espacio para los datos (variables) y la pila (llamadas a funciones). Un proceso durante su ejecución no puede hacer referencia a direcciones fuera de su espacio de memoria. Si lo intenta el SO lo detecta y genera una excepción (ejemplo: pantallazo azul de Windows)
2. Crea estructura de información (PCB, Bloque de control de proceso). Esta contiene
	 **identificador** del proceso PID
	**estado actual**
	espacio de **direcciones de memoria**
	información de **planificación** (prioridad, quantum, estadísticas)
	**información para el cambio de contexto**: valor de los registros de la CPU, contador de programa, puntero a pila. Información para cambiar de la ejecución de un proceso a otro
	 **recursos usados**: archivos abiertos, conexiones, etc. 

#### Planificador

**Planificador del procesador**: Decide cuánto tiempo de ejecución se le asigna a cada proceso del sistema y en cada momento.
La transición de estados es transparente para el proceso todo lo realiza el sistema operativo. Desde el punto de vista del proceso él siempre se ejecuta en la CPU sin esperas.

(Ojo: Un sistema monousuario y monotarea no tendría que decidir nada)

La **estrategia de planificación** debe buscar que los procesos obtengan turnos de ejecución de forma apropiada, junto con buen rendimiento y minimización de sobrecarga.

Se buscan como objetivos:
- **Equidad**: Todos los procesos obtienen su turno de ejecución hasta terminación con éxito
- **Rendimiento**: Finalizar el mayor número de procesos por unidad/tiempo.
- **Tiempo de respuesta**: No deben ser demasiado largos
- **Tiempo de retorno**: No aplazar indefinidamente. El usuario no debe percibir el programa como "colgado"
- **Eficacia**: Procesador ocupado el 100% del tiempo.

Los sistemas informáticos tendrán carga diferente según las características de los procesos. Puede haber:
- Procesos que hacen uso intensivo de la CPU
- Procesos con gran cantidad de operaciones de Entrada/Salida
- Procesos por lotes, interactivos, en tiempo real
- Procesos de menor o mayor duración

Según como sean la mayoría de los procesos habrá que decidir unos u otro algoritmos que darán mejor o peor rendimiento.

##### Planificación apropiativa y no apropiativa

**Planificación no apropiativa**: Cuando al proceso le toca su turno, no puede ser suspendido hasta que no termina. Problema: Ciclos infinitos podrían aplazar indefinidamente a otros programas. Procesos largos penalizan a procesos cortos si entran primero.

**Planificación apropiativa**: El sistema puede suspender el proceso (arrebatarle el uso de la CPU). Hay un reloj que lanza interrupciones periódicas en las cuales el planificador toma el control y decide si el proceso sigue ejecutándose o se le da su turno a otro. 

-----

Algunos algoritmos para decidir el orden de ejecución de procesos son: 
- Algoritmo de **Round Robin**: Apropiativo. Algoritmo rotativo. Se le da a cada proceso un pequeño periodo de tiempo (quantum) y si no termina, pasa a cola. 
![](ud02-5.png)

- Algoritmo por **prioridades fijas**: Apropiativo. Los procesos tienen asignada una prioridad (por ejemplo prioridad número más altos, alta prioridad). En el momento en el que llega un proceso de alta prioridad y se está ejecutando uno de baja, queda suspendido y se atiende el siguiente.
![](ud02-6.png)

- Algoritmo **tiempo restante más corto** (SRTF, Shortest Remaining Time First): Apropiativo. Le da prioridad al que le quede menos. Este algoritmo en la vida real no podría ser implementado a la perfección porque no es posible estimar el tiempo restante de CPU muchas veces... Prioriza los procesos cortos. Pero un proceso largo podría quedarse indefinidamente en espera por culpa de una llegada de muchos de ellos. 

![](ud02-9.png)

- Algoritmo el **trabajo más corto primero** (SJF, Shortest Job First): No apropiativo. No es interrumpido por otros. Penaliza a procesos cortos que llegan después y deben esperar a los largos. 

![](ud02-7.png)

- Algoritmo **primero en llegar, primero en ejecutarse** (FCFS, FIFO, First Come First Served): No apropiativo. Se ejecutan en orden de llegada. Su tiempo de respuesta puede ser alto, especialmente si varían mucho los tiempos de ejecución. La sobrecarga del sistema es mínima. Penaliza los procesos cortos y los procesos con operaciones de Entrada/Salida
![](ud02-8.png)

Información adicional: Comunicación y sincronización de procesos https://www.cartagena99.com/recursos/alumnos/apuntes/Tema3.L1-Introduccion-y-Conceptos.pdf


---
- **múltiples colas.** Es una combinación de Round Robin y de por prioridad y el implementado en los sistemas operativos actuales. Todos los procesos de una misma prioridad, estarán en la misma cola. Cada cola será gestionada con el algoritmo Round-Robin. Los procesos de colas de inferior prioridad no pueden ejecutarse hasta que no se hayan vaciado las colas de procesos de mayor prioridad.

### 3.4. Cambio de contexto en la CPU

Un proceso es una **unidad de trabajo completa**. El sistema operativo se encarga de gestionar los procesos de forma eficiente evitando que haya conflictos en el uso que hacen de los recursos del sistema. 

Como se ha comentado, a cada proceso se asigna un conjunto de información (PCB) y unos mecanismos de protección (espacio de direcciones de memoria al que debe limitarse y prioridad de ejecución). 

El planificador al realizar cambio de una aplicación a otra debe guardar el estado en el que se encuentra el microprocesador y cargar el estado en el que estaba este cuando cortó la ejecución e otro proceso para continuar con este.

**Estado de la CPU**: La CPU además de los circuito que realizan las operaciones tiene pequeños espacios de memoria llamados registros en los que se almacena temporalmente la información que en cada instante necesita la instrucción que esté procesando la CPU. El conjunto de registros de la CPU es su estado. 

Entre los registros destaca el **Registro Contador de Programa** y el **puntero a pila**.

- El **contador de programa** almacena la dirección de la siguiente instrucción a ejecutar en cada instante. (Cada instrucción y sus datos son llevados de la memoria principal a un registro de la CPU para que sea procesada. El resultado de la ejecución, según el caso, se vuelve a llevar a memoria. A la dirección que ocupe la variable). El contador de programa apunta la dirección a la siguiente dirección que debe traerse de la memoria, **permitiendo continuar en cada proceso por la instrucción en donde se dejó todo**
- El **puntero a pila** apunta en cada instante a la parte superior de la pila del proceso de en ejecución. Allí es donde será almacenado el contexto de la CPU y de donde se recuperará cunado el proceso vuelva a ejecutarse. 

### 3.5. Servicios. Hilos

Un proceso está formado por, al menos, un hilo de ejecución.

Los **hilos** comparten información de la aplicación. 
Los cambios de contexto entre hilos son más rápidos y menos costoso que cambio de contexto entre proceso. Solo hay que cambiar el valor del registro contador de programa de la CPU y no todos los valores de los registros de la CPU. 

Un **servicio** es un proceso que suele ser cargado en el arranque del sistema y que queda a la espera de que otro le solicite que realice una tarea.

### 3.6. Creación de procesos en Java

Java no está diseñado para crear y gestionar procesos en sí mismo; para ello, normalmente se recurre a mecanismos proporcionados por el sistema operativo o a bibliotecas externas. Java proporciona clases para ejecutar procesos del sistema operativo, pero estos procesos son externos al entorno de ejecución de Java. 

Se disponen de las clases `Process` y `Runtime` del paquete `java.lang`
- **Runtime**: Lanzar ejecución de un programa en el sistema. Interesantes el método `exec(commando)` que devuelve un objeto `Process` que representa al proceso en ejecución que realiza el comando. 
- **Process**: Controlar los procesos creados desde el código

Posibles excepciones: 
- `SecurityException` No tiene permitido crear subprocesos en la política de seguridad
- `IOException` Error de E/S
- `NullPointerException` o `IllegalArgumentException`



**Con `Runtime`**

```java
Process miProceso;
Process miOtroProceso;
try {
// Una prueba
	miProceso = Runtime.getRuntime().exec("notepad.exe");

// Otra prueba
	miProceso = Runtime.getRuntime().exec("cmd /c dir");
      // Capturar la salida del comando
            BufferedReader reader = new BufferedReader(new InputStreamReader(miProceso.getInputStream()));
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
    // Esperar a que el proceso termine 
    int exitCode = miProceso.waitFor();
    System.out.println("El proceso terminó con el código: " + exitCode);

} catch (Exception e) {
	e.printStackTrace();
}
```

**Con `ProcessBuilder`**

```java
    public static void main(String[] args) {
        ProcessBuilder processBuilder = new ProcessBuilder();
        // Configura el comando que quieres ejecutar
        processBuilder.command("cmd.exe", "/c", "dir");

        try {
            // Inicia el proceso
            Process process = processBuilder.start();

            // Captura la salida estándar del proceso
            BufferedReader reader = new BufferedReader(new InputStreamReader(process.getInputStream()));
            String line;
            System.out.println("Salida del comando:");
            while ((line = reader.readLine()) != null) {
                System.out.println(line); // Imprimir cada línea de la salida del comando
            }

            // Captura la salida de error del proceso (si la hay)
            BufferedReader errorReader = new BufferedReader(new InputStreamReader(process.getErrorStream()));
            System.out.println("Salida de error (si la hay):");
            while ((line = errorReader.readLine()) != null) {
                System.err.println(line); // Imprimir cada línea de la salida de error
            }

            // Esperar a que el proceso termine y obtener el código de salida
            int exitCode = process.waitFor();
            System.out.println("El proceso terminó con el código: " + exitCode);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```


**¿Por qué es mejor `ProcessBuilder`?**

**`Runtime`** es adecuado para ejecutar comandos simples y rápidos con una configuración mínima. **`ProcessBuilder`** es preferido cuando necesitas mayor control y flexibilidad sobre el proceso, como configurar el directorio de trabajo, variables de entorno, y redirección de flujos.

- Permite configurar de manera más detallada los procesos. Puedes establecer el directorio de trabajo, variables de entorno, redirección de entradas y salidas, etc.  Ejemplo: `processBuilder.directory(new File("path/to/directory"));`
- Proporciona métodos integrados para redirigir los flujos de entrada, salida y error. Ejemplo: `processBuilder.redirectOutput(new File("output.txt"));`

```java
ProcessBuilder processBuilder = new ProcessBuilder();
processBuilder.command("cmd.exe", "/c", "dir");
processBuilder.directory(new File("path/to/directory"));
processBuilder.environment().put("MY_VAR", "myValue");
processBuilder.start();
processBuilder.redirectOutput(new File("output.txt"));
```

-----------------------------------------

### 3.7. Creación de procesos en C

Como ya se ha comentado, el sistema operativo administra todos los procesos y reserva regiones de memoria para cada uno de ellos. (Su propio stack, su propio heap, su propio puntero de instrucciones).

Para ejecutar otro programa dentro del nuestro o ejecutar una parte de nuestro programa simultáneamente, puede ser útil crear **procesos hijos**.

Los procesos se identifican por su PID (process indentifer). Los que están corriendo pueden verse con `ps -e`, por ejemplo. 
Cada proceso tiene a su vez un proceso padre que lo creó  (el PID de ese proceso padre le podríamos llamar PPID).

Al inicio, el sistema de Unix tiene un proceso llamado `init` con PID 1. Es el antepasado de todos los demás procesos ejecutados. 

#### Fork 

Con `fork`  (librería `unistd.h`) nuestro proceso crea un clon exacto de él en otro proceso y es ejecutado simultáneamente. Aunque son iguales en instrucciones, cada uno de esos proceso tiene su propia memoria reservada en la RAM.

Mediante la respuesta de `fork` se puede distinguir si el proceso es padre o hijo puesto que:
 - Al padre le da el PID del hijo
 - Al hijo le da 0
 - En caso de error, da -1. 

Si es 0, es un proceso hijo. Si es un PID es el padre. Si es -1, error.

##### La shell usa fork...

Cuando introducimos un comando en la shell, como `ls` esta crea un proceso hijo que ejecuta el programa `/bin/ls`.
No puede ejecutarlo la shell porque si no, el proceso `shell` sería subreescrito por el programa ls y no podría volver a ejecutarse la shell. 

#### La importancia de esperar al proceso hijo 

Ejecuto un programa que hace fork. 
La shell (abuelo), espera al proceso padre (hijo) pero no al proceso hijo (nieto). (vuelve a sacar el prompt).

##### Proceso huérfano
Cuando el padre finaliza sin esperar a su hijo, este es un proceso huérfano que es adoptado por `init` y eliminado por el sistema. 

#### Proceso zombie
El proceso zombie finaliza su tarea pero queda en el sistema esperando a que su padre para reconocerlo. El sistema ya ha liberado sus recursos pero mantiene su bloque de control del proceso, incluyendo su PID. (Si por ej. creamos un bucle infinito en el proceso padre, puede observarse esa situación)

El proceso zombie no es problema siempre que el padre lo recupere. Ni consume energía, ni ocupa espacio de memoria. Son eliminados por `init` cuando lleguen a ser procesos huérfanos. Pero si el proceso padre nunca termina y crea hijos regularmente sin esperarlos la tabla de procesos del sistema puede saturarse, bloqueando el sistema al no poder ejecutar nuevos procesos. 

#### Comandos `wait` y `waitpid`

Pertenecen a librería `<sys/wait.h>`

`pid_t wait(int *status);`
`pid_t waitpid(pid_t pid, int *status, int options);
`
`wait`: Recupera al primer proceso hijo terminado. 
`waitpid`:  Espera para que acabe el proceso con el pid indicado.

- `pid` del proceso hijo para el que esperamos . Si ponemos -1, esperamos para el primero que termina. 
- `status` int* en el que puede almacenarse el código de respuesta del proceso hijo
* `options` Varios opciones WNOHANG por ejemplo retorna inmediatamente si el proceso hijo no terminó todavía. Sin esta opción, proceso padre queda a la espera de que el hijo ejecute su tarea.   (Si terminó retorna el pid. Si no, termina -1)

#### Para analizar el código de salida de un proceso hijo

Usar las macros 

* `WIDFEXITED` Da true si el hijo terminó normalmente (exit o finalizar la función main).   Si esto está true puede usarse `WEXITSTATUS` para retornar el código de salida. 
* `WIFSIGNALED`Da true si el hijo fue forzado a terminar por una señal.  Si esto está true puede usarse `WTERMSIG`para saber el número de señal que lo provocó. 

```C
#include <unistd.h>
#include <sys/wait.h>
#include <stdlib.h>
#include <stdio.h>

// Define a macro for a specific child exit code (if we do not
// specify this exit code during compilation with the 
// -D CHILD_EXIT_CODE=[number] option), by default, it will be 42:
#ifndef CHILD_EXIT_CODE
# define CHILD_EXIT_CODE 42
#endif

// Define a macro for the expected exit status
#define EXPECTED_CODE 42

// Child process routine:
void	child_routine(pid_t pid)
{
	printf("\e[36mChild: Hi! I'm the child. PID received from fork = %d\e[0m\n",
			pid);
	printf("\e[36mChild: Exiting with exit code %d.\e[0m\n",
			CHILD_EXIT_CODE);
	exit(CHILD_EXIT_CODE);
}

// Parent process routine:
void	parent_routine(pid_t pid)
{
	int	status;

	printf("Parent: I'm the parent. PID received from fork = %d\n", pid);
	printf("Parent: Waiting for my child with PID [%d].\n", pid);
	waitpid(pid, &status, 0); // Wait for child
	printf("Parent: My child exited with status %d\n", status);
	if (WIFEXITED(status)) // If child exited normally
	{
		printf("Parent: My child's exit code is %d\n",
				WEXITSTATUS(status));
		if (WEXITSTATUS(status) == EXPECTED_CODE)
			printf("Parent: That's the code I expected!\n");
		else
			printf("Parent: I was not expecting that code...\n");
	}
}

int	main(void)
{
	pid_t	pid; // Store fork's return value

	pid = fork(); // Create child process
	if (pid == -1)
		return (EXIT_FAILURE);
	else if (pid == 0) // Child process
		child_routine(pid);
	else if (pid > 0) // Parent process
		parent_routine(pid);
	return (EXIT_SUCCESS);
}
```

#### Comando Kill

De la librería `signal.h` 
Se usa `kill` para enviar una señal al proceso hijo que lo fuerza a terminar. Se envía el pid y la señal. 

Con Valgrind puede mutearse los errores del proceso hijo con `--child-silent-after-fork=yes` 


### 3.7. Comandos para la gestión de procesos en el terminal

Como es obvio son necesarias órdenes para lanzar procesos al sistema. Es la forma de comunicarnos con el sistema operativo y de poder usar los resultados de esas órdenes. La administración de sistemas es efectiva en líneas de comandos ¡no en interfaz gráfica!

**Windows**
- tasklist: Lista de procesos presentes en el sistema. Muestra nombre ejecutable, pid y porcentaje de uso..
- taskkill: Mata proceso. Con opción /pid especificamos el pid del proceso que queremos matar.

**GNU/Linux**
- ps: Procesos presentes en el sistema
- pstree: Procesos en forma de árbol, mostrando qué procesos han creado otros. Con opción "AGu" construye el árbol con líneas guía y muestra nombre del usuario propietario del proceos.
- kill: Envía señal a los procesos. `kill -9 PID` mata el proceso (SIGKILL). ¡no solo sirven para matar!
- killall. Mata procesos por su nombre
- nice. Cambia prioridad de un proceso `nice -n 5 <comando>` lo ejecuta con prioridad 5. Por defecto la prioridad es 0. Estas están entre -20 (más alta) y 19 (más baja).

### 3.8. Herramientas gráficas para gestión de procesos

**Windows**: Administrador de tareas. SysInternals (tilidades avanzadas para sistemas Windows publicadas como freeware. En particular recomendamos las herramientas gráficas "_**Process Explore**r_" y "_**Process Monitor**_". "_Process Explorer_" nos dará información más completa sobre los procesos activos en el sistema; y "_Process Monitor_" nos informará de la actividad (de E/S) de los procesos e hilos activos en el sistema: archivos a los que están accediendo, actividad en red, creación de hilos, etc.)

**GNU/Linux**: Monitor del sistema

Muestran:
- Listado de los procesos que se encuentran activos (PID, usuario, ubicación de ejecutable)
- Posibilidad de terminar o finalizar proceso
- Información sobre uso de CPU, memoria principal y virtual, red..
- Posibilidad de cambiar la prioridad de ejecución de los proceoss

## 4. Programación concurrente



### 4.1. Sentido de la concurrencia



### 4.2. Condiciones de competencia





## 5. Comunicaciones entre procesos



### 5.1. Mecanismos básicos de comunicación



### 5.2. Tipos de comunicación


## 6. Sincronización entre procesos



### 6.1. Regiones críticas

#### 6.1.1 Categoría de proceso cliente-suministrador

### 6.2. Semáforos

### 6.3. Monitores

#### 6.3.1. Monitores: Lecturas y escrituras bloqueantes en recursos compartidos


### 6.4. Memoria compartida


### 6.5. Cola de mensajes


## 7. Requisitos: seguridad, vivacidad, eficiencia y reusabilidad


### 7.1. Arquitecturas y patrones de diseño


### 7.2. Documentación



### 7.3. Dificultades en la depuración



## 8. Programación paralela y distribuida


### 8.1. Conceptos básicos

### 8.2. Tipos de paralelismo


### 8.3. Modelos de infraestructura para la programación distribuida




