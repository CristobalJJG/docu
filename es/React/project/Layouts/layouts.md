# Layouts

Los layouts son componentes que envuelven a otros componentes. Son útiles para definir la estructura de la página, como la barra de navegación, el pie de página, la barra lateral, etc.

En el caso que he visto yo, encontramos 3 tipos de Layouts:

## Header.jsx
```js
import styled from 'styled-components';

export const Header = styled.div`
    display: flex;
    color: ${props => props.theme.colors.text};
    background-color: ${props => props.theme.colors.primary};
    height: 9vh;
    max-height: 50px;
`;
```

## Body.jsx
```js
import styled from 'styled-components';

export const Body = styled.div`
    display: flex;
    flex-direction: column;
    background-color: ${props => props.theme.colors.background};
    height: 91vh;
    max-height: calc(100vh - 50px);
`;
```
## Window.jsx
```js
import styled from 'styled-components';

export const Window = styled.div`
    display: flex;
    flex-direction: column;
    height: 100vh;
    max-height: 100vh;
`;
```

Podemos diferencias los 3 tipos de Layouts por su altura y color de fondo.  
El `Header` tiene una altura del 9% de la ventana y un color de letra y de fondo pasado como parametro.  
El `Body` tiene una altura del 91% de la ventana y un color de fondo de fondo como parámetro.  
El `Window` tiene una altura del 100% de la ventana y no tiene color de fondo.