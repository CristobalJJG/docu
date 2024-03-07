# DJANGO

(WIP)

## Instalación de Django

[Instalacion desde la página oficial](https://docs.djangoproject.com/en/5.0/topics/install/#installing-official-release)

1. Instalar pip.
2. En caso de ser necesario, cambiar el entorno virtual (venv)
3. Instalar Django con `pip install Django`
4. Comprobar que realmente tenemos Django instalado, y comprobar también la versión del mismo con `print(django.get_version())` en una terminal python.


## Creación de proyecto 
[Tutorial 1](https://docs.djangoproject.com/en/5.0/intro/tutorial01/)
[Tutorial 2 - más usado](https://medium.com/vibentec-it/use-django-to-create-a-backend-application-37990f1f06cf)

Ejecutar en terminal `django-admin startproject mysite`.

Encontraremos una distribución de directorios y ficheros tal que:

```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```

* **mysite/**: Directorio raíz del proyecto. El nombre no importa para Django, por lo que se podría cambiar a otro nombre sin problema.
* **manage.py**: Un script que ayuda con la gestión del proyecto. Con él se pueden crear aplicaciones, iniciar el servidor de desarrollo, etc.
* **mysite/**: Directorio que contiene el proyecto. Su nombre es el paquete de Python para el proyecto. Es el nombre que se usará para importar cosas del proyecto.
* **mysite/__init__.py [No modificado]**: Un fichero vacío que le dice a Python que este directorio debe ser considerado un paquete de Python.
* **mysite/settings.py**: Configuración del proyecto.
* **mysite/urls.py**: Las definiciones de las URLs del proyecto.
* **mysite/asgi.py  [No modificado]**: Un punto de entrada para servidores compatibles con ASGI.
* **mysite/wsgi.py  [No modificado]**: Un punto de entrada para servidores compatibles con WSGI. Realmente, esta es la parte importante para el despliegue del back, como mínimo en Heroku.


## Ejecución del servidor
Para ejecutar el servidor, estando dentro del directorio del proyecto, ejecutaremos `python manage.py runserver`.  
Si lo necesitamos, podremos cambiar el puerto con `python manage.py runserver 8080`.  
En caso de querer cambiar la IP del servidor, podremos hacerlo con `python manage.py runserver 0.0.0.0:8000`.  


## Despliegue en Heroku
Para desplegar el servidor en Heroku, necesitaremos:
* un archivo `Procfile` en el directorio raíz del proyecto, con el siguiente contenido:
```
web: gunicorn mysite.wsgi
```
* un archivo requirements con las librerías necesarias para el despliegue. Para ello, ejecutaremos `pip freeze > requirements.txt` en la terminal. Tenemos que tener en cuenta que haremos uso de **gunicorn** y **psycopg2** para el despliegue, por lo que estas 2 tienen que estar instaladas.


## CORS
[Tutorial y explicación CORS](https://www.stackhawk.com/blog/django-cors-guide/)  
Tendremos que tener insladas algunas de las librerias auxiliares que nos aporta Django para el desarrollo de la API. En este caso, necesitaremos `pip install django-cors-headers`.  
A continuación, tendremos que añadir la librería a la lista de aplicaciones instaladas en `settings.py`:  
```python
INSTALLED_APPS = [
    ...
    'corsheaders',
    ...
]
```

Y añadir el middleware de la librería a la lista de middlewares en `settings.py`:
```python
MIDDLEWARE = [
    ...
    'corsheaders.middleware.CorsMiddleware',
    'django.middleware.common.CommonMiddleware',
    ...
]
```

Por último, tendremos que añadir la configuración de CORS en `settings.py`:
```python
CORS_ALLOWED_ORIGINS = [
    "https://domain.com",
    "https://api.domain.com",
    "http://localhost:8080",
    "http://127.0.0.1:9000"
]
```

También podríamos añadirlo como *REGEX*:
```python
CORS_ALLOWED_ORIGIN_REGEXES = [
    r"^https://\w+\.domain\.com$",
]
```

```python
CORS_ALLOW_METHODS = [
    'DELETE',
    'GET',
    'PATCH',
    'POST',
    'PUT',
]
```
