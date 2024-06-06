# Index.js

Este archivo es el punto de entrada de la aplicación React. Es el archivo que se encarga de renderizar el componente principal de la aplicación.

Aqui tenemos la configuracion del **Provider** (Redux) , **PersistGate** (Redux), **ThemeProvider** (TypeScript).
Además, indicamos la ruta base con **BrowserRouter** (react-router-dom) e importamos *store* y *persistor* de **store** y *theme* de **theme**.

**App** es el componente de React base que se renderiza en el DOM (fichero [App.js](/es/React/project/main/appjs.md)).

```js
import React from 'react';
import ReactDOM from 'react-dom/client';

import { BrowserRouter } from 'react-router-dom';
import { Provider } from 'react-redux';
import { PersistGate } from 'redux-persist/integration/react';
import { ThemeProvider } from 'styled-components';
import { store, persistor } from 'store';
import App from 'App';
import theme from 'theme';
import './index.css';

import { ROOT_PREFIX } from 'Constants/ComponentRoutes';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <Provider store={store}>
    <PersistGate loading={null} persistor={persistor}>
      <ThemeProvider theme={theme}>
        <BrowserRouter basename={ROOT_PREFIX}>
          <App />
        </BrowserRouter>
      </ThemeProvider>
    </PersistGate>
  </Provider>
);
```