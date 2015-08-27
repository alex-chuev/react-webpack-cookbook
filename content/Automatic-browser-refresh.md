Когда **webpack-dev-server** запущен, он будет отслеживать изменения ваших файлов, при которых он будет переупаковывать ваш проект и уведомляет браузер, который ожидает это уведомление для того, чтобы обновить страницу. Для запуска этого поведения вам необходимо изменить ваш *index.html* файл в папке `build/`.

*build/index.html*

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8"/>
  </head>
  <body>
    <script src="http://localhost:8080/webpack-dev-server.js"></script>
    <script src="bundle.js"></script>
  </body>
</html>
```

Мы добавили скрипт, который обновляет приложение при возникновении изменений. Вы также должны добавить точку входа в конфигурацию: 

*webpack.config.js*

```javascript
var path = require('path');

module.exports = {
    entry: ['webpack/hot/dev-server', path.resolve(__dirname, 'app/main.js')],
    output: {
        path: path.resolve(__dirname, 'build'),
        filename: 'bundle.js',
    },
};
```
Вот и все! Теперь ваше приложение будет автоматически обновляться при изменении файлов.

## Процесс переупаковки в строке состояния

В приведенном выше примере мы создали файл *index.html*, чтобы дать больше свободы и контроля. Также можно запустить приложение из **http://localhost:8080/webpack-dev-server/bundle**. Это по-умолчанию откроет *index.html* файл в iframe, что позволит в строке состояния отслеживать процесс переупаковки.
