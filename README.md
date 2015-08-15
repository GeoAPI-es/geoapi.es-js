# geoapi.es-js
Libreria en JS para GeoAPI.es

### Como empezar

Es preferible leer la [documentacion general](https://github.com/GeoAPI-es/geoapi.es-docs) a la par con esta documentacion.

La libreria esta disponible en [npm](https://npmjs.org/).

Para instalar <b>geoapi.es-js</b> y sus dependencias, es suficiente con añadir

    "@geoapi.es/js": "~0.0.1"

en la seccion `dependencies` de tu archivo `package.json`.

### Como funciona a nivel funcional

La libreria tiene 2 partes importantes.

De base usaremos el siguiente codigo para poder explicar mejor cada parte.

```javascript
var app = angular.module('app', ['GeoAPI']);
app.controller('MainCtrl', function($scope, $timeout, GeoAPI){ ...
```

* Configuracion

    El metodo `setConfig` sirve para definir los parametros que usara la libreria para hacer las
    peticiones. Dichos parametros estan explicados en la [documentacion general](https://github.com/GeoAPI-es/geoapi.es-docs).

    ```javascript
    //
    GeoAPI.setConfig("key", "...");
    GeoAPI.setConfig("sandbox", 0);
    ...
    ```

* Metodos

    La libreria dispone de varios metodos, los cuales se usan para realizar las distintas peticiones. Cada uno de los metodos puede tener 0 o mas parametros, que se usan para,
    por ejemplo, filtrar o concretar la busqueda. Los metodos reciben un unico argumento del
    tipo Object, que a su vez debe contener parejas de valores siendo:

    * la clave - una cadena de texto especificando el parametro que se desea enviar
    * el valor - o bien una cadena de texto o bien un numero que da valor al parametro

    Ejemplos:

    ```javascript
    //
    GeoAPI.comunidades({});
    GeoAPI.provincias({
        'CCOM': '08'
    });
    ...
    ```

    Todos los metodos disponibles, asi como sus parametros, estan especificados en la [documentacion general](https://github.com/GeoAPI-es/geoapi.es-docs).

### Como funciona a nivel tecnico

La libreria realiza peticiones `GET` al endpoint y ejecuta un callback (usando `$q` de Angular),
pasandole como parametros los datos recibidos. De esta manera se consigue un codigo asincrono.

```javascript
GeoAPI.comunidades({
    //Sin argumentos
}).then(function($respuesta) {
    console.log($respuesta);
});
```
