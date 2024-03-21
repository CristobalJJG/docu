# Capítulo 4 - Modelos y campos básicos

[https://www.odoo.com/capitulo4](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/04_basicmodel.html)

## Mapeo relacional de datos

Odoo usa un **ORM**. Esto, por lo que tengo entendido, significa en en vez de escribir llamadas SQL, se **crearán modelos** con python que "sustituirán" las llamadas a la BBDD.

Los objetos extienden del `Model (from odoo import models)` .

Los modelos se configuran estableciendo atributos.  
`_name` es el esencial, que **da nombre a la TABLA y al MODELO**

Nos dará un warning si no tiene un atributo `_descripcion`, por lo que también sería conveniente ponerlo.

```python
from odoo import models

class EstateProperty(models.Model):

    #Modelo estate.property
    _name = 'estate.property'
    _description = "Prueba para que no aparezca warning por falta de _descripcion"
```

> Si tienes algún problema/no se importa el modelo en la BBDD, **asegúrate** de hacer las importaciones necesarias, tanto en el `__init__.py` de **models** como en el **general** del módulo.

## Tipos

Basándonos en el código anterior, tenemos los distintos tipos: [odoo/fields](https://www-odoo-com.translate.goog/documentation/14.0/developer/reference/addons/orm.html?_x_tr_sl=auto&_x_tr_tl=en&_x_tr_hl=en#reference-orm-fields)

Los tipos son los generales: `Integer`, `Char`, `Text`, `Float` y `Boolean`.  
Estos se recogen desde la importación de `fields`.  
En caso de ser una selección concreta de números, tendremos que declarar un `Selection` de la forma:

```python
    variable = fields.Selection(
        selection=[("north", "North"), ("east", "East"), ("south", "South"), ("west", "West")]
    )
```

También podemos asignarles las restricciones que tendrían en una BBDD, por ejemplo:

```Python
from odoo import fields, models

class EstateProperty(models.Model):
    _name = 'estate.property'
    _description = "Prueba para que no aparezca warning por falta de _descripcion"

    name = fields.Char(required=True)
```

De forma que acabaríamos el capítulo 4 con:

```python
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