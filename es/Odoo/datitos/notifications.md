# Notificaciones / Alertas

Odoo nos aporta un gran tipo de Notificaciones, como pueden ser: 

## Sticky Notifications
Odoo nos ofrece unas notificaciones que se quedan "ancladas" en la parte superior derecha de la pantalla, estas notificaciones se pueden cerrar manualmente o se cerrarán automáticamente después de un tiempo.
Para poder usarlo se tiene que retornar el diccionario tal que: `return self.sticky_notification()`
```python
def sticky_notification(self):
    return {
        'type': 'ir.actions.client',
        'tag': 'display_notification',
        'params': {
            'title': _('Warning'),
            'type': 'warning',
            'message': 'You cannot do this action now',
            'sticky': True,
        }
    }
```

## Rainbow man
Asumo que Odoo pretende que usemos este tipo de notificaciones como temrinación de un proceso complicado o algo así, pero la verdad es que no tengo idea de para qué sirve ni la utilidad real del mismo. 
```python
def sticky_notification(self):
    return {
        'effect': {
            'fadeout': 'slow',
            'message': 'Sale order is confirmed',
            'type': 'rainbow_man',
            'title': 'Success'
        } 
    }
```

## Alerts
Son apartados que nos muestran un pequeño mensaje en la parte superior de la pantalla, estos mensajes se cierran automáticamente después de un tiempo.
```xml
<xpath expr="//form/sheet" position="before"> 
    <div class="alert alert-danger" role="alert" style="margin-bottom:0px;" attrs="{'invisible': [('state', '!=', 'sale')]}"> 
        Your sale order 
        <bold> 
            <a class="alert-link" role="button"><field name="name" readonly="True"/></a> 
        </bold> 
        going to be expired on 
        <bold> <field name="validity_date" readonly="True"/> </bold>
    </div>
</xpath>
```


## Raising Exceptions
Modal, rollo wizard, que nos muestra un mensaje y para la ejecución del código.
```python
def raise_exception(self):
    raise UserError(_('You cannot do this action now'))
```
