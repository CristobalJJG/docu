# TypeScript

JavaScript tipado.

## Propiedades de un componente
### Visibilidad
Dentro de un componente podemos tener 4 tipos de visibilidades:
* **Public**: Esta variable se podría usar en cualquier componente del proyecto.
* **Protected**: Esta variable solo sería visible dentro del componente del que se está definiendo.
* **Private**: Esta variable solo la podrá usar el fichero ts donde se está definiendo.
* Al no poner nada se crea un mix extraño. Se asemeja en la mayoría de las acciones a un *protected*.  

### Tipos de datos
* string: cadena de texto
* number: números, tanto enteros como flotantes
* boolean: verdadero o falso
* Any: Cualquier tipo, se asemeja al uso de JavaScript
* Array[T]: cadena de elementos

### Métodos
#### Constructor()
El método básico de todos los componentes es el constructor, al cual se le pasan los parámetros.
```javascript
    import { Component } from '@angular/core';
    @Component({ selector: 'empleados', templateUrl: '{{title}}' })
    export class Ex1Component {
        protected title = "Ejercicio 1";
        constructor(){ console.log(this.title); }
    }
```

#### Otros métodos
La creación de métodos ayuda a la modularidad de la aplicación.
Para crear un método hay que colocarle un nombre, y los parámetros necesarios para que este funcione dependiendo de su ubicación.
```javascript
    import { Component } from '@angular/core';
    @Component({ selector: 'empleados', templateUrl: '{{title}}' })
    export class Ex1Component {
        protected title = "Ejercicio 1";
        constructor(){ console.log(this.title); }
        changeTitle(){ this.title = "hola" }
    }
```

### Clases, Modelos, Datos y Objetos
Una clase se crea tal que:
```javascript
export class Empleado {
    constructor(
        private nombre: string,
        private edad: number,
        private contratado: boolean
    ) {
        this.nombre = nombre;
        this.edad = edad;
        this.contratado = contratado;
    }
} 
```
Al usar export, podemos importar esta clase en cualquier elemento.
```html
<h1>{{title}}</h1>
<p>Empleado</p>
<p>{{trabajadores[1].nombre}}</p>
<p>{{trabajadores[1].edad}}</p>
<p>{{trabajadores[1].contratado}}</p>
```