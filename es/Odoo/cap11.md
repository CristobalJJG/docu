# Capítulo 11 - Restricciones

[https://www.odoo.com/capitulo11](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/11_constraints.html)

## Restricciones SQL

[Pagina oficial PostgreSQL](https://www.postgresql.org/docs/current/ddl-constraints.html#DDL-CONSTRAINTS-UNIQUE-CONSTRAINTS)

Se utiliza la variable reservada `_sql_constratins` con una lista de restricciones de la forma:

```python
_sql_constraints =[
    ('check_price_positive','CHECK(price >= 0)',
        'El precio debe ser positivo')
]
```

Otro ejemplo sería con una variable única:

```python
_sql_constraints =[
    ('check_unique_name','UNIQUE(name)',
        'El nombre de la propiedad ya existe')
]
```

## Restricciones con Python

```python
@api.constrains('price')
defcheck_lower_than_90p_of_expected(self):
    for record in self:
        if record.price < record.property_id.expected_price *0.9:
            raise models.ValidationError('Precio no puede ser inferior al 90% del precio esperado')
```
