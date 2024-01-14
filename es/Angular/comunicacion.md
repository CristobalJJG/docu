# Comunicación entre componentes

Para pasar información de un componente a otro, tenemos que tener clara la jerarquía:

<!-- tabs:start -->

<!-- tab:**Padre** -->
El dato se le manda al hijo usando ```[nombre-dato]="variable del padre"``` 
El dato se recibe del hijo gracias a la directia ```(event)=funcion($event)```
El dato se recibe exactamente igual que como se envía:
Si se envía ```13```, ```$event=13```; si se envía un objeto, se recogerá el objeto entero. 
```HTML
Padre manda a hijo <input type="number" [(ngModel)]="hijo1">
<div class="hijo hijo1">
    <h2>Hijo1</h2>
    <hijo1 [dato]="hijo1"></hijo1>
</div>

Padre recibe de hijo {{hijo2}}
<div>
    <h2>Hijo2</h2>
    <hijo2 (event)="recieve($event)"></hijo2>
</div>
```
```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-padre',
  templateUrl: './padre.component.html',
  styleUrls: ['./padre.component.scss']
})
export class PadreComponent {
  hijo1 = 0;
  hijo2 = 0;

  recieve(event: any) {
    this.hijo2 = event;
  }
}
```

<!-- tab:**De Padre a Hijo** -->
(Recibe informacion del padre)  
La variable que asignemos con la directiva **@Input()** será como si hicieramos un Two Way Data Binding entre la variable del padre y la del hijo.

```HTML
<p>Padre manda a hijo: {{dato}}</p>
```
```javascript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'hijo1',
  templateUrl: './padre-hijo.component.html'
})
export class PadreHijoComponent {
  @Input() dato: number | undefined;
}
```

<!-- tab:**De Hijo a Padre** -->
(Envía informacion al padre)  
Para enviar información tendremos que crear un **EventEmitter** con la propiedad **@Output()**.
En este caso, como queremos que cada vez que cambie el número, se envíe el cambio al padre, se usó la directiva **(change)**, que ejecuta la función send()
```HTML
Hijo manda a padre <input type="number" value=0 #hijo (change)="send(hijo.value)">
```
```javascript
import { Component, EventEmitter, Output } from '@angular/core';

@Component({
  selector: 'hijo2',
  templateUrl: './hijo-padre.component.html'
})
export class HijoPadreComponent {
  @Output() event = new EventEmitter();

  send(number: string) {
    this.event.emit(+number);
  }
}
```
<!-- tabs:end -->