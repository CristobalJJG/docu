## Ejecución en Paralelo

[Documentación](https://github.com/open-cli-tools/concurrently#readme) Oficial
[[Documentación](https://github.com/open-cli-tools/concurrently#readme)](https://github.com/open-cli-tools/concurrently#readme)

**Instalación** de Concurrently

```bash
npm i concurrently -g
```

Si ejecutamos la orden `concurrently \"npm run docs\" \"npm run start\"` deberíamos ver la ejecución de ambas órdenes de forma paralela. Las podremos ubicar de acuerdo a los números de procesos que encontraremos al principio de la línea entre corchetes.

![Concurrently base](../assets/csc.png)

Para una mejor compresión de los procesos, podemos utilizar las configuraciones:

* **-n** para que en vez de que aparezca el número de proceso, aparezca un nombre.
* **-c** para añadirle un color al

```bash
concurrently -n \"doc,ng\" -c \"blue,magenta\" \"npm run docs\" \"npm run start\"
```

![Concurrently con minima configuracion](../assets/ccc.png)
