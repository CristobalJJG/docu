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