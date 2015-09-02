## Классы

Начиная с ReactJS версии 0.13 вы можете определять компоненты, как классы.

```javascript
class MyComponent extends React.Component {
  constructor() {
    this.state = {message: 'Hello world'};
  }
  render() {
    return (
      <h1>{this.state.message}</h1>
    );
  }
}
```

Это даёт вам возможность пользоваться очень кратким и красивым синтаксисом для написания компонентов. Недостаток использования классов заключается в отсутствии возможности использовать миксины. Тем не менее, есть выход. Давате посмотрим, как мы могли бы продолжить использование важного **PureRenderMixin**.

```javascript
import React from 'react/addons';

class Component extends React.Component {
  shouldComponentUpdate() {
    return React.addons.PureRenderMixin.shouldComponentUpdate.apply(this, arguments);
  }
}

class MyComponent extends Component {
  constructor() {
    this.state = {message: 'Hello world'};
  }
  render() {
    return (
      <h1>{this.state.message}</h1>
    );
  }
}
```
