# 3 - Configuración de ES6 con Babel y Gulp

Ahora vamos a utilizar la sintaxis de ES6, que es una gran mejora sobre la "antigua" sintaxis ES5. Todos los navegadores y entornos JS comprenden bien el ES5, pero no ES6. Así que vamos a utilizar una herramienta llamada Babel para transformar archivos ES6 en archivos ES5. Para ejecutar Babel, vamos a utilizar Gulp, un corredor de tarea. Es similar a las tareas que se encuentran bajo `scripts` en` package.json`, pero escribir tu tarea en un archivo JS es más sencillo y claro que un archivo JSON, así que instalaremos Gulp y el plugin de Babel para Gulp:

- Ejecuta `hilados agregar --dev gulp`
- Ejecuta `hilados agregar --dev gulp-babel`
- Ejecuta `yarn add --dev babel-preset-latest`
- En `package.json`, agrega un campo` babel` para la configuración babel. Haz que use el último preset de Babel sea como este:

```json
"babel": {
  "presets": [
    "latest"
  ]
},
```

**Nota**: También se podría usar un archivo `.babelrc` en la raíz de su proyecto en lugar del campo` babel` de `package.json`. Su carpeta raíz se hará cada vez más hinchada con el tiempo, así que mantenga la configuración de Babel en `package.json` hasta que crezca demasiado.

- Mueve tu `index.js` a una nueva carpeta` src`. Aquí es donde escribirá su código ES6. Una carpeta `lib` es donde el código ES5 compilado irá. Gulp y Babel se encargarán de crearlo. Elimine el código anterior `color`-related en` index.js` y reemplácelo por un simple:

```javascript
const str = 'ES6';
console.log (`Hello ${str}`);
```

Estamos usando una *una modelo de string* aquí, que es una característica ES6 que nos permite inyectar variables directamente dentro de la cadena sin concatenación usando `$ {}`. Tenga en cuenta que las cadenas de plantilla se crean utilizando **acentos graves**.

- Crea una `gulpfile.js` que contenga:

```javascript
const gulp = require ('gulp');
const babel = require ('gulp-babel');
const del = require ('del');
const exec = require ('child_process').

const paths = {
  allSrcJs: 'src / ** / *. Js',
  libDir: 'lib',
};

gulp.task ('clean', () => {
  Return del (paths.libDir);
});

gulp.task ('build', ['clean'], () => {
  Return gulp.src (paths.allSrcJs)
    .pipe (babel ())
    .pipe (gulp.dest (paths.libDir));
});

gulp.task ('main', ['build'], (devolución de llamada) => {
  Exec (`node $ {paths.libDir}`, (error, stdout) => {
    Console.log (stdout);
    Devolver devolución de llamada (error);
  });
});

gulp.task ('watch', () => {
  gulp.watch (paths.allSrcJs, ['main']);
});

gulp.task ('default', ['watch', 'main']);

```

Tomemos un momento para entender todo esto.

El API de Gulp en sí es bastante sencillo. Define `gulp.task`s, que puede hacer referencia a los archivos` gulp.src`, aplica una cadena de tratamientos con `.pipe ()` (como `babel ()` en nuestro caso) y envía los nuevos archivos a `Gulp.dest`. También puede `gulp.watch` para los cambios en su sistema de archivos. Las tareas Gulp pueden ejecutar tareas previas, pasando una matriz (como `['build']`) como segundo parámetro de `gulp.task`. Consulte la [documentación] (https://github.com/gulpjs/gulp) para obtener una presentación más completa.

Primero definimos un objeto `paths` para almacenar todas nuestras diferentes rutas de archivos y mantener las cosas DRY.

Luego definimos 5 tareas: `build`,` clean`, `main`,` watch` y `default`.

- `build` es donde Babel está llamado a transformar todos nuestros archivos fuente ubicados bajo` src` y escribir los transformados a `lib`.
- `clean` es una tarea que simplemente elimina toda nuestra carpeta` lib` generada automáticamente antes de cada `build`. Esto suele ser útil para deshacerse de los antiguos archivos compilados después de cambiar el nombre o eliminar algunos en `src`, o para asegurarse de que la carpeta` lib` está sincronizada con la carpeta `src` si su compilación falla y no se da cuenta. Utilizamos el paquete `del` para eliminar archivos de una manera que se integra bien con el flujo de Gulp (este es el [recomendado] (https://github.com/gulpjs/gulp/blob/master/docs/recipes/delete-files -folder.md) para eliminar archivos con Gulp). Ejecutar `yarn add --dev del` para instalar ese paquete.
- `main` es el equivalente a ejecutar` node .` en el capítulo anterior, excepto que esta vez, queremos ejecutarlo en `lib / index.js`. Dado que `index.js` es el archivo predeterminado que Node busca, podemos simplemente escribir` node lib` (usamos la variable `libDir` para mantener las cosas secas). La parte `require ('child_process'). Exec` y` exec` en la tarea es una función Node nativa que ejecuta un comando shell. Enviaremos `stdout` a` console.log () `y devolveremos un error potencial usando la función de devolución de llamada` gulp.task`. No se preocupe si esta parte no es muy clara para usted, recuerde que esta tarea es, básicamente, sólo ejecuta `nodo lib`.
- `watch` ejecuta la tarea` main` cuando ocurren cambios en el sistema de archivos en los archivos especificados.
- `default` es una tarea especial que se ejecutará si simplemente llama` gulp` desde la CLI. En nuestro caso queremos que ejecute tanto `watch` como` main` (para la primera ejecución).

**Nota**: Quizás se pregunte por qué estamos utilizando algún código ES6 en este archivo Gulp, ya que no se transporta a ES5 por Babel. Esto se debe a que estamos utilizando una versión de Node que soporta las características de ES6 fuera de la caja (asegúrese de que está ejecutando Nodr> 6.5.0 ejecutando `node -v`).

¡Bien! Veamos si esto funciona.

- En `package.json`, cambia tu ` start` a: `"start": "gulp"`.
- Ejecutw `yarn start`. Debe imprimir "Hello ES6" y empezar a ver los cambios. Trate de escribir un código malo en `src / index.js` para ver a Gulp mostrar el error automáticamente al guardar.

- Agregue `/ lib /` a su `.gitignore`

Siguiente sección: [4 - Uso de la sintaxis ES6 con una clase] (/tutorial/4-es6-syntax-class)

Volver a la [sección anterior] (/tutorial/2-packages) o la [tabla de contenido] (https://github.com/verekia/js-stack-from-scratch#table-of-contents).
