# Spring Boot + SQL Server + Docker

ESTE SERIA EL MODELO DEL BACK DE MANERA SIMPLE CON LA CONFIGURACION PARA SOLO ZIPEAR Y LLEVARNOS LOS ARCHIVOS

## ESTRUCTURAR ANGULAR

ESTRUCTURAR UN PROYECTO CON ANGULAR 19

Habilitando una estructura de proyecto con angular 19:

Node = 22.14.0
npm = 11.3.0 (versión actualizada en pasos anteriores)
Angular = 19

Paso N° 0: Resumen de los pasos anteriores realizados:
```
cd C:\Users\Juan\Documents\VSC
```
```
ng new my-project --style=scss
```
```
cd C:\Users\Juan\Documents\VSC\my-project
```
Paso N° 1: abrir un PowerShell como Administrador y ejecutar:

```
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```
Paso N° 2: abrir un cmd como Administrador y ejecutar:
```
powershell -Command "Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned"
```
Paso N° 3: abrir la carpeta del proyecto angular en Visual Studio Code:
(en mi caso la carpeta del proyecto es my-project-scss y esta en este directorio)
C:\Users\Juan\Documents\VSC\my-project


A partir de aquí, ejecutar los comandos en la terminal de Visual Studio Code:

Paso N° 4: crear la carpeta “environments” y sus 2 archivos, prueba y producción:
```
mkdir src/environments
New-Item -ItemType File -Path src/environments/environment.ts -Force
New-Item -ItemType File -Path src/environments/environment.prod.ts -Force
```
Paso N° 5: crear las carpetas “core”, “feature”, “layout” y “”shared”:
```
mkdir src/app/core
mkdir src/app/feature
mkdir src/app/layout
mkdir src/app/shared
```
Paso N° 6: crear las carpetas “interfaces” y “services” dentro de “core”:
```
mkdir src/app/core/interfaces
mkdir src/app/core/services
```

Creación de recursos en Angular enfocado a “customer”,  
recuerda que esto igualmente se puede aplicar para la creación de recursos como “product”:

Paso N° 7: crear las interfaces “customer”:
```
ng generate interface core/interfaces/customer
```
(yes)

Paso N° 8: crear el servicio “customer”:
```
ng generate service core/services/customer
```
Paso N° 9: crear los componentes “customer-form” y “customer-list”:
```
ng generate component feature/customer/customer-form
ng generate component feature/customer/customer-list
```
Paso N° 10: crear los .gitkeep para que GitHub reconozca carpetas vacías:
```
New-Item -ItemType File -Path src/app/layout/.gitkeep -Force
New-Item -ItemType File -Path src/app/shared/.gitkeep -Force
```


## CONFIGURACION ANGULAR

CONFIGURAR UN PROYECTO CON ANGULAR 19

Configuración para que se muestre los componentes de “customer”:

Paso N° 1: Reemplazar todo el contenido en el siguiente archivo del proyecto:

src/app/app.config.ts   (copiar y pegar todo el contenido)
```
import { ApplicationConfig, provideZoneChangeDetection } from '@angular/core';
import { provideRouter } from '@angular/router';


import { routes } from './app.routes';
import { provideClientHydration, withEventReplay } from '@angular/platform-browser';


//new import
import { provideHttpClient } from '@angular/common/http';


export const appConfig: ApplicationConfig = {
  providers: [provideZoneChangeDetection({ eventCoalescing: true }), provideRouter(routes), provideHttpClient()]
};
```

Paso N° 2: Reemplazar todo el contenido en el siguiente archivo del proyecto:
src/app/app.routes.ts   (copiar y pegar todo el contenido)
```
import { Routes } from '@angular/router';


//new import
import { CustomerFormComponent } from './feature/customer/customer-form/customer-form.component';
import { CustomerListComponent } from './feature/customer/customer-list/customer-list.component';


export const routes: Routes = [
    {
        path: 'customer-form',
        component: CustomerFormComponent
    },
    {
        path: 'customer-list',
        component: CustomerListComponent
    },
    {
        path: '',
        pathMatch: 'full',
        redirectTo: 'customer-form'
    }
];
```

Paso N° 3: Reemplazar todo el contenido en el siguiente archivo del proyecto:
src/app/app.component.ts   (copiar y pegar todo el contenido)
```
import { Component } from '@angular/core';
import { RouterOutlet } from '@angular/router';


@Component({
  selector: 'app-root',
  imports: [RouterOutlet],
  template: '<router-outlet/>'           //new
  //templateUrl: './app.component.html',
  //styleUrl: './app.component.scss'
})
export class AppComponent {
  title = 'my-project';
}
```
Paso N° 4: Ejecutar el proyecto Angular:
```
npm start
```
Paso N° 5: Puedes visualizar tus componentes de Formulario y Lista:
http://localhost:4200/customer-form	(Formulario Vacío)
http://localhost:4200/customer-list	(Lista Vacía)


Ahora toca empezar a diseñar las interfaces de los componentes “customer”:

Paso N° 6: Añadir un formulario básico en el siguiente archivo del proyecto:
src/app/feature/customer/customer-form/customer-form.component.html
```
<p>customer-form works!</p>


<h2>Formulario de Clientes</h2>


  <form action="/enviar" method="post">
    <label for="id">ID:</label><br>
    <input type="text" id="id" name="id"><br><br>


    <label for="nombre">Nombre:</label><br>
    <input type="text" id="nombres" name="nombre"><br><br>


    <label for="apellidos">Apellidos:</label><br>
    <input type="text" id="apellidos" name="apellidos"><br><br>


    <input type="submit" value="Enviar">
</form>
```

Paso N° 7: Añadir una lista básico en el siguiente archivo del proyecto:
src/app/feature/customer/customer-list/customer-list.component.html
```
<p>customer-list works!</p>


<h2>Tabla de Clientes</h2>


  <table>
    <thead>
      <tr>
        <th>ID</th>
        <th>Nombres</th>
        <th>Apellidos</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>1</td>
        <td>Ana</td>
        <td>Pérez</td>
      </tr>
    </tbody>
</table>
```

Paso N° 8: Control + S (guardar los cambios en los archivos) y revisar:
http://localhost:4200/customer-form	(Formulario Básico)
http://localhost:4200/customer-list	(Lista Básica)


(Estructura actual hasta el momento enfocado en el Maestro de “customer”)
```
/src
├── app
│   ├── core
│   │   ├── interfaces
│   │   │   ├── customer
│   │   ├── services
│   │   │   ├── customer.service
│   │   feature
│   │   ├── customer
│   │   │   ├── customer-form/ (incluye 4 archivos)
│   │   │   ├── customer-list/ (incluye 4 archivos)
│   │   layout
│   │   │
│   │   shared

```

(Estructura futura enfocado en los Maestro de “customer” y “product”)
```
/src
├── app
│   ├── core
│   │   ├── interfaces
│   │   │   ├── customer
│   │   │   ├── product
│   │   ├── services
│   │   │   ├── customer.service
│   │   │   ├── product.service
│   │   feature
│   │   ├── customer
│   │   │   ├── customer-form/ (incluye 4 archivos)
│   │   │   ├── customer-list/ (incluye 4 archivos)
│   │   ├── product
│   │   │   ├── product-form/ (incluye 4 archivos)
│   │   │   ├── product-list/ (incluye 4 archivos)
│   │   layout
│   │   │
│   │   shared

```
## MAS ESTRUCTURA 

Estructuración del proyecto angular y todo el flujo de trabajo:
```
/src
├── app
│   ├── core           Recursos que se configuran solo una vez
│   │   ├── interfaces Interfaces (modelos)
│   │   │   ├── customer
│   │   │   ├── product
│   │   │  
│   │   ├── services   Servicio de consumo de los request HTTP
│   │   │   ├── customer.service
│   │   │   ├── product.service
│   │   │
│   ├── feature       Funcionalidades principales (por dominio/maestros)
│   │   ├── customer
│   │   │   ├── customer-form/ Formulario (incluye 4 archivos)
│   │   │   ├── customer-list/ Lista (incluye 4 archivos)
│   │   │
│   │   ├── product
│   │   │   ├── product-form/ Formulario  (incluye 4 archivos)
│   │   │   ├── product-list/ Lista  (incluye 4 archivos)
│   │   │
│   ├── layout/                      Estructura base de la app
│   │   └── admin-layout/ Layout principal de admin (incluye 4 archivos)
│   │   |   └── components/          Subcomponentes del layout
│   │   |   |    ├── header/  Cabecera (incluye 4 archivos)
│   |   |   |    └── sidebar/ Barra lateral (incluye 4 archivos)
│   │   │   │
│   ├── shared/             Elementos/componentes reutilizables
│   │   ├── components/     Componentes (botones, modales, alert, etc.)
│   │   │  
│   ├── app.config.ts       Configuraciones globales (para standalone) 
│   ├── app.routes.ts       Definición central de rutas de componentes
|
├── environments            Manejo de Variables
│   └── environment.prod.ts Entorno de producción
│   └── environment.ts      Entorno de desarrollo (por defecto)

```




Paso N° 0: Funcionalidades CRUD desde Spring Boot a consumir en Angular:
findAll            (GET - listar a todos)
findByState   (GET - listar x ID)
findById         (GET - listar x Estado)
save       	(POST - registrar)
update   	(PUT - actualizar)
delete    	(PATH - eliminar)
restore  	(PATH - restaurar)
https://github.com/juancondorijara/SQL_Server/blob/develop-be/src/main/java/pe/edu/vallegrande/project/rest/CustomerRest.java

Paso N° 1: Verificar de tener esta notación en los archivos “rest” de tu backend:

src/main/java/pe/edu/vallegrande/project/rest/CustomerRest.java
```
import org.springframework.web.bind.annotation.CrossOrigin; //import


@CrossOrigin(origins = "*")  //Acceso para que angular pueda acceder
@RestController
@RequestMapping("/v1/api/customer")
```
Paso N° 2: dependencias a instalar en caso el diseño que uses sea: Angular material”,  en la terminal, raíz del proyecto:
```
npm install @angular/material @angular/cdk
ng add @angular/material
npm install sweetalert2
```
Paso N° 3: dependencias a instalar en caso el diseño que uses sea: HTML y scss/css
```
npm install sweetalert2
```
Paso N° 4: Contenido de referencia en el archivo “Environment”:
src/environments/environments.ts   (ajustar según la url de ejecución de tu backend)
```
export const environment = {
    production: false,
    urlBackEnd: 'http://localhost:8080'
  };
```


Paso N° 5: Contenido de referencia en el archivo “Interface”:
src/app/core/interfaces/customer.ts   (ajustar según tus campos y tipo de datos)
```
export interface Customer {
    id: number;
    dni: number;
    cellPhone: number;
    firstName: string;
    lastName: string;
    state: string;
}
```

Paso N° 6: Contenido de referencia en el archivo “Service”:
src/app/core/services/customer.service.ts   (ajustar según tus request HTTP de tu backend)

https://github.com/juancondorijara/SQL_Server/blob/develop-fe/src/app/core/services/customer.service.ts


Los siguientes componentes son compatibles con el diseño ANGULAR MATERIAL

Paso N° 7: Contenido de referencia en el componente “Formulario” (4 archivos):
src/app/feature/customer/customer-form

https://github.com/juancondorijara/SQL_Server/tree/develop-fe/src/app/feature/customer/customer-form

Paso N° 8: Contenido de referencia en el componente “Lista” (4 archivos):
src/app/feature/customer/customer-list

https://github.com/juancondorijara/SQL_Server/tree/develop-fe/src/app/feature/customer/customer-list


Los siguientes componentes son compatibles con el diseño simples TYPESCRIPT y HTML 
(sin ANGULAR MATERIALl)

Paso N° 9: Contenido de referencia en el componente “Formulario” (4 archivos):
src/app/feature/customer-form-html/customer-form-html

https://github.com/juancondorijara/SQL_Server/tree/develop-fe/src/app/feature/customer-html/customer-form-html

Paso N° 10: Contenido de referencia en el componente “Lista” (4 archivos):
src/app/feature/customer-list-html/customer-list-html

https://github.com/juancondorijara/SQL_Server/tree/develop-fe/src/app/feature/customer-html/customer-list-html


