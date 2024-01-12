En cada versión de Angular puede cambiar la forma de hacer llamadas http. 

En mi caso, una de las tantas formas posibles fue usar HttpClient.
Para poder usarla sin errores habrá que importar su módulo en el fichero `app.module.ts` tal que:
```javascript
@NgModule({
  declarations: [
    FormsComponent,
    PeticionesComponent,
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    FormsModule,
    HttpClientModule // Deberemos importarlo para poder hacer llamadas http
  ],
  providers: [],
  bootstrap: [AppComponent]
})
```