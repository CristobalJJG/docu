# Capítulo 13 - Herencia / Inheritance

[https://www.odoo.com/capitulo13](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/13_inheritance.html)

## Herencia CRUD

Nosotros hemos heredado los modelos de Odoo. Estos modelos tienen funciones que podemos sobrescribir. En concreto, las 4 de CRUD, `create()`, `read()`, `write()` y `unlink()`.

Para ello, tendremos que hacer uso de la api, definir la funcion con el mismo nombre, y al final de la misma retornar el método `super.function(vals)` dependiendo de la función a la que estemos sobreescribiendo:

```python
@api.model
def create(self,vals):
    # Do some business logic, modify vals...
    ...
    # Then call super to execute the parent method
    return super().create(vals)
```

>**Ejercicio**  
>Agregue lógica de negocios a los métodos CRUD.  
>* Evitar la **eliminación** de una propiedad si su estado no es **"Nuevo"** o **"Cancelado" ** 
>Consejo: sobreescriba `unlink()` y recuerde que `self` puede ser un conjunto de registros con más de un registro.  
>* Al **crear** la oferta, establezca el estado de la propiedad en **"Oferta recibida"**. También genera un error si el usuario intenta crear una oferta con un monto menor que una oferta existente.  
<!-- tabs:start -->
<!-- tab:estate_property.py -->
```python
def unlink(self):
    if self.state in ['of_ace', 'vendido', 'of_rec']:
        raise UserError('No se puede eliminar una propiedad con ofertas o vendida')
    
    return super().unlink()
```

<!-- tab:estate_property_offer.py -->
```python
@api.model
def create(self, vals):
    property = self.property_id
    property.state = "of_rec"
    if property.best_offer <= vals.get('price'):
        property.best_offer = vals.get('price')
    else:
        raise ValidationError(
            'El precio de la oferta no puede ser inferior al valor máximo de las ofertas existentes')

    return super().create(vals)
```
<!-- tabs:end -->

## Herencia de modelos
Ahora de repente nos piden que creemos un nuevo modelo, y heredemos de `res.users`.

Para heredar de un modelo ya creado tenemos que hacer uso de la variable `_inherit` en la clase del modelo que estamos creando.

```python
class Users(models.Model):
    _inherit = "res.users"
```
Una vez dentro del modelo, podemos agregar campos, métodos, etc. que serán los campos adicionales que se agregarán al modelo original.

```python
class Users(models.Model):
    _inherit = "res.users"

    property_ids = fields.One2many('estate.property', 'seller_id', string="Propiedades")
```

>**Ejercicio**  
> Agregar un campo a Usuarios.
> * Agrega un campo ``property_ids`` que sea un **One2many** a ``estate.property``, con un campo inverso que haga referencia al vendedor de ``estate.property``.
```python
# users.py - Heredamos de res.users
from odoo import fields, models

class Users(models.Model):
    _inherit = "res.users"

    property_ids = fields.One2many('estate.property', 'seller_id', string="Propiedades")
```

## Herencia de vistas
>**Ejercicio**
>Agregue campos a la vista Usuarios.  
>Agregue el campo `property_ids` a `base.view_users_form` una nueva página del `notebook`.  
>Consejo: [aquí](https://github.com/odoo/odoo/blob/691d1f087040f1ec7066e485d19ce3662dfc6501/addons/gamification/views/res_users_views.xml) se puede encontrar un ejemplo de herencia de la vista de los usuarios.  


```xml
<!-- views - Vista general que hereda de res.users -->
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <record id="users_model_view_form" model="ir.ui.view">
        <field name="name">Usuarios</field>
        <field name="model">res.users</field>
        <field name="inherit_id" ref="base.view_users_form"/>
        <field name="arch" type="xml">
            <notebook position="inside">
                <page string="Propiedades" name="estate">
                    <h1><field name="id"/></h1>
                    <field name="property_ids" domain="[('seller_id.id', '=', id)]"/>
                </page>
            </notebook>
        </field>
    </record>
</odoo>
```