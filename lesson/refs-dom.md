# Refs & DOM
> 在典型的 React 数据流中, 属性（props）是父组件与子代交互的唯一方式。要修改子组件，你需要使用新的 props 重新渲染它。但是，某些情况下你需要在典型数据流外强制修改子代。要修改的子代可以是 React 组件实例，也可以是 DOM 元素。对于这两种情况，React 提供了解决办法。

### 何时使用 Refs
* 处理焦点、文本选择或媒体控制。

* 触发强制动画

* 集成第三方 DOM 库

> 如果可以通过声明式实现，则尽量避免使用 refs

### Refs 与函数式组件
你不能在函数式组件上使用 ref 属性，因为它们没有实例：
```jsx
function MyFunctionalComponent() {
  return <input />;
}

class Parent extends React.Component {
  render() {
    // 这里 `ref` 无效！
    return (
      <MyFunctionalComponent
        ref={(input) => { this.textInput = input; }} />
    );
  }
}
```
