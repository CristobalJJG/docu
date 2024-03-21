# Capítulo 3 - Una nueva aplicación/módulo

[https://www.odoo.com/capitulo3](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/03_newapp.html)

Con este capítulo se pretende crear un nuevo módulo para Odoo.

Los módulos se forman teniendo dentro de un directorio un fichero `__init__.py` y un fichero `__manifest__.py`.

## **__init__.py**

Este fichero sirve para importar los modelos.  
(He terminado el tutorial, si tiene algún otro propósito, no se ha enseñado en el tutorial)

```python
from . import models
```

## **__manifest__.py**

Este fichero contiene la información del módulo/aplicación que tendrá nuestro modúlo. Para ver un fichero con la información auxiliar necesaria, se puede acceder a [github/odoo/manifest](https://github.com/odoo/odoo/blob/fc92728fb2aa306bf0e01a7f9ae1cfa3c1df0e10/addons/crm/__manifest__.py) para completar el capítulo 3, el fichero manifest básico para encontrarlo filtrado por aplicación:

```python
{
    'name': 'estate',
    'depends': [
        'base_setup'
    ],
    'application': True,
}
```
