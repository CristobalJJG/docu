# SonarQube
Si tienes algun problema con la instalación, puedes acceder directamente a la página de SoanrQube[](https://n-saikiran.gitbook.io/sonarqube/installation-of-sonarqube).

## Instalación


Primero tendremos que descargar los 2 zips útiles para nosotros, que son: 
* El que contiene el servidor: [SonarSource](https://www.sonarsource.com/products/sonarqube/downloads/success-download-community-edition/)
* El que contiene el CLI de sonar-scanner: [SonarSource](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner/)

### Windows
Tenemos la carpeta servidor en Descargas, la ubicamos en un sitio donde podamos tener fija esa carpeta. Por ejemplo, Documentos, o incluso, añadirla a ProgramFiles.  
Tendremos 2 carpetas, la del servidor, que tendremos que abrir para inicarlo, y el CLI, que añadiremos al *PATH* de windows para poder utilizarlo:

#### Servidor
Accederemos al directorio de windows dentro de bin:
```shell
cd ./sonarqube/bin/windows-x86-64
```

Para mayor comodidad para ejecutar el servidor, podemos dar click derecho al fichero StartSonar.bat > Send To > Desktop, y así tendremos un acceso directo al fichero en nuestro escritorio.  
Para ejecutar el servidor simplemente tendremos que ejecutar el fichero (doble click sobre el fichero).   
Se abrirá una terminal de windows y empezará a ejecutarse los comandos necesarios. 
Nosotros iremos a un navegador y accederemos a [http://localhost:9000/](http://localhost:9000/), si no da error, llegará un momento en el que se abra el servidor.

#### CLI
Accederemos al directorio de bin dentro de sonar-scanner.
Tendremos que añadir la ubicación de bin dentro del PATH de windows, para ello, haremos click derecho sobre cualquiera de los ficheros > propiedades y copiamos la localización completa del fichero.
A continuación, clicamos la tecla de Windows, escribimos *Variables de entorno* (*Environments variables* en inglés).  
Clicamos en *Path* > Edit... > New, y pegamos la localización del fichero.

Para confirmar que está bien, podemos abrir una terminal y escribir:
```shell
sonar-scanner -h
```

![sonar-scanner funciona](../../assets/sonar-scanner.png)