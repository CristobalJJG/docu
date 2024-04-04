# Variables relacionadas
Problema, tenemos dos tablas, una llamada `nutritional_product` y otra llamada `nutritional_type`. En la tabla `nutritional_product` tenemos un campo llamado `nutritional_type_id` que es una relación a la tabla `nutritional_type`. Queremos mostrar en la vista de la tabla `nutritional_product` **las unidades** del tipo nutricional al que pertenece el producto. ¿Cómo podemos hacer esto?

```python
# nutritional_product.py
from odoo import fields, models

class NutricionalProduct(models.Model):
    """Product nutritional information."""

    _name = 'nutritional.product'
    _description = 'Relate products with its nutritional information'
    
    ...
    nutritional_id = fields.Many2one('nutritional.type', required=True)
    ...
    units = fields.Char(related='nutritional_id.units')
    ...
```

Gracias a esto, tendremos la variable `unit`, que hace referencia al campo `unit` de nutritional_type, y, por tanto, podremos mostrarla en la vista de la tabla `nutritional_product`.