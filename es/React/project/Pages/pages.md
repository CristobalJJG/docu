# Pages

En esta carpeta se encuentran las páginas de la aplicación. Cada página es un componente de React que se encarga de mostrar una vista específica de la aplicación.

Esta se basa en los layouts, y dentro de esto va usando componentes para ir generando la pagina.
Por ejemplo:
La pagina de inicio, que es la pagina principal de la aplicación, se compone de un layout que tiene un header, un body y un footer.
```js
import React from 'react';
import Layout from '../Layouts/Layout';
import Header, Body, Footer from '../Layouts';

const Home = () => {
    return (
        <Layout>
            <Header color={whitesmoke} background={blue}>
            <Body background={whitesmoke}>
                <h1>Home</h1>
                <p>Esta es la pagina de inicio</p>
            </Body>
            <Footer />
        </Layout>
    );
};
```