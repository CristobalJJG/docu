# Directorio hasta ahora

```
estate
    - models (Modelos de la BBDD)
        - __init__.py
        - estate_property.py
    -security
        - ir.model.access.csv
    - __manifest__.py
    - __init__ .py
```
<!-- tabs:start -->

<!-- tab:./manifest.py -->
* **name**: Nombre del módulo  
* **depends**: Dependencias del módulo - En este caso, solo el módulo base_setup, pero no encontraremos que puede ser necesario depender tanto de módulos propios como externos.  
* **data**: Ficheros de datos que se cargarán al instalar el módulo - En nuestro caso, y hasta donde he visto, irán las vistas de la página, así como los ficheros de datos.  
* **application**: Si es True, se mostrará en la lista de aplicaciones instaladas.  
```python
# ./__manifest__.py
{
    'name': 'estate',
    'depends': [
        'base_setup'
    ],

    'data': [
        'security/ir.model.access.csv',
    ],
    'application': True,
}
```
<!-- tab:./init.py -->
Sirve, en principio, solo para importar los modelos.
```
# ./__init__.py
from . import models
```
<!-- tab:./models/init.py -->
Sirve, en principio, para importar **TODOS** los modelos dentro de este fichero.
```python
# ./models/.__init__.py
from . import estate_propety
```
<!-- tab:./models/estate.py -->
Este es el modelo que nos han pedido crear. Contiene un número de campos que se han ido añadiendo a lo largo de los capítulos anteriores.

```python
# ./models/estate_property.py
from odoo import fields, models
class EstateProperty(models.Model):
    _name = 'estate.property'
    _description = "Prueba para que no aparezca warning por falta de _descripcion"

    name = fields.Char(required=True)
    description = fields.Text()
    postcode = fields.Char()
    date_availability = fields.Char()
    expected_price = fields.Float(required=True)
    selling_price = fields.Float()
    bedrooms = fields.Integer()
    living_area = fields.Integer()
    facades = fields.Integer()
    garage = fields.Boolean()
    garder = fields.Boolean()
    garden_area = fields.Integer()
    garden_orientation = fields.Selection(
        selection=[("north", "North"), ("east", "East"), ("south", "South"), ("west", "West")]
    )
```

<!-- tab:./security/ir.model.access.csv -->
Este es el archivo que nos piden crear en el capítulo 5.
```csv
#./security/ir.model.access.csv
id,name,model_id:id,group_id:id,perm_read,perm_write,perm_create,perm_unlink
access_estate_property,access_estate_property,model_estate_property,base.group_user,1,0,0,0
```
## Actualizacion
Lo ideal seria tener los permisos tal que ```1,1,1,0``` y cambiar estos permisos segun el grupo.

<!-- tabs:end -->
