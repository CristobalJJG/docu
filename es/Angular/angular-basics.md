# Nociones básicas de Angular

## Two Way Data Binding

Esto no es más que poder modificar una variable dinámicamente a partir de un input. Esto se consigue gracias a una directiva llamada ```[(ngModel)]```, que nos registra una variable del modelo del componente y nos permite modificarlo, por ejemplo:
```javascript
@Component({
  selector: 'app-twdb',
  template: `
    <input type="text" [(ngModel)]="color" />
    <pre>{{color}}</pre>
    <p [ngStyle]="{'background':color, 'padding':'30px'}"></p>
  `
})
export class TwdbComponent {
  color: string = 'red';
}
```

Para poder hacer uso del Two Way Data Binding1

## Ficheros

### app.module.ts

```javascript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { SnakePipe } from './pipes/snake.pipe';

@NgModule({
  declarations: [
    //pages

    //Components
    AppComponent,

    //pipes
    SnakePipe
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    FormsModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

* **declarations**:  se utiliza para importar componentes, *directivas* y pipes, que usas en tus plantillas.
* **imports:** sirve para importar otros módulos que vas a usar en este NgModule
* **providers**: sirve para importar servicios(~ modelos: las clases para obtener y manejar datos). Una vez importados son accesibles en cualquier parte de tu app.
* **boostrap**: La vista o componente principal de la aplicación, llamado componente raíz.Por default es nuestro AppComponent.
* **exports**: sirve para declarar elementos de tu modulo(componentes, directivas, modulos o pipes) que serán visibles y usables en las plantillas de componentes de otros NgModules (es opcional). Para que otros módulos puedan usarlos, primer deben importar este modulo. Esto nos permite controlar que partes de nuestro modulo son accesibles desde otros módulos.

### app-routing.module.ts
Este fichero contendrá todas las rutas y su componente asignado, lo importante de este módulo será tener bien declarada la variable **routes**, que es la que nos permitirá redireccionar los enlaces de la página de forma correcta.

```javascript
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'ex1', component: Ex1Component },
  { path: 'ex2', component: Ex2Component },
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

Más en [Routing](/es/Angular/routing.md).

## Funciones

### ngOnInit()
Esta función es la primera que se ejecuta al crear el componente en la página, antes incluso que el [constructor()](ts.md) 
```javascript
import { Component, OnInit } from '@angular/core';
@Component({ selector: 'empleados' })
export class Ex1Component implements OnInit{
  ngOnInit(): void {}
  protected title = "Ejercicio 1"
}
```
