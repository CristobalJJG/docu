# App.js

Este archivo es el punto de entrada de la aplicación React. Es el archivo que se encarga de renderizar el componente principal de la aplicación.

En esta se podría hacer la **primera carga de datos** de la aplicación y la configuración de rutas, entre otras cosas.

```js
import { useEffect } from 'react'; 
import { useDispatch, useSelector } from 'react-redux';
import { Routes, Route } from 'react-router-dom';
import { fetchData, fetchItems, fetchUsers } from './slices/**';
import { HOME_ROUTE, LOGIN_ROUTE, SETTINGS_ROUTE } from './Constants/routes';

function App() {
  const dispatch = useDispatch();
  const firstRender = useSelector((state) => state.firstRender);

  /* Primera carga de datos */
  useEffect(() => {
    if (firstRender) {
      dispatch(fetchUsers());
      dispatch(fetchData());
      dispatch(fetchItems());
    }
  }, []);

  /* 
   * También podriamos colocar elementos que queramos  
   * que sean perennes en la aplicación, por ejemplo:
   * - En caso de querer tener un loading, podríamos
   *     colocar aqui un elemento que verifique si 
   *     hay algo en estado pendiente (pending | isLoading)
   * 
   * - Si quisieramos tener un timer registrando si
   *     hay conexión a internet, podríamos colocarlo
   *     en esta zona también.
   */

  return (
    <>
      <Routes>
        <Route path={HOME_ROUTE} element={<HomePage/>} />
        <Route path={LOGIN_ROUTE} element={<LoginPage/>} />
        <Route path={SETTINGS_ROUTE} element={<SettingsPage/>} />
      </Routes>
      <!--
        Si tenemos elementos que solo aparecen en un cierto momento,
        como puede ser un "Modal" o un "Toast", se debe colocar aqui.
      -->
      <Modal/>
    </>
  );
}

export default App;
```
