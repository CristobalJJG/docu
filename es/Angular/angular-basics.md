# Nociones básicas de Angular

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



## Funciones

### ngOnInit()
Esta función es la primera que se ejecuta al crear el componente en la página, antes incluso que el [constructor()](ts.md) 
```
import { Component, OnInit } from '@angular/core';
@Component({ selector: 'empleados' })
export class Ex1Component implements OnInit{
  ngOnInit(): void {}
  protected title = "Ejercicio 1"
}
```
