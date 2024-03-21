# Capitulo 9 - Campos calculados y cambios

[https://www.odoo.com/capitulo9](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/09_compute_onchange.html)

Resumen de 1/3 de la página:

## Computar algo (Compute method)

Para que un campo se actualice solo al colocar algún otro elemento, deberemos crear una función que sea la que haga el cálculo:

```python
total_area = fields.Integer(compute='_compute_total_area')
def_compute_total_area(self):
    for rec in self:
        rec.total_area = rec.living_area + rec.garden_area
```

A esta función le colocaremos el decorador `@api.compute` con las variables que se usarán dentro de la función, quedando al final tal que:

```python
garden_area = fields.Integer()
living_area = fields.Integer()
total_area = fields.Integer(compute='_compute_total_area')

@api.depends("living_area","garden_area")
def_compute_total_area(self):
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
            record.validity =(fecha1 - fecha2).days
```

## onchange

Sirve rollo web, cada vez que se actualice una variable, ocurrirán ciertas cosas.

```python
@api.onchange("garden")
def_onchange_garden(self):
    if self.garden:
        self.garden_area =10
        self.garden_orientation ="north"
    else:
        self.garden_area =0
        self.garden_orientation =""
```

## Nota / Tips

**Compute** se llama en cada cambio a las dependencias, mientras que **Inverse** se llama solo al guardar el registro.

Con respecto a **Compute** y **onchange** la diferencia reside en la forma en la que se guardan o no los datos en la BBDD. Según el tutorial, pone que es preferible el uso del `compute` antes que el uso del `onchange`.

Según la sabiduría de la experiencia (Alejandro), **compute** debería usarse con la intención de **generar un resultado** por ejemplo, calcular una media.  
Mientras que **onchange** debería usarse para **modificar varios campos** a la vez en función de 1 único cambio.
