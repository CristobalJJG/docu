# Capítulo 6 - Interfaz de Usuario (Menús)

[https://www.odoo.com/capitulo6](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/06_firstui.html)

[Archivos de datos XML](https://www-odoo-com.translate.goog/documentation/14.0/developer/reference/addons/data.html?_x_tr_sl=auto&_x_tr_tl=en&_x_tr_hl=en#reference-data)

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

* **id**: Identificador único para la acción.
* **model**: `ir.actions.act_window` es el modelo de acción de ventana. Existen muchos, y muy variados, se irán viendo a lo largo del Tutorial.
* **name**: Nombre de la acción.
* **res_model**: Modelo al que se refiere la acción.
* **view_mode**: Modo de vista de la acción. En este caso, `tree,form` significa que se mostrará en forma de árbol y formulario. También se pueden añadir `kanban` o `calendar` para verlo en modo kanban o calendario, respectivamente.

## Tener de forma visual nuestro modelo

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

Se intenta explicar con los comentarios.
Los ids tienen que ser únicos, y se pueden usar para referenciarlos en otros archivos.
En este caso, podemos ver 3 niveles de menús, con el último nivel siendo la acción que hemos creado en el ejercicio anterior.
Esto implica que:

* Tendremos **Estate App** en la **lista de aplicaciones** (En la versión community, sería clicar los cuadraditos ubicados en la esquina superior izquierda, en la cabecera).
* Dentro de **Estate App**, tendremos **First Level**.
* Al clicar en **First Level**, se nos mostrará lista de elementos dentro, yal clicar en **Propiedades** la acción de estate.property, que es la lista de propiedades.

(Hay que tener clara esta jerarquía, ya que si no, no se mostrará correctamente en la interfaz de usuario) Al terminar el tutorial, tendremos algo parecido a esto como gestión de menús.

```xml
<!-- LLamada a Estate property -->
<record id="estate_property_action" model="ir.actions.act_window">
    <field name="name">Propiedades</field>
    <field name="res_model">estate.property</field>
    <field name="view_mode">tree,form</field>
</record>
<!-- LLamada a Estate property con vista **Kanban** -->
<record id="estate_type_kanban_action" model="ir.actions.act_window">
    <field name="name">Propiedades Kanban</field>
    <field name="res_model">estate.property</field>
    <field name="view_mode">kanban</field>
</record>
<!-- LLamada al tipo de propiedad -->
<record id="estate_property_type_action" model="ir.actions.act_window">
    <field name="name">Tipos de propiedad</field>
    <field name="res_model">estate.property.type</field>
    <field name="view_mode">tree,form</field>
</record>
<!-- LLamada a las etiquetas -->
<record id="estate_property_tag_action" model="ir.actions.act_window">
    <field name="name">Tags</field>
    <field name="res_model">estate.property.tag</field>
    <field name="view_mode">tree,form</field>
</record>

<!-- Menu general - se veran en aplicaciones -->
<menuitem id="estate_menu_root" name="Estate App">
    <!-- Menu First View, se vera en la cabecera de la aplicacion -->
    <menuitem id="estate_first_level_menu" name="First Level">
        <!-- Opcion - estate-property - al desplegar First Level -->
        <menuitem id="estate_property_menu_action" action="estate_property_action"/>
        <!-- Opcion - estate-property-kanban - al desplegar First Level -->
        <menuitem id="estate_kanban_menu_action" action="estate_type_kanban_action"/>
    </menuitem>
    <!-- Menu Settings, se vera en la cabecera de la aplicacion -->
    <menuitem id="estate_type_menu" name="Settings">
        <!--  Opcion - estate-property-type - al desplegar Settings  -->
        <menuitem id="estate_type_property_menu_action" action="estate_property_type_action"/>
        <!--  Opcion - estate-property-tag - al desplegar Settings  -->
        <menuitem id="estate_tag_property_menu_action" action="estate_property_tag_action"/>
    </menuitem>
</menuitem>
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
last_seen = fields.Datetime("Last Seen", default=lambda self: fields.Datetime.now())
number = fields.Integer(default="2")
```

> El número predeterminado de dormitorios es 2
> La fecha de disponibilidad predeterminada es en 3 meses
> Consejo: esto podría ayudarte : today()

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
