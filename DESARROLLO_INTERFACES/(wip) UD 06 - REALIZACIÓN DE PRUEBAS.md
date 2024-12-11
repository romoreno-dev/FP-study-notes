
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


## 8. Pruebas de aceptación


## 9. Pruebas alfa y beta


## 10 Pruebas manuales y automáticas


## 11. Herramientas de software para la realización de pruebas



