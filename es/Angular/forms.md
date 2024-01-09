# Formularios

Una de las mejores formas en las que yo veo el funcionamiento de una característica es en un ejemplo real:


## coche.ts
Tenemos un clase coche, con el fichero en la carpeta de modelos:
```javascript
export class Coche {
    constructor(
        public nombre: string,
        public color: string,
        public caballaje: string
    ) { }
}
```

## forms.component.html
Lo realmente importante estaría en el fichero html, ya que puede ser el causante de: 
* No filtrar bien los contenidos escritos, que pueden llevar a inyección maliciosa de código
* Una mala estructuración del formulario, haciendo que este pueda ser ejecutado en cualquier momento
* O lo más simple, una mala experiencia de usuario por no haber añadido ciertas características al formulario.
```html
    <h1>De coches va la cosa</h1>
    <form action="" #formCoche="ngForm" (ngSubmit)="send(nombre.value, caballaje.value, color.value); formCoche.reset();">
        <!-- Nombre -->
        <label for="nombre">Nombre:</label>
        <input type="text" name="nombre" #nombre="ngModel" [(ngModel)]="coche.nombre" required><br>
        <p *ngIf="nombre.touched && nombre.invalid">El nombre es incorrecto.</p>

        <!-- Caballaje -->
        <label for="caballaje">Caballaje:</label>
        <input type="text" name="caballaje" #caballaje="ngModel" [(ngModel)]="coche.caballaje" required
            pattern="[0-9]+"><br>
        <p *ngIf="caballaje.dirty && caballaje.invalid">El caballaje es incorrecto.</p>

        <!-- Color -->
        <label for="color">Color:</label>
        <input type="color" name="color" #color="ngModel" [(ngModel)]="coche.color" required pattern="#[0-9a-fA-F]+"><br>
        <p *ngIf="color.dirty && color.invalid">El color es incorrecto.</p>
        <br>
        <input type="submit" value="Enviar" class="btn-active" [disabled]="!formCoche.form.valid">
    </form>

    <h2>Coche:</h2>
    <pre>{{coche | json}}</pre>

    <h2>Coches:</h2>
    <pre *ngFor="let c of coches, let i=index">
        {{c|json}}
    </pre>
```

### Cómo recoger los datos
<!-- Nombre -->
```html
<label for="nombre">Nombre:</label>
<input type="text" name="nombre" #nombre="ngModel" [(ngModel)]="coche.nombre" required>
```
* El atributo **name** viene acompañado de la *label*, para asegurarnos que el input y la label están unidos.
* El atributo **#nombre** es con el que se revisarán los datos dentro del formulario HTML. Este será un modelo de nuestro fichero TS.
* El modelo al que hace referencia se encuentra en **[(ngModel)]**
* Por último, el required nos deja claro que para hacer enviar el formulario, este campo tiene que estar escrito.

### Formas de uso de los formularios
#### Errores
Angular nos permite verificar de forma activa los cambios dentro de los inputs, y, por tanto, podemos generar un mensaje de error en cualquier momento.
Los más comunes suelen ser:
* **dirty** - Nos dice si un elemento ya ha sido escrito.
* **touched** - Nos dice si un elemento ha sido *focuseado*.
* **invalid** - Es true en caso de que no cumpla el patrón, sea requerido, o cualquier otro motivo de invalidez (Dentro de este ámbito, encontramos el resto de posibilidades: si el patrón es correcto, si el objeto es requerido, si necesita una logitud exacta, etc.)
```html
<p *ngIf="nombre.dirty && nombre.invalid">El color es incorrecto.</p>
```

#### Deshabilitar submit
Una de las ventajas que nos aporta los formularios de Angular es la posibilidad de añadir el atributo **[disabled]** dentro de un elemento, y asignarle una variable. En caso afirmativo, éste estará deshabilitado, y en caso negativo, estará disponible para poder hacer *submit*.
```html
<input type="submit" value="Enviar" [disabled]="!formCoche.form.valid">
```

#### Ejecución de órdenes al enviar
Al estar usando Angular, éste nos aporta algunas directivas como puede ser el **(ngSubmit)**. Lo que hace esto es que al presionar un botón de submit, se ejecutan las funciones que contine la directiva
En este caso, primero se envía el dato para colocar el elemento en el array, y justo después se limpia el input **nombre**
```html
<form #formCoche="ngForm" (ngSubmit)="send(nombre.value, caballaje.value, color.value); formCoche.reset();">
    <!-- Nombre -->
    <label for="nombre">Nombre:</label>
    <input type="text" name="nombre" #nombre="ngModel" [(ngModel)]="coche.nombre" required><br>
    <p *ngIf="nombre.touched && nombre.invalid">El nombre es incorrecto.</p>

    <input type="submit" value="Enviar"  [disabled]="!formCoche.form.valid"/>
</form>
```

## forms.component.ts
Aqui se encuentra el *modelo*, anteriormente mencionado, tenemos **coche**, que es una instancia vacía de **Coche**. Cada atributo de este objeto se va modificando gracias al Two Way Data Binding y a los formularios.
Lo realmente importante estaría en el fichero html, ya que puede ser el causante de: 
* No filtrar bien los contenidos escritos, que pueden llevar a inyección maliciosa de código
* Una mala estructuración del formulario, haciendo que este pueda ser ejecutado en cualquier momento
* O lo más simple, una mala experiencia de usuario por no haber añadido ciertas características al formulario.
```javascript
@Component({
  selector: 'app-forms',
  templateUrl: './forms.component.html',
  styleUrls: ['./forms.component.scss']
})
export class FormsComponent {
  protected coche: Coche = new Coche("", "", "");

  protected coches: Coche[] = [
    new Coche("Toyota Papa", "120", "#ffffff")
  ]

  send(nombre: string, caballaje: string, color: string) {
    debugger
    this.coches.push(new Coche(nombre, color, caballaje));
  }
}
```