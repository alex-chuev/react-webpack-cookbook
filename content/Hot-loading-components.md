С React JS и react-hot-loader вы можете изменить код класса вашего компонента и увидеть, что DOM его экземпляров изменился без потери их состояния. Это практически то же самое, как обновление CSS, только в отношении ваших компонентов.

## Настроем это

Этот шаг требует использование **webpack-dev-server**, который был представлен в предыдущих главах. Сейчас нам просто нужно установить загрузчик `npm install react-hot-loader --save-dev` и сделать небольшие изменения конфигурации:

```javascript
var webpack = require('webpack');
var path = require('path');

var config = {
  entry: ['webpack/hot/dev-server', './app/main.js'],
  output: {
    path: path.resolve(__dirname, './build'),
    filename: 'bundle.js'
  },
  module: {
    loaders: [{
      test: /\.js$/,

      // Используем свойство "loaders" вместо "loader" и 
      // добавляем "react-hot" перед вашим существующим "jsx" загрузчиком
      loaders: ['react-hot', 'babel']
    }]
  }
};

module.exports = config;
```

Также потребуется небольшой фрагмент кода во входном файле вашего приложения. В примере выше был файл *main.js*, размещенный в папке `app/`.

*app/main.js*
```javascript
// Основной компонент вашего приложения,
// возможно он использует react-router
var RootComponent = require('./RootComponent.jsx');

// Сохраняем компонент в переменную
var rootInstance = React.render(RootComponent(), document.body);

// И просто скопируйте и вставьте эту часть в конец файла
if (module.hot) {
  require('react-hot-loader/Injection').RootInstanceProvider.injectProvider({
    getRootInstances: function () {
      // Поможем React Hot Loader определить основной компонент на странице:
      return [rootInstance];
    }
  });
}

```

Это так просто! Отрендерите компонент в DOM и измените код класса компонента. Он обновится, сохранив существующее состояние. Круто?

Подробнее о [react-hot-loader](http://gaearon.github.io/react-hot-loader/getstarted/).
