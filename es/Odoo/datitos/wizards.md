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
