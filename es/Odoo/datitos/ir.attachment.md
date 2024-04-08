# Problemas con ir.attachment
Es posible o probable que el algún momento te encuentres con un problema parecido a este:
```bash
FileNotFoundError: [Errno 2] No such file or directory: 'C:\\Users\\cristobal.jimenez\\AppData\\Local\\OpenERP S.A\\Odoo\\filestore\\test_rt_pur_cjg\\6a/6ad87633490735f27b4f73d8d984193d8d7d6947'
2024-04-08 08:54:49,223 18972 INFO test_rt_pur_cjg werkzeug: 127.0.0.1 - - [08/Apr/2024 08:54:49] "GET /web/content/32217-18e45b7/web.assets_backend.css HTTP/1.1" 404 - 2 0.008 0.024
2024-04-08 08:54:49,223 18972 INFO test_rt_pur_cjg werkzeug: 127.0.0.1 - - [08/Apr/2024 08:54:49] "GET /web/webclient/load_menus/af709db13bfb5a62521e94abb3c219c4c8eeb5e697f85a44eabff7b15fe13fa5 HTTP/1.1" 200 - 1 0.004 0.026
2024-04-08 08:54:49,223 18972 INFO test_rt_pur_cjg werkzeug: 127.0.0.1 - - [08/Apr/2024 08:54:49] "GET /web/content/32218-c2adede/web.assets_common.js HTTP/1.1" 404 - 2 0.010 0.022
2024-04-08 08:54:49,224 18972 INFO test_rt_pur_cjg werkzeug: 127.0.0.1 - - [08/Apr/2024 08:54:49] "GET /web/content/32220-ed85b8e/web.assets_backend_prod_only.js HTTP/1.1" 404 - 2 0.009 0.023
2024-04-08 08:54:49,227 18972 INFO test_rt_pur_cjg odoo.addons.base.models.ir_attachment: _read_file reading C:\Users\cristobal.jimenez\AppData\Local\OpenERP S.A\Odoo\filestore\test_rt_pur_cjg\57/579e668e19474b58b956a400aa9c054a3097c89d 
Traceback (most recent call last):
  File "C:\Users\cristobal.jimenez\workspace\odoo\odoo\api.py", line 789, in get
    field_cache = field_cache[record.env.cache_key(field)]
KeyError: (None, None)

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "C:\Users\cristobal.jimenez\workspace\odoo\odoo\fields.py", line 937, in __get__
    value = env.cache.get(record, self)
  File "C:\Users\cristobal.jimenez\workspace\odoo\odoo\api.py", line 793, in get
    raise CacheMiss(record, field)
odoo.exceptions.CacheMiss: 'ir.attachment(32219,).datas'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "C:\Users\cristobal.jimenez\workspace\odoo\odoo\api.py", line 789, in get
    field_cache = field_cache[record.env.cache_key(field)]
KeyError: (None,)

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "C:\Users\cristobal.jimenez\workspace\odoo\odoo\fields.py", line 937, in __get__
    value = env.cache.get(record, self)
  File "C:\Users\cristobal.jimenez\workspace\odoo\odoo\api.py", line 793, in get
    raise CacheMiss(record, field)
odoo.exceptions.CacheMiss: 'ir.attachment(32219,).raw'
```

Donde podemos ver un gran número de problemas relacionados en su mayoría con `ir.attachment`. Para solucionar este problema, debemos hacer lo siguiente:
1. Hablar con un superior, que nos diga si realmente puede que ese seal el problema.
2. `delete from ir_attachment;` dentro de la base de datos que estemos utilizando.