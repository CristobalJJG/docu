# Capítulo 8 - Relaciones entre modelos

[https://www.odoo.com/capitulo8](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/08_relations.html)

## Muchos a 1

Si queremos que **muchos** modelos puedan acceder a **un solo** modelo tendremos que utilizar el campo `fields.Many2one("modelo", string="nombre")`  
Por ejemplo, queremos que muchos **EstateProperty** tengan 1 solo **Comprador/Vendedor**

## Muchos a Muchos

Si queremos que **muchos** modelos puedan acceder a **muchos** modelos tendremos que utilizar el campo `fields.Many2Many("modelo", string="nombre")`  
Por ejemplo, queremos que muchos **EstateProperty** tengan muchos **Tags**

En el caso de los **tags**, queda bastante estético recogerlos en el xml tal que:

```xml
<field name="tags_id" widget="many2many_tags"/>
```

## 1 a Muchos

Si queremos que **un solo** modelo pueda acceder a **muchos** modelos tendremos que utilizar el campo `fields.Many2one('modelo',  string="name")`  
Por ejemplo, queremos que un **EstateProperty** tengan muchas **Ofertas**
