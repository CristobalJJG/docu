# Templates

En las primeras versiones de Angular, para mostrar o no mostrar un elemento en el HTML había que hacer:
```html
<div *ngIf="administrador">Eres admin</div>
<div *ngIf="!administrador">No eres admin</div>
```

En la actualidad podemos usar templates, pequeños trozos de código que solo cargan en la página si los elementos con el ngIf los llaman.  
Su forma de uso es tal que:
```html
<div *ngIf="administrador; else noAdmin">Eres Admin</div>
<ng-template #noAdmin>No eres admin</ng-template>
```

O, incluso, solo generar templates:
```html
<div *ngIf="administrador; then admin ;else noAdmin"></div>

<ng-template #admin>Eres admin</ng-template>
<ng-template #noAdmin>No eres admin</ng-template>
```