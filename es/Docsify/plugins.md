Plugin

## Emojis

[Emojis](https://github.com/docsifyjs/docsify/blob/develop/docs/emoji.md) nos permite colocar emojis de forma sencilla dentro de los ficheros MD.
Despues de la versión 4.13 no es necesario colocar el script dentro del fichero HTML.
En caso de estar en una versión anterior, se debe colocar:

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/emoji.min.js"></script>
```

## Barra de Búsqueda

[Barra de Búsqueda](https://docsify.js.org/#/plugins?id=full-text-search)
Siempre que tengamos la inicialización de Docsify, solo habrá que añadir al extensión al fichero HTML.
```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>
```

Esta barra podrá ser configurada desde el propio script que inicializa docsify:
```html
<script>
  window.$docsify = {
    search: 'auto', // default

    search: [
      '/',            // => /README.md
      '/guide',       // => /guide.md
      '/get-started', // => /get-started.md
      '/zh-cn/',      // => /zh-cn/README.md
    ],

    // complete configuration parameters
    search: {
      maxAge: 86400000, // Expiration time, the default one day
      paths: [], // or 'auto'
      //General
      placeholder: 'Search...',

      // Localization
      placeholder: {
        '/': 'Buscar...',
        '/es': 'Buscar...',
        '/en': 'Search...',
      },

      noData: 'No Results!',

      // Localization
      noData: {
        '/': 'Sin resultados',
        '/es': 'Sin resultados',
        '/en': 'No Results',
      },

      // Headline depth, 1 - 6
      depth: 2,

      hideOtherSidebarContent: false, // whether or not to hide other sidebar content

      // To avoid search index collision
      // between multiple websites under the same domain
      namespace: 'website-1',

      // Use different indexes for path prefixes (namespaces).
      // NOTE: Only works in 'auto' mode.
      //
      // When initialiazing an index, we look for the first path from the sidebar.
      // If it matches the prefix from the list, we switch to the corresponding index.
      pathNamespaces: ['/', '/es', '/en'],

      // You can provide a regexp to match prefixes. In this case,
      // the matching substring will be used to identify the index
      pathNamespaces: /^(\/(es|en))?/,
    },
  };
```

## Varios temas y sus modificaciones