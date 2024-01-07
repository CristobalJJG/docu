## **Instalación** de Docsify

```bash
npm i docsify-cli -g
```

## **Inicialización** de un proyecto con Docsify

```bash
docsify init ./docs
```

Siendo **docs** el nombre de la carpeta contenedora del proyecto, que, lo más común es que sea la carpeta de la documentación (/docs).

Esta orden genera 3 ficheros en el directorio ./docs:

* **index.html** como el fichero general html, donde se añadirán los plugins y configuraciones de Docsify.
* **README.md** como la home page de nuestra documentación.
* **.nojekyll** prevents GitHub Pages from ignoring files that begin with an underscore

## **Ver** la documentación

```bash
docsify serve docs
```

Por defecto, tendremos que acceder a http://localhost:3000 para poder ver nuestra documentación.
En caso de querer cambiar el puerto tendremos que añadir esta opción a la orden:
```bash
docsify serve docs -p 4200
```


