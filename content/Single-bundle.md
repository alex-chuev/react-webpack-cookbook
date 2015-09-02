Используйте единый бандл, когда:

- у вас небольшое приложение,
- вы будете редко обновлять его,
- вам не критично время первоначальной загрузки.

Давайте посмотрим на простейшие настройки, с помощью которых вы сможете собрать своё приложение. 

*webpack.production.config.js*

```javascript
var path = require('path');
var config = {
  entry: path.resolve(__dirname, 'app/main.js'),
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    loaders: [{
      test: /\.js$/,
      loader: 'babel'
    }]
  }
};

module.exports = config;
```
