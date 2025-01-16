
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

![](PROGRAMACION_SERVICIOS_PROCESOS/resources/ud01-1.png)
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
![](SISTEMAS_INFORMATICOS/Andalucía/resources/ud02-5.png)

- Algoritmo por **prioridades fijas**: Apropiativo. Los procesos tienen asignada una prioridad (por ejemplo prioridad número más altos, alta prioridad). En el momento en el que llega un proceso de alta prioridad y se está ejecutando uno de baja, queda suspendido y se atiende el siguiente.
![](SISTEMAS_INFORMATICOS/Andalucía/resources/ud02-6.png)

- Algoritmo **tiempo restante más corto** (SRTF, Shortest Remaining Time First): Apropiativo. Le da prioridad al que le quede menos. Este algoritmo en la vida real no podría ser implementado a la perfección porque no es posible estimar el tiempo restante de CPU muchas veces... Prioriza los procesos cortos. Pero un proceso largo podría quedarse indefinidamente en espera por culpa de una llegada de muchos de ellos. 

![](SISTEMAS_INFORMATICOS/Andalucía/resources/ud02-9.png)

- Algoritmo el **trabajo más corto primero** (SJF, Shortest Job First): No apropiativo. No es interrumpido por otros. Penaliza a procesos cortos que llegan después y deben esperar a los largos. 

![](SISTEMAS_INFORMATICOS/Andalucía/resources/ud02-7.png)

- Algoritmo **primero en llegar, primero en ejecutarse** (FCFS, FIFO, First Come First Served): No apropiativo. Se ejecutan en orden de llegada. Su tiempo de respuesta puede ser alto, especialmente si varían mucho los tiempos de ejecución. La sobrecarga del sistema es mínima. Penaliza los procesos cortos y los procesos con operaciones de Entrada/Salida
![](SISTEMAS_INFORMATICOS/Andalucía/resources/ud02-8.png)

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
- Posibilidad de cambiar la prioridad de ejecución de los procesos

## 4. Programación concurrente

Los procesos pueden necesitar comunicarse entre ellos o acceder a un recurso compartido. **Debe controlarse la forma en el que estos se comunican o acceden** para que no haya errores, resultados incorrectos o inesperados. 

La concurrencia:
- Dos procesos son concurrentes cuando la primera instrucción de un proceso se ejecuta después de la primera y antes de l última de otro proceso. 
- La propia planificación, alternando instantes de ejecución en la gestión de procesos hace que estos se ejecuten de forma concurrente. Así **multiproceso = concurrencia**

La **programación concurrente** da **mecanismos de comunicación y sincronización** entre los procesos que se ejecutan de forma simultánea en un sistema informático. Permite **definir qué instrucciones se ejecutan de forma simultánea** y **cuáles deben ser sincronizadas con las de otros procesos**-

MS-DOS era un sistema **monousuario y monotarea**. El desarrollador debía implementar la alternancia en la ejecución de las diferentes instrucciones de los procesos que constituían la aplicación para interactuar con el usuario. Capturaban las interrupciones hardware del equipo.
MS-DOS tampoco **impedía que unos procesos pudieran acceder al espacio de trabajo de otros procesos**, ni tampoco al espacio de trabajo del propio sistema operativo. 

La **multitarea** llegó con Windows 95.

UNIX (antepasado de GNU/Linux) era **portable**, **multitarea**, **multiusuario** y **en red** desde su origen en 1969.
### 4.1. Sentido de la concurrencia

- **Optimizar la utilización de recursos**: Simultanear operaciones de E/S en procesos. CPU poco ociosa. Similar a una cadena de producción.
- **Proporcionar interactibilidad a usuarios (y animación gráfica)**: Esos tiempos de espera se reducen. Solo podrían ejecutarse procesos por lotes. 
- **Mejorar disponibilidad**: Atender peticiones simultáneamente
- **Conseguir diseño conceptualmente más comprensible y mantenible**. Modularidad. Claridad
- **Aumentar protección**. Seguridad de cada proceso. Poder finalizarlo en caso de mal funcionamiento sin que suponga la caída del sistema. 

La concurrencia debe tenerse en cuenta en los nuevos entornos hardware como:
- Microprocesadores con múltiples núcleos que comparten la memoria principal del sistema: 
- Entornos multiprocesador con memoria compartida: Todos usan un mismo espacio de memoria sin tener conciencia de donde está instalados los módulos de memoria físicamente
- Entornos distribuidos: Equipos heterogéneos o no conectados por red y/o internet. 

**Ventajas** 
- **Claridad** sobre lo que cada proceso debe hacer y cuando
- **Reducción del tiempo de ejecución**
- **Flexibilidad de planificación**
- **Modelado previo del comportamiento del programa** y **análisis más fiable** 

### 4.2. Condiciones de competencia

**Tipos básicos de interacción entre procesos concurrentes**
- **Independientes**: Solo interfieren en el uso de la CPU
- **Cooperantes**: Un proceso genera información o proporciona un servicio que otro necesita. Ej.: Productor - Consumidor
- **Competidores**: Necesitan usar los mismos recursos de forma exclusiva. Ej.: Lector - Escritor

En los casos **cooperantes** y **competidores** se necesitan componentes que permitan acciones de sincronización y comunicación entre procesos.

**Cooperantes**
En el proceso productor-consumidor el productor puede escribir siempre que lo desee; el consumidor queda bloqueado mientras no haya información disponible.

**Competidores**
**Región de exclusión mutua o región crítica**: Conjunto de instrucciones en las que el proceso usa un recurso y se deben ejecutar de forma exclusiva con respecto a otros procesos competidores por ese mismo recurso. 

Los competidores deben **pedir su uso antes de usarlo**. Una vez que lo obtienen, los demás quedan bloqueados al pedir ese mismo recurso. El proceso hace un lock sobre un recurso cuando obtiene su uso en exclusión muta.

Si dos o más procesos compiten por recursos distintos y ambos necesitan ambos recursos para continuar se puede producir **deadlock o interbloqueo**. Los proceso no pueden obtener nunca los recursos necesario para continuar su tarea. El interbloqueo es una situación muy peligrosa porque puede llevar al sistema a su caída o cuelga. 

## 5. COMUNICACIÓN entre procesos

**Comunicación entre procesos**: Un proceso da o deja información y el otro recibe o recoge información.

Cada proceso tiene su espacio de direcciones privado al que no pueden acceder el resto de procesos (mecanismo de seguridad). Existen formas de comunicación por las que un proceso puede recoger la información de otro proceso.

**Primitiva de sincronización**: Son proporcionados por los lenguajes de programación y sistemas operativos para facilitar la interacción entre procesos. Una primitiva hace referencia a una operación de la cual se conocen sus restricciones y efectos pero no su implementación. 
El uso de primitivas se traduce en usar objetos y sus métodos teniendo en cuenta las repercusiones reales en el comportamiento de los procesos. 

Las interacciones entre procesos se pueden clasificar:
- Sincronización: Un proceso puede conocer el punto de ejecución en el que está otro en determinado instante
- Exclusión mutua: Mientras que un proceso accede a un recurso ningún otro proceso accede al mismo recurso o variable compartida 
- Sincronización condicional: Solo se accede a un recurso cuando está en determinado estado interno

### 5.1. Mecanismos básicos de comunicación

- **Intercambio de mensajes**: Primitivas `send` y `receive`
- **Recursos compartidos**: Primitivas`write` y `read`

**Comunicar procesos en la misma máquina, intercambio de mensajes puede hacerse con**
- Buffer de memoria
- Socket

El socket intercambia entre distintas máquinas a través de la red mientras que un buffer de memoria crea un canal de comunicación entre dos procesos usando la memoria principal del sistema.
Es más común el uso de sockets actualmente.

En Java los sockets y buffers se usan como cualquier otro tipo de datos. Se usan `read-write`

Las **lecturas y escrituras** son bloqueantes. Un proceso queda bloqueado hasta que los datos estén listos para ser leídos. Escritura bloquea al proceso que intenta escribir hasta que el recurso no esté preparado. 


El uso de buffers plantea un problema y es que los buffers suelen crearse dentro del espacio de memoria de cada proceso, por lo que no son accesibles por el resto. Se puede decir que no poseen una dirección o ruta que se pueda comunicar y sea accesible entre los distintos procesos, como sí sucede con un socket o con un archivo en disco.

Una solución intermedia, soportada por la mayoría de los SO, es permitir a los procesos utilizar **archivos proyectados (o "mapeados") en memoria** (memory-mapped files). Al utilizar un fichero proyectado en memoria, abrimos un archivo de disco, pero indicamos al SO que queremos acceder a la zona de memoria en la que el SO va cargando la información del archivo. El SO utiliza la zona de memoria asignada al archivo como buffer intermedio entre las operaciones de acceso que estén haciendo los distintos procesos que hayan solicitado el uso de ese archivo y el archivo físico en disco. Podemos ver un archivo proyectado en memoria como un archivo temporal que existe solamente en memoria (aunque obviamente tendrá su correspondiente ruta de acceso a archivo físico en disco).

En Java pueden usarse ficheros mapeados en memoria usando la clase `java.nio.channels.FileChannel`

### 5.2. Tipos de comunicación

**Elementos fundamentales**
1. **Mensaje**: Información objeto de la comunicación.
2. **Emisor**: Entidad que genera el mensaje.
3. **Receptor**: Entidad que recibe el mensaje.
4. **Canal**: Medio por el que se envía y recibe el mensaje.

**Tipos de canales** 
1. **Símplex**:- Comunicación en un solo sentido.
2. **Dúplex (Full Duplex)**: - Comunicación en ambos sentidos simultáneamente.
3. **Semidúplex (Half Duplex)**: - Comunicación en ambos sentidos, pero no simultáneamente.

**Clasificación según la sincronización** 
1. **Síncrona**:- El emisor se bloquea hasta que el receptor recibe el mensaje.  Ambos se sincronizan en la recepción.
2. **Asíncrona**: El emisor continúa su ejecución inmediatamente después de enviar el mensaje. Independientemente de si el receptor lo recibe o no.
3. **Invocación Remota**: El emisor se suspende hasta recibir la confirmación del receptor. - Luego, ambos ejecutan un segmento de código común síncronamente.

**Clasificación según el comportamiento de los interlocutores
1. **Simétrica**:- Todos los procesos pueden enviar y recibir información.
2. **Asimétrica**:- Solo un proceso actúa como emisor; el resto solo escuchan.

Conocer las características de la comunicación que necesitamos establecer entre procesos nos permitirá seleccionar el canal, herramientas y comportamiento más convenientes.

Ej.: Emisión de radio es: Símplex, asíncrona y asimétrica.

## 6. SINCRONIZACIÓN entre procesos

Como se ha comentado, dos procesos se comunican si hay cierta **sincronización entre ellos**. O bien unos deben esperar a que otros finalicen, o bien realizar tareas al mismo tiempo.

La **sincronización entre procesos la hace posible el sistema operativo**. Los lenguajes de programación lo que hacen es encapsular los mecanismos de sincronización que proporciona cada SO en objetos, métodos y funciones.

Los lenguajes de programación proporcionan primitivas de sincronización entre los distintos hilos que tiene un proceso. Debe, por tanto, consultarse la documentación de clases para conocer todas las peculiaridades. 

En la **programación concurrente** siempre se accede a un recurso compartido debiendo tener en cuenta las condiciones en las que el proceso hace uso de este recurso. (Condiciones de competencia)

**Lector-escritor**
En el caso de lecturas y escrituras en un archivo debemos determinar si queremos acceder al archivo como sólo lectura, escritura, o lectura-escritura, así como utilizar los objetos que nos permitan establecer los mecanismos de sincronización necesarios para que un proceso pueda bloquear el uso del archivo por otros procesos cuando él lo esté utilizando.

Esto se conoce como el **problema de los procesos lectores-escritores**. El **sistema operativo, nos ayudará** a resolver los problemas que se plantean, ya que:

- si el acceso es de **sólo lectura**, permitirá que todos los procesos lectores (los que sólo quieren leer información del archivo) **puedan acceder simultáneamente** a él;
- en el caso de **escritura**, o lectura-escritura. El SO nos permitirá pedir un tipo de **acceso** de **forma exclusiva** al archivo. Esto significará que el proceso deberá esperar a que otros procesos lectores terminen sus accesos. Y otros procesos (lectores o escritores), esperarán a que ese proceso escritor haya finalizado su escritura.

### 6.1. Regiones críticas

**Región o sección crítica**: Instrucciones en las que un proceso accede a un recuros compartido. Se ejecutarán de forma indivisible o atómica y de forma exclusiva con respecto a otros procesos que accedan al recurso compartido.

- Se protegerán con secciones críticas solo instrucciones que acceden al recurso compartido
- Deben ser las mínimas. Solo las imprescindibles
- Se pueden definir tantas secciones críticas como sean necesarias
- Solo podrá entrar un único proceso a la sección. El resto esperan. El recurso está bloqueado
- Al final de cada sección crítica el recurso debe ser liberado. 

 Cualquier actualización de datos en un recurso compartido, necesitará establecer una región crítica que implicará como mínimo estas instrucciones:
- **leer el dato que se quiere actualizar.** Pasar el dato a la zona de memoria local al proceso;
- **realizar el cálculo de actualización.** Modificar el dato en memoria;
- **escribir el dato actualizado.** Llevar el dato modificado de memoria al recurso compartido.

#### 6.1.1 Categoría de proceso productor-consumidor (cliente-suministrador)

**Conceptos Básicos**

1. **Cliente**: Proceso que solicita información o servicios.
2. **Suministrador**: Proceso que proporciona información o servicios. Es un término más amplio que "servidor" y puede operar a través de memoria compartida, archivos, red u otros recursos.

**Características de la Comunicación**

- La información o servicio es perecedero: la información desaparece al ser consumida por el cliente y el servicio se presta cuando cliente y suministrador están sincronizados.
- La sincronización entre cliente y suministrador se puede lograr mediante intercambio de mensajes o recursos compartidos. Los procesos se comunican mediante protocolos, que son conjuntos de mensajes y reglas. Se pueden usar protocolos existentes (como FTP, HTTP, etc.) o crear nuevos.

**Sincronización entre Cliente y Suministrador**

Se debe disponer de mecanismos de sincronización que permitan que: 
    - El cliente no debe leer datos incompletos para asegurar la consistencia.
    - El suministrador no debe escribir si se ha alcanzado el límite de almacenamiento para evitar desbordes.
Así:
    - El cliente espera a que el suministrador genere el dato.
    - El suministrador genera el dato y avisa al cliente de alguna forma de que puede consumirlo. 

Podría intentar darse solución con programación secuencial pero esto es poco eficiente ya que:
- el cliente puede entrar en un bucle continuo verificando si el dato está disponible, consumiendo tiempo de CPU de manera ineficiente **espera activa** 
- si el suministrador se bloquea, el cliente también queda bloqueado.

- **Primitivas de Programación Concurrente**: Para resolver los problemas de sincronización de manera eficiente, se usan semáforos y monitores.
    - **Semáforos**: Controlan el acceso a recursos compartidos y sincronizan la ejecución de procesos.
    - **Monitores**: Encapsulan la sincronización dentro de objetos, facilitando la coordinación segura entre procesos.

Estas primitivas ayudan a proteger las secciones críticas del código, evitando condiciones de carrera y garantizando la correcta sincronización entre procesos cliente y suministrador.
### 6.2. Semáforos

Un **semáforo** es un componente de bajo nivel de abstracción que permite arbitrar los acceso a un recurso compartido en un entorno de programación conurrente. 

En su uso es un tipo de dato que puede instanciarse. El semáforo contendrá un conjunto de valores y se podrá realizar con él un conjunto de operadores. El semáforo tendrá una lista de procesos suspendidos a la espera de entrar en el mismo.

Los semáforos pueden ser:
- Semáforos binarios. Solo tienen valor 0 o 1. (Un permiso)
- Semáforos generales. Pueden tomar cualquier valor. (Varios permisos)

En el sistema UNIX los semáforos pueden ser:
- Sin nombre
- Con nombre. Se les asigna un nombre.

- El semáforo se inicializa con unos permisos indicando cuantos procesos pueden entrar concurrentemente en él. 

El semáforo permite dos operaciones:
- `sem.wait()`: Si el semáforo tiene permisos, decrementa en uno el valor del semáforo. Si el semáforo no tiene permisos, queda a la espera.
- `sem.signal()`: Libera el permiso. Incrementando en 1 el valor de estos y permitiendo que otor proceso entre. 


El semáforo tiene operaciones seguras como la operación de chequeo del valor y su posterior actualización. 

```
Para utilizar semáforos, seguiremos los siguientes pasos:

1. Un proceso padre creará e inicializará tanto semáforo.
2. El proceso padre creará el resto de procesos hijo pasándoles el semáforo que ha creado. Esos procesos hijos acceden al mismo recurso compartido.
3. Cada proceso hijo, hará uso de las operaciones seguras wait y signal respetando este esquema:
    1. objSemaforo.wait(); Para consultar si puede acceder a la sección crítica.
    2. Sección crítica; Instrucciones que acceden al recurso protegido por el semáforo objSemaforo.
    3. objSemaforo.signal(); Indicar que abandona su sección y otro proceso podrá entrar.
        - El proceso padre habrá creado tantos semáforos como tipos secciones críticas distintas se puedan distinguir en el funcionamiento de los procesos hijos (puede ocurrir, uno por cada recurso compartido).
```

Los semáforos tienen gran capacidad funcional pero debido a su bajo nivel de abstracción pueden ser fuente de errores. 

En Java existe la clase `java.util.concurrent.Semaphore` para arbitras hilos mediante semáforo.
### 6.3. Monitores

Un **monitor** es un componente de alto nivel de abstracción que gestiona los recursos que van a ser accedidos de forma concurrente. 

>Los monitores nos ayudan a resolver las desventajas que encontramos en el uso de semáforos. El fundamental de los semáforos es que recae sobre el programador o programadora la tarea implementar el correcto uso de cada semáforo para la protección de cada recurso compartido. Y, por otro lado, el recurso sigue estando disponible para utilizarlo sin la protección de un semáforo. Los monitores son como guardaespaldas, encargados de la protección de uno o varios recursos específicos pero que además encierran esos recursos de forma que el proceso sólo puede acceder a esos recursos a través de los métodos que el monitor proporcione.

- **Declaración de un Monitor**:
    1. **Componentes Privados**: Constantes, variables, procedimientos y funciones solo visibles para el monitor.
    2. **Interfaz Pública**: Procedimientos y funciones accesibles por otros procesos que el monitor expone y que son interfaz a través de las que los procesos acceden al monitor
    3. **Cuerpo del Monitor**: Código que se ejecuta al instanciar o inicializar el monitor para inicializar variables y estructuras internas.
- **Exclusión Mutua**: Acceso garantizado al código interno de forma exclusiva.
- **Lista de Espera**: Procesos que son suspendidos al intentar acceder al monitor cuando está ocupado.

 **Java y Monitores**: Java no proporciona una clase Monitor específica, pero se pueden implementar usando semáforos. Objetos como `FileReader` actúan como monitores al bloquear procesos durante operaciones de E/S, aunque no garantizan exclusión mutua en todos sus métodos. Podemos decir que **utilizamos objetos de tipo monitor al acceder a los recursos del sistema**, aunque no tengan como nombre Monitor.

**Ventajas de los Monitores**
1. **Uniformidad**: Proveen exclusión mutua de manera única y clara. No hay confusión con semáforos.
2. **Modularidad**: Separan el código en exclusión mutua del resto del programa.
3. **Simplicidad**: Facilitan la tarea del programador al manejar la exclusión mutua.
4. **Eficiencia**: Implementación subyacente puede limitarse a semáforos.

**Desventajas de los Monitores**
- **Complejidad**: Aumenta significativamente con el número y la interacción de múltiples condiciones de sincronización.
#### 6.3.1. Monitores: Lecturas y escrituras bloqueantes en recursos compartidos

En el proceso productor-consumidor:
1. **Buffer Compartido**: El suministrador introduce elementos y el cliente los extrae.
2. **Variable Compartida**: Se sincronizan usando una variable compartida que indica el número de elementos en el buffer, con un tamaño máximo N.
    - **Suministrador**: Verifica que la variable es menor que N antes de introducir un elemento y luego la incrementa en uno.
    - **Cliente**: Extrae un elemento del buffer y decrementa la variable si hay elementos disponibles.

Los mecanismos de sincronización de este funcionamiento entre procesos son las lecturas y escrituras bloqueantes en recursos compartidos del sistema. En Java se dispone de: 

**Arquitectura `java.io`**:
    - **Clientes**: Clases derivadas de `Reader` (`InputStream`, `InputStreamReader`, `FileReader`) con métodos `read(buffer)` y `read(buffer,desplazamiento,tamaño).
    - **Suministradores**: Clases derivadas de `Writer` con métodos `write(info)` y `write(info,desplazamiento,tamaño)`

**Arquitectura `java.nio`**:
    - **Clientes**: Clases `FileChannel` y `SocketChannel` con métodos `read(buffer)` y `read(buffer,desplazamiento,tamaño)`.
    - **Suministradores**: Clases `FileChannel` y `SocketChannel` con métodos `write(info)` y  `write(info,desplazamiento,tamaño)`.

En el caso del `FileChannel` debe hacerse uso del método `lock()` para implementar las secciones críticas de forma correcta. Tanto suministradores como clientes cuando se esté haciendo uso de un fichero como canal de comunicación entre ellos. 

#### Ejemplo

`FileLock lock = channel.lock();`

- **Bloqueo Exclusivo**: El método `lock()` sin parámetros adquiere un bloqueo exclusivo en el archivo, lo que significa que ningún otro proceso puede acceder al archivo hasta que se libere el bloqueo.
- **Bloqueo Compartido**: Al usar `lock(long position, long size, boolean shared)`, podemos especificar un bloqueo compartido, permitiendo que otros procesos lean pero no escriban en el archivo. Solo en una región específica del archivo.

Bloqueo exclusivo para el productor (que escribe)
Bloque compartido para el consumidor (que lee)

----

- **Sincronización**: Usaremos `FileChannel` para manejar la exclusión mutua mediante bloqueo de archivos.

```java
import java.io.RandomAccessFile;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;
import java.nio.channels.FileLock;
import java.util.Random;

public class Productor {
    private static final String FILE_PATH = "shared.dat";

    public static void main(String[] args) {
        try (RandomAccessFile file = new RandomAccessFile(FILE_PATH, "rw");
             FileChannel channel = file.getChannel()) {

            ByteBuffer buffer = ByteBuffer.allocate(8);
            Random random = new Random();

            while (true) {
                int number = random.nextInt(100);
                buffer.clear();
                buffer.putInt(number);
                buffer.flip(); // Preparar buffer para la lectura despues de haber escrito datos en el

                try (FileLock lock = channel.lock()) {
                    System.out.println("Productor escribe: " + number);
                    channel.write(buffer);
                    channel.force(true); // Asegurar que los datos se escriban en el disco
                }

                Thread.sleep(1000); // Esperar antes de producir el siguiente número
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

```java
import java.io.RandomAccessFile;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;
import java.nio.channels.FileLock;

public class Consumidor {
    private static final String FILE_PATH = "shared.dat";

    public static void main(String[] args) {
        try (RandomAccessFile file = new RandomAccessFile(FILE_PATH, "rw");
             FileChannel channel = file.getChannel()) {

            ByteBuffer buffer = ByteBuffer.allocate(8);

            while (true) {
                buffer.clear(); // Restalece indices de posicion y limite para escribir nuevos datos desde el principio aunque no los borra 

                try (FileLock lock = channel.lock(0, Long.MAX_VALUE, true)) {
                    channel.position(0);
                    int bytesRead = channel.read(buffer);
                    if (bytesRead > 0) {
                        buffer.flip();
                        int number = buffer.getInt();
                        System.out.println("Consumidor lee: " + number);
                    }
                }

                Thread.sleep(1000); // Esperar antes de intentar leer nuevamente
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

### 6.4. Memoria compartida

Los mecanismos de sincronización (regiones críticas, semáforos, monitores) tienen su razón de ser en la existencia de recursos compartidos entre los que se encuentra la memoria compartida.

La zona de memoria del proceso (instrucciones, datos, pila de ejecución) es privada a otros procesos. Otra cosa es la programación multihilo que permite tener varios flujos de ejecución en el mismo proceso (ahí sí comparten entre ellos la memoria asignada)

La programación distribuida o multiproceso puede solucionar muchos problemas.

OpenMP. Es una API para la **programación multiproceso de memoria compartida** en múltiples plataformas. Es un estándar disponible en muchas arquitecturas, incluidas las plataformas de Unix y de Microsoft Windows. Se compone de un conjunto de directivas de compilador, rutinas de biblioteca, y variables de entorno que influencian el comportamiento en tiempo de ejecución. OpenMP es un modelo de programación portable y escalable que proporciona a los programadores una interfaz simple y flexible para el desarrollo de **aplicaciones paralelas** para las plataformas que van desde las computadoras de escritorio hasta las supercomputadoras. También existe una implementación de OpenMP en Java.

### 6.5. Cola de mensajes

El **paso de mensajes** es una técnica utilizada para aportar sincronización entre procesos y permitir la exclusión mutua de forma similar a semáforos y monitores. **No necesita memoria compartida**

Intervienen el proceso que envía, el que recibe y el mensaje.

Según si el proceso que envía se espera a que el mensaje sea recibido se puede hablar de:
- **Paso de mensajes asíncrono**: El proceso que envía no espera a que sea recibido el mensaje y continúa su ejecución, pudiendo generar otro mensaje y enviarlo. Se suelen emplear **buzones** o **colas** que almacenan los mensajes a la espera de que un proceso lo reciba. Así el proceso que envía mensajes solo se bloquea o para al finalizar su ejecución o si el buzón está lleno. Se puede establecer protocolo entre emisor y receptor para que el receptor pueda indicar qué capacidad le queda en su cola de mensajes y si está lleno o no.

- **Paso de mensajes síncrono**: El proceso que envía el mensaje espera a que un proceso lo reciba para continuar su ejecución. Se suele llamar técnica encuetro (rendezvous). Aquí se incluye la llamada a procedimiento remoto (RCP), popular en arquitecturas cliente/servidor. 

## 7. Requisitos de calidad que debe cumplir un programa concurrente: seguridad, vivacidad, eficiencia y reusabilidad

**Propiedades aplicadas específicamente a la programación concurrente**
- **Seguridad (Safety)**: En cada instante no debe haberse producido algo que haga entrar al programa en un estado erróneo.
	- Dos programas **no deben entrar simultáneamente en una sección crítica**
	- **Se respetan condiciones de sincronizació**n. Ej.: El consumidor no debe consumir dato antes de que el productor lo haya producido. El productor no debe producir dato si el buffer está lleno.  

- **Vivacidad (Liveness)**: Cada sentencia que se ejecute conduce a un **avance constructivo para alcanzar el objetivo funcional del programa**. Son dependientes  de la política de planificación que se use. **No debe haber**: 
	- **bloqueos activos** (livelock): Procesos que ejecutan de forma continuada sentencias que no conducen a un proceso constructivo.
	- **Inanición**, aplazamiento indefinido (starvation): Estado al que llega un programa que, pudiendo avanzar de forma constructiva, no se le asigna tiempo de procesador en la planificación o en las condiciones de sincronización hay criterios de prioridad que le perjudican.
	- Interbloqueo (deadlock): Los proceso no pueden obtener los recursos encesarios para finalizar su tarea. 

**Más generales:**
- **Eficiencia**: No usar más recursos de los necesarios. Rigurosidad en su implementación, toda la funcionalidad esperada de forma correcta y concreta.

- **Reusabilidad**: Implementar código de forma modular y documentarlo correctamente. 

Estas 4 características se consiguen mediante **patrones de diseño**, **documentación** y **depuración**

### 7.1. Arquitecturas y patrones de diseño

Se llama **arquitectura de software** o **arquitectura lógica** al conjunto de patrones y abstracciones coherentes con base a las cuales se pueden resolver los problemas. Es el diseño de más alto nivel de la estructura de un sistema. Indica la estructura, funcionamiento e interacciones entre las partes del software. 

Deben satisfacerse la mayor funcionalidad y requerimientos funcionales del sistema (de desempeño) así como los requerimientos no funcionales (confiabilidad, escalabilidad, portabilidad, disponibilidad, mantenibilidad, auditabilidad, flexibilidad e interacción)

Se suele adoptar una arquitectura conocida en función de las ventajas e inconvenientes para cada caso concreto.

Las más famosas
- **Monolítica**: Grupos funcionales muy acoplados
- **Cliente-servidor**: Reparte su carga de cómputo entre dos partes: consumir servicio y proporcionar servicio
- **Tres niveles**: Arquitectura dividida en capas con reparto de funciones. Capa de presentación (UI), capa de cálculo (lógica o modelado de negocio) y capa de almacenamiento (persistencia)

Otras:
- **Pipeline**: Modelar proceso comprendido por varias fases secuenciales. La entrada de una es la salida de la anterior
- **Entre pares**: Similar a cliente-servidor. Pero cada elemento es igual a otro (simultáneamente cliente y servidor)
- **Orientada a servicios (SOA)**: Se diseñan servicios de aplicación basados en definición formal independiente de la plataforma subyacente y del lenguaje de programación como una interfaz estándar.
- **Dirigda por eventos**: Producción, detección, consumo y reacción a eventos.

Los **patrones de diseño** son soluciones de diseño válidas en distintos contextos y aplicadas con éxito en ocasiones anteriores.

- Ayudan a comenzar en el diseño de un programa complejo: Descomposición de objetos inicial, pensados para un programa escalable, probados por otros
- Ayuda a reutilizar técnicas: Mucha gente los conoce, alto nivel de abstracción aplicables a diferentes situaciones.

**Modelos básicos de los programas concurrentes**:
- Programa resulta de actividad de objetos activos que interaccionan entre sí directamente o a través de recursos y servicios pasivos
- Programa resulta de la ejecución concurrente de tareas. Cada tarea es unidad de trabajo abstracta y discreta que idealmente puede realizarse independientemente de otras tareas. 

Los patrones **no son obligatorios** solo aconsejables en el caso de tener un problema similar al que el patrón soluciona.

**Páginas muy recomendadas para leer**
- https://sourcemaking.com/
- https://refactoring.guru/design-patterns
- https://github.com/orgs/RefactoringGuru/repositories?type=all
- https://www.docirs.cl/uml.asp
- https://wiki.c2.com/?DesignPatternsBook

>SourceMaking.com is an authorized reseller of several products originated from Refactoring.Guru project. Both projects have similar content, but RG has more recent stuff.

### 7.2. Documentación

Debe documentarse **todo lo que no es evidente.** No debe indicarse lo que se hace sino por qué
```
¿De qué se encarga una clase? ¿Un paquete?
¿Qué hace un método? ¿Cuál es el uso esperado de un método?
¿Para qué se usa una variable? ¿Cuál es el uso esperado de una variable?
¿Qué algoritmo estamos usando? ¿De dónde lo hemos sacado?
¿Qué limitaciones tiene el algoritmo? ¿... la implementación?
¿Qué se debería mejorar ... si hubiera tiempo?
```

|[Javadoc](https://educacionadistancia.juntadeandalucia.es/formacionprofesional/mod/glossary/showentry.php?displayformat=dictionary&concept=javadoc%20%28DAM_PSP01%29 "Ver la definición de")|Una línea|Tipo C|
|---|---|---|
|Sintáxis|Comienzan con "/**", se pueden prolongar a lo largo de varias líneas (que probablemente comiencen con el carácter "*") y terminan con los caracteres "*/".<br><br>Cuenta con etiquetas específicas tipo: @author, `@param`, @return,...|Comienzan con "//" y terminan con la línea.|Comienzan con "/*", se pueden prolongar a lo largo de varias líneas (que probablemente comiencen con el carácter "*") y terminan con los caracteres "*/".|
|Propósito|Generar documentación externa.|Documentar código que no necesitamos que aparezca en la documentación externa.|Eliminar código.|
|Uso|**Obligado:**<br><br>- Al principio de cada clase.<br>- Al principio de cada método.<br>- Antes de cada variable de clase.|- Al principio de fragmento de código no evidente.<br>- A lo largo de los bucles.<br>- Siempre que hagamos algo raro o que el código no sea evidente.|Ocurre a menudo que código obsoleto no queremos que desaparezca, sino mantenerlo "por si acaso". Para que no se ejecute, se comenta.|

Al documentar se destacarán:
- Las condiciones de sincronismo
- Las regiones críticas identificadas y el recuros compartido a proteger

### 7.3. Depuración. Dificultades que se producen

Al depurar aplicaciones con mecanismos de sincronización y acceso concurrente se presenan como problemas:
- Los problemas de depuración de aplicación secuencial
- Errores de temporización y sincronización propios de programación concurrente

Programas **secuenciales** tienen línea simple de control de flujo. Operaciones en secuencial temporal lineal. 
- Comportamiento del programa solo en función de las operaciones individuales que lo constituyen y de su orden
- El tiempo que tarda cada operación no tiene consecuencias sobre el resultado
- Para validar: Se comprueba la correcta respuesta a cada sentencia y el correcto orden de ejecución

Para validar programas concurrentes:
- Se comprueban los aspectos anteriores
- Las sentencias se pueden validar individualmente solo si no están involucradas en recursos compartidos
- En recursos compartidos, los efectos de interferencia entre sentencias pueden ser muy variados y su validación es difícil. Se debe comprobar la corrección en definición de regiones críticas y que se cumple la exclusión muta.
- Al comprobar la implementación del sincronismo entre aplicaciones, se puede forzar la ejecución secuencial de tareas de distintos procesos introduciendo sentencias explícitas de sincronización. El tiempo no influye en el resultado.

Los depuradores no ofrecen todas las herramientas para depurar la concurrencia. Se contará
- Con el depurador. Netbeans sí está preparado para depuración concurrente dentro de hilos del mismo proceso. No para procesos independientes...
- Volcados de actividad en fichero log o pantalla de salida
- Herramientas de depuración específicas como TotalView o StreamIt Debugger Tool.

Los mismos errores podrían desaparecer cuando se introduce código para identificar el problema.

Es complicado depurar. Debe tenerse en cuenta patrones de diseño que resuelven errores comunes de la concurrencia. Estos nos ayudarán a resolver problemas tipo en condiciones de sincronismo y/o accesos concurrentes. 

## 8. Programación paralela y distribuida

Dos procesos son **paralelos** si las instrucciones de ambos se ejecutan realmente de forma simultánea. Sucede en sistemas con más de un núcleo de procesamiento.

La programación paralela y distribuida considera los aspectos conceptuales y físicos de la computación paralela para mejorar las prestaciones aprovechando la ejecución simultánea de tareas.

Ambas tienen ejecución simultánea de tareas que resuelven un problema común. Pero...

- **Programación paralela**: Centrada en microprocesadores multinúcleo o supercomputadores con equipos idénticos conectados entre sí y con  SO propios
- **Programación distribuida**: Ordenadores heterogéneos interconectados entre sí pro redes de propósito general, área local, metropolitana, internet...Se gestionan con componentes, protocolo estándar y sistemas operativos de red

En computación paralela y distribuida
- Cada procesador tienen que resolver una porción del problema
- En paralela: Procesos intercambian datos a través de direcciones de memoria compartidas o red de interconexión propia
- En distribuida: Intercambio de datos y sincronización se hace mediante intercambio de mensajes
- El sistema se presenta como una unidad **ocultando la realidad de las partes que lo forman**
### 8.1. Conceptos básicos

#### **Clasificaciones de sistemas distribuidos y paralelos**

**En función de los conjuntos de instrucciones y datos (Taxonomía de Flynn)**
- Arquitectura secuencial (SISD, Single Instruction Single Data)
- Arquitecturas paralelas o distribuidas en grupos:
	- SIMD (Single instruction Multiple Data)
	- MISD (Multiple Instruction Single Data)
	- MIMD (Multiple Instruction Multiple Data)
	- SPMD (Single Program Multiple Data)

**Por comunicación y control**
- **Sistemas de multiprocesamiento simétrico (SMP)** Son MIMD con memoria compartida. Procesadores se comunican a través de memoria compartida. (Microprocesadores de múltiples núcleos de los PCs)
- **Sistemas MIMD con memoria distribuida**: Memoria distribuida entre procesadores (nodos) del sistema. Cada uno con su propia memoria local en la que poseen su propio programa y datos asociados. Una red de interconexión conecta los microprocesadores y sus memoria locales mediante enlaces (links) de comunicación usados para intercambio de mensajes entre los procesadores. Los procesadores intercambia datos entre sus memorias cuando se pide el valor de variables remotas. Tipos de estos sistemas son:
	- Clústers: Colección de ordenadores (no homogéneos necesariamente) conectados por red para trabajar concurrentemente en tareas del mismo programa. La interconexión puede no ser dedicada
	- Grid: Clúster con interconexión a través de internet

#### **Definiciones para desarorllar en sistemas distribuidos**
- **Distribución**: Construcción de una aplicación por partes. A cada parte se le asigna un conjunto de responsabilidades dentro del sistema.
- **Nodo de red**: Uno o varios equipos se comportan como una unidad de asignación integrada en el sistema distribuido.
- **Objecto distribuido**: Módulo de código con plena autonomía que puede instanciarse en cualquier nodo de la red y a cuyos servicios pueden acceder clientes de otro nudo o nodo
- **Componente**: Elemento de software que encapsula una serie de funcionalidades. Puede usarse en conjunto con otro componente para formar sistema más complejo (y reutilizable). Tiene específicado:
	- Los servicios que ofrece
	- Los requerimientos necesarios para poder ser instalado en un nudo
	- Posibilidades de configuración que ofrece
	- No está ligado aninguna aplicación,
	- Puede instanciarse en cualqueir nudo
	- Gestionado por herramientas automáticas.
	- Caracterizado por alta cohesión (todos los elementos del componente están estrechamente relacionados) y bajo acoplamiento (independencia de un componente frente a otros)
- **Transacciones**: Actividades ejecutadas en diferentes nudos de una plataforma distribuida para ejecutar una tarea de negocio. La transacción finaliza cuando todas las partes implicadas confirman que sus actividades han concluido con éxito. Propiedades ACID:
	- Atomicidad: Unidad indivisible de trabajo. Todas las actividades deben ser ejecutadas con éxito
	- Congruencia: De un estado correcto a otro correcto. Al finalizar la transacción debe estar correcto y, si falla, retornarlo al estado original previo.
	- Aislamiento: No deben interferir entre ellas aunque se ejecuten de forma concurrente. Debe sincronizar el acceso a los recursos compartidos y garantizar que las actuaciones concurrentes sean compatibles
	- Durabilidad: Los efectos de la transacción son permanentes
- **Gestor de transacciones**: Controla y supervisa la ejecución de transacciones, asegurando sus propiedades ACID.

### 8.2. Tipos de paralelismo

Las mejoras arquitectónicas que han sufrido los computadores se han basado en la obtención de rendimiento explotando los diferentes niveles de paralelismo

**Niveles de paralelismo**:

- **A nivel de bit**: Se consigue incrementando el tamaño de la palabra del microprocesador. Realizar operaciones sobre el mayor número de bits. Paso de palabras de 6 bits, a 16, a 32, a 64 bits
- **A nivel de instrucciones**: Introduciendo pipeline en la ejecución de instrucciones máquina en el diseño de procesadores
- **A nivel de bucle:**: Dividir las interacciones de un bucle en partes que pueden realizarse de forma complementaria. Por ejemplo bucle de 0 a 100 equivalente a bucle de 0 a 49 y de 50 a 100
- **A nivel de procedimientos:** Identificando qué fragmentos de código dentro de un programa pueden ejecutarse de forma simultánea sin interferir la tarea de una en la de otra. 
- **A nivel de tareas dentro de un programa**: Tareas que cooperan para la solución del programa general (sistemas distribuidos y paralelos)
- **A nivel de aplicación dentro de un ordenador:** Gestión de procesos por el sistema operativo multitarea. (Como se vio más arriba)

**Tamaño de grano o granularidad**

Medida de la cantidad de computación de un proceso software. Es el segmento de código escogido para su procesamiento paralelo. 

- **Paralelismo de grano fino**: No requiere mucho conocimiento del código. Se obtiene paralelización de forma casi automática. Buenos resultados en eficiencia en poco tiempo. Ej.: Descomposición de bucles
- **Paralelismo de grano grueso**: Engloba al grano fino. Paralelización de alto nivel. Requiere mayor conocimiento del código al paralelizar mayor cantidad de él. Consigue mejores rendimientos que la paralelización fina ya que intenta evitar los overhead (exceso de recursos asignados y usados) que se suelen producir al dividir el programa en secciones muy pequeñas. Un ejemplo de este paralelismo es al descomponer el problema en dominios (dividiendo en conjunto de datos a procesar acompañando estos de las acciones que deben realizarse sobre ellos)
----

En la **programación paralela** además de CPUs se usan GPUs (unidades de procesamiento de tarjetas gráficas). Estas poseen mayor potencia de cómputo al ser específicamente diseñadas para resolver tareas intensivas de cómputo en tiempo real de direccionamiento de gráficos en 3D de alta resolución. En general tienen muy buen comportamiento en algoritmos de ordenación rápida de grandes listas de datos y transformaciones bidimensionales.  (Ej.: Sistemas CUDA, NVidia)

### 8.3. Modelos de infraestructura para la programación distribuida

Los modelos de infraestructura que permiten la implementación de la comunicación entre componentes son:
- **Sockets**: Generación dinámica de canales de comunicación. Bajo nivel de abstracción. No son adecuados a nivel de aplicación
- **Remote Procedure Call (RPC)**: Abstrae comunicación a nivel de procedimientos. Es adecuado para programación estructurada basada en librerías
- **Invocación remota de objetos**: Abstrae comunicación a la invocación de métodos de objetos distribuidos por el sistema distribuido. Se localizan por su identidad. Adecuado para aplicaciones basadas en paradigma POO.


**RMI** (Remote Method Invocation): Solución de Java para comunicación de objetos Java distribuidos. Inconveniente: Paso de parámetros por valor implica tiempo para hacer serialización, enviar objetos y deserializar.

**CORBA** (Common Object Request Brocker Architecture): Facilitar diseño de aplicaciones basadas en paradigma cliente-servidor. Se definen servidores estandarizados a través de un modelo de referencia, patrones de interacción ente clientes y servidores y especificaciones de las APIs.

**MPI** (Message Passing Interface). Define síntaxis y semántica de funciones contenidas en biblioteca de paso de mensajes diseñada para ser usada en programas que exploten la existencia de múltiples procesadores. 
La MPI es un protocolo de comunicación entre computadores. Estándar de comunicación entre nodos que ejecutan programa en sistema de memoria distribuida. Las llamadas se dividen en cuatro clases:
- Llamadas para inicializar, administrar y finalizar comunicaciones
- Llamadas para transferir datos entre un par de procesos
- Llamadas para transferir datos entre varios procesos
- Llamadas para crear tipos de datos definidos por el usuario

**Máquina paralela virtual**. Paquetes software para ver el conjunto de nodos disponibles como una máquina virtual paralela, ofreciendo una opción práctica, económica y popular para aproximarse al cómputo paralelo. 

--

Hay listas de proyectos de computación distribuida (https://en.wikipedia.org/wiki/List_of_volunteer_computing_projects) donde voluntarios donan tiempo de computación a causas específicas. 