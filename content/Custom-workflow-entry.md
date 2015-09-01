При запуске рабочего процесса из **http://localhost:8080/web-dev-server/bundle** вы не контролируете *index.html* файл, в котором загружен скрипт.

## Запуск собственного файла index.html
В вашем *package.json* у вас есть свой *dev* скрипт. `"webpack-dev-server --devtool eval --progress --colors --content-base build/"`. Параметр *--content-base build/* сообщает webpack-dev-server-у, откуда загружать ваше приложение. В этом примере это будет `build/`.

## Создание файла index.html
В папке `build/` создайте новый *index.html* с этим содержимым.
