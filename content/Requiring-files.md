## Модули

Webpack прямо "из коробки" позволяет вам использовать различные варианты определения модулей, но "под капотом" все они работают одинаково.

#### ES6 modules

```javascript
import MyModule from './MyModule.js';
```

#### CommonJS

```javascript
var MyModule = require('./MyModule.js');
```

#### AMD

```javascript
define(['./MyModule.js'], function (MyModule) {

});
```

## Понимание путей

Модуль загружается по файловому пути (filepath). Представим следующую структуру:

- /app
  - /modules
    - MyModule.js
  - main.js (точка входа)
  - utils.js

Давайте откроем файл *main.js* и подключим *app/modules/MyModule.js* двумя наиболее распространенными способами:

*app/main.js*
```javascript
// ES6
import MyModule from './modules/MyModule.js';

// CommonJS
var MyModule = require('./modules/MyModule.js');
```

Префикс `./` определяет, что путь к модулю указан относительно текущего файла.

А теперь давайте откроем файл *MyModule.js* и подключим **app/utils**.

*app/modules/MyModule.js*
```javascript
// ES6 относительный путь
import utils from './../utils.js';

// ES6 абсолютный путь
import utils from '/utils.js';

// CommonJS относительный путь
var utils = require('./../utils.js');

// CommonJS абсолютный путь
var utils = require('/utils.js');
```

**Относительный путь** является относительным к текущему файлу. **Абсолютный путь** является относительным к точке входа, которой в данном случае является *main.js*.

### Необходимо ли указывать расширение файла?

Нет. Можно не указывать *.js*, но это делает более явным то, что вы собираетесь подключать. У вас могут быть некоторые *.js* файлы и некоторые *.jsx* файлы, и даже изображения и *.css* могут быть подключены с помощью Webpack. Это также более понятно отличает подключенные файлы из node_modules.

Помните, что Webpack — сборщик модулей! Это значит, что вы можете настроить его на загрузку любых форматов, какие вы только пожелаете. Мы углубимся в эту тему позже.
