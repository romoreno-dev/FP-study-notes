
## Primera idea de la arquitectura hexagonal 

Busca llevar el concepto de **Clean architecture** a su máxima expresión.

La arquitectura hexagonal busca separar un proyecto en tres componentes principales:
- **Infraestructura** `infraestructure`: (Externa)
- **Aplicación** `application`: (Media, Comunicación)
- **Dominios:** `domain` (Interna). Todo lo que es propio. 

Se conoce también como arquitectura de **puertos** y **adaptadores** por ser esta la forma de comunicación de las capas **desde el dominio hacia la infraestructura**. 
Es una de las arquitecturas más complejas de interpretar. No en todos los proyectos es necesario implementarla. Debe usarse cuando:
- 1.- Tenemos una lógica de negocio propia muy compleja
- 2.- Necesitamos mucha escalabilidad
- 3.- Necesitamos hacer testing; necesitamos garantía de que lo que implementamos está bien implementado. 

En la arquitectura hexagonal debe buscarse:
> Que el dominio esté limpio de cualquier dependencia o framework. Solo entidades, lógica de negocio, servicios complejos (Azure, AWS), cálculos, dependencias con las bases de datos...
> Libera de cualquier dependencia externa, de cualquier cosa que no sea creada por uno. 

Muy recomendable la **modularización** (subproyectos dentro del proyecto principal), lo que ayuda a respetar la arquitectura hexagonal cuidando dependencias. 

- **infraestructure**: Contiene las externalidades (API, BBDD). Además en ella se exponen los servicios. 
	- **rest**: Servicios que van a exponerse (`@RestController`). El controlador debe estar completamente limpio. El control de excepciones debe delegarse a quien competa. 
		- controller:
		- advice:  `@ControllerAdvice`  `@ExceptionHandler`
	- **adapter**: Entidades externas (Azure, AWS, JPA...) ¡Ojo JPA es una externalidad, no puede estar en la lógica de dominio!
		- entity
		- exception
		- mapper
		- repository
- **application**: Capa comunicadora que comunica la infraestructura con el dominio.
	- **usecases**: Determina la interfaz de la lógica de negocio. qué es lo que va a hacer, cómo lo va a hacer. (`UseService`)
	- **service**: Se implementa la lógica de negocio para que se comunique con el dominio. (Implementa los `usecases`) (`UserManagementService` )
- **domain**: 
	- **port**: 
	-  **model**:
		- **constant**
		- **dto** 
	- **service**: 

---
Si en un futuro quisiera migrar JPA a un microservicio podría seguir utilizandolo todo igual ya que quitaría esa parte de la infraestructura y application seguiría comunicándose a través de su puerto. 

---

El dominio tiene una interfaz que se comunica con los puertos (del puerto hacia el adapter) y llama a la implementación de la BBDD. 

Ej.: En `TaskManagementService` que implementa `TaskService` se inyecta `TaskAudioPort` que es implementada en el adapter `AwsAudioService` (aquí sí se puede enfatizar la tecnología que se usa). (Se comunicará con AWS... y se implementará toda la lógica que se necesita para trabajar con AWS). 


**controller** llama al **usecase** que es implementado por el **service**. En él se hace lógica de negocio, se hace las transformaciones de datos necesarias...  Dentro de él se inyecta el **port** que es implementada en el **adapter**. También se inyecta el **mapper**.
La capa de **domain** tiene las entidades del dominio (la que hace la lógica de negocio). 
Al trabajar en JPA se tendrá como espejo una clase del `domain` (¡¡Las anotaciones JPA no deben estar en la capa de `domain`!!)

(Le gusta más tener la implementación de los servicios en el dominio. Parecido a arquitectura por capas, patrón facade. 

Si crece mucho se pueden usar servicios dentro del dominio (mucho más complejos)- 
El uso del mapeo de datos. (UserEntity yo Domain). Esto no está en el dominio sino en la infraerstructura. 

Mapeo de una entidad de dominio a una entidad de infrarstructuras (`TaskSpringJpaAdapter`., implementa `TaskPersistencePort`). 

La lógica debe ser viva. No tener que estar comentando la tecnología en todas partes. Que sea autodescriptivo. 


**Test**
- Test unitarios en dominio
- Test de integración en infraestructura

---

Domain centry: El dominio está libre de cualquier externalidad.
DDD (Domain Driven Development)

----

## Arquitectura hexagonal más completa

**PRIMERO**: Separar el proyecto internamente en forma modular para evitar que un desarrollador lo pueda romper.

Ej.: En el `domain` no debe haber ningún framework. Si coge alguien y en el `domain` pone `@Service`, dependencia de Spring Boot, podría hacerlo. Pero si separa en módulos, no. Porque eso obligaría al desarrollador a instalar la dependencia ahí. 

Cada uno tendrá su pom y manejará sus dependencias:

**infraestructure**: Accesos a BBDD y dependencias de Spring
```xml

<!--Dependencia del domain-->
<!--Dependencia de aplication-->

<dependency>
	<groupId>com.h2database</groupId>
	<artifactId>h2</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-web</artifactId>
</dependency>
<dependency>
	<groupId>ccom.fasterxml.jackson.core</groupId>
	<artifactId>jackson-annotations</artifactId>
</dependency>
```

**application**: 
```xml
//Dependencia del domain

<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-context</artifactId>
	<optional>true</optional>
</dependency>
<dependency>
	<groupId>org.projectlombok</groupId>
	<artifactId>lombok</artifactId>
	<version>${lombok.version}$/version>
	<scope>compile</scope>
</dependency>
```


**domain**: Sin librerías, ni dependencias. Solo Lombok
```xml
<dependency>
	<groupId>org.projectlombok</groupId>
	<artifactId>lombok</artifactId>
	<version>${lombok.version}$/version>
	<scope>compile</scope>
</dependency>
```

----------------------
---------

**Patrones**
- Patrón repository. Obtener y separar los cambios de estado de la app en un caso de diseño aparte.

- Patrón Dao. Algo que requiera obtención de datos.

- Patrón CQRS. Separar entrada a software en dos puntos:
	- Todo lo que son cambios de estado en la app
	- Todo lo que es obtención de datos o información

	 Dos paquetes en la application:
		 - commands. `TaskCreateHandler`. Comunica entre la infraestructura y el dominio. Crear va al servicio de creación `TaskCreateService` en el domain. `TaskSuperComplexService`, segmentar servicio muy complejo aparte. 
		 - queries

		`model`, `port`, `service`.


- Patrón ValueObject. Busca volver los valores un objeto. En lógica de negocio muy compleja se busca validaciones. Tantas validaciones que al final provocan que la clase crezca demasiado (¡ojo! no deberían estar en un servicio; cada clase debe ser responsable de sí misma; una tarea debería  validar su lógica y responsabilizarse de sí misma y no delegarla en un servicio )
- id -- TaskId
- name -- TaskName
- description -- TaskDescription
- ....

---
----

En servicios muy transaccionales en los que no es necesario hacer ninguna lógica. El handler ayuda a no tener que ir directamente a crear un servicio que no hace nada. (hadler --> servicio --> infraestructura)
(handler --> dao --> infrestructura)


------------
----------

**¿Por qué debe crearse un bean configuration en infraestructure?**

- **application**: 
- **bootloader**: Clase name para poderse ejecutar. 
- **domain**: 
- **infraestructure**: 


----
-----

El código debe ser estructurado para que el desarrollador lea lo que necesita. Entienda lo que necesita, sin obligar a nadie a leer todo el fragmento del código si no lo necesita. 