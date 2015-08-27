Webpack может быть удобным для упаковки вашей библиотеки под всеобщее пользование. Вы можете применять его для формирования UMD - формата, который совместим с различными загрузчиками модулей (CommonJS, AMD, global).

## Как сформировать UMD для моей библиотеки?

Это можно сделать, используя следующий фрагмент:

```javascript
output: {
    path: './dist',
    filename: 'mylibrary.js',
    libraryTarget: 'umd',
    library: 'MyLibrary',
},
```

Для того, чтобы избежать подключения больших зависимостей, как ReactJS, вы можете использовать дополнительную конфигурацию, наподобие этой:

```javascript
externals: {
    react: 'react',
    'react/addons': 'react'
},
```
## Как сформировать сжатую версию библиотеки?

Вот основная идея:

```javascript
output: {
    path: './dist',
    filename: 'awesomemular.min.js',
    libraryTarget: 'umd',
    library: 'Awesomemular',
},
plugins: [
    new webpack.optimize.UglifyJsPlugin({
        compress: {
            warnings: false
        },
    }),
]
```
