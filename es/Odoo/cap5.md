
# Capítulo 5 - Seguridad

[https://www.odoo.com/capitulo5](https://www.odoo.com/documentation/14.0/developer/tutorials/getting_started/05_securityintro.html)  
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


El capítulo 5 nos pide como ejercicio que:

> Agregue derechos de acceso.  
> Cree el archivo `ir.model.access.csv` en la carpeta adecuada y defínalo en el archivo `__manifest__.py`.  
> Dar permisos de lectura, escritura, creación y desvinculación al grupo `base.group_user`.  
> **Consejo**: el mensaje de advertencia en el registro le brinda la mayor parte de la solución ;-)

```csv
id, name, model_id/id, group_id, perm_read, perm_write, perm_create, perm_unlink
access_estate_property,access_estate_property,model_estate_property,base.group_user,1,0,0,0
```

Si tienes mal esta parte, la propia terminal te dará un error diciéndote el mínimo que tienes que colocar en este fichero para que esté correcto.

## Actualizacion
Lo ideal seria tener los permisos tal que ```1,1,1,0``` y cambiar estos permisos segun el grupo.