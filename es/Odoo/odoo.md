# Odoo

(Se asume que tanto el **Core** como los **addons** están instalados y funcionando)

# Capítulo 3 - Una nueva aplicación/módulo

[https://www.odoo.com/capitulo3](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/03_newapp.html)

Los módulos se forman teniendo dentro de un directorio un fichero `__init__.py` y un fichero `__manifest__.py`.

## ****manifest**.py**

Este fichero contiene la información del módulo/aplicación/nombre que tendrá nuestro modúlo. Para ver un fichero con la información auxiliar necesaria, se puede acceder a [github/odoo/manifest](https://github.com/odoo/odoo/blob/fc92728fb2aa306bf0e01a7f9ae1cfa3c1df0e10/addons/crm/__manifest__.py)  
para completar el capítulo 3, el fichero manifest básico para encontrarlo filtrado por aplicación:

```python
{
    'name': 'estate',
    'depends': [
        'base_setup'
    ],
    'application': True,
}
```

# Capítulo 4 - Modelos y campos básicos

[https://www.odoo.com/capitulo4](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/04_basicmodel.html)

## Mapeo relacional de datos

Odoo usa un ORM, que significa en en vez de escribir mucho SQL, se crearán modelos que "sustituirán" las llamadas a la BBDD.

Los objetos extienden del `Model (from odoo import models)` .

Los modelos se configuran estableciendo atributos. `_name` es el esencial, que **da nombre a la TABLA**

Nos dará un warning si no tiene un atributo `_descripcion`, por lo que también sería conveniente ponerlo.

```python
from odoo import models

class EstateProperty(models.Model):

    _name = 'estate.property'
    _description = "Prueba para que no aparezca warning por falta de _descripcion"
```

> Si tienes algún problema / no se importa el modelo en la BBDD, **asegúrate** de hacer las importaciones necesarias, tanto en el `__init__.py` de **models** como en el **general** del módulo.

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

# Capítulo 5 - Seguridad

[https://www.odoo.com/capitulo10](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/05_securityintro.html)
Odoo es un sistema altamente **impulsado por datos**.

```csv
"id","country_id:id","name","code"
state_us_1,us,"Alabama","AL"
state_us_2,us,"Alaska","AK"
```

- `id` es un identificador externo . Se puede utilizar para hacer referencia al registro (sin conocer su identificador en la base de datos).
- `country_id:id` se refiere al país utilizando su identificador externo .
- `name` es el nombre del estado.
- `code` es el código del estado.

Si tienes mal esta parte, la propia terminal te dará un error diciéndote el mínimo que tienes qeu colocar en este fichero para que esté correcto.

El capítulo 5 nos pide como ejercicio que:

> Agregue derechos de acceso.  
> Cree el archivo `ir.model.access.csv` en la carpeta adecuada y defínalo en el archivo `__manifest__.py`.  
> Dar permisos de lectura, escritura, creación y desvinculación al grupo `base.group_user`.  
> **Consejo**: el mensaje de advertencia en el registro le brinda la mayor parte de la solución ;-)

```csv
id, name, model_id/id, group_id, perm_read, perm_write, perm_create, perm_unlink
access_estate_property,access_estate_property,model_estate_property,base.group_user,1,0,0,0
```

---

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

# ./__init__.py
from . import models

# ./models/.__init__.py
from . import estate_propety

# ./models/state_property.py
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

#./security/ir.model.access.csv
id,name,model_id:id,group_id:id,perm_read,perm_write,perm_create,perm_unlink
access_estate_property,access_estate_property,model_estate_property,base.group_user,1,0,0,0

## Actualizacion, lo ideal seria tener los permisos tal que 1,1,1,0 y cambiar estos permisos segun el grupo
```

---

# Capítulo 6 - Interfaz de Usuario

[https://www.odoo.com/capitulo6](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/06_firstui.html)

(Archivos de datos XML)[https://www-odoo-com.translate.goog/documentation/14.0/developer/reference/addons/data.html?_x_tr_sl=auto&_x_tr_tl=en&_x_tr_hl=en#reference-data]

## Crear un menu minimo

Información básica:

> Añade una acción.  
> Cree el estate_property_views.xml archivo en la carpeta adecuada y defínalo en el **manifest**.pyarchivo.  
> Crea una acción para el modelo estate.property.

```xml
<?xml version="1.0"?>
<odoo>
    <data>
        <record id="estate_property_action" model="ir.actions.act_window">
            <!-- Nombre  del item-->
            <field name="name">Propiedades</field>
            <!-- Modelo, que sera el nombre cambiando _ por . -->
            <field name="res_model">estate.property</field>
            <!-- Se cambia la forma en la que se ve -->
            <field name="view_mode">tree,form</field>
        </record>
    </data>
</odoo>
```

## Ver visualmente nuestro modelo

> Agregar menús.  
> Cree el archivo `estate_menus.xml` en la carpeta adecuada y defínalo en el archivo `__manifest__.py`. Recuerda la carga secuencial de los archivos de datos ;-)  
> Crea los tres niveles de menús para la acción `estate.property` creada en el ejercicio anterior.

```xml
<?xml version="1.0"?>
<odoo>
    <data>
        <record id="estate_property_action" model="ir.actions.act_window">
            <!-- Nombre  del item-->
            <field name="name">Propiedades</field>
            <!-- Modelo, que sera el nombre cambiando _ por . -->
            <field name="res_model">estate.property</field>
            <!-- Se cambia la forma en la que se ve -->
            <field name="view_mode">tree,form</field>
        </record>

        <!-- General, se ve en la lista de desplegables -->
        <menuitem id="estate_menu_root" name="Estate App">
        <!-- Una vez dentro de la aplicacion, se ve este texto en la cabecera -->
            <menuitem id="estate_first_level_menu" name="First Level">
            <!-- Al desplegar el item de la cabecera, podemos ver este (es, en esencia, un alias de la accion tal que record.id = menuitem.action) -->
                <menuitem id="estate_property_menu_action" action="estate_property_action"/>
            </menuitem>
        </menuitem>
    </data>
</odoo>
```

## Tener restricciones dentro de los campos

Volvemos al modelo para ponerle restricciones dentro de cada atributo.
Atributos más comunes de un field:

- `readonly=True`: Solo lectura.
- `required=True`: El valor que se le inserta no puede ser nulo.
- `copy=False`: El atributo no se copiará al duplicar el registro.
- `default=value`: Valor o callable por defecto.

> Establecer el precio de venta como de solo lectura.  
> Evitar la copia de la fecha de disponibilidad y los valores del precio de venta.

```python
    selling_price = fields.Float(readonly=True, copy=False)
    date_availability = fields.Char(name="Available From", copy=False)
```

### Valores predeterminados

```python
name = fields.Char(default="Unknown")
last_seen = fields.Datetime("Last Seen", default=lambda self: fields.Datetime.now())
number = fields.Integer(default="2")
```

> El número predeterminado de dormitorios es 2  
> La fecha de disponibilidad predeterminada es en 3 meses
> Consejo: esto podría ayudarte:today()

```python
    date_availability = fields.Date(name="Available From", copy=False, default=lambda self: fields.date.today() + timedelta(days=92))
    bedrooms = fields.Integer(default=2)
```

## Campos reservados

Campos como `name` o `active` son reservados para ciertas funciones.
En este caso, nos piden que coloquemos una tributo ative dentro del modelo, para poder asignarlo como filtro como checkbox dentro de Odoo.

> Agregue el activecampo al estate.propertymodelo.

```python
    active = fields.Boolean(default=True)
```

> Agregue un statecampo al estate.propertymodelo. Son posibles cinco valores: Nuevo, Oferta recibida, Oferta aceptada, Vendido y Cancelado. Debe ser obligatorio, no debe copiarse y debe tener su valor predeterminado establecido en "Nuevo".  
> ¡Asegúrate de utilizar el tipo correcto!

```python
    state = fields.Selection(
        selection=[("nuevo", "Nuevo"), ("of_rec", "Oferta Recibida"), ("of_ace", "Oferta Aceptada"), ("vendido", "Vendido"), ("cancelado", "Cancelado")],
        required=True,
        copy=False,
        default="nuevo"
    )
```

# Capítulo 7 - Vista básicas (creacion de vistas)

[https://www.odoo.com/capitulo7](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/07_basicviews.html)

Para crear una vista, tendremos que crear otro record, que nos aporte la vista, este tendran un nombre y el modelo que querramos observar:

```python
<record id="estate_property_tree_view" model="ir.ui.view">
    <field name="name">Estate View</field>
    <field name="model">estate.property</field>
</record>
```

Para tener las columnas concretas tendremos que usar las etiquetas `<tree name="variable_name"/>`

## Trees

Especifica los componentes que se encuentran en la vista de tree.  
¿Qué significa? Según accedemos a la visión general del atributo, podemos ver que solo nos muestra el nombre, por lo que, **modificando la tree view**, podremos ver, esta vista de listas, **las columnas** que nosotros queramos. No es necesario poner todos los atributos del modelo, solo los que necesites.

Pone la siguiente advertencia, pero como soy super listo, ni se me ocurrió la de copiar y pegar, pero de aqui en adelante sí, jeje.

> **Advertencia**  
> Probablemente utilizará algo de copiar y pegar en este capítulo, por lo tanto, asegúrese siempre de que el **id** siga siendo único para cada vista.

> Defina una vista de lista para el `estate.property `modelo en el archivo XML apropiado. Consulte el Objetivo de esta sección para ver los campos que se mostrarán.  
> **Consejos:**  
> No agregue el atributo` editable="bottom"` que puede encontrar en el ejemplo anterior. Volveremos a ello más tarde.  
> Es posible que sea necesario adaptar algunas etiquetas de campo para que coincidan con la referencia.

```python
<field name="arch" type="xml">
    <tree string="datos">
        <field name="name"/>
        <field name="postcode"/>
        <field name="bedrooms"/>
        <field name="living_area"/>
        <field name="expected_price"/>
        <field name="selling_price"/>
        <field name="date_availability"/>
    </tree>
</field>
```

![tree_view](./img/tree_view.png)

## Form View

Especifica los datos que se ven a la hora de tener un elemento en concreto.  
¿Qué significa? Cuando clicamos uno de los elementos de la lista (tree), nos llevará a esta vista. Por lo general, he escuchado que se llama "**Vista de producto**" o "**Vista individual**"

Form > Sheet

- **group** se usa para agrupar un conjunto de campos. Genera un grupo tal que:

```html
<b>tag</b><span>tag_value</span>
```

- **notebook** se usa para tener distintas pestañas, asumo que es bastante intuitivo verlo en el caso de tener un excesivo número de datos y sea incómodo tener todo en 1 sola página.
- **page** se usa como separación entre pestañas. El atributo **string** proporcionará el nombre que se ve en la pestaña.

```xml
<notebook>
    <page string="Description">
        <group>
            <field name="description"/>
            <field name="bedrooms"/>
        </group>
    </page>
</notebook>
```

> En el ejercicio te piden que lo dejes como en la foto de los objetivos, es aproximadamente asi

```python
<record id="estate_property_form_view" model="ir.ui.view">
        <field name="name">Form View</field>
        <field name="model">estate.property</field>
        <field name="arch" type="xml">
            <form string="Test">
                <sheet>
                    <group>
                        <group>
                            <field name="postcode"/>
                            <field name="date_availability"/>
                        </group>
                        <group>
                            <field name="expected_price"/>
                            <field name="selling_price"/>
                        </group>
                        <notebook>
                            <page string="Description">
                                <group>
                                    <field name="description"/>
                                    <field name="bedrooms"/>
                                    <field name="living_area"/>
                                    <field name="facades"/>
                                    <field name="garage"/>
                                    <field name="garden"/>
                                    <field name="garden_area"/>
                                    <field name="garden_orientation"/>
                                </group>
                            </page>
                        </notebook>
                    </group>
                </sheet>
            </form>
        </field>
    </record>
```

![Form view](./img/form_view.png)

## Search View

Nos aporta cierta información, filtros y agrupaciones dentro de la vista de Lista (Tree).

Hay (según se ve en el tutorial), 3 tipos de búsquedas:

- **Campos** por los que buscar:

```python
<field name="name"/>
```

- **Campos** por los que agrupar:

```python
<group expand="1" string="Group by...">
    <filter name="postcode" string="Postcode"
            context="{'group_by' : 'postcode'}"/>
</group>
```

- **Filtros** por los que buscar:

```python
<filter name="Available"
    domain="['|', ('active', '=', True), ('active', '=', False)]"/>
```

> El **ejercicio** te pide recrear las fotos que ponen, en esencia, es este código:

```python
<record id="estate_property_search_view" model="ir.ui.view">
    <field name="name">Property state Search View</field>
    <field name="model">estate.property</field>
    <field name="arch" type="xml">
        <search string="estate_property_search">
            <field name="name"/>
            <field name="postcode"/>
            <field name="expected_price"/>
            <field name="bedrooms"/>
            <field name="living_area"/>
            <field name="facades"/>
            <group expand="1" string="Group by...">
                <filter name="postcode" string="Postcode"
                            context="{'group_by' : 'postcode'}"/>
            </group>
            <field name="active"/>
            <filter name="Available"
                        domain="['|', ('active', '=', True), ('active', '=', False)]"/>
        </search>
    </field>
</record>
```

![Fields - campos de busqueda](./img/search/fields.png)
![Filters](./img/search/filter.png)
![Group By - Agrupar por un campo en concreto](./img/search/group.png)

# Capítulo 8 - Relaciones entre modelos

[https://www.odoo.com/capitulo8](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/08_relations.html)

## Muchos a 1

Si queremos que **muchos** modelos puedan acceder a **un solo** modelo tendremos que utilizar el campo `fields.Many2one("modelo", string="nombre")`  
Por ejemplo, queremos que muchos **EstatesProperties** tengan 1 solo **Comprador/Vendedor**

## Muchos a Muchos

Si queremos que **muchos** modelos puedan acceder a **muchos** modelos tendremos que utilizar el campo `fields.Many2Many("modelo", string="nombre")`  
Por ejemplo, queremos que muchos **EstatesProperties** tengan muchos **Tags**

En el caso de los **tags**, queda bastante estético recogerlos en el xml tal que:

```xml
<field name="tags_id" widget="many2many_tags"/>
```

## 1 a Muchos

Si queremos que **un** modelo pueda acceder a **muchos** modelos tendremos que utilizar el campo `fields.Many2one('modelo',  string="name")`  
Por ejemplo, queremos que una **Propiedad** tengan muchas **Ofertas**

# Capitulo 9 - Campos calculados y cambios

[https://www.odoo.com/capitulo9](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/09_compute_onchange.html)

Resumen de 1/3 de la página:

## Computar algo (Compute method)

Para que se actualice solo, deberemos crear una función que sea la que haga el cálculo:

```python
total_area = fields.Integer(compute='_compute_total_area')
def _compute_total_area(self):
    for rec in self:
        rec.total_area = rec.living_area + rec.garden_area
```

A esta función le colocaremos el decorador `@api.compute` con las variables que se usarán dentro de la función, quedando al final tal que:

```python
garden_area = fields.Integer()
living_area = fields.Integer()
total_area = fields.Integer(compute='_compute_total_area')

@api.depends("living_area", "garden_area")
def _compute_total_area(self):
    for rec in self:
        rec.total_area = rec.living_area + rec.garden_area
```

## Invertir algo (Inverse method)

El metodo inverso se usa con la intención de modificar un atributo en el momento de guardar.
Pa

```python
    def inverse_date_deadline(self):
        for record in self:
            fecha1 = record.date_deadline
            fecha2 = record.create_date
            record.validity = (fecha1 - fecha2).days
```

## onchange

Sirve rollo web, cada vez que se actualice una variable, ocurriran ciertas cosas.

```python
@api.onchange("garden")
def _onchange_garden(self):
    if self.garden:
        self.garden_area = 10
        self.garden_orientation = "north"
    else:
        self.garden_area = 0
        self.garden_orientation = ""
```

## Nota / Tips

**Compute** se llama en cada cambio a las dependencias, mientras que **Inverse** se llama solo al guardar el registro.
Con respecto a **Compute** y **onchange** la diferencia reside en la forma en la que se guardan o no los datos en la BBDD. Según el tutorial, pone que es preferible el uso del `compute` antes que el uso del `onchange`.
Según la sabiduría de la experiencia (Alejandro), **compute** debería usarse con la intención de generar un resultado por ejemplo, calcular una media.
Mientras que **onchange** debería usarse para modificar varios campos a la vez en función de 1 único cambio.

# Capítulo 10 - ¿Preparado para algo de Acción?

[https://www.odoo.com/capitulo10](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/10_actions.html)

En este capítulo se han visto la ubicación de cosas en **cabecera**, las **acciones de botones** dentro de un modelo, el _lanzamiento de errores_ con **UserError**, y la capacidad de añadir **iconos** a los botones.

## Cabecera

Funciona igual que las cabeceras de html, se ubican dentro del apartado pertinente (_tree o form_), antes del _sheet_, y dentro (asumo) puede llevar cualquier cosa, no solo botones.

```xml
<form string="Test">
    <header>
        <button name="action_sold" type="object" string="SOLD"/>
        <button name="action_cancel" type="object" string="CANCEL"/>
    </header>
    <sheet>
        <field name='campo'/>
    </sheet>
</form>
```

![Header](./img/cap10/header.png)

## Acción en botones

Funciona de forma parecida a web, lo que en web se usa como un `onClick="moduleAction()`, aqui funciona como `name='module_action'` que tiene que estar ubicado en el modelo pertinente.

```xml
<header>
    <button name="action_sold" type="object" string="SOLD"/>
    <button name="action_cancel" type="object" string="CANCEL"/>
</header>
```

```python
def action_cancel(self):
    self.state = "cancelado"

def action_sold(self):
    self.state = "vendido"
```

## Lanzamiento de errores con UserError

Asumo que habrá millones de tipos de errores, en este caso, se lanza un error de usuario.

```python
from odoo.exceptions import UserError

def action_cancel(self):
    if self.state == 'vendido':
        raise UserError('No se puede cancelar una propiedad vendida')
    self.state = "cancelado"

def action_sold(self):
    if self.state == 'cancelado':
        raise UserError('No se puede vender una propiedad cancelada')
    self.state = "vendido"
```

![userError](./img/cap10/userError.png)

## Iconos

La forma de añadir iconos a un botón sería utilizando la etiqueta `icon="icon_name"` dentro de `<button />`

```xml
<button name="action_accept" type="object" icon="fa-check"/>
<button name="action_refuse" type="object" icon="fa-times"/>
```

![Iconos de check y cross](./img/cap10/icons.png)

# Capítulo 11 - Restricciones

[https://www.odoo.com/capitulo11](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/11_constraints.html)

## Restricciones SQL

[Pagina oficial PostgreSQL](https://www.postgresql.org/docs/current/ddl-constraints.html#DDL-CONSTRAINTS-UNIQUE-CONSTRAINTS)

Se utiliza la variable reservada `_sql_constratins` con una lista de restricciones de la forma:

```python
_sql_constraints = [
    ('check_price_positive', 'CHECK(price >= 0)',
        'El precio debe ser positivo')
]
```

otro ejemplo sería con una variable única:

```python
_sql_constraints = [
    ('check_unique_name', 'UNIQUE(name)',
        'El nombre de la propiedad ya existe')
]
```

## Restricciones con Python

```python
@api.constrains('price')
def check_lower_than_90p_of_expected(self):
    for record in self:
        if record.price < record.property_id.expected_price * 0.9:
            raise models.ValidationError('Precio no puede ser inferior al 90% del precio esperado')
```

# Capítulo 12 - Agrega las "¿¿chispas??"

[https://www.odoo.com/capitulo12](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/12_sprinkles.html)

Este capítulo es tan confuso como atractivo. Se ve cómo "crear un formulario con información que pertenece a un modelo externo", **statusbar** como widget, el **orden** por defecto en la lista de un modelo, **handler** comom widget para ordenar dinámicamente los campos

## Crear un Tree con los datos de un modelo externo

Creo que el ejemplo que se pone en la [página](https://www-odoo-com.translate.goog/documentation/14.0/developer/tutorials/getting_started/12_sprinkles.html?_x_tr_sl=auto&_x_tr_tl=en&_x_tr_hl=en#tutorials-getting-started-12-sprinkles) es bastante _accurate_:

Queremos obtener las variables de **text_model_line** desde **text_model**, para ello, creamos una variable (`model_id`) que una `test.model.line`, con `test_model`.

> Many to One porque muchas propiedades a un tipo.

```python
# test_model_line.py
from odoo import fields, models

class TestModelLine(models.models):
    _name = "test.model.line"
    _description = "descripcion1"

    model_id = fields.Many2one('test.model')
    name = fields.char()
    field_1 = fields.Char()
    field_2 = fields.Char()
    field_3 = fields.Char()
```

En **test_model**, queremos mostrar ciertos datos del modelo **test_model_line**, para ello, creamos la variable `line_ids`, con un campo `uno a muchos` (Por lo contrario del caso anterior).

```python
# text_model.py
from odoo import fields, models

class TestModel(models.models):
    _name = "test.model"
    _description = "descripcion"

    name = fields.char()
    line_ids = fields.One2many('test.model.line', 'model_id')
```

En nuestra vista, tendremos x campos, y el **_field_** que queramos rellenar contendrá `name=line_ids`.  
Dentro crearemos un _tree_/lista y en su interior existirán las variables que tenga el modelo. En este caso, podríamos acceder desde `line_ids`, al los campos `field_1`, `field_2`, `field_3` y `name`

```xml
<!-- test_model.xml -->
    <form>
    <field name="description"/>
    <field name="line_ids">
        <tree>
            <field name="field_1"/>
            <field name="field_2"/>
        </tree>
    </field>
</form>
```

## Widgets

### Statusbar

En las aplicaciones las transiciones visuales entre pasos ayudan. En odoo esto se hace con el `widget="statusbar"`.
En el caso del ejercicio, la transición sería nuevo > oferta recibida > oferta aceptada > vendido.

Esto se conseguiría con:

```xml
<header>
    <field name="state" widget="statusbar"
           statusbar_visible="nuevo,of_rec,of_ace,vendido"/>
</header>
```

```python
STATE_SELECTION = [
    ("nuevo", "Nuevo"),
    ("of_rec", "Oferta Recibida"),
    ("of_ace", "Oferta Aceptada"),
    ("vendido", "Vendido"),
    ("cancelado", "Cancelado")
]

state = fields.Selection(
    selection=STATE_SELECTION,
    copy=False,
    default="nuevo",
    string="Estado"
)
```

Necesitamos colocar `statusbar_visible="..."` para decir qué **estados se muestran**, ya que, por ejemplo, en este caso, no mostramos cancelado por defecto, simplemente si el state es canceled **aparece** de forma puntual en ese caso.

### Handle

En caso de querer modificar de forma manual el orden de las listas podemos utilizar `widget="handle"`

```xml
<tree string="datos">
   <field name="sequence" widget="handle"/>
   <field name="name"/>
   <field name="state"/>
   <field name="postcode"/>
   <field name="bedrooms"/>
   <field name="living_area"/>
   <field name="expected_price"/>
   <field name="selling_price"/>
   <field name="date_availability"/>
</tree>
```

![handler widget](./img/cap12/handler.png)

## Orden de listas

Podemos asignar un orden por defecto a los _tree_/listas de cada modelo.
Por ejemplo:

```python
# estate.property.py
class EstateProperty(models.Model):
    _name = 'estate.property'
    _description = "Propiedad Inmobiliaria"
    _id = "id desc"

# estate.property.offers.py
class EstatePropertyOffer(models.Model):
    _name = 'estate.property.offer'
    _description = "Ofertas de las propiedades de bienes raíces"
    _id = "price desc"
```

## Atributos y opciones

He estado esperando desde que empezó la UI a esto ejejej:
Capacidad para mostrar o no ciertos elementos según atributos u opciones.
Si queremos **_colorear nuestros tags_**, tendremos que añadir la variable con el nombre en el modelo del `tag`, y colocar el atributo `options` dentro del field de `tags_id`.

```python
#estate_property_tag.py
class EstatePropertyTag(models.Model):
    _name = 'estate.property.tag'
    _description = "Tags de Propiedad"
    _id = "name"

    name = fields.Char(required=True)
    color = fields.Integer()
```

```xml
<!-- estate_menu.xml -->
<field name="tags_id" widget="many2many_tags" options="{'color_field': 'color', 'no_create_edit': True}"/>
```

### Mostrar u ocultar campos en funcion de X

#### En función de estados

Si tenemos un conjunto de estados, como en este caso, que tenemos:

```python
STATE_SELECTION = [
        ("nuevo", "Nuevo"),
        ("of_rec", "Oferta Recibida"),
        ("of_ace", "Oferta Aceptada"),
        ("vendido", "Vendido"),
        ("cancelado", "Cancelado")
    ]
```

Usaremos el atributo `states=` donde colocaremos los estados donde se tiene que mostrar el componente.

```xml
<button name="action_cancel" type="object" string="CANCEL" states="nuevo,of_rec,of_ace"/>
```

#### Funciones booleanas

Si queremos hacer uso de una función _booleana_ para comprobar si se tiene que mostrar ese campo o no, se usa `attrs=` con el texto `{'invisible': [('var1', '=', 'var2'), ('var3', '!=', ''var4')]}`

```xml
<field name="garden_area" attrs="{'invisible': [('garden', '=', False)]}"/>
<field name="garden_orientation" attrs="{'invisible': [('garden', '=', False)]}"/>
```

Se puede usar el atributo `invisible=1` para hacer que un campo no se muestre.

```xml
<field name="is_partner" invisible="1"/>
```

#### Uso de python

Al estar usando python, podemos utilizar algunas de las ventajas que nos aporta este lenguaje tal que:

```xml
<field name="offers_ids" attrs="{'readonly':[('state','in',('vendido', 'cancelado', 'of_ace'))]}"/>
```

## Listas

Si le colocamos el atributo `editable='True'` podremos modificar las variables desde la vista de Lista/Tree.

```xml
<record id="estate_property_tree_view" model="ir.ui.view">
   <field name="name">Estate View</field>
   <field name="model">estate.property</field>
   <field name="arch" type="xml">
       <tree string="datos" editable="True">
           <field name="sequence" widget="handle"/>
           <field name="name"/>
           <field name="tags_id" widget="many2many_tags" options="{'color_field': 'color', 'no_create_edit': True}"/>
        </tree>
   </field>
</record>
```

## Mostrar datos de una vista en otra

**Da asco**, revisa los ficheros ubicados en ./Cap12/

# Capítulo 13 - Herencia / Inheritance

[https://www.odoo.com/capitulo13](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/13_inheritance.html)

Nosotros hemos heredado los modelos de Odoo. Estos modelos tienen funciones que nosotros podemos sobrescribir. En concreto, las 4 de CRUD,m `create()`, `read()`, `write()` and `unlink()`.

Para ello, tendremos que hacer uso de la api, definir la funcion con el mismo nombre, y al final de la misma retornar el método `super.function(vals)` dependiendo de la función a la que estemos sobreescribiendo:

```python
    @api.model
    def create(self, vals):
        # Do some business logic, modify vals...
        ...
        # Then call super to execute the parent method
        return super().create(vals)
```

# Capitulo 14

[https://www.odoo.com/capitulo14](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/14_other_module.html)

# Capitulo 15

[https://www.odoo.com/capitulo15](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/15_qwebintro.html)

# Cosas útiles

(0, 0, { values }) link to a new record that needs to be created with the given values dictionary
(1, ID, { values }) update the linked record with id = ID (write _values_ on it)
(2, ID) remove and delete the linked record with id = ID (calls unlink on ID, that will delete the object completely, and the link to it as well)
(3, ID) cut the link to the linked record with id = ID (delete the relationship between the two objects but does not delete the target object itself)
(4, ID) link to existing record with id = ID (adds a relationship)
(5) unlink all (like using (3,ID) for all linked records)
(6, 0, [IDs]) replace the list of linked IDs (like using (5) then (4,ID) for each ID in the list of IDs)
