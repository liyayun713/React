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
### 状态提升
### 组合 vs 继承
### React 理念
