# Decoradores

Todos los ficheros de Angular tienen una propiedad por cada clase, que le asigna un valor al mismo:

<!-- https://jhildenbiddle.github.io/docsify-tabs/#/ -->

<!-- tabs:start -->

<!-- tab:**@Component** -->

En este caso, el decorador es __@Component__, donde las variables que se pueden asignar entre otras serían:

* *selector*: que define la etiqueta que usará el componente, en este caso, se hará uso del componente con `<app-root></app-root>`
* *template*: define el código HTML literalmente entre `` que tendrá el componente.
* *templateUrl*: define la dirección del fichero HTML que se usará como plantilla del componente.
* *stylesUrl*: es un array con la dirección de los ficheros de estilos que __afectarán__ al componente

```javascript
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {
  title = 'curso-angular';
}
```

Otra forma de añadir un componente es dándole un único uso al ts del componente, como sería:

```javascript
@Component({
  selector: 'app-root',
  template: `
    <h1>Hola mundo</h1>
    <p>Que tal estamos?</p>
  `
})
export class AppComponent {
  title = 'curso-angular';
}
```

<!-- tab:**@NgModule** -->

```javascript
const routes: Routes = [];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

<!-- tab:**@Service** -->
## Servicios

Funcionan como un tipo de auxiliar para la comunicación entre nuestra página y una api res, llamadas HTTP, etc...
```javascript
@Injectable({
  providedIn: 'root'
})
export class AuthService {
  constructor() { }
}
```

<!-- tab:**@Pipe** -->

## Pipes/Tuberías

Las Pipes / Tuberías o Filtros son pequeñas funciones que ayudan a los programadores a facilitar el formateo en cierta medida de las vistas, por ejemplo:
* Formatear fechas
* Formatear el texto como camelCase, snake_case, PascalCase, todo MAYUSCULA o minuscula etc...
* Añadir un formato de moneda: Euro, Libra, Dólar...
* Hay ciertas librerias que gracias a estas pipes, nos permite traducir nuestra página.
* Una de las mejores formas de ver los datos en crudo en con la pipe de json.

```javascript
@Injectable({
  providedIn: 'root'
})
export class RopaService {

  constructor() { }
}
```

<!-- tabs:end -->
