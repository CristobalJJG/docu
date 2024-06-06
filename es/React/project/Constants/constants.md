# Constants

Este directorio deberá contener todos los archivos que contienen las constantes de la aplicación. Cada archivo deberá contener un grupo de constantes relacionadas entre sí.

Por ejemplo:
```js
// ./Constants/ApiRoutes.js
export const API_URL = 'https://api.example.com';

export const APP_ENDPOINT = '/app';
export const LOGIN_ENDPOINT = '/login';
export const REGISTER_ENDPOINT = '/register';
...
```

También podria contener los estatus de las peticiones:
```js
// ./Constants/ApiStatus.js
export const SUCCESS = 'success';
export const ERROR = 'error';
export const LOADING = 'loading';
...
```

O incluso conclusiones de mensajes de error:
```js
// ./Constants/ErrorMessages.js
export const INVALID_EMAIL = 'Invalid email';
export const INVALID_PASSWORD = 'Invalid password';
...
```

No confundir esto último con los mensajes de error que se pueden mostrar en la aplicación, ya que estos deberian ubicarse en el i18n.

La idea principal es tener un lugar donde se puedan almacenar todas las constantes de la aplicación, de manera que sea fácil de encontrar y modificar en caso de ser necesario.