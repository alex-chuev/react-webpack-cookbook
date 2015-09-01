> Прежде чем начать, вам необходимо убедиться, что у вас установлены последние версии Node.js и NPM. Посетите [nodejs.org](http://nodejs.org/) для получения подробностей по установке. Мы будем использовать NPM для установки различных инструментов.

Начать работать с Webpack – просто. Я покажу вам, как настроить простой проект на его основе. Первый шаг – выбрать директорию для вашего проекта, выполнить `npm init` и ответить на некоторые вопросы. Это создаст файл `package.json` для вас. Не переживайте, если некоторые поля не выглядят хорошо, вы можете изменить их позже.

## Установка Webpack

Далее вам необходимо установить Webpack. Мы будет устанавливать его локально и сохраним его в качестве засимости проекта. Таким образом, вы сможете запустить сборку где угодно. Выполните `npm i webpack --save-dev`. Если вы желаете запустить инструмент, выполните `node_modules/.bin/webpack`.

## Структура директорий

Организуйте структуру вашего проекта таким образом:

- /app
  - main.js
  - component.js
- /build
  - bundle.js (создан автоматически)
  - index.html
- package.json
- webpack.config.js

В этом случае `bundle.js` будет создан с помощью Webpack, основываясь на `/app`. Для того, чтобы сделать это возможным, давайте создадим `webpack.config.js`.

## Создание конфигурации Webpack

В нашем случае, базовая конфигурация могла бы выглядеть так:

*webpack.config.js*

```javascript
var path = require('path');


module.exports = {
    entry: path.resolve(__dirname, 'app/main.js'),
    output: {
        path: path.resolve(__dirname, 'build'),
        filename: 'bundle.js',
    },
};
```

## Запуск вашей первой сборки

Сейчас, имея базовую конфигурацию, нам нужно что-то, что будем собирать. Давайте начнём с классического `Hello World` приложения. Организуйте `/app` таким образом:

*app/component.js*

```javascript
'use strict';


module.exports = function () {
    var element = document.createElement('h1');

    element.innerHTML = 'Hello world';

    return element;
};
```

*app/main.js*

```javascript
'use strict';
var component = require('./component.js');


document.body.appendChild(component());

```

Сейчас запустите `webpack` в терминале и ваше приложение будет собрано. В папке `/build` появится файл *bundle.js*. В папке `build/` понадобится файл *index.html* для запуска приложения.

*build/index.html*

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8"/>
  </head>
  <body>
    <script src="bundle.js"></script>
  </body>
</html>
```

> Этот файл можно было бы создать с помощью Webpack, используя [html-webpack-plugin](https://www.npmjs.com/package/html-webpack-plugin). You can give it a go if you are feeling adventurous. It is mostly a matter of configuration. Generally this is the way you work with Webpack.

## Running the Application

Just double-click the *index.html* file or set up a web server pointing to the `build/` folder.

## Setting Up `package.json` *scripts*

It can be useful to run build, serve and such commands through `npm`. That way you don't have to worry about the technology used in the project. You just invoke the commands. This can be achieved easily by setting up a `scripts` section to `package.json`.

In this case we can move the build step behind `npm run build` like this:

1. `npm i webpack --save` - If you want to install Webpack just a development dependency, you can use `--save-dev`. This is handy if you are developing a library and don't want it to depend on the tool (bad idea!).
2. Add the following to `package.json`:

```json
  "scripts": {
    "build": "webpack"
  }
```

To invoke a build, you can hit `npm run build` now.

Later on this approach will become more powerful as project complexity grows. You can hide the complexity within `scripts` while keeping the interface simple.

The potential problem with this approach is that it can tie you to a Unix environment in case you use environment specific commands. If so, you may want to consider using something environment agnostic, such as [gulp-webpack](https://www.npmjs.com/package/gulp-webpack).

> Note that NPM will find Webpack. `npm run` adds it to the `PATH` temporarily so our simple incantation will work.
