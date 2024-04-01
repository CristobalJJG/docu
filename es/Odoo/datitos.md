# Datos extra de Odoo
Estos datos pueden ser ayudas para el desarrollo o cosas que no se han dado en el tutorial.
**(WIP)**

- [Datos extra de Odoo](#datos-extra-de-odoo)
- [Generar Stat\_button en condiciones](#generar-stat_button-en-condiciones)
- [Internacionalización :es: :uk:](#internacionalización-es-uk)
  - [Obtener los ficheros iniciales](#obtener-los-ficheros-iniciales)
  - [Traducción en XML](#traducción-en-xml)
  - [Traducción en Python](#traducción-en-python)
- [Wizards](#wizards)
- [Problemas con comparaciones](#problemas-con-comparaciones)
- [Ocultar botones esenciales de Crear, Eliminar y Modificar](#ocultar-botones-esenciales-de-crear-eliminar-y-modificar)
- [Mostrar u ocultar campos en un Tree (Tres puntos arriba derecha)](#mostrar-u-ocultar-campos-en-un-tree-tres-puntos-arriba-derecha)

# Generar Stat_button en condiciones

```xml
<!-- Recubrimiento exterior -->
<div class="oe_button_box" name="button_box">
    <!-- Boton con icono -->
    <button position="after" type="action" name="%(inventory_reader_exportation_action)d"
            class="oe_stat_button" icon="fa-file">
        
        <div class="o_field_widget o_stat_info">
            <span class="o_stat_value">
                <field string="Exportaciones" name="exportations_count" widget="statinfo"/>
            </span>
            <span class="o_stat_text">Exportaciones</span>
        </div>
    </button>
</div>
```


# Internacionalización :es: :uk:
Yo solo he usado i18n con Angular, y esta forma de hacerlo me ha resultado extraña. 

En términos generales, tendremos un directorio llamado i18n, que contendrá 2 ficheros, uno con las traducciones **idioma origen** y **idioma destino**, y otro como **"plantilla"**.
Estos ficheros se consiguen exportándolos de Odoo, es la forma más sencilla de tenerlos.

## Obtener los ficheros iniciales

Para ello, estando con el modo debug activado (Extensión de Gorila), entraremos a Ajustes > Traducciones > Importar/Exportar > Exportar traducción.
Eso lo tendremos que hacer 1 vez para el fichero de idiomas, y otra vez para el fichero de la plantilla.
Idiomas:
* Idioma: Spanish/Español
* Formato de archivo: PO
* Aplicacion a exportar: (Escribiremos el módulo que queremos traducir)

Damos a exportar, esperamos, y descargammos el fichero .po que nos aporta el *wizard*.

Haremos lo mismo con la plantilla, pero en este caso, seleccionaremos la opción de "Plantilla" en lugar de "Idioma".
* Idioma: Nuevo idioma (plantilla de traduccion vacia)
* Formato de archivo: PO
* Aplicacion a exportar: (Escribiremos el módulo que queremos traducir / Debería ser el mismo que el anterior)

## Traducción en XML
Al realizar el apartado anterior, tendremos que colocar dentro de la orden para ejecutar la aplicación `--i18n-overwrite`.
Y deberia funcionar sin problemas.

## Traducción en Python
Para traducir en Python, se hace de la siguiente forma:
Y luego, en el campo que queramos traducir, añadimos el `_` al principio de la cadena.
```python
from odoo import api, fields, models, _
name = fields.Char(string=_("Nombre"))
```


# Wizards
Los wizards son ventanas emergentes que se utilizan para realizar acciones que no se pueden hacer en una vista normal.
(Todavía no he hecho ninguno, pero dejo un ejemplo de cómo debería hacerse)
Todo esto iría dentro del módulo que estemos trabajando:

```
module/
    models/
        __init__.py
        module.py
    views/
        module.xml
    wizards/
        __init__.py
        module_wizard.py
        module_wizard.xml
    __init__.py
    __manifest__.py
```

```python
from odoo import models, fields, api

class Wizard(models.TransientModel):
    _name = 'module.wizard'
    _description = 'Wizard description'

    name = fields.Char(string='Name', required=True)
    date = fields.Date(string='Date', required=True)

    def action_confirm(self):
        # Do something
        return {'type': 'ir.actions.act_window_close'}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<odoo>
    <record id="view_module_wizard" model="ir.ui.view">
        <field name="name">module.wizard.form</field>
        <field name="model">module.wizard</field>
        <field name="arch" type="xml">
            <form string="Wizard">
                <group>
                    <field name="name"/>
                    <field name="date"/>
                </group>
                <footer>
                    <button name="action_confirm" string="Confirm" type="object" class="btn-primary"/>
                    <button string="Cancel" class="btn-secondary" special="cancel"/>
                </footer>
            </form>
        </field>
    </record>
</odoo>
```

# Problemas con comparaciones

A veces, nos dirá que no se puede colocar cierto caracter dentro de una comparación, por ejemplo, un `<`. Por lo que para poder usarlos de forma normal, tendremos que hacer la conversión a:
`&lt;` (<), `&amp;` (&), `&gt;` (>), `&quot;` ("), and `&apos;` (').

# Ocultar botones esenciales de Crear, Eliminar y Modificar

Podemos tener la necesidad de tener que ocultar de alguna manera los botones de Crear, Eliminar o Modificar. Para ello, podemos hacer uso de la siguiente forma:
```xml
<record id="inventory_reader_exportation_tree" model="ir.ui.view">
    <field name="name">Exports Tree View</field>
    <field name="model">inventory.reader.exportation</field>
    <field name="arch" type="xml">
        <tree string="Exports" create="false" edit="false" delete="false">
            <field name="create_uid"/>
            <field name="create_date" string="Date"/>
            <field name="name"/>
        </tree>
    </field>
</record>
```

No lo he probado, pero asumo que tambien debería funcionar con las vistas de Form y Kanban.

# Mostrar u ocultar campos en un Tree (Tres puntos arriba derecha)

Para mostrar o no, los datos de un Tree, tenemos que usar el atributo optional dentro del campo que queramos mostrar u ocultar.
```xml
<!-- Por defecto oculto -->
<field name="create_uid" optional="hide"/>

<!-- Por defecto visible -->
<field name="create_date" optional="show"/>
```