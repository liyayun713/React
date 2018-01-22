# React.js Notes
## runoob
1. [React Introduction](https://github.com/liyayun713/React/blob/master/lesson/Introduction.md)
2. [React 安装](https://github.com/liyayun713/React/blob/master/lesson/Installation.md)
3. [React JSX](https://github.com/liyayun713/React/blob/master/lesson/JSX.md)
4. [React 组件](https://github.com/liyayun713/React/blob/master/lesson/Component.md)
5. [React State(状态)](https://github.com/liyayun713/React/blob/master/lesson/State.md)
6. [React Props](https://github.com/liyayun713/React/blob/master/lesson/Props.md)
7. [React 组件API](https://github.com/liyayun713/React/blob/master/lesson/ComponentAPI.md)
8. [React 组件生命周期](https://github.com/liyayun713/React/blob/master/lesson/Lifecycle.md)
9. [React Ajax](https://github.com/liyayun713/React/blob/master/lesson/Ajax.md)
10. [React 表单与事件](https://github.com/liyayun713/React/blob/master/lesson/FormEvent.md)
11. [React Refs](https://github.com/liyayun713/React/blob/master/lesson/Refs.md)

## 官方 API
### State & 生命周期
### 事件处理
### 条件渲染
### 列表 & Keys
Keys可以在DOM中的某些元素被增加或删除的时候帮助React识别哪些元素发生了变化。因此你应当给数组中的每一个元素赋予一个确定的标识。

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```
### 表单
```jsx
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```
### 状态提升
使用 react 经常会遇到几个组件需要共用状态数据的情况。这种情况下，我们最好将这部分共享的状态提升至他们最近的父组件当中进行管理

在我们改写 `Calculator` 组件之前，我们先花点时间总结下 `TemperatureInput` 组件的改变。我们将其自身的 `state` 从组件中移除，使用 `this.props.temperature` 替代 `this.state.temperature` ，当我们想要响应数据改变时，使用父组件提供的 `this.props.onTemperatureChange()` 而不是 `this.setState()` 方法

在React应用中，对应任何可变数据理应只有一个单一“数据源”。通常，状态都是首先添加在需要渲染数据的组件中。此时，如果另一个组件也需要这些数据，你可以将数据提升至离它们最近的父组件中。你应该在应用中保持 自上而下的数据流，而不是尝试在不同组件中同步状态。

### 组合 vs 继承
### React 理念
