# AOS - Animate On Scroll Library

Página oficial de AOS: [https://michalsnik.github.io/aos/](https://michalsnik.github.io/aos/)

## Instalación general
**Añadir los archivos de AOS al proyecto**: Primero, hay que descargar los archivos de AOS y añadirlos a tu proyecto. Puedes hacerlo manualmente o utilizando un CDN. 
    
```html
<link rel="stylesheet" href="https://cdn.rawgit.com/michalsnik/aos/2.1.1/dist/aos.css" />
<script src="https://cdn.rawgit.com/michalsnik/aos/2.1.1/dist/aos.js"></script>
```

**Inicializar AOS**: Después de añadir los archivos de AOS, es necesario inicializarlo. Esto se hace añadiendo un script al final del archivo HTML:
```html
<script>
  AOS.init();
</script>
```

**Usar AOS en tus elementos HTML**: Ahora, es posible usar AOS en los elementos HTML añadiendo el atributo ``data-aos`` a los elementos que se quieran animar.  
```data-aos-duration```: También es posible añadir un atributo  
```data-aos-duration``` para especificar la duración de la animación en milisegundos.  
```data-aos-delay```:Para especificar el retraso de la animación en milisegundos.  
```data-aos-easing```: para especificar la función de aceleración de la animación en milisegundos.  
```data-aos-offset``` para especificar el desplazamiento (en píxeles) desde el borde superior de la ventana del navegador hasta el elemento al que se le aplica la animación.  
```data-aos-anchor-placement```: Especifica la posición del elemento en relación con el elemento de anclaje. Los valores posibles son: top-bottom, top-center, top-top, center-bottom, center-center, center-top, bottom-bottom, bottom-center, bottom-top. El valor por defecto es top-bottom.  

```html
<div data-aos="fade-up">
  <h1>Hola, mundo!</h1>
</div>
```