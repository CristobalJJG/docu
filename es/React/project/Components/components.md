# Components

Este directorio deberá contener todos los componentes de la aplicación. Cada componente deberá estar en su propio directorio, el cual deberá contener todos los archivos necesarios para su correcto funcionamiento.

Una forma de obtener los **componentes** en las *paginas* de manera sencilla puede ser tal que:
``` 
-- Components
    -- Componente1
        · index.js
        · Componente1.jsx
    -- Componente2
        · index.js
        · Componente2.jsx
    · index.js
```

Donde el **fichero .jsx** tiene **la vista y la logica** del componente y el **fichero .js** tiene la **exportación** del componente.

```js
// ./Componente1/Componente1.jsx
import styled from 'styled-components';
export const Componente1 = ({ child, bg, color, bold }) => {
  return (
    <Container background={bg} color={color} bold={bold}>
      {child}
    </Container>
  );
};

// Styled components:
const Container = styled.div`
    width: 100%; height: 10%;
    background-color: ${props => props.background};
    color: ${props => props.color};
    font-weight: ${props => props.bold ? 'bold' : 'normal'};
`;
```

--- 

```js
// ./Componente1/index.js
export * from './Componente1.jsx';
```

---

```js
// ./index.js
export * from './Componente1';
export * from './Componente2';
```