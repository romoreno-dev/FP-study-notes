(UF4 Comunicación asíncrona cliente-servidor)
## 1. Mecanismos de comunicación asíncrona

**AJAX** (_**A**synchronous **J**avaScript **A**nd **X**ML_, JavaScript asíncrono y XML) es una técnica de desarrollo web que permite comunicar el navegador del usuario con el servidor, en un segundo plano. Es una tecnología que existe desde el año 2005 y se considera un conjunto de diferentes tecnologías unidos con el objetivo de:
- **Conseguir una presentación basada en estándares** utilizando XHTML, CSS y diferentes técnicas de DOM que permitan mostrar la información de forma dinámica. 
- **Intercambiar y manipular los datos** usando **XML** y **XSLT**.
- **Recuperar los datos de forma asíncrona** usando **XMLHTTPRequest**
- **Usar JavaScript** para unificar todos los componentes.

**Tecnologías más importantes que forman AJAX**
- **XHTML y CSS**: Representación basada en estándares
- **DOM**: Interacción y manipulación dinámica de la presentación
- **XML, XSLT y JSON**: Intercambio y manipulación de información
- **XMLHttpRequest**: Intercambio asíncrono de información
- **JavaScript**: Unifica a todos los componentes anteriores

La mayor parte de las acciones del usuario se producen en la interfaz, disparando solicitudes HTTP al servidor web. Este recopila la información y devuelve una página HTML al cliente en cuestión. Cuando se realizan peticiones al servidor, el usuario no puede hacer otra cosa que esperar ya que la página cambia a otra distinta y hasta no mostrar el resultado el usuario no podrá interactuar con el navegador. 
AJAX pretende evitar esas esperas para que el cliente pueda realizar solicitudes al servidor mientras que el navegador sigue mostrando la misma página web. 
Incontables empresas usan AJAX como Google (Gmail, Google Suggest, Google Maps).

**Ventajas**
- Basado en estándares abiertos, su usabilidad
- Válido en cualquier plataforma o navegador
- Cuenta con beneficios aplicables a las páginas webs: compatible con flash, la base de web 2.0, etc. 

## 2. Comunicación asíncrona

Las aplicaciones AJAX eliminan las esperas y bloqueos producidos en el cliente: El usuario puede seguir actuando con la página web mientras realiza la petición al servidor haciendo uso del motor AJAX. 

El motor AJAX se encarga de llevar a cabo la gestión de las peticiones AJAX del usuario además de comunicarse con el servidor. Este motor permite que la interacción se realice de forma asíncrona **para que el usuario no necesite estar pendiente del indicador de carga del navegador**. 
## 3. Objetos relacionados. Propiedades y métodos de los objetos

Debe crearse un objeto de tipo `XMLHttpRequest` que permitirá llevar a cabo las modificaciones en segundo plano.

**Métodos del objeto XMLHttpRequest**

| Método                                        | Descripción                                                                                                                                       |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `abort()`                                     | Cancela la solicitud actual                                                                                                                       |
| `getAllResponseHeaders()`                     | Devuelve todos los headers                                                                                                                        |
| `getResponseHeader(header)`                   | Devuelve la información de un header concreto                                                                                                     |
| `open(method, url, async, usuario, password)` | Especifica el método HTTP de solicitud, la URL, si la solicitud debe solicitarse de forma asíncrona y otros atributos opcionales de la solicitud. |
| `send(datos)`                                 | Envía la solicitud al servidor. Si se usa el método POST se manda el cuerpo de la petición en "datos", si no, se manda null                       |
| `setRequestHeader(header, value)`             | Añade headers en pares clave-valor                                                                                                                |

**Atributos del objeto XMLHttpRequest**

| Atributo       | Descripción                                   |
| -------------- | --------------------------------------------- |
| `readyState`   | Devuelve el estado del objeto                 |
| `responseBody` | Devuelve la respuesta como array de bytes     |
| `responseText` | Devuelve la respuesta como cadena de texto    |
| `responseXML`  | Devuelve la respuesta como XML                |
| `status`       | Devuelve el estado en formato número          |
| `statusText`   | Devuelve el estado en formato cadena de texto |

**XMLHttpRequest**

```javascript
//////////////////////////////////////////////////
////////////////////
////////FUNCIÓN CROSS-BROWSER PARA CREAR OBJETO
XMLHTTPRequest////////
//////////////////////////////////////////////////
////////////////////
function objetoXHR(){
if(window.XMLHTTPRequest){
//El navegador implementa la interfaz XHR
de forma nativa
return new XMLHTTPRequest();
}else if(window.ActiveXObject){
var versionesIE = new Array(‘MsXML2.XMLHTTP.
5.0’, ‘MsXML2.XMLHTTP.4.0’,’MsXML2.XMLHTTP.
3.0’,’MsXML2.XMLHTTP’, ‘Microsoft.XMLHTTP’);
for(var i = 0; i < versionesIE.length;
i++){
try{
/* Se intenta crear el objeto en
Internet Explorer comenzando en la versión más moderna
del objeto hasta la primera versión.
En el momento que se consiga
crear el objeto, saldrá del bucle devolviendo el
nuevo objeto creado.
*/
return new ActiveXObject(versionesIE[
i]);
}catch(errorControlado){} //Capturamos
el error
}
}
/*
Si llegamos aquí es porque el navegador no posee
ninguna forma de crear el objeto.
Emitimos un mensaje de error usando el objeto
Error.
Más información sobre gestión de errores en:
http://www.javascriptkit.com/javatutors/trycatch2.
sHTML
*/
throw new Error(“No se pudo crear el objeto
XMLHTTPRequest”);
}
//Para crear un objeto XHR lo podremos hacer con
la siguiente llamada.
var objetoAjax = new objetoXHR();
```

## 4. Modificación dinámica del documento utilizando comunicación asíncrona

#### El problema de la asincronía
 
Si se realiza una llamada con `XMLHttpRequest`, el navegador puede continuar ejecutando las instrucciones que vienen a continuación sin esperar a que finalice la solicitud. 

```javascript
function cargarAsync() {
    let miXHR = new XMLHttpRequest();
    miXHR.open("GET", "datos.txt", true); // true = asíncrono
    miXHR.send(); // Se envía la solicitud

    console.log(miXHR.responseText); // ❌ Aquí aún NO hay respuesta
}
```

#### La solución

Cuando se realiza una petición asíncrona, esta pasa por una serie de estados (del 0 al 4, en la propiedad `readyState` del objeto XHR).
También es conveniente evaluar el estado devuelto por el servidor. Si el valor de status es OK, se pueden comprobar los datos que ha devuelto la petición en la propiedad `responseText` o `responseXML` correspondiente al objeto XHR. 

```javascript
function cargarAsync() {
    let miXHR = new XMLHttpRequest();
    miXHR.open("GET", "datos.txt", true); // Modo asíncrono
    miXHR.onreadystatechange = function () {
        if (miXHR.readyState === 4 && miXHR.status === 200) {
            document.getElementById("texto").innerHTML = miXHR.responseText;
        }
    };
    miXHR.send(); // Enviamos la solicitud
}
```

### 4.1. Estados de una solicitud asíncrona

La propiedad `readyState` de un objeto `XMLHttpRequest` puede tener los siguientes valores:

| Valor | Estado               | Descripción                                                                              |
| ----- | -------------------- | ---------------------------------------------------------------------------------------- |
| `0`   | **UNSENT**           | El objeto `XMLHttpRequest` ha sido creado, pero aún no se ha llamado al método `open()`. |
| `1`   | **OPENED**           | Se ha llamado a `open()`, pero aún no se ha enviado la solicitud (`send()`).             |
| `2`   | **HEADERS_RECEIVED** | La solicitud ha sido enviada (`send()`) y el servidor ha respondido con los encabezados. |
| `3`   | **LOADING**          | El servidor está enviando la respuesta y el navegador la está recibiendo parcialmente.   |
| `4`   | **DONE**             | La operación está completa y la respuesta está lista para ser procesada.                 |

## 5. Formatos para el envío y la recepción de información

**Formato de la información**

Al crear aplicaciones basadas en AJAX es importante considerar el formato de intercambio de datos que se utilizará. El objeto XHR permite intercambiar información con el servidor en cualquier formato (XML, HTML, JSON, Texto, Datos binarios, Form Data)

**Petición XML**

XML es uno de los formatos más conocidos y usados a la hora de intercambiar información. (¡¡Hace mil años porque hoy en día se usa JSON!!).
La petición del recurso devuelve respuesta en formato XML que puede leerse con propiedades de lectura como `responseXML`. Así se puede realizar el tratamiento del documento XML de forma sencilla. Se obtiene un objeto DOM de forma directa sin que sea necesario procesar una cadena de texto para que lo genere. 

**JSON (JavaScript Object Notation)**
El organismo de normalización IETF (Internet Engineering Task Force) compila en el documento RFC 4627 las distintas especificaciones de JSON (JavaScript Object Notation). Es también conocido por las siglas IETF y usa una sintaxis parecida a la usada por JavaScript.

JSON cuanta con la serialización (marshalling) consistente en codificar un objeto en un medio de almacenamiento (buffer o archivo) para transmitirlo por la red como una serie de bytes o en formato XML o JSON entre otros. (¡¡¡XML también tiene esto!!!)

Ventajas:
- Posibilidad de **almacenar el objeto en memoria o en un archivo determinado** para simplificar su transmisión en la red
- **Popular**, **sencillo**, **legible**,**rápido de procesar**.
- Permite representar la información haciendo uso de una **serie de predefinida de tipos primitivos** (cadena, numérico, booleano, nulo) **junto con dos tipos estructurados** de datos (objeto: parejas de tipo clave-valor en el que la clave se corresponde con una cadena de caracteres; array: hace referencia a una secuencia ordenada desde 0 hasta n elementos)
- La **forma de crear un objeto en formato JSON es parecida a la que tiene JavaScrip**t con la diferencia de que a la hora de acotar JSON utiliza comillas dobles del par clave-valor.
- Además puede disponerse de una** serie de librerías que ayudan en el proceso de formateo de objetos mediante la sintaxis de JSON**. 

**FormData**

Se encuentra recogido en la especificación XMLHttpRequest Level 2 y permite establecer un conjunto de pares clave-valor para que se puedan enviar una serie de datos complejos cuando se realicen distintas peticiones.

Su objetivo es el envío de los datos más allá de que sean entendidos como valores simples. Por ejemplo, en el caso de los archivos.

FormData permite convertir un formulario de una página web en un objeto FormData utilizando el mètodo `getFormData()`. Así puede enviarse toda la información sin necesidad de recurrir a cada uno de los elementos de forma particular para enviarlos mediante `send`

Veamos un ejemplito en JavaScript antiguo
```javascript
var formulario = document.getElementById(“miFormulario”);
var xhr = new XMLHttpRequest();
xhr.open(“POST”,”index.aspx”);
xhr.send(formulario.getFormData());
```

Veamos un **ejemplito** en JavaScript moderno:
```javascript
document.getElementById("miFormulario").addEventListener("submit", function(event) {
    event.preventDefault(); // Evita el envío normal del formulario

    const form = event.target;  // Referencia al formulario
    const formData = new FormData(form);  // Convierte el formulario en un objeto FormData

    // Ver los datos en consola
    for (let [key, value] of formData.entries()) {
        console.log(key, value);
    }

    // Enviar la solicitud mediante fetch()
    fetch("https://ejemplo.com/api/enviar", {
        method: "POST",
        body: formData
    })
    .then(response => response.json())
    .then(data => console.log("Respuesta del servidor:", data))
    .catch(error => console.error("Error:", error));
});
```

La petición se vería así:
```
POST /api/enviar HTTP/1.1
Host: ejemplo.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryXyz123
Content-Length: 678
Connection: keep-alive

------WebKitFormBoundaryXyz123
Content-Disposition: form-data; name="nombre"

Juan
------WebKitFormBoundaryXyz123
Content-Disposition: form-data; name="email"

juan@example.com
------WebKitFormBoundaryXyz123
Content-Disposition: form-data; name="archivo"; filename="documento.pdf"
Content-Type: application/pdf

(binary data)
------WebKitFormBoundaryXyz123--
```

- `Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryXyz123`: Indica que los datos se envían en formato `multipart/form-data`, separando las partes con el **boundary** (`----WebKitFormBoundaryXyz123`).
- Cada campo del formulario (`nombre`, `email`, `archivo`) se separa con el **boundary**.
- Cada parte tiene una **cabecera interna** con `Content-Disposition`, especificando el nombre del campo y el contenido.
- En el caso del archivo, se indica también su nombre y tipo (`Content-Type: application/pdf`).
- El contenido del archivo se envía en **binario**, sin codificación de texto.

Ejemplifiquemos qué pasa al llegar a una API de Spring Boot:
```java
@PostMapping("/enviar")
    public ResponseEntity<String> handleFormUpload(
            @RequestParam("nombre") String nombre,
            @RequestParam("email") String email,
            @RequestParam("archivo") MultipartFile archivo) {
    // Si no hay archivo llegará un multipart/form-data pero no se usa MultipartFile obviamente... 
    // RequestParam MultipartFile (Formulario estándar y archivos parte de el)
    // RequestPart MutiparFile  (JSON + archivos en la misma solicitud)

        // Imprimir los datos del formulario
        System.out.println("Nombre: " + nombre);
        System.out.println("Email: " + email);
        System.out.println("Archivo recibido: " + archivo.getOriginalFilename());

        // Guardar el archivo en una carpeta temporal (opcional)
        try {
            File file = new File("uploads/" + archivo.getOriginalFilename());
            archivo.transferTo(file);
        } catch (IOException e) {
            return ResponseEntity.badRequest().body("Error al guardar el archivo");
        }

        return ResponseEntity.ok("Datos recibidos correctamente");
    }
}
```


**Binario**
El envío de información en binario se emplea también cuando la información consiste en archivos o imágenes en formato distinto a XML o no estructurado. 

**Envío de parámetros**
- **GET**: En caso de que sea necesaria se utilizan parámetros incluidos en la cabecera `queryString` (URL) de la petición correspondiente.
- **POST**: Se envían parámetros a través de POST en el método `send(...). 
- **JSON**: JSON debe formatear los objetos o información que se desee enviar. Se pueden utilizar formateadores como el método `JSON.stringify`

## 6. Librerías de actualización dinámica

La programación con AJAX es uno de los pilares de lo que se conoce como **web 2.0**. Se incluyen aquí las diferentes aplicaciones web que permiten facilitar que se comporta información, interoperabilidad, diseño que está centrado en el usuario y la colaboración web. Ejemplos.: Redes sociales, alojamiento de vídeos, blogs y wikis. 

Esta necesidad ha hecho que se desarrollen gran cantidad de herramientas y frameworks para el desarrollo web empleando JavaScript, HTML, AJAX,... ahorrando tiempo y código en las diferentes aplicaciones. 

Puede llegarse a hacer peticiones con una sola instrucción de código sin preocuparse de crear objetos XHR, gestionar códigos de respuesta, estados, con compatibilidad entre distintos ordenadores (**crossbrowser**) de forma que la propia librería puede crear una petición AJAX según el tipo de navegador que se use, etc. 


En 2008, Google consiguió liberar su **API de librerías AJAX** con la que se eliminan las distintas dificultades que se encontraban a la hora de desarrollar mashups (combinación de diferentes fuentes de datos, servicios o aplicaciones para crear un producto) en JavaScript.
A través de dicha API es posible acceder a librerías open source realizadas con JavaScript como jQuery, Prototype, Scriptaculous, MooTols, Dojo, SWFObject, Chrome-frame, Webfont,...
Los scripts son accesibles mediante descargas o método `google.load()`

**jQuery**
- jQuery permite **simplificar las tareas de programación en JavaScript** incorporando una infraestructura que permite crear aplicaciones complejas en la parte del cliente.
- Se basa en la filosofía de "**escribir menos y producir más**"
- Con esta librería se pueden crear **interfaces de usuario**, utilizar **efectos** dinámicos, **AJAX**, **acceder al DOM**
- Posee **plugins** que permiten realizar presentaciones con imágenes, validaciones de formularios, menús dinámicos, etc.
- Es **gratuita** y puede usarse **en cualquier plataforma personal o comercial.** Una vez cargada la librería queda almacenada en caché para que el resto de las páginas la puedan usar. 


**Función `$.AJAX()` en jQuery**

Es equivalente a los métodos empleados en JavaScript vanilla.
La instrucción extensa ya que tiene gran cantidad de opciones. 

```javascript
$.AJAX({
url: [URL],
type: [GET/POST],
success: [function callback exito(data)],
error: [function callback error],
ifModified: [bool comprobar E-Tag],
data: [mapa datos GET/POST],
async: [bool que nos indica sincronia/asincronia]
});

$.ajax({
  url: 'https://jsonplaceholder.typicode.com/posts',  // URL de la API
  type: 'GET',  // Solicitud GET
  success: function(data) {
    console.log('Datos recibidos:', data);
  },
  error: function(xhr, status, error) {
    console.log('Error al cargar datos:', error);
  }
});
```

Como es una función tediosa, existen otras funciones de más alto nivel para facilitar el proceso y poder gestionar las respuestas obtenidas. 

**Método .load()**
Método más sencillo de jQuery para obtener datos del servidor y luego insertar el contenido de la respuesta directamente en un elemento del DOM.
```javascript
$(selector).load( url, [datos], [callback] )
```

**Función $.post()**
Llevar a cabo peticiones AJAX al servidor usando método POST
```javascript
$.post( url, [datos], [callback], [tipo] )
```

**Función $.get() y $.getJSON()**
Llevar a cabo peticiones AJAX usando el método GET. Al recibir los datos en JSON puede emplearse `getJSON` en su lugar. 

```javascript
//$.get()
$.get( url, [datos], [callback], [tipo] )
//$.getJSON()
$.getJSON( url, [datos], [callback], [tipo] )
```


### Ejemplito de AJAX con JQuery


```javascript
    /* Variables Javascript que guardan las direcciones (ContextPath) a las que se harán las peticiones
    * AJAX en cada caso */

    /* Para protocolo HTTP (Puerto 8080)*/
    var contextPath = "http://localhost/buscarPorProvincia"
    var contextPath2 = "http://localhost//buscarPorMunicipio"
    var contextPath3 = "http://localhost//buscarPorTipo"

            /* Buscar municipios segun provincia seleccionada */
            $('#provincia').change(
                    function () {
                      $.getJSON(contextPath,
                              {
                                provincia: $(this).val(),
                              },
                              function (data) {
                                var html = '<option value="">Seleccione municipio</option>';
                                var len = data.length;
                                for (var i = 0; i < len; i++) {
                                  html += '<option value="' + data[i] + '">'
                                          + data[i]
                                          + '</option>';
                                }
                                html += '</option>';
                                $('#municipio').html(html);
                              });
                    });

    /* Buscar centro según municipio seleccionado */
    $('#municipio').change(
            function () {
              $.getJSON(contextPath2,
                      {
                        municipio: $(this).val(),
                      },
                      function (data) {
                        var html = '<option value="">Seleccione tipo de centro</option>';
                        var len = data.length;
                        for (var i = 0; i < len; i++) {
                          html += '<option value="' + data[i].tipo + '">'
                                  + data[i].tipo
                                  + '</option>';
                        }
                        html += '</option>';
                        $('#tipo').html(html);
                      });
            });

    /* Buscar centro educativo según tipo seleccionado */
    $('#tipo').change(
            function () {
              $.getJSON(contextPath3,
                      {
                        municipio: $('#municipio').val(),
                        tipo: $(this).val(),
                      },
                      function (data) {
                        var html = '<option value="">Seleccione centro educativo</option>';
                        var len = data.length;
                        for (var i = 0; i < len; i++) {
                          html += '<option value="' + data[i].id + '">'
                                  + data[i].nombre
                                  + '</option>';
                        }
                        html += '</option>';
                        $('#centro').html(html);
                      });
            });
```

## 7. Comparativa entre lo moderno y lo antiguo

### 7.1. JavaScript vanilla antiguo (XHR `XMLHttpRequest` )

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>AJAX con XMLHttpRequest</title>
</head>
<body>
    <div id="data-container"></div> <!-- Aquí se mostrarán los datos -->
    <script>
        var xhr = new XMLHttpRequest();  // Crear el objeto XMLHttpRequest

        xhr.open('GET', 'https://jsonplaceholder.typicode.com/posts', true);

        xhr.onreadystatechange = function() {
            if (xhr.readyState === 4 && xhr.status === 200) {
                var data = JSON.parse(xhr.responseText);
                
                // Almacenar los datos en una variable
                var displayData = '';
                data.forEach(post => {
                    displayData += `<p>${post.title}</p>`;  // Usamos el título del post
                });

                // Mostrar los datos en el div con id="data-container"
                document.getElementById('data-container').innerHTML = displayData;
            }
        };

        xhr.send();
    </script>
</body>
</html>
```

### 7.2. JavaScript vanilla actual (Con promesas `fetch()` y `async/await`)

```javascript
// Usando fetch() para hacer una solicitud GET
fetch('https://jsonplaceholder.typicode.com/posts')
    .then(response => response.json())  // Convertir la respuesta a JSON
    .then(data => {
        console.log(data);  // Mostrar los datos en la consola
    })
    .catch(error => {
        console.error('Error:', error);  // Manejo de errores
    });
```

```javascript
async function fetchData() {
    try {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts');  // Solicitud GET
        const data = await response.json();  // Convertir la respuesta a JSON
        console.log(data);  // Mostrar los datos en la consola
    } catch (error) {
        console.error('Error:', error);  // Manejo de errores
    }
}

// Llamar a la función asíncrona
fetchData();
```

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>AJAX con fetch()</title>
</head>
<body>
    <div id="data-container"></div> <!-- Aquí se mostrarán los datos -->
    <script>
        async function fetchData() {
            try {
                const response = await fetch('https://jsonplaceholder.typicode.com/posts');
                const data = await response.json();

                // Almacenar los datos en una variable
                let displayData = '';
                data.forEach(post => {
                    displayData += `<p>${post.title}</p>`;  // Usamos el título del post
                });

                // Mostrar los datos en el div con id="data-container"
                document.getElementById('data-container').innerHTML = displayData;
            } catch (error) {
                console.error('Error:', error);
            }
        }

        // Llamar a la función de manera inmediata
        fetchData();
    </script>
</body>
</html>
```
## 7.2. Angular

`app.module.ts`  (Importa `HttpClientModule`)
```typescript
import { HttpClientModule } from '@angular/common/http';
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, HttpClientModule],
  providers: [],
  bootstrap: [AppComponent],
})
export class AppModule {}

```


`app.component.ts`
```typescript
import { Component, OnInit } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
})
export class AppComponent implements OnInit {
  constructor(private http: HttpClient) {}

  ngOnInit() {
    this.fetchData();
  }

  fetchData() {
    // Hacemos la solicitud HTTP usando HttpClient
    this.http.get('https://jsonplaceholder.typicode.com/posts')
    .subscribe(
      (data: any[]) => {
        // Almacenamos los datos en la variable 'posts'
        this.posts = data;
      },
      (error) => {
        console.error('Error:', error);
      }
    );
}
```

`app.component.html`
```html
<div *ngIf="posts.length > 0">
  <h2>Lista de Posts</h2>
  <div *ngFor="let post of posts">
    <p>{{ post.title }}</p> <!-- Mostramos el título del post -->
  </div>
</div>

<div *ngIf="posts.length === 0">
  <p>Cargando...</p>
</div>
```

## 8. Babeljs 

**Babel.js** es un **transpilador** (compilador) de JavaScript que se utiliza para convertir el código de JavaScript moderno (ES6/ES7 y versiones posteriores) en versiones más antiguas y compatibles de JavaScript (como ES5) que puedan ser entendidas por navegadores más antiguos.

JavaScript es un lenguaje en constante evolución. Las nuevas versiones de ECMAScript (por ejemplo, **ES6**, **ES7**, **ES8**, etc.) introducen nuevas características que no son siempre soportadas de inmediato por todos los navegadores o entornos de ejecución.

Babel permite a los desarrolladores usar las **últimas características** de JavaScript (como **arrow functions**, **async/await**, **destructuring**, **modules**, etc.) y compilar el código a una versión de JavaScript que sea más ampliamente compatible.

## 9. Node.js

**Node.js** es un entorno de ejecución para JavaScript en el servidor. Está basado en el motor **V8** de Google Chrome, lo que significa que puedes ejecutar código JavaScript fuera del navegador, en el servidor. Node.js es conocido por ser **asíncrono** y **event-driven**, lo que lo hace ideal para aplicaciones escalables y de alto rendimiento, como APIs, aplicaciones en tiempo real (chat en vivo, por ejemplo) y servidores HTTP.


**Instalar Node.js**
Descargar la versión LTS que ya incluye también npm (Node Package Manager) por lo que no se necesita instalar nada más.

En Linux:
```shell
sudo apt update
sudo apt install nodejs npm
# Verificar que se instalaron bien
node -v
npm -v
```

**npm** (Node Package Manager) es el gestor de paquetes oficial de **Node.js** y permite que los desarrolladores manejen las dependencias de sus proyectos.

**Inicializar un proyecto Node.js con npm**:
```shell
npm init
```

**Instalar dependencias**:
```shell
npm install express
```
Esto descargará el paquete **express** y lo agregará como una dependencia en tu archivo `package.json`.

**Instalar dependencias de desarrollo**: (Como nodemon para reiniciar automaticamente el server mientras se desarrolla)
```shell
npm install --save-dev nodemon
```

**Instalar todas las dependencias necesarias** (Alguien ha compartido un proyecto o ya existe un archivo `package.json`)
```shell
# Instalar
npm install
# Desinstalar
npm unistall  <nombre-paquete>
# Actualizar
npm update
```

(Ejemplo de paquete a instalar: **Bower** es un gestor de paquetes para el **front-end** que se utilizaba principalmente para gestionar bibliotecas del lado del cliente (por ejemplo, **jQuery**, **Bootstrap**, **AngularJS**, etc.). Fue popular en su tiempo, pero con la evolución de herramientas como **npm** y la aparición de **Webpack**, **Bower** ha quedado obsoleto y ya no se recomienda para nuevos proyectos.)

**Uso del módulo http**
Node.js viene con un módulo llamado `http` que te permite crear servidores web, algo que es muy útil si estás desarrollando una API o un servidor. A continuación, te voy a mostrar cómo puedes crear un servidor básico para responder con un "Hola Mundo" usando **`http.createServer`**.

```javascript
// Cargar el modulo http
var http = require('http');

// Configurar servidor HTTP para responder con Hola Mundo a las peticiones
var server = http.createServer(function(request,response) {
	response.writeHead(200, {'Content-Type', 'text/plain'});
	rewsponse.end("Hola Mundo");
});

// Escucha en el puerto 8000. IP 127.0.0.1 (la por defecto)
server.listen(8000)
console.log("Server runinng at http://127.0.0.1.8000")
```

**Levantar el servidor**
```
node holamundo.js
```

----
----
## 10. multipart/form-data vs multipart/related (MTOM) vs SOAP request

Los encabezados **`Content-Type`** con los parámetros `boundary` y `start` son clave en solicitudes **multipart** (como `multipart/form-data` y `Multipart/Related`).
`boundary` es una **cadena única** que separa las diferentes partes del mensaje en una solicitud **`multipart`**.

```
POST /api/upload HTTP/1.1
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryXyz123

------WebKitFormBoundaryXyz123
Content-Disposition: form-data; name="nombre"

Juan
------WebKitFormBoundaryXyz123
Content-Disposition: form-data; name="email"

juan@example.com
------WebKitFormBoundaryXyz123
Content-Disposition: form-data; name="archivo"; filename="documento.pdf"
Content-Type: application/pdf

(binary data)
------WebKitFormBoundaryXyz123--

```



En **MTOM (SOAP con archivos adjuntos)**, se usa `Multipart/Related`, donde:
- **`boundary`** separa las partes del mensaje (igual que en `multipart/form-data`).
- **`start`** indica **qué parte contiene el XML principal** de la solicitud.

🔹 **`start="<rootpart>"` indica que la primera parte con `Content-ID: <rootpart>` es el mensaje XML principal.**  
🔹 **`boundary="MIME_boundary"` separa cada parte.**  
🔹 **El archivo (`archivo123`) se adjunta como parte binaria en la misma solicitud.**

```xml
POST /soap-service HTTP/1.1
Content-Type: Multipart/Related; type="application/xop+xml"; start="<rootpart>"; boundary="MIME_boundary"

--MIME_boundary
Content-Type: application/xop+xml; charset=UTF-8; type="text/xml"
Content-Transfer-Encoding: binary
Content-ID: <rootpart>

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:ser="http://ejemplo.com/servicio">
   <soapenv:Header/>
   <soapenv:Body>
      <ser:SubirArchivo>
         <ser:Nombre>documento.pdf</ser:Nombre>
         <ser:Contenido>
            <xop:Include href="cid:archivo123" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>
         </ser:Contenido>
      </ser:SubirArchivo>
   </soapenv:Body>
</soapenv:Envelope>

--MIME_boundary
Content-Type: application/pdf
Content-Transfer-Encoding: binary
Content-ID: <archivo123>

(binary data)

--MIME_boundary--
```

En la petición SOAP simple es más sencillita:

```
POST /webservice/servicio HTTP/1.1
Host: www.ejemplo.com
Content-Type: text/xml; charset=UTF-8
Content-Length: 348

<?xml version="1.0" encoding="UTF-8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:web="http://www.ejemplo.com/servicio">
   <soapenv:Header/>
   <soapenv:Body>
      <web:RealizarOperacion>
         <web:Parametro1>valor1</web:Parametro1>
         <web:Parametro2>valor2</web:Parametro2>
      </web:RealizarOperacion>
   </soapenv:Body>
</soapenv:Envelope>

```

## 11. application/octect-stream

El tipo de contenido **`application/octet-stream`** se utiliza cuando el servidor está enviando un archivo binario a través de HTTP, sin especificar el formato o tipo de archivo. Es una forma genérica para transferir cualquier archivo binario, y se usa comúnmente cuando no se puede determinar el tipo de archivo o cuando no es necesario especificarlo.


```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
Content-Disposition: attachment; filename="largefile.bin"
Content-Length: 10485760

(binary data)
```


---
#### Subir ficheros

|**Tipo**|**Uso recomendado**|**Ventajas**|**Desventajas**|
|---|---|---|---|
|`multipart/form-data`|📌 Cuando subes archivos desde formularios o junto con otros datos (ej. ID, descripción, etc.)|✅ Permite enviar archivos y otros datos en la misma petición  <br>✅ Soportado por navegadores y frameworks  <br>✅ Compatible con múltiples archivos|❌ Un poco más complejo que `octet-stream`|
|`application/octet-stream`|📌 Cuando solo subes un archivo sin datos extra, como un **stream binario**|✅ Más eficiente para grandes archivos  <br>✅ No tiene sobrecarga de `multipart`|❌ No permite enviar otros datos (como ID, nombre, etc.)  <br>❌ Menos compatible con APIs REST estándar|
 **La mejor opción** es `multipart/form-data`, donde envías **archivo + JSON** en una sola petición.  
 **Si necesitas una API más flexible**, puedes enviar JSON primero y luego subir el archivo en otra petición (`application/octet-stream`), pero es menos eficiente.
 -----
- **`application/json`**: Es ideal para enviar datos estructurados en formato JSON, pero no está diseñado para enviar archivos binarios como imágenes o archivos comprimidos.
    
- **`multipart/form-data`**: Es el tipo de contenido adecuado para enviar archivos (como imágenes, videos, documentos, o archivos comprimidos). Se utiliza comúnmente en formularios web, y permite enviar múltiples archivos en una sola solicitud HTTP.
    
- **`application/octet-stream`**: Es un tipo de contenido genérico para enviar datos binarios sin una estructura específica. Si bien se puede usar para enviar archivos comprimidos, no ofrece la misma flexibilidad que `multipart/form-data`, y podría ser más difícil de manejar si necesitas enviar múltiples archivos o combinar archivos con otros datos (como texto).
----

- **Metadatos adicionales**:  
    Con `multipart/form-data`, puedes incluir fácilmente metadatos relacionados con los archivos que envías. Cada parte de la solicitud puede contener un campo de cabecera que describa el archivo (por ejemplo, su nombre, tipo de contenido, etc.). Esto te permite, por ejemplo, enviar información adicional sobre cada archivo (como el nombre de la foto o descripciones), lo que no es posible con `octet-stream`.
    
- **Varios archivos y campos**:  
    `multipart/form-data` permite enviar **múltiples archivos** y **otros datos** (como texto o formularios) dentro de una misma solicitud. Cada archivo o campo se organiza como una parte separada en el cuerpo de la solicitud, lo que lo hace ideal para cargar varios archivos de forma estructurada. En cambio, con `octet-stream`, los archivos se envían de forma continua como un flujo de bytes, lo que hace más difícil manejar varios archivos o incluir metadatos de manera eficiente.
    
- **Facilidad de uso en formularios web**:  
    Es ampliamente soportado en formularios HTML, lo que lo hace la opción preferida cuando se necesita subir archivos desde aplicaciones web. Además, muchas bibliotecas y frameworks están diseñados para trabajar con `multipart/form-data`, lo que simplifica su implementación.
    
- **Más adecuado para la interacción con la API**:  
    Las APIs REST suelen usar `multipart/form-data` para manejar casos donde se suben archivos junto con otros parámetros. Es una forma más estandarizada de enviar archivos, mientras que `octet-stream` es más genérico y no ofrece la misma claridad en cuanto al formato de los datos.

Cuando solo necesitas enviar **un archivo** (por ejemplo, un único fichero comprimido), **`application/octet-stream`** podría ser suficiente, y es cierto que en términos de **velocidad** y **eficiencia** puede ser más directo y "ligero", ya que simplemente envías los datos binarios sin necesidad de estructuras adicionales.
Sin embargo, si en el futuro planeas enviar más **tipos de datos**, como **metadatos** adicionales, **varios archivos**, o **parámetros de texto**, **`application/octet-stream`** se vuelve **limitante**. Aquí es donde entra la importancia de la **flexibilidad** y la **escabilidad** del diseño de la API, y por eso **`multipart/form-data`** sería más adecuado a largo plazo.

-----
#### Descargar ficheros

Usa `application/octet-stream`, que **fuerza la descarga** del archivo.

El **multipart/form-data** se usa para **subir archivos**, no para descargarlos. No es eficiente porque envía datos en partes separadas y no como un solo flujo binario.


