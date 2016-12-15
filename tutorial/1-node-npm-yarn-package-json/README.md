# 1 - Node, NPM, Yarn, y package.json

En esta sección configuraremos Node, NPM, Yarn y un archivo `package.json` básico.

Primero, necesitamos instalar Node, el cual no sólo se utiliza para el Back-End con JavaScript, sino que también coloca a tu disposición todas las herramientas que necesites para crear un Stack Front-End moderno.

Dirigete a la [pagina de descarga](https://nodejs.org/en/download/current/) para obtener los binarios para macOS o Windows, o a la [página de instalación vía manejador de paquetes](https://nodejs.org/en/download/package-manager/) para distribuciones Linux.

Para distribuciones como **Ubuntu / Debian** podrías correr el siguiente comando para instalar Node:

```bash
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
```
Si deseas cualquier version de Node > 6.5.0

`npm`, el manejador de paquedos por defecto de Node, viene automaticamente con Node, por lo tanto no tiene que instalarlo ud mismo.

**Nota**: Si Node ya esta instalado, otra opción es `nvm` ([Manejador de Versión de Node](https://github.com/creationix/nvm)), y correr `nvm` install y usar la versión más reciente de Node o cualquiera que requieras para tu desarrollo.

[Yarn](https://yarnpkg.com/) es otro manejador de paquetes el cual es mucho mas rápido que NPM, posee sorporte offline, y busqueda [más predicible](https://yarnpkg.com/en/docs/yarn-lock) de dependencias. Desde su [liberación](https://code.facebook.com/posts/1840075619545360) en Octubre de 2016, ha recibido una rápida adopción y se esta convirtiendo en el nuevo manejador de paquetes por elección de la comunidad de JavaScript. Vamos a usar Yarn en este tutorial. Si deseas usar NPM en su lugar para este tutorial, puedes simplemente reemplazar todos los comandos `yarn add` y `yarn add --dev` por `npm install --save` y `npm install --dev`.

- Para instalar Yarn sigue las siguientes [instrucciones](https://yarnpkg.com/en/docs/install). Puedes instalarlo con `npm install -g yarn` o `sudo npm install -g yarn` (Si, estamos usando NPM para instalar Yarn, tal cual como usarias ¡Internet Explorer o Safari para instalar Chrome!).
- Creamos un nuevo directorio para trabajar y con el comando `cd` ingresamos en él.
- Corre `yarn init` y responde a las preguntas (`yarn init -y` para saltarte todas las preguntas), para generar automaticamente un archivo `package.json`.
- Crea un archivo `index.js` que contenga `console.log('Hello world')`.
- Corre `node .`  en este directorio (`index.js` es el archivo por defecto que Node buscará en el directorio actual). Debería imprimir "Hello world".

En vez de correr `node .`  para ejecutar nuestro programa podemos usar un script NPM/Yarn en su lugar para disparar la ejecución del código. Esto nos dará una buena abstracción para poder usar `yarn start` o `npm start`, aun cuando nuestro programa se vuelva más complejo.

- En `package.json`, añadimos un objeto `scripts` al objeto raíz de la siguiente forma:

```
"scripts": {
  "start": "node ."
}
```

El `package.json` debe ser un archivo JSON valido, lo que significa que no puede tener comillas. Por tanto, se cuidadoso cuando edites tu archivo `package.json` manualmente.

- Corre `yarn start`. debería imprimir `Hello world`.

- Crea un archivo `.gitignore` y agregale lo siguiente:

```
npm-debug.log
yarn-error.log
```

**Nota**: Si revisas el archivo `package.json` que esta en este capítulo, verá un script `tutorial-test` en cada capítulo. Estos scripts permiten probar que el capítulo funciona adecuadamente cuando corren `yarn && yarn start`. Puede borrarlos en sus propios proyectos.

Siguiente Sección: [2 - Instalar y usar un paquete](/tutorial/2-packages)

Volver a la [Tabla de Contenidos](https://github.com/AlexR1712/js-stack-from-scratch).
