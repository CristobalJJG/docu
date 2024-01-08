# Enrutamientos

## Fichero app-routing.module.ts
Lo primero será tener una buena configuración del fichero app-routing:
```javascript

const routes: Routes = [
  {
    path: 'ejercicios', children: [
      { path: 'ex1', component: Ex1Component },
    ]
  },
  {
    path: 'temas', children: [
      { path: 'tema1', component: Tema1Component },
      { path: 'tema2', component: Tema2Component },
    ]
  },
  {
    path: 'topicos', children: [
      { path: 'topico1', component: T1Component },
      { path: 'topico2', component: T2Component },
    ]
  },
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```


## RouterLink
Para poder viajar entre los enlaces de la página será necesario utilizar la directiva **[routerLink]**
```html
<nav >
  <a [routerLink]="['/ejercicios/ex1']">Ejercicio1</a>
</nav>
```

## RouterLinkActive
Con esta directiva podemos marcar dentro del navegador en qué enlace nos encontramos.
```html
<nav >
  <a [routerLink]="['/temas/tema1']" [routerLinkActive]="['active']">Tema1</a>
  <a [routerLink]="['/temas/tema2']" [routerLinkActive]="['active']">Tema2</a>
</nav>
```

```css
a.active{
    background-color:gray;
}
```

## Pasar parámetros
Tendremos que decir en el enlace que se pueden pasar parámetros al componente haciendo ```{ path: 'ex1/:id', component: Ex1Component }```:
```javascript
const routes: Routes = [
  {
    path: 'exer', children: [
      { path: 'ex1', component: Ex1Component },
      { path: 'ex1/:id', component: Ex1Component },
    ]
  }
];
```

Para obtener el/los datos pasados por parámetros será necesario tener inicializada la variable como string para poder recogerla al leer los parámetros del enlace.

```javascript
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute, Params, Router } from '@angular/router';
import { Empleado } from 'src/app/models/empleado';

@Component({
  selector: 'empleados',
  templateUrl: './ex1.component.html'
})
export class Ex1Component implements OnInit {
  protected empleado: string = '';

  constructor( private route: ActivatedRoute ) {}

  ngOnInit() {
    this.route.params.forEach((p: Params) => {
      console.log(p)
      this.empleado = p['id']
    })
  }
}
```

## Redireccionar desde TS

En caso de querer redireccionar:
```javascript
import { Component } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'empleados',
  templateUrl: './ex1.component.html'
})
export class Ex1Component {

  constructor( private router: Router ) {}

  redirigir() {
    this.router.navigate(['/exer/ex1/'])
  }
}
```

En caso de querer redireccionar enviando un parámetro tendremos que añadir al final del enlace el parámetro:
```javascript
  redirigir() {
    this.router.navigate(['/exer/ex1/', this.nombre])
  }
```
