
## 1. Instalación de herramientas y ejecución inicial

#### **Node.js** versión LTS (22.14.0). 
Es un entorno de ejecución para JavaScript. Ambiente de ejecución. Permite ejecutar código JavaScript fuera del navegador. 
- Permite trabajar desde el cliente (aplicaciones JavaScript con React, Angular,...  Angular CLI trabaja con Node.js por debajo,..)
- Permite trabajar desde el back (aplicaciones que corren desde el servidor con frameworks como Express,...)

Se instala desde la web oficial nodejs.org
Con él viene incluido npm también.
**npm** (Node Packages Manager) es un administrador de paquetes para JavaScript. 

Revisemos las versiones:
```
node -v  
# Devuelve v22.14.0
npm -v
# Devuelve 10.9.2
```

#### **Angular CLI**

Se instala con npm.
Puede hacerse localmente (en la carpeta `node_modules` del proyecto actual, solo disponible en ese proyecto específico) o globalmente (en un directorio accesible desde cualquier proyecto, para herramientas que se necesitan en toda la máquina como `@angular/cli`, mediante la flag `-g`)

```
npm install -g @angular/cli

ng version
```

Devuelve:

```
Angular CLI: 19.1.7
Node: 22.14.0
Package Manager: npm 10.9.2
OS: win32 x64

Angular:
...

Package                      Version
------------------------------------------------------
@angular-devkit/architect    0.1901.7 (cli-only)
@angular-devkit/core         19.1.7 (cli-only)
@angular-devkit/schematics   19.1.7 (cli-only)
@schematics/angular          19.1.7 (cli-only)
```

Usuarios de Linux y MacOS deben limpiar el caché:
```
sudo npm cache clean --force
```

## 2. Nuevo proyecto de Angular

**Crear proyecto**
```
ng new nombre_del_proyecto
```

Se pedirá:
- Qué hoja de estilos se quiere usar. Elegiremos CSS
- Si se quiere habilitar el Server-Side Rendering (SSR) y Static Site Generation (SSG/Prerenderinng): Se le indica que no

La documentación de Angular se encuentra en www.angular.dev

**Levantar proyecto**

```
# Ejecutar
npm start
# O bien
ng serve
```


- En el `package.json` se tiene `npm start` para levantar el proyecto ( `ng serve` ) y `npm build` para construirlo (`ng build`) y los componentes y dependencias propias. Después las dependencias de desarrollo no irán a producción. 

- Carpeta **public** para hojas de estilos, imágenes, favicons...

- Carpeta **src**: Código fuente, configuraciones...

## 3. Estructura de los componentes de Angular

- **src/index.html**: Es la puerta de entrada a la aplicación. En la de ejemplo se observa que `<app-root></app-root>`  es el componente principal. 

```html
<body>  
  <app-root></app-root>
</body>
```

Aprovechamos para meterle Bootstrap
```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
```

Cada componente se divide en cuatro ficheros:
-  `.ts`: Código de TypeScript
-  `.html`: Plantilla del componente
- `.css`: Hoja de estilos del propio componente (Se puede configurar, es opcional...)
- `.spec.ts`: Para pruebas unitarias del componente

Configuraciones de la aplicación:
- `app.config.ts`
- `app.routes.ts` 

### El fichero de TypeScript

TypeScript incluye JavaScript moderno (ECMAScript 6, partió de esta versión y luego fue evolucionando a la 7, 2015, 2016,... hasta la fecha. Tiene todas las novedades de JavaScript e incluye programación orientada a objetos mucho más robusta y fuertemente tipada. 

Podríamos poner:
```  
title = 'pruebas_angular';
title : string = 'pruebas_angular';
```

El componente se define con el decorador `@Component` en el fichero `.ts`. Permite asociar una clase TypeScript con su plantilla HTML, estilos y configuración.

El decorador posee los atributos:
- `selector`: Define el nombre del elemento HTML con el que se usará el componente
- `imports`: Permite importar dependencias de otros módulos dentro de los componentes individuales
- `templateUrl`: Ubicación del HTML
- `styleUrl`: Ubicación del CSS que afecta al componente. (Para estilos globales no usar esta sino usar `styles.css`)

`export class AppComponent`: Define la clase del componente. Con esto puede manejar datos, lógica y eventos. 
Inicialmente se encuentra definida la variable `title`, que es usada en `app.component.html`. Todo atributo de la clase componente debe ser público. 


```typescript
@Component({  
  selector: 'app-root',  
  imports: [RouterOutlet],  
  templateUrl: './app.component.html',  
  styleUrl: './app.component.css'  
})  
export class AppComponent {  
  title = 'pruebas_angular';  
}
```

```html
<h1>Hello, {{ title }}</h1>
```


Vamos a vaciar todo el fichero `app-component.html` y a usar solo un `title`

### Creación de componentes

También vamos a crear: 
- un directorio de `components`
- un directorio de `modules`

Con AngularCLI se generan los cuatro ficheros de componentes de forma fácil con `ng generate`

```
ng generate component components/products
# O bien
ng g c components/productsd
```

Para incluirlo en `app.component.html`, incluyámoslo dentro de su HTML.

```html
<div class="container py-4">  
  <div class="row">  
    <div class="col">  
      <app-products></app-products>    </div>  </div>  
</div>
```

E importémoslo en `imports` de su ts:

```typescript
imports: [RouterOutlet, ProductsComponent],
```


### Creación de modelos

```
ng generate class models/product
```

(Borremos el `spec.ts`...)
Y pongamos lo que necesitamos dentro del modelo. **Debe inicializarse** o declararse como opcional. 

```typescript
export class Product {  
  id!: number  
  name!: string  
  description!: string  
  price!: number  
}
```

## 4. Agregando Componente Table

Vamos a declarar una lista de productos.
Implementaremos en `AppComponent` un método `OnInit` para cuando se inicia la aplicación poblar la lista de productos. 

```ts
@Component({  
  selector: 'app-root',  
  imports: [ProductsComponent],  
  templateUrl: './app.component.html',  
  styleUrl: './app.component.css'  
})  
export class AppComponent implements OnInit {  
  
  products: Product[] = [];  
  
  ngOnInit(): void {  
    this.products = [  
      {  
        id: 1,  
        name: 'Monitor Asus 35 pulgadas',  
        price: 1000,  
        description: 'Buen monitor'  
      },  
      {  
        id: 2,  
        name: 'Iphone Pro',  
        price: 1700,  
        description: 'Es muy de Apple'  
      }  
    ]  
  }  
  
}
```

Del componente padre, tendremos que pasarle los productos al componente hijo.
Se hace de la siguiente forma: En el padre se pasa al componente como `[atributo del hijo]="atributo del padre"`

```html
<table-product [products]="products"></table-product>
```

En el hijo es necesario declararlo con el decorador `@Input()`:

```ts
@Input() products: Product[] = [];
```

------------------------

**Recorrer el array en el HTML y poner condicionales**

Utilizar la directiva `@for` para recorrer
y la directiva `@if` para condicionales

```html
<h2>{{ title }}</h2>  
  
@if(products.length > 0) {  
<table class="table table-striped table-hover">
    <thead>    <tr>      <th>id</th>  
      <th>name</th>  
      <th>description</th>  
      <th>price</th>  
    </tr>    </thead>  
    <tbody>      @for(product of products; track $index) {  
        <tr>  
          <td>{{product.id}}</td>  
          <td>{{product.name}}</td>  
          <td>{{product.description}}</td>  
          <td>{{product.price}}</td>  
        </tr>      }  
    </tbody>  
  </table>} @else {  
  <div class = "alert alert-danger"> No hay registros en el sistema</div>  
}
```

## 5. Agregando Componente Form

- `ng g c components/form`
- Se quita `spec.ts` y `css` y se mueve al directorio componentes
- Al `selector` se le pone `product-form`
- El padre `app.component.ts` debe tener `ProductsComponent` en el `imports`.

En el `form.component.ts` se inicializa por defecto el objeto `Product`:

```
product: Product = {  
  id: 0,  
  name: '',  
  description: '',  
  price: 0  
};
```

El formulario `FormComponent` tiene que:
- tener **importado `FormModule` de Angular**
- tener estos elementos mapeados en él, esto se hace con la directiva **ngModel** de la siguiente forma: `[(ngModel)]="product.name"`
- luego un evento que lo envíe. Este el elemento se indica con la directiva **ngSubmit**.

```html
<h2>Form  {{ product.id > 0 ? 'Update' : 'Create'}} Product</h2>  
  
<form (ngSubmit)="onSubmit()">
  <div>    <input class="form-control my-2"  
           placeholder="Name"  
           name="name"  
           [(ngModel)]="product.name">  
  </div>  
  <div>    <input class="form-control my-2"  
           placeholder="Description"  
           name="description"  
           [(ngModel)]="product.description">  
  </div>  <div>    <input class="form-control my-2"  
           type="number"  
           placeholder="Price"  
           name="price"  
           [(ngModel)]="product.price">  
  </div>  <div>    <button type="submit" class="btn btn-primary my-2">  
      {{ product.id > 0 ? 'Update' : 'Create'}}  
    </button>  
  </div></form>
```


```ts
onSubmit() : void {  
  console.log(this.product);  
}
```

**Debemos enviar esto al componente padre**
Para ello desde el `form.component.ts` se utilizará un **EventEmitter** y se llamará en el `onSumit`

```
@Output() addProductEvent = new EventEmitter();

onSubmit(): void {
	console.log(this.product);
	this.addProductEvent.emit(this.product);
}
```

En el component padre se recibirá del component `product-form` mediante la directiva **adProductEvent**: 

```html
<product-form (addProductEvent)="addProduct($event)"></product-form>
```


**Método para agregar:**
Para no modificar el array que ya estaba, se crea uno nuevo usando el operador `spread ...`:
- Se copian todos los elementos del array actual en un nuevo arreglo.  `... this.products`
- Se copian las propiedades del objeto dentro de otro nuevo `... product`.

```
countId = signal(3)  // Guardar elementos de estado en Angular (Un contador)
```

```ts
addProduct(product:Product): void {  
  this.products = [... this.products, {... product, id: this.countId()}];
  this.countId.update(id => id + 1);
}
```

## 6. Implementando Editar y Eliminar

- Es importante comunicar los datos desde la acción del botón al formulario.
- También debe aplicarse después la acción de editar, eliminar.

Así, en cada elemento de la tabla hay dos botones: 

```html
  <td><button class="btn btn-sm btn-primary"  
  (click)="onUpdateProduct(product)">Actualizar</button></td>  
  <td><button class="btn btn-sm btn-danger"  
  (click)="onRemoveProduct(product.id)">Eliminar</button></td>  
```

Y en el .ts, estos métodos emitirán su correspondiente objeto al padre:
```ts
// Emitir objeto producto al padre  
@Output() updateProductEvent = new EventEmitter();

onUpdateProduct(product: Product): void {  
  this.updateProductEvent.emit(product);  
}  
  
// Emitir el id al padre  
@Output() removeProductEvent = new EventEmitter(); 

onRemoveProduct(id: number): void {  
  this.removeProductEvent.emit(id)  
}
```

El padre a su vez, contempla que este objeto pueda ser emitido por la lista de productos:

```html
<div class="col">  
  <table-product [products]="products"  
  (updateProductEvent)="updateProduct($event)"  
  (removeProductEvent)="removeProduct($event)"></table-product>  
</div>
```

Y, en caso de ser emitido, llaman a su correspondiente método:

```ts
  updateProduct(product: Product): void {
    this.productSelected = {...product};
  }

  removeProduct(id: Number): void {
    this.products = this.products.filter(product => product.id !== id);
}
```

`productSelected` se ocupará de ser el objeto que llene el formulario;:

```html
<product-form [product]="productSelected"  
              (addProductEvent)="addProduct($event)"></product-form>
```

Ya que en él está marcado como `@Input`: 
```ts
@Input() product: Product = this.newProduct()
```
### Sweet Alert

Debe estar instalado en el proyecto el paquete Sweet Alert
`npm install sweetalert2`

Importante que esté el import:
`import Swal from 'sweetalert2';`

**Advertencia**
```ts
Swal.fire({  
  title:"Producto creado",  
  text:"Producto creado con éxito",  
  icon:"success"  
})
```

**Cuadro de diálogo**
```ts
    Swal.fire({
      title:"¿Desea eliminar el producto?",
      text:"Los cambios no podrán revertirse",
      icon:"warning",
      showCancelButton: true,
      confirmButtonColor: "#3085d6",
      cancelButtonColor: "#d33",
      confirmButtonText: "Eliminar"}).then((result) => {
        if (result.isConfirmed) {
          this.products = this.products.filter(product => product.id !== id);
          Swal.fire({
            title:"Producto eliminado",
            text:"Producto eliminado con éxito",
            icon:"success"
          })
        }
    });
```

## 7. Validación de formulario

La validación se hace en el HTML. Veamos el siguiente ejemplo:

```html
<h2>Form  {{ product.id > 0 ? 'Update' : 'Create'}} Product</h2>

<form (ngSubmit)="onSubmit(productForm)" #productForm="ngForm">
  <div>
    <input class="form-control my-2"
           placeholder="Name"
           name="name"
           #name="ngModel"
           required
           minlength="4"
           [(ngModel)]="product.name">
    @if(name.invalid && (name.dirty || name.touched)) {
      <div class="text-danger">
        @if(name.errors!['required']) {
          Nombre es requerido
        }
        @if(name.errors!['minlength']) {
          Nombre debe tener al menos cuatro caracteres
        }
      </div>
    }
  </div>
  <div>
    <input class="form-control my-2"
           placeholder="Description"
           name="description"
           #description="ngModel"
           required
           [(ngModel)]="product.description">
    @if(description.invalid && (description.dirty || description.touched)) {
      <div class="text-danger">
        @if(description.errors!['required']) {
          Descripcion es requerida
        }
      </div>
    }
  </div>
  <div>
    <input class="form-control my-2"
           type="number"
           placeholder="Price"
           name="price"
           #price="ngModel"
           required min="10"
           [(ngModel)]="product.price">
    @if(price.invalid && (price.dirty || price.touched)) {
      <div class="text-danger">
        @if(price.errors!['required']) {
          Precio es requerida
        }
        @if(price.errors!['min']) {
          Precio debe ser mayor a 10
        }
      </div>
    }
  </div>
  <div>
    <button type="submit" [disabled]="productForm.form.invalid" class="btn btn-primary my-2">
      {{ product.id > 0 ? 'Update' : 'Create'}}
    </button>
  </div>
</form>

```

## 8. Implementando Service con HttpClient para consumir API Rest

En `app.config.ts`, indicaremos que se debe proveer cliente HTTP:
`provideHttpClient()`

Creamos el servicio:
```
ng g service services/product 
```

Vamos a inyectar en el constructor del `product.service.ts` el  `HttpClient`. 

El método que realiza la petición HTTP  en el service devuelve un `Observable`. (parecido a los Flows de Kotlin ya que son asíncronos, sus valores cambian en el tiempo, se pueden observar por uno o varios suscriptores... )
Debe ser de un tipo de dato concreto, que debe ser indicado.

Veamos el ejemplo del service: 

```ts
import { Injectable } from '@angular/core';  
import {HttpClient} from '@angular/common/http';  
import {Observable} from 'rxjs';  
import {Product} from '../models/product';  
  
@Injectable({  
  providedIn: 'root'  
})  
export class ProductService {  
  
  private url: string = "localhost:8080/miapi/product"
  
  constructor(private http: HttpClient) { }  

  findAll(): Observable<Product[]> {  
    return this.http.get<Product[]>(this.url)  
  }  
 /*  
  findAll(): Observable<Product[]> {    return this.http.get(this.url).pipe(      map((response: any) => response as Product[])    );  }*/  
  
  create(product: Product): Observable<Product> {  
    return this.http.post<Product>(this.url, product);  
  }  
  
  update(product: Product): Observable<Product> {  
    return this.http.put<Product>(`${this.url}/${product.id}`, product);  
  }  
  
  delete(productId: Number): Observable<Product> {  
    return this.http.delete<Product>(`${this.url}/${productId}`);  
  }  
  
}
```

## 9. Impresión de JSON

Si se quiere mostrar directamente el JSON de la response, se puede poner tipo `any`: 
```ts
findAll(): Observable<any> { return this.http.get<any>(this.url); }
```

Asignarlo a una variable: 

```ts
this.service.findAll().subscribe((msg: any) => {
  console.log(msg);  // Esto imprimirá todo el JSON
  this.msg = msg;    // Si quieres guardar el JSON en 'this.msg'
});
```

Y usando la pipe `json` se puede convertir automáticamente a una cadena con formato legigle:

```html
<div> <pre>{{ msg | json }}</pre> </div>
```

También podría usarse `JSON.stringify()` ( `stringify()`)
