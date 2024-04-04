# Mostrar u ocultar campos en un Tree (Tres puntos arriba derecha)

Para mostrar o no, los datos de un Tree, tenemos que usar el atributo optional dentro del campo que queramos mostrar u ocultar.
```xml
<!-- Por defecto oculto -->
<field name="create_uid" optional="hide"/>

<!-- Por defecto visible -->
<field name="create_date" optional="show"/>
```