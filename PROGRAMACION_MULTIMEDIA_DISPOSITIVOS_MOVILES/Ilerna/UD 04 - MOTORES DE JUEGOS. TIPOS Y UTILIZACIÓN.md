## 0. Concepto de videojuego. Origen de los videojuegos y primeros videojuegos

Se llama **videojuego** a un juego electrónico que se **visualiza** en una pantalla. 

**En los 70**
- Pong (1972)
- Breakout (1976)
- Space Invaders (1978)
**En los 80**
- Pac-Man (1980)
- Tetris (1984)
- Super Mario Bros (1985)
**Consola en casa**
- Sega: El auge de Genesis/Mega Drive
- Nintendo: La revolución con NES y Game Boy
- Sony: La entrada con PlayStation
**En los 90**
- Doom (1993)
- Final Fantasy VII (1997)
- The Legend of Zelda: Ocarina of Time (1998)
**La batalla entre XBOX, Sony & Nintendo**
- Xbox: Halo
- Sony: PlayStation 2
- Nintendo: Wii
**Aparición de los primeros videojuegos para móviles**
- Primer videojuego para móvil: Tetris(1994) para móviles MT-2000 Hagenuk
- Snake (1997) de Nokia. Posibilidad de jugar con un contrincante mediante infrarrojos.

	Estos primeros videojuegos:
	- Sientan las bases de los juegos para móviles, que mueven millones de dólares en el mundo
	- Pantalla monocroma
	- Poco consumo de recursos: No ocupaban mucho espacio, ni tenían grandes requerimientos de memoria ya que los móviles eran limitados (no smartphones)
	- Se distribuían con el propio Sistema Operativo. Posteriormente ya podían ser descargados pagando un sobrecoste. 
**Juegos en los 2000**
- World of Warcraft (2004)
- Grand Theft Auto: San Andreas (2004)
- Minecraft (2009)
**Juegos móviles en el auge de los smartphones**
- Angry Birds
- Candy Crush
- Importancia de las microtransacciones
**Juegos móviles en la actualidad**
- En los smartphones: Aumento de tamaño, calidad de pantallas, procesadores de última generación, consumo de streaming los sitúan a la altura de muchos PCs o videoconsolas incluyendo incluso realidad aumentada.
- Hay en torno a 383000 juegos en Google Play (15,34% de las apps de Google Play)

## 1. Motores de juegos: Tipos y utilización

Un **motor gráfico** o **motor de videojuego** es la representación gráfica de unas rutinas de programación concretas, las cuales ofrecen un diseño en un escenario gráfico en 2D o 3D. 

La **principal tarea de un motor gráfico** es proveer al juego de:
- un motor de renderizado para los gráficos 2D/3D
- motor físico o detector de colisiones
- sonidos
- scripts de programación
- animaciones
- IA
- gestión de memoria
- escenario gráfico

**Los motores suelen proporcionar**
- API y SDK para el desarrollo
- Algunos motores permiten crear juegos sin necesidad de escribir código. Tan solo debe hacerse uso de los mecanismos implementados y documentados en su API. Algunos requieren del uso de su propio lenguaje de programación
- Conjunto de herramientas de edición
- A pesar de no proporcionar conjuntos ya creados de elementos visuales, permiten su creación a través de herramientas de edición de software proporcionado.


**Ejemplos de motores de juegos**
- Source 2 -> Half-Life 2, Portal 2
- Unreal Engine 4 -> Batman Arkham Knight
- Unity 5 -> Pokemon GO, Among US
- Cryengine 3 -> Far Cry, Crysis, Ryse: Son of Rome
- UbiArt Framework -> Rayman Legends
- Game Maker -> Hotline Miami
- BuildBox -> Drag and drop game maker
- Stencyl -> Iniciación a la programación
- Ogre3D
- Doom Engine
- Gdevelop

>Ogre (open source), Doom Engine, Quaky Engine, Unity, CryEngine, Souce engine, Unreal engine, Game Maker


**Los motores gráficos en la creación de videojuegos**
El objetivo de los motores gráficos es trasladar las ideas creativas de los diseñadores a la pantalla, facilitando la plasmación gráfica del juego.

**Generación y manipulación de modelado 3D**
Unity puede importar archivos desde Maya (colocando archivo .mb .ma en la carpeta correspondiente del proyecto). Puede importar:
- Nodos con posición rotación y escala
- Meshes con colores de vértices, normales y hasta dos conjuntos de UV
- Materiales con Texture y color diffuse
- Animaciones Fk & KI
- Animaciones basadas en huesos
- BlendShapes
Al importar formatos en 3D se suele recurrir a formatos de archivo 3D importados (.obj) o archivos propios de la aplicación 3D como un archivo de blender (.blend). Ventaja: Solo se exportan los datos que se necesitan. También se puede importar mediante conversión de archivos como blender, cinema 4D, .ma, etc. Los archivos que se importen se almacenarán como assets de Unity, dividiéndose en otros assets. 
### 1.1. Clasificación de motores gráficos

##### Según las facilidades ofrecidas
- **Librerías gráficas**: Según sus facilidades para el desarrollo y uso. SDL, XNA, DirectX, OpenGL.
- **Motores**: Si el motor ya tiene un desarrollo visual completo o requiere scripts de programación para uso de elementos visuales. Por ej.: OGRE, Unreal o id Tech requieren uso de scripts de apoyo para la funcionalidad
- **Herramientas de creación especializadas**: Algunos motores se han desarrollado con carácter exclusivo orientados a su finalidad como pueden ser videojuegos u otros tipos. Por ej.: GameMaker o ShiVa son exclusivamente para desarrollo de juegos. En el caso de Unity puede usarse para diferentes géneros.

##### Según la licencia
- Motores **privados** (algunos con licencia gratuita)
- Motores **open source**

La elección de un determinado motor gráfico es muy subjetiva. La elección estará condicionada por el tipo de aplicación del juego a desarrollar y los recursos disponibles de los que se dispone para su desarrollo. 

## 2. Conceptos de animación 2D y 3D

Una **animación**: es el cambio en una o varias propiedades de un objeto que lo hacen ser visto con un aspecto distinto a lo largo del tiempo

La **base de creación de estas animaciones reside en la programación**. Android ofrece una serie de mecanismos dedicados a la creación de animaciones para objetos tanto 2D como 3D.

- **Canvas**: Plantilla que permite definir un control a nivel de interfaz de usuario en las aplicaciones. Puede suponer la representación de cualquier objeto como formas sencillas (óvalos, líneas, rectángulos, triángulos)

- **Animadores (Animators)**: Propiedad para añadir un objeto a una animación utilizando propiedades o estilos de programación

- **Dibujables animados (Drawable animation)**: Permite cargar una serie de recursos drawable para crear una animación mediante el uso de animaciones tradicionales (solapar una imagen detrás de otra como en películas animadas)

- **Open GL**: Es una librería para gráficos de alto rendimiento 2D y 3D. Android incluye soporte para su uso. 

## 3. Arquitectura del juego. Componentes

Al comenzar el desarrollo de un juego para plataforma móvil se debe definir cuál va a ser su arquitectura, que permitirá detallar cómo será la estructura de desarrollo de la aplicación.

**Bloques**
La estructura de desarrollo está formada por una serie de bloques con función específica en el juego.

- **Interfaz de usuario**: Recoge los eventos que el usuario ha creado
- **Lógica de juego**: Parte central del videojuego. Procesa los eventos del usuario y dibuja la escena del juego continuamente (game loop). Continuamente se comprueba el estado del juego y se dibuja una nueva interfaz para cada estado. En este bloque se controlan colisiones y sprites. Con el uso de librerías como OpenGL se modelan y diseñan los personajes dentro del juego. Con esta es posible generar animaciones en personajes utilizando sprites (imágenes con transferencia), esto se conoce como **renderizado de canvas**. Cada renderizado queda encapsulado en un **frame de animación**
- **Recursos utilizados**: En la lógica del juego también deben controlarse todos los efectos de sonido e imágenes. Este bloque es parte fundamental para el desarrollador ya que todas las funciones deben ser programadas y controladas a través de código. Los juegos consumen muchos recursos por lo que estos deben ser optimizados.
- **Framework Android**: Android es un framework potente que permite animar una gran cantidad de objetos de multitud de formas. Para ello cuenta, cuenta con diferentes mecanismos que ofrecen esta funcionalidad: Animación de propiedades, de vistas y de dibujables.
	- **Animación de propiedades (property animations)**: Definir propiedades del objeto para ser animado (duración de la animación, tiempo de interpolación, repetición de comportamiento o animaciones, agrupación de series de animaciones en forma secuencial, frames de actualización de una animación, etc.)
	- **Animación de vistas (view animations)**: Permite hacer uso de los diferentes mecanismos de animación de vistas (traslaciones, rotaciones, escalados,...). Con ellos se da la sensación de transformar una imagen en otra en determinado momento.
	- **Animación de dibujables (drawable animations**): Haciendo uso de los recursos drawable se pueden crear una serie de animaciones como si se tratase de una película.
- **Salida**: Sucesión de escenas que se actualizan en la interfaz de usuario. 

Los frames son procesados uno detrás de otro ofreciendo al usuario una sensaciónde continuo movimiento y animación. 

## 4. Ventajas de utilización de un motor de juegos. Librerías utilizadas según el área de especialización y lenguajes de programación

Los videojuegos pueden llegar a tener una gran complejidad tecnológica (emulan la realidad: reglas internas, leyes físicas, múltiples personajes, efectos de audio y vídeo, gráficos tridimensionales).
Los motores de juegos simplifican este proceso al proporcionar herramientas preconstruidas para resolver problemas comunes como renderizado, físicas, IA, optimización y compatibilidad. Esto permite a los desarrolladores enfocarse en la parte creativa del juego sin tener que reinventar lo ya inventado. 

**Motor de juego a utilizar según el lenguaje a programar**
Cuando se programa en Java o Kotlin una alternativa gratuita a nuestra disposición es LibGDX. Dispone de módulo de colisiones, renderizado, IA y es compatible con múltiples plataformas. 

Para programar en C# una buena opción es Unity por su gran difusión y facilidad de uso. 

Otra opción es Unreal Engine pero con una mayor curva de aprendizaje y programación en lenguaje C.

**Lenguaje a elegir según el juego**
- Los juegos 2D o plataformas que trabajan con sprites sencillos suelen estar realizados en C.
- Juegos con mayor complejidad gráfica como objetos tridimensionales se usa C++, C# y Java.

**Clasificación de librerías utilizadas segúnel área de especialización**
- **Renderizados y efectos**: OpenGL, Direct3D, GKS, PHIGS, PEX,...
- **Basados en gráficos de escena:** OpenGL Performer, Open Inventor, OpenGL Optimizer, PHIGS+,..
- **Librerías de herramientas gráficas**: World Toolkit, AVANGO, Games Engines

**Librerías**
- **Allegro**: Libre y de código abierto basada en lenguaje C. Permite uso de elementos gráficos, sonidos, dispositivos como teclado y ratón, imágenes,...
- **Gosu**: Desarrollo 2D. Basada en C++ y Ruby. De software libre bajo licencia del MIT.
- **SDL**: Diseño de elementos 2d. Software libre. Basada en C. Permite C++, C#, Basic, Ada, Java
- **libGDX**: Basada en Java. Orientada a aplicaciones multiplataforma.
- **LWJGL**: Juegos en lenguaje Java. Acceso a librerías como OpenGL.
- **Direct3D**: Conjunto de librerías multimedia. Gran competidor de OpenGL. Uso de elementos como líneas, puntos, polígonos. Gestión de texturas o transformaciones geométricas. Propiedad de Microsoft.

- **OpenGL**
	- OpenGL (Open Graphics Library) es una especificación de una API (Application Programming Interface) multiplataforma y de código abierto para el desarrollo de aplicaciones de gráficos en 2D y 3D.
	- Desarrollada por Khronos Group
	- Ampliamente usada en la industria del videojuego, visualización científica, simulación y otras áreas con gráficos en tiempo real
	- Proporciona una capa de abstracción entre el software y el hardware gráfico, que permite a los desarrolladores crear aplicaciones gráficas sin fijarse en las diferencias entre las arquitecturas de GPU y sistemas operativos
	- Ofrece una amplia gama de funciones para el control de primitivas geométricas, texturas, shaders, iluminación, transformaciones y otros aspectos de procesamiento gráfico
	- Es compatible con una amplia variedad de plataformas y dispositivos, desde ordenadores de sobremesa hasta dispositivos móviles
	- Se ha convertido en un estándar en el desarrollo de aplicaciones gráficas y es usado por numerosos motores gráficos, incluido Unity y otros motores de juego populares.

## 5. Componentes de un motor de juego

Un **motor de juego** es una parte fundamental del código de programación de un juego. Se encarga de la mayor parte de los aspectos gráficos del juego. Una de sus tareas es establecer la comunicación y aprovechar todos los recursos que una tarjeta gráfica ofrece. 

Recogen de forma global todos los elementos que aparecen en un juego. 

Los principales **componentes de un motor de juego** son:

- **Librerías**: Permiten representar figuras, polígonos, luces y sombras, etc.
- **Motor físico**: Es el encargado de realizar los cálculos necesarios para que un objeto simule tener atributos físicos como peso, volumen, estado físico, gravedad, etc.  Gestionar colisiones, animaciones, scripts de programación, sonidos, físicos (gravedad), etc. 
- **Motor de renderizado:** Encargado de renderizar todas las texturas de un mapa, los relieves, el suavizado de objetos, gravedad, el trazado de rayas.

  Es el encargado de mostrar las imágenes 2D o 3D en pantalla, así como de calcular algunos aspectos como los polígonos, la iluminación, difuminado, texturas, entre otros. Se basa en librerías para gráficos de alto rendimiento 2D y 3D y están implementadas a nivel de API. Algunas de las librerías más importantes son DirectX y OpenGL.

## 5.1. Recursos en un motor de juego

Cada uno de los elementos que aparecen en un juego forman parte de un conjunto de recursos del motor gráfico. 

- **Assets**: Representa todos los elementos o recursos que formarán parte de un juego: Modelos 3D, texturas, materiales, animaciones, sonidos, scripts,... 

- **Renderizado**: Todas las texturas y materiales de esta parte hacen uso de los recursos (assets) diseñados para el motor gráfico. Mostrará el aspecto visual y potencia del motor gráfico.

- **Sonidos**: Dentro del motor configurar cómo serán las pistas de audio del juego. El sonido del videojuego dependerá de la capacidad de procesamiento de estos sonidos. Algunas opciones configurables son: modificación del tono, repetición en bucle de sonidos (looping), etc.

- **Inteligencia Artificial**: Una de las características más importantes del motor de juego. Añadir estímulos al juego permitiendo que el desarrollo del mismo suceda en función de una toma de decisiones definida en base a una serie de reglas. Además define el comportamiento de todos los elementos del juego que no son controlados por el usuario.

- **Scripts visuales**: Son porciones de código (partes del juego) que pueden ejecutarse en tiempo real dentro del aspecto gráfico del juego.

- **Sombreados y luces:** El motor gráfico dota de colores y sombras a toda la escena del juego (a cada uno de los vértices que forman parte de la escena)

Algunos motores emplean técnicas que permiten renderizar los terrenos o materiales y que no consumen recursos, sino que aparecen dentro del espacio visual, **culling**.

## 5.2. Motor gráfico o de renderizado (2D/3D). Técnicas de animación 2D y 3D mediante motores

### 5.2.1. Animación 2D

Se necesitará el personaje 2D con imágenes de la animación separada en poses clave. (Personaje que salta, duerme, habla,... con varias imágenes para cada acción)

- **Sprites**  ("duendecillos).  Son imágenes, generalmente en formato bitmap o  mapa de bits, dibujados en la pantalla de ordenador por hardware gráfico especializado. Es un objeto gráfico 2D usado en videojuegos y aplicaciones de animación para representar personajes, elementos interactivos o efectos visuales.  Pueden moverse, rotarse, escalarse y animarse en la pantalla. Los sprites se almacenan en hojas de sprites, que son archivos de imagen que contienen múltiples elementos gráficos organizados en una cuadrícula. Al separar y manipular estas imágenes individualmente en tiempo real, los desarrolladores pueden crear animaciones y efectos visuales, mejorando la experiencia del usuario y la inmersión en el juego o aplicación. (Sprite es individual; Conjunto de sprites son muchas "imágenes")


- **Creación de animaciones**: Para crear una animación se puede usar un sprite que esté dividido en partes (conjunto de sprites), de forma que podamos cargar las que se necesiten para representar una imagen en movimiento lo más real posible o para crear un escenario tan grande como se quiera.
  La imagen se importa en el proyecto y se toman los elementos que se necesiten para representar el movimiento tanto en 2D como en 3D.
  También se puede usar un único sprite dividido en partes (cabeza por un lado, brazo por otro, etc.)
  También se puede recurrir a servicio freelance de diseño para videojuegos que diseñen el Sprite (Ej.: www.fiverr.com)

- **Procesos más importantes**
	- **División de animaciones**: Modelos de varios tiposd
		- Animaciones predivididas: Exportadas una a una, dividas con su nombre adecuado.
		- Animaciones sin dividir: Clip de duración extensa, puede definirse el rango de frames que se corresponde a cada secuencia de animación.

	- **Curvas de animación**: Permiten añadir datos adicionales a los fotogramas claves y se pueden conectar con clips importados desde (Animation import settings). Las curvas permiten hacer más suaves las transiciones de animaciones o agregar nuevos timing usando con más facilidad las leyes de la animación. 

	- **Estados de máquina**: Las acciones típicas están referenciados como states, el personaje que está en determinado estado realiza determinada acción. Puede pasar de un estado a otro debiendo tener State transitions. Todo eso forma la State machine. Para representar los estados se usa a veces un diagrama en el que los nodos representan los estados y las flechas las transiciones. Cada estado tendrá un motion que se reproducirá cuando la máquina esté en ese estado.
	- **Parámetros de animación en estados de máquina**: Los parámetros de animación están definidas dentro de un Animator controller en el que se pueden asignar valores de scripts. Los valores del parámetro se configuran en Parámetros de la ventana > Animator (Int, Float, Bool, Trigger que es un parámetro booleano que se reinicia cuando se realiza una transición). 
### 5.2.2. Animación 3D. MECANIM

Unity tiene el sistema MECANIM que permite la animación a objetos 3D. Tiene animation clips estructurados en el Animator controller, que permitirá crear animaciones de modelos 3D. Unity tiene también el sistema Avatar que permite otorgar características especiales a personajes humanoides. Estas funcionalidades se integran en el Animator component. 
- Los animator clip se importan o crean en Unity
- Se agregan en un Animator controller que se visualiza como un asset en la ventana del proyecto
- El personaje se integra con Avatar a través de un mapeo
- El personaje tendrá un componente animator adjunto para darle animación

## 5.2. Grafo de escena

El **grafo de escena** muestra una visión global de los elementos de la escena que forma parte del juego. En él se crean los elementos gráficos: fondos, árboles, rocas, nubes, ascensores, enemigos, portales,...
Tiene una barra de herramientas con opciones que ayudan en el diseño (como la opción 2D, opción 3D de las capas que componen la escena) 

La **escena** en este tema la entenderemos como un nivel del juego, de forma que se podrán crear y diseñar diferentes escenas y pasar de una a otra según el jugador avance en su aventura.
Los atributos de cada elemento de la escena se podrán modificar seleccionando desde el árbol de elementos o haciendo clic sobre el objeto visible en el grafo de escena. 

¡Ojo! en un juego 3D se puede por ejemplo modelas como sprites planos a ciertos elementos si se considera que pueden tener más ventajas. (En la coordenada Z, solapar elementos, dar profundidad)
## 5.3. Motor de físicas

El **motor de físicas** es el módulo responsable de calcular el movimiento y determinar la interacción natural de los elementos representados en una escena, teniendo en cuenta las leyes físicas. **Incluye al motor de colisiones**.

En Unity, el principal elemento de este módulo es el `rigidbody`. Este puede tener asociado un `collider` y tiene un objeto `transform` que permite definir la posición y el ángulo del elemento dentro de la escena. 

### 5.3.1. Detector de colisiones (motor de colisiones)

El **detector de colisiones** permitirá determinar los efectos que el juego debe sufrir ante una colisión. Está incluido dentro del motor de físicas. 
Esto Unity se hace añadiendo un elemento `collider` que tendrá la forma que se decida y acompañarán al elemento asociado.
Pueden darse tanto en 2D como en 3D.
El `collider` comunicará un evento de colisión siempre que choque con otro `collider`. Debe tenerse cuidado puesto que las matemáticas de cálculo de colisiones son complejas y, cuanto más elementos se encuentren en escena, el cálculo completo requerirá de un mayor tiempo para completarse.

### 5.3.2. El atributo `bodyType`

Desde código se pueden manipular los objetos `rigidbody` para mover los personajes dentro de la escena (`transform`) y sus `colliders` indicarán cuándo se toca. 
El `rigidbody`tiene un atributo `bodyType` que define su movimiento físico en la escena. Este puede tener tres valores:
- **Dynamic**:  Se mueve bajo estímulo y no cambiando directamente los valores de su `transform`. Es sensible a la gravedad y a las fuerzas de empuje que se le apliquen al elemento. Es el más común. Con un `collider` asociado detecta colisiones con todos los demás objetos. Se usa para el jugador principal, enemigos, cajas, etc.
- **Kinematic:** El programador especifica la posición y el movimiento. No se ven afectados por las leyes básicas de la física (no tienen atributos como masa o fuerza de rozamiento). Solo colisionan con otros ¿Kinematic?. Son más sencillos, necesitan menos recursos del sistema. Usados para puentes levadizos, puertas corredizas, rayos láser, etc.
- **Static:** No se moverán ante estímulos o colisiones. Se comportan como objetos inamovibles de masa infinita. Usado en paredes, muros, decoración del fondo, etc. ¿Solo colisionarán con objetos dynamic?

### 5.3.3. Otros componentes que mejoran las simulaciones físicas

- **Physics material**: Permite ajustar el índice de rozamiento y elasticidad de los componentes para que al verse arrastrados o colisionar tengan un comportamiento más realista.
- **Joints**: Permite unir diferentes objetos mediante una articulación para poder crear objetos complejos articulados.
- **Constant force**: Permite aplicar una fuerza constante a un objeto para que se vea empujado siguiendo la 2ª ley de Newton.
- **Effectors**: Permiten dirigir las fuerzas físicas de una forma personalizada cuando hay colisión entre objetos. Ej.: Saltar hacia plataformas atravesándolas pero luego quedarse en ellas sin volver a caer. Elementos de atracción o repulsión. Hacer que elementos floten. Cambiar la fuerza o el ángulo de la fuerza. 

## 5.4. Motor de inteligencia artificial

- Los motores de juegos contienen módulos de IA (que simulan por ejemplo el comportamiento de enemigos).
- Cada vez pueden desarrollarse aventuras gráficas más potentes, jugadores automáticos (nom-player characters) que actúan con propia personalidad. Gracias a miles de algoritmos de IA construidos por matemáticos y programadores durante décadas.
- Hoy cada vez más gracias al gran desarrollo de software, la IA está presente en casi todas partes. Sin embargo, aún siguen existiendo problemas relacionados con sentimientos, razón y ética en el ámbito de la inteligencia artificial.
- En **Unity se cuenta con machine learning que permite que los elementos aprendan a partir de los hechos**, haciéndose más inteligentes o más eficientes en sus tareas. 

Algunas características del módulo de IA de Unity son: 
- **Finite state machines y Behavior trees**: Permiten controlar el estado de los agentes inteligentes y sus acciones. Ej.: Enemigos pueden pasar a uno de los estados siguientes: haciendo ronda, persiguiendo jugador, disparando jugador. Al entrar en contacto con el jugador podría perseguirlo y, a más corta distancia, disparar.
- **Flocking**: Imitar la inteligencia de colmena o enjambre en los agentes automáticos. Movimiento conjunto pero descentralizado de agentes autoorganizados (abejas, hormigas, aves, rebaños). Describir el movimiento de ejércitos en una batalla, asemejándose al comportamiento natural.
- **Steering**: Algoritmos necesarios para que el agente se mueva dentro de una trayectoria preestablecidas. Ej.: Para que los agentes conduzcan dentro de un circuito de carreras, esquivándose mutuamente pero sin abandonarlo. 
- **Path finding y Navigation mesh**: Uso en los NPC. Los algoritmos de búsqueda de camino como A\* dan ruta más eficiente desde un punto a otro de un plano preestablecido (debe crearse un plano virtual para que el algoritmo realice los cálculos). Ej.: Calcular camino más rápido que debe tomar un enemigo para alcanzar a un jugador. Mediante Navigation mesh, una vez diseñada la escena con los obstáculos, no es necesario crear ningún mapa con base a ellos sino que Unity lo creará de forma automática y calculará las rutas necesarias de un punto a otro del plano. 
- **Machine learning**: Unity Machine Learning Agents Toolkit usa herramientas de redes neuronales para que los agentes aprendan de forma automática las tareas que se necesita que realicen. Esto requiere bastantes conocimientos sobre IA. 
## 5.5. Motor de sonidos

- El **motor de sonidos** permite el control de audio, sonido 3D, mezcladores de sonido en tiempo real y muchas más. 
- Soporta formatos AIFF, WAV, MP3, OGG
- Conseguir efectos de sonido es simple: Solo arrastrar archivos de sonido desde el explorador hasta el panel de proyecto. Unity lo convierte en un `audio clip` que puede ser arrastrado a un `audio source` o usado desde un script. 
- Para añadir música de ambiente: Unity permite importar archivos .xm, .mod, .it, .s3m como `tracker modules` que darán lugar a objetos `audio clip`

**Clases más útiles relativas al sonido**
- `Audio clip`: Datos de sonido (mono, estéreo o multicanal), usado directamente por audio source
- `Audio source`: Reproduce un `Audio clip` en escena mediante un `Audio listener` o un `Audio mixer`
- `Audio listener`: Actúa como un micrófono, obteniendo el sonido de un `Audio source` y lo emitiéndolo hacia los altavoces.
- `Audio mixer`: Procesamiento más complejo de sonido generado desde un `Audio source`. Puede llamarse desde este. 

**Ejemplo**
- **Audio Clip:** Archivo de audio asignado al **Audio Source**.
- **Audio Source:** Reproduce el audio configurado y puede ser controlado en el script.
- **Audio Listener:** Captura el sonido en la posición de la cámara para que el jugador lo escuche.
- **Audio Mixer:** Permite controlar el volumen, añadir efectos y mezclar varios sonidos.

Controlar la reproducción del audio con las teclas:
- **P** para reproducir.
- **S** para detener.
- **Flechas Arriba y Abajo** para ajustar el volumen.

```csharp
using UnityEngine;
using UnityEngine.Audio;

public class AudioExample : MonoBehaviour
{
    public AudioSource audioSource; // Asigna el Audio Source en el Inspector
    public AudioMixer audioMixer;   // Asigna el Audio Mixer en el Inspector

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.P))
        {
            if (!audioSource.isPlaying)
            {
                audioSource.Play();
                Debug.Log("Audio started playing");
            }
        }

        if (Input.GetKeyDown(KeyCode.S))
        {
            audioSource.Stop();
            Debug.Log("Audio stopped");
        }

        if (Input.GetKeyDown(KeyCode.UpArrow))
        {
            SetVolume(1.0f); // Sube el volumen
        }

        if (Input.GetKeyDown(KeyCode.DownArrow))
        {
            SetVolume(0.1f); // Baja el volumen
        }
    }

    public void SetVolume(float volume)
    {
        // Cambia el volumen del Audio Mixer
        audioMixer.SetFloat("MasterVolume", Mathf.Log10(volume) * 20);
        Debug.Log($"Volume set to: {volume}");
    }
}

```
## 5.6. Gestión de redes

Normalmente se utilizará un servidor central que controlará las sesiones del juego y dispondrá el mundo virtual que todos los jugadores podrán compartir. El estado de cada elemento será sincronizado entre todos. 
Todo este proceso (comunicaciones, sincronización del estado, control de sesión) es bastante complejo. Unity pone a disposición dos tipos de API para el desarrollo de videojuegos en red: Una de alto nivel y otra de bajo nivel que requiere de mayores conocimientos.

La API de alto nivel requiere:
- Controlar el estado del juego usando un network manager
- Desarrollo de juegos albergados en el propio cliente, en lugar de usar un servidor central en Internet
- Serializadores de datos para facilitar la comunicación de nuestros objetos de juego
- Envio y recepción de mensajes a través de la red entre clientes
- Envío de comandos desde los clientes al servidor
- Llamadas a procedimientos remotos (RPC) de servidor a clientes
- Envío de eventos desde servidor a clientes

## 6. Librerías que proporcionan las funciones básicas de un motor 2D/3D 

El funcionamiento de este tipo de librerías consiste en tratar de aceptar como entrada una serie de primitivas: líneas, puntos, polígonos y convertirlas en píxeles.

OpenGL actualmente tiene versión 4. A partir de la versión 3, tiene su propio lenguaje de renderizado (GLSL). 

Direct 3D ofrece una API 3D debajo nivel en la que se pueden encontrar elementos básicos (sistemas de coordenadas, transformaciones, polígonos, puntos y rectas). 

## 7. Estudio de juegos existentes

Es recomendable hacer un **estudio de mercado** antes del desarrollo, centrando la atención en juegos de carácter similar al que se va a crear.
Si va a ser publicado en internet es importante saber **a qué tipo de público está destinado**. Conocer las **limitaciones de desarrollo** y mediar la **cantidad de recursos necesarios** para su creación, desarrollo y publicación,
## 8. Aplicación de modificaciones sobre juegos existentes

- Los **juegos Android** ocupan el mayor porcentaje de descarga de aplicaciones relacionadas con el ocio.
- El ritmo de vida en sociedad obliga a los equipos a renovarse continuamente para conseguir que los juegos se adapten a los nuevos tiempos. 
- Los juegos no suelen ser de código abierto por lo que no suele poderse añadir de forma legal modificaciones al juego si no se forma parte del equipo de desarrollo o se es el autor de uno de ellos. 
- Al publicar un juego en Internet en plataformas como Google Play, se adquiere un compromiso de mantenimiento con esa aplicación por el que los desarrolladores deben corregir todos aquellos errores que se detecten tanto por parte de los usuarios como de los propios desarrolladores. 
