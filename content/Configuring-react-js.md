## Установка ReactJS

`npm install react --save`

И больше ничего. Теперь вы можете начать использовать ReactJS в вашем коде.

## Использование ReactJS в коде

**component.jsx**

```javascript
import React from 'react';

export default class Hello extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}
```

**main.js**

```javascript
import React from 'react';
import Hello from './component.jsx';

main();

function main() {
    React.render(<Hello />, document.getElementById('app'));
}
```

**build/index.html**

```javascript
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8"/>
  </head>
  <body>
    <div id="app"></div>

    <script src="http://localhost:8080/webpack-dev-server.js"></script>
    <script src="bundle.js"></script>
  </body>
</html>
```

## Преобразование JSX

Чтобы использовать синтаксис JSX, вам потребуется Webpack для преобразования его в JavaScript. Это работа для loader-а. Мы будем использовать [Babel](https://babeljs.io/), так как он приятный и имеет множество функций.

`npm install babel-loader --save-dev`

Теперь нам нужно настроить Webpack для использования этого loader-а.

*webpack.config.js*
```javascript
var path = require('path');
var config = {
  entry: path.resolve(__dirname, 'app/main.js'),
  output: {
    path: path.resolve(__dirname, 'build'),
    filename: 'bundle.js'
  },
  module: {
    loaders: [{
      test: /\.jsx?$/, // Регулярное выражение для проверки требуемого пути. Соответствует js или jsx.
      loader: 'babel' // Модуль, который должен быть загружен. "babel" - сокращение для "babel-loader".
    }]
  }
};

module.exports = config;
```

Webpack будет тестировать каждый путь запрашиваемый в вашем коде. В этом проекте мы используем синтаксис ES6 для загрузки модулей. Это означает, что для `import MyComponent from './Component.jsx';` запрашиваемый путь будет  `'./Component.jsx'`.

Запустите `npm run dev` в консоли и обновите страницу для того, чтобы что-то увидеть.
