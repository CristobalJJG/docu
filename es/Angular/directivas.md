# Directivas

Las directivas con tipo ```*ngX```, son directivas de **condicionales** y **estructuras de control**. POr ejemplo, *ngIf, *ngFor...  
Las directivas de tipo ```(X)``` son directivas de **evento**. Por ejemplo, (click), (mouseenter)...  
Las directivas de **binding** son de tipo ```[ngX]```. Por ejemplo, [ngSwitch], [ngClass]...  


## Directivas Condicionales y Estructuras de control

### *ngIf 
Funciona como un *if* de TS, donde en este caso, el bloque de código se mostrará en el DOM o no, en funció de la resolución del if.
```javascript
@Component({
  selector: 'app-ng-if',
  template: `
    <p *ngIf="shown">Se ve</p>
    <p *ngIf="notShown">No se ve</p>
  `
})
export class NgIfComponent {
  notShown = false;
  shown = true;
}
```

### *ngFor
Nos permite crear bucles dentro del HTML
```javascript
@Component({
  selector: 'app-ngfor',
  template: `
  <div>
    <ul> 
    <li *ngFor="let t of workers; let i = index">{{t | json}}, {{i}}</li> 
    </ul>
  </div>
  `,
})
export class NgforComponent {
  protected workers: Array<Worker>;

  constructor() {
    this.workers = [
      new Worker("Manolo", 23, true),
      new Worker("Lorito", 18, true),
      new Worker("Gonzalez", 32, true),
      new Worker("Roberto", 45, true)
    ]
  }
}
```

## Directivas de Evento

### (click) 
Se asemeja a la función por defecto de HTML OnClick. Ejecuta una función del fichero TS al ser pulsado el elemento que contiene el *(click)*.
```javascript
@Component({
  selector: 'app-click',
  template: '<p (click)="sayHello()">Botón</p>',
})
export class ClickComponent {
  sayHello() { alert("HelloWorld :):") }
}
```

---

## Directivas de Binding

### [ngSwitch]
Se asemeja a la función por defecto de HTML OnClick. Ejecuta una función del fichero TS al ser pulsado el elemento que contiene el *(click)*.
```javascript
@Component({
  selector: 'app-click',
  template: '<p (click)="sayHello()">Botón</p>',
})
export class ClickComponent {
  sayHello() { alert("HelloWorld :):") }
}
```

### [ngStyle] 
Asemeja al atributo *style* de html, con la diferencia que gracias al Two Way Data Binding, podremos usar variables como estilos dentro de los elementos. En este caso, ```color:string ='red'```, si de alguna forma cambiaramos la variable al nombre de otro color, este cambiaría el estilo del elemento, y cambiaría el switch
```html
<h3>Colores</h3>
<ul [ngSwitch]="color">
    <li *ngSwitchCase="'red'" [ngStyle]="{background:color, 'padding':'11px'}">De color rojo</li>
    <li *ngSwitchCase="'blue'" [ngStyle]="{background:color, 'padding':'12px'}">De color azul</li>
    <li *ngSwitchCase="'brown'" [ngStyle]="{background:color, 'padding':'13px'}">De color marron</li>
</ul>
```

Otra forma de utilizarlo podria ser ir atributo por atributo asignándole un booleano:
```html
    <pre [style.border]="color == 'red' ? '3px gray solid' : ''">{{color}}</pre>
```

### [ngClass] 
Asemeja al atributo *class* de html, con la diferencia que gracias al Two Way Data Binding, podremos usar variables como estilos dentro de los elementos.
```javascript
@Component({
  selector: 'app-ng-class',
  styleUrls: ['./ng-class.component.scss'],
  template: `
  <input type="text" [(ngModel)]='clase'>
    <pre [ngClass]="{
      fondoDefault:clase,
      fondoAzul: clase == 'azul',
      fondoVerde: clase == 'verde',
    }">
    {{clase}}
  </pre>

  `
})
export class NgClassComponent {
  clase = 'verde';
}
```

Otra forma de utilizarlo podria ser ir atributo por atributo asignándole un booleano:
```html
    <pre [class.bordeAzul]="clase == 'bordeAzul'">{{clase}}</pre>
```