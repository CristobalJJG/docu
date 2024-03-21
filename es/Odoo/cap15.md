# Capitulo 15 - Kanban

[https://www.odoo.com/capitulo15](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/15_qwebintro.html)

Hay info "útil" en la página oficial [kanban](https://www-odoo-com.translate.goog/documentation/14.0/developer/reference/addons/views.html?_x_tr_sl=auto&_x_tr_tl=en&_x_tr_hl=en#reference-views-kanban).

Para crear una vista kanban, lo primero es definir una vista como kanban. En este caso, se usó la de `estate.property`:
```xml
<record id="estate_type_kanban_action" model="ir.actions.act_window">
    <field name="name">Propiedades Kanban</field>
    <field name="res_model">estate.property</field>
    <field name="view_mode">kanban</field>
</record>
<menuitem id="estate_menu_root" name="Estate App">
    <menuitem id="estate_first_level_menu" name="First Level">
        <menuitem id="estate_kanban_menu_action" action="estate_type_kanban_action"/>
    </menuitem>
</menuitem>
```

## Kanban minimo
La vista mínima de Kanban sería tal que:
```xml
<kanban>
    <templates>
        <t t-name="kanban-box">
            <div class="oe_kanban_global_click">
                <field name="name"/>
            </div>
        </t>
    </templates>
</kanban>
```

## Vistas condicionales en kanban

```xml
<kanban>
    <field name="state"/>
    <templates>
        <t t-name="kanban-box">
            <div class="oe_kanban_global_click">
                <field name="name"/>
            </div>
            <div t-if="record.state.raw_value == 'new'">
                This is new!
            </div>
        </t>
    </templates>
</kanban>
```


* `t-if`: el elemento `<div>` se muestra si la condición es verdadera.
* `record`: un objeto con todos los campos solicitados como atributos. Cada campo tiene dos atributos `value` y `raw_value`. El primero tiene el formato de acuerdo con los parámetros de usuario actuales y el segundo es el valor directo de un archivo [read()](https://www-odoo-com.translate.goog/documentation/14.0/developer/reference/addons/orm.html?_x_tr_sl=auto&_x_tr_tl=en&_x_tr_hl=en#odoo.models.Model.read).

## Agrupación por columnas

```xml
<record id="kanban_view" model="ir.ui.view">
    <field name="name">Types Kanban</field>
    <field name="model">estate.property</field>
    <field name="arch" type="xml">
        <!-- Aqui asignamos que se agrupen en funcion del tipo -->
        <kanban default_group_by="type_id">
            <field name="state"/>
            <templates>
                <t t-name="kanban-box">
                    <div class="oe_kanban_global_click">
                        <h2> <field name="name"/> </h2>
                        <div t-if="record.state.raw_value == 'nuevo'"  style="color: blue"> This is new! </div>
                    </div>
                </t>
            </templates>
        </kanban>
    </field>
</record>
```

## Final

* `<templates>`: define una lista de plantillas QWeb Templates . Las vistas Kanban deben definir al menos una plantilla raíz kanban-box, que se representará una vez para cada registro.
* `<t t-name="kanban-box">`: `<t>`es un elemento marcador de posición para [directivas QWeb](https://www-odoo-com.translate.goog/documentation/14.0/developer/reference/javascript/qweb.html?_x_tr_sl=auto&_x_tr_tl=en&_x_tr_hl=en#reference-qweb). En este caso, se utiliza para configurar la plantilla `name` en `kanban-box`
* `<div class="oe_kanban_global_click">`: `oe_kanban_global_click` hace que se pueda hacer clic en `<div>` para abrir el registro.
* `<field name="name"/>`: esto agregará el campo `name` a la vista.

Así se vería la vista kanban final:
```xml
<record id="kanban_view" model="ir.ui.view">
    <field name="name">Types Kanban</field>
    <field name="model">estate.property</field>
    <field name="arch" type="xml">
        <kanban default_group_by="type_id">
            <field name="state"/>
            <templates>
                <t t-name="kanban-box">
                    <div class="oe_kanban_global_click">
                        <h2> <field name="name"/> </h2><br/>
                        <section>
                            <article>
                                <div t-if="record.state.raw_value == 'nuevo'"  style="color: blue"> This is new! </div>
                            </article>
                            <article>
                                Precio esperado: <field name="expected_price"/><br/>
                                <div t-if="record.best_offer.raw_value != 0.00">
                                    Mejor oferta: <field name="best_offer"/><br/>
                                </div>
                            </article>
                            <article>
                                Precio de venta: <field name="selling_price"/><br/>
                                <field name="tags_id"/><br/>
                            </article>
                        </section>
                    </div>
                </t>
            </templates>
        </kanban>
    </field>
</record>
```
