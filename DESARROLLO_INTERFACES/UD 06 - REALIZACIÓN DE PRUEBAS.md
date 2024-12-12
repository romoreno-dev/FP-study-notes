
Mediante las **pruebas** se puede verificar que el producto diseñado no presenta errores y que desempeña de forma correcta las tareas para las que ha sido diseñado. 
## 1. Objetivo, importancia y limitaciones del proceso de prueba. Estrategias

Las pruebas deben diferenciarse en diversos **conjuntos** y particiones para solventar el mayor número de casos posibles dado que existe la **limitación** de que será imposible realizar todas las comprobaciones del producto en cuestión.
### Tipos de pruebas
- **Prueba de caja negra o pruebas de comportamiento**: Objetivo principal especificar entradas y salidas que produce un determinado producto. No es necesario conocer la implementación.
- **Prueba de caja blanca o pruebas estructurales**: Examinar la lógica interna sin considerar aspectos sobre su rendimiento. 

### Consideraciones
- Cada caso de prueba debe definir un resultado de salida esperado que debe ser comparado con el obtenido realmente
- Evitar que el desarrollador pruebe su propio programa (¿salvo que esté haciendo TDD?)
- Inspeccionar resultados de cada prueba para detectar síntomas de defectos
- Al generar casos de prueba incluir entradas válidas y no válidas
- Probar si el software no hace lo que debe
- Probar si el software hace lo que debe
- Considerar que esta es una tarea creativa
- Planificar y diseñar pruebas para detectar el mayor número de defectos minimizando el tiempo y el esfuerzo

## 2. Prueba unitaria

Buscan comprobar que el código funciona de forma correcta mediante la **comprobación de cada módulo de forma individual**.

### Descripción
- Particiones en los módulos para que al ser más pequeños sea más fácil realizar pruebas oportunas
- Cada unidad define casos de prueba (caja blanca)
- Deben recorrerse todos los caminos de ejecución posibles dentro del código de prueba (cubrimiento)
- Considerar: Rutinas de excepción y de error, manejo de parámetros, validaciones, valores válidos, límites, rangos,...
- Técnica: Compara resultado esperado con respecto a resultado obtenido

## 3. Pruebas de integración: ascendentes y descendentes

Se aplican a los módulos de forma conjunta para intentar detectar errores a la hora de unirlos o devolver valores no esperados.

Mezclar todos los módulos en la prueba podría ser caótico y dar lugar a numerosos errores.  Por ello, existen incorporaciones de forma:

Se pueden añadir más incorporaciones en forma ascendente o descendente:
- **Ascendente (Bottom-Up Integration Testing**
	- Combinaciones de módulos de bajo nivel que tengan asignadas tareas determinadas. Se combinan y prueban primero y se integran progresivamente con módulos de niveles más altos. Se usan _drivers_ para simular módulos superiores aún no desarrollados.
	- Se **diseña un programa que controle las distintas pruebas y pueda llevar un control más exhaustivo sobre la entrada y salida de estas**. 
	- Se permite la comprobación del funcionamiento en grupo. 
	- Está capacitado para eliminar los distintos gestores y permite movilidad a los grupos existentes por toda la estructura del programa.
- **Descendente (Top-Down Integration Testing)**. 
	- Se prueban módulos de nivel superior de la jerarquía. Se combinan y prueban y luego se integran con los más bajos. Se usan _stubs_ para simular módulos inferiores aún no desarrollados.
	- Usar el **módulo de control principal para llevar control sobre la prueba en cuestión**. 
	- Se puede **sustituir los resguardos subordinados por módulos reales (uno por uno)**. 
	- Se realizan **diferentes pruebas cada vez que se integran módulos nuevos**. 

Cuando se generan casos de prueba por cualquiera de las dos integraciones se usan pruebas de caja negra. 

## 4. Pruebas del sistema: configuración, recuperación, entre otras

Buscan comprobar el funcionamiento del sistema verificando que los elementos se integraron correctamente. 
Así: 
- Debe cumplir todos los requisitos funcionales definidos
- Funcionamiento y rendimiento de las interfaces hardware, software y de usuario debe ser óptimo
- Documentación de usuario debe ser adecuada
- Rendimiento debe ser el esperado

Se usarán aquí también pruebas de caja negra comenzando por:
- Pruebas alfa: En el entorno de desarrollo
- Pruebas beta: En el entorno del cliente

Se puede distinguir según lo que comprueban entre:
- **Pruebas de comunicaciones**: Interfaces locales y remotas funcionan de forma correcta
- **Pruebas de rendimiento**: Tiempos de respuesta de la aplicación
- **Pruebas de recuperación**: Forzar fallo de software para comprobar capacidad de recuperación
- **Pruebas de volumen**: Funcionamiento del software con cantidades similares a la capacidad total de procesamiento
- **Pruebas de sobrecarga**: Mismas que pruebas de volumen pero llegando al límite de su capacidad
- **Pruebas de tensión**: Similares a sobrecarga pero disminuyendo el tiempo disponible
- **Pruebas de disponibilidad de los datos**: Si se ha mantenido al integridad de los datos tras recuperación del sistema
- **Pruebas de facilidad de uso**: Referidas al usuario final
- **Pruebas de entorno**: Interacción con otro tipo de sistemas
- **Pruebas de seguridad**: Mecanismos de control de acceso al sistema
- **Pruebas de usabilidad**: Lo utilizable que es el sistema
- **Pruebas de almacenamiento**: Cantidad de mrmoai principal y secundaria que usa el programa y el tamaño de los archivos temporales
- **Pruebas de configuración**: Software con diversos tipos de hardware, sistemas operativos, antivirus...
- **Pruebas de instalación**: Automatización para la facilidad al usuario final
- **Prueba de documentación**: La documentación técnica para desarrolladores y la documentación de usuario

## 5. Pruebas de uso de recursos

Buscan, como se ha comentado, averiguar cuales son los elementos críticos del sistema. Se revisa la memoria RAM, rendimiento de la CPU o el espacio en disco.

## 6. Pruebas funcionales

- Buscan comprobar si el sistema cumple los requisitos especificados. 
- Se basan en ejecución, revisión, retroalimentación de funcionalidades diseñadas.
- Se diseñan modelos de prueba para evaluar cada una de las opciones con las que cuenta el paquete informático.
- Se ingresan entradas y examinan sus salidas mediante
	- Partición de equovalencia
	- Analizar el valor límite
	- Utilizar un grafo-causa-efecto
	- Suposición de errores
	
## 7. Pruebas de simulaciones

Permiten **diseñar y ejecutar las pruebas de carga** para comprobar cómo va a responder el sistema ante las condiciones de trabajo. 

Pruebas de humo, tensión de carga, rendimiento de la aplicación y diseño de la capacidad.

Modelos que llevan a cabo la simulación:
- **Constante**: Misma carga de usuario en determinado espacio de tiempo
- **Paso**: Al aumentar valores de carga se supervisa la aplicación. Permite conocer los umbrales en los que los tiempos de respuesta de la aplicación se encuentran dentro de los parámetros.
- **Basado en objetivos**: Parecida a la anterior aunque se puede seleccionar cuándo se va a detener el aumento de la carga. 
## 8. Pruebas de aceptación

Son realizadas por el usuario, que puede ser ayudado por las personas que forman parte del equipo de desarrollo. 
Se caracterizan por:
 - El usuario participa de forma activa
 - Demuestran si los requisitos de aceptación no se cumplen
 - Se realizan en la etapa final del desarrollo de software
## 9. Pruebas alfa y beta

El desarrollador pierde perspectiva sobre cómo el usuario se desenvuelve en la aplicación. 
Por eso existen las pruebas _alfa_ y _beta_

- Pruebas alfa: Desarrollador con grupo de usuarios finales en entrono controlado y anotando los problemas que se presenten
- Pruebas beta: Usuario sin supervisor del desarrollador en un entrono no controlado. El cliente notifica los errores para transmitirlos al equipo.  
## 10 Pruebas manuales y automáticas. Los cuatro cuadrantes de pruebas

Es necesario realizar un **plan de pruebas** y decidir si las pruebas serán:
- **Automáticas**: Usuario no interviene en el proceso. Es repetible y portable. Se pueden sustituir las horas que emplearía el usuario y su coste por el tiempo de ejecución del equipo. En el punto negativo el control de la prueba se deja a una máquina, existiendo tasa de error. (Ej.: Selenium)
- **Manuales**: Usuario es el protagonista del plan. Permite tener un control exhaustivo del plan de prueba gracias al usuario pero con más gastos. 

Para pruebas automatizadas de software hay diversas herramientas según la utilidad:
- Seguimiento de defectos: Bugzilla y Bugrat
- Evaluación de pruebas de carga y rendimiento: Jmeter
- Gestión y manejo de pruebas: fth, Qatrag
- Pruebas unitarias: JUnit

Existen diferentes vertientes y opiniones sobre la materia. 
Según el libro Agile Testing, se recomienda la elección siguiendo el siguiente cuadro:

![](resources/ud06-1.png)

- Q1: Recomendado **pruebas automáticas.** Unitarias y recursos del sistema.
- Q2: A elección entre **pruebas manuales y automáticas.** Aspectos funcionales, de capacidad y rendimiento.
- Q3: Pruebas **manuales**: Usabilidad y alfa y beta
- Q4: Pruebas de verificación mediante **herramientas** destinadas para tal fin. 

----------

Viendo esta basura de libro, se lo pregunté a ChatGPT

Los **Cuatro Cuadrantes de Pruebas Ágiles** son un modelo conceptual que ayuda a las organizaciones a planificar y ejecutar pruebas en un entorno ágil. Este marco fue introducido por Lisa Crispin y Janet Gregory en su libro _Agile Testing_. Los cuadrantes dividen las pruebas en cuatro áreas principales, basándose en el propósito de la prueba, el enfoque y quién la realiza.

### Descripción de los Cuadrantes:

**Cuadrante 1 (Q1):**  
    **Objetivo:** Soporte al desarrollo.  
    **Tipo de pruebas:** Pruebas automatizadas de nivel técnico. 
    **Ejemplos:**
    - Pruebas unitarias.
    - Pruebas de integración.
    - Verificación de API y recursos del sistema.  
        Estas pruebas son diseñadas para garantizar que cada componente del software funcione correctamente. Suelen ser rápidas y ejecutadas continuamente durante el desarrollo.

**Cuadrante 2 (Q2):**  
    **Objetivo:** Validación de funcionalidades.  
    **Tipo de pruebas:** Pruebas funcionales, automatizadas o manuales.  
    **Ejemplos:**    
    - Pruebas de aceptación.
    - Pruebas exploratorias.
    - Pruebas de rendimiento básico.  
        Estas pruebas aseguran que las características entregadas cumplen con las expectativas del cliente y con los requisitos definidos.
    
1. **Cuadrante 3 (Q3):**  
    **Objetivo:** Validación enfocada en el cliente.  
    **Tipo de pruebas:** Pruebas manuales, centradas en la experiencia del usuario.  
    **Ejemplos:**
    - Pruebas de usabilidad.
    - Pruebas alfa y beta.  
        Este cuadrante aborda aspectos subjetivos, como la facilidad de uso y la satisfacción del cliente con el producto.

1. **Cuadrante 4 (Q4):**  
    **Objetivo:** Verificación no funcional.  
    **Tipo de pruebas:** Automatizadas o mediante herramientas especializadas.  
    **Ejemplos:**
    - Pruebas de carga.
    - Pruebas de estrés.
    - Pruebas de seguridad.  
        Este cuadrante se enfoca en atributos de calidad del sistema, como rendimiento, escalabilidad y seguridad.

---
##### Propósito del Modelo:

- **Organización de las pruebas:** Ayuda a los equipos a identificar qué pruebas deben realizarse, por qué y cómo.
- **Equilibrio entre pruebas:** Se asegura que el producto sea funcional, técnicamente sólido y satisfactorio para los usuarios.
- **Colaboración:** Promueve la colaboración entre desarrolladores, testers y stakeholders al planificar estrategias de prueba.

Los Cuatro Cuadrantes no son rígidos, y las pruebas pueden adaptarse según las necesidades específicas de cada proyecto.
## 11. Herramientas de software para la realización de pruebas

**Pruebas en Visual Studio**
En Visual Studio se siguen los pasos siguientes:
- Se crea un proyecto partiendo de las plantillas de test disponibles
- Se crea un archivo de pruebas automatizando las opciones de testing. Los archivos de pruebas pueden tener extensión: `.runsettings`, `.testsettings`, `.testrunconfig`, `.vsmdi`
- Estructura de un archivo de pruebas: Se selecciona un tipo de lenguaje para su representación como puede ser XML. 

