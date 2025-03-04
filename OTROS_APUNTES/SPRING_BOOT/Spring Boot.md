
## h2

```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```


La entidad se puede definir sin problemas

La **precarga de los inserts** se hace a partir del fichero `src/main/resource/data.sql`

En `application.properties`: 

```
# Configurar H2 en memoria
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=password
spring.sql.init.platform=h2
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect

# Crear tablas automáticamente
spring.jpa.hibernate.ddl-auto=update

# Habilitar consola H2
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
```

- **none**: No realiza ninguna acción sobre la base de datos. (Debes crear las tablas manualmente).
- **validate**: Verifica que el esquema de la base de datos coincida con las entidades de JPA, pero no lo modifica. Si hay diferencias, lanza un error.
- **update**:Modifica la base de datos solo para agregar o actualizar columnas, pero sin eliminar tablas o datos existentes.
- **create**: Crea todas las tablas en cada arranque de la aplicación, pero elimina los datos previos.
- **create-drop:** Igual que create, pero elimina todas las tablas al cerrar la aplicación.


---


Los **volúmenes nombrados** son gestionados por Docker y no dependen de la ubicación en el sistema de archivos del host. Docker se encarga de gestionar el ciclo de vida del volumen y puede mover los datos de manera transparente entre contenedores.+


