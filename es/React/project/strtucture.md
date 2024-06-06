# Estructuración de un proyecto en React

Esta es una buena forma de estructurar los proyectos React que usan Redux Toolkit y React Router.

```
- src
  -- Assets (Images, Fonts, etc.)
  -- Components (Pequeños componentes reutilizables)
  -- Constants
    · ApiRoutes.js (Rutas de la API)
    · Routes.js (Rutas de la aplicación)
    (En definitiva, cualquier constante que se necesite en la aplicación)
  -- Layouts (Base estructural de la aplicación)
    · Body.jsx
    · Footer.jsx
    · Header.jsx
    · Sidebar.jsx
  -- Pages (Páginas de la aplicación)
    · Home.jsx
    · Login.jsx
    · Register.jsx
    ...
  -- Slices (Reducers de Redux Toolkit)
    · AuthSlice.js
    · UserSlice.js
    ... (Se usan por lo general para los fetch de las API)
  -- Utils
    -- Components (Componentes Auxiliares)
      · Modal
      · Snackbar
      · Toast
      ...
    -- Hooks (Hooks personalizados)
      · useClickOutside.jsx
      ...
  · App.js
  · index.css
  · index.js
  · store.js
  · theme.jsx
```
