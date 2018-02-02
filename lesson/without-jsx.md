# 不使用JSX
> 编写React的时候，JSX并不是必须的。当你不想在你的构建环境中安装相关编译工具的时候，不使用JSX编写React会比较方便。

每一个JSX元素都只是 React.createElement(component, props, ...children) 的语法糖。因此，任何时候你用JSX语法写的代码也可以用普通的 JavaScript 语法写出来。

例如，下面这段代码是用JSX语法写的：

```jsx
class Hello extends React.Component {
  render() {
    return <div>Hello {this.props.toWhat}</div>;
  }
}

ReactDOM.render(
  <Hello toWhat="World" />,
  document.getElementById('root')
);
```

可以被编译成下面这段不使用JSX的代码：

```jsx
class Hello extends React.Component {
  render() {
    return React.createElement('div', null, `Hello ${this.props.toWhat}`);
  }
}

ReactDOM.render(
  React.createElement(Hello, {toWhat: 'World'}, null),
  document.getElementById('root')
);
```
