# 深入JSX
> 本质上来讲，JSX 只是为 React.createElement(component, props, ...children) 方法提供的语法糖

## 指定 React 元素类型
#### 点表示法

#### 首字母大写
React 会将小写开头的标签名认为是 HTML 原生标签

#### 在运行时选择类型
不能使用表达式来作为 React 元素的标签。如果你的确想通过表达式来确定 React 元素的类型，请先将其赋值给大写开头的变量

## 属性
#### 使用 JavaScript 表达式
```jsx
<MyComponent foo={1 + 2 + 3 + 4} />
```

#### 字符串常量
```jsx
<MyComponent message="hello world" />

<MyComponent message={'hello world'} />
```

#### 默认为 True
```jsx
<MyTextBox autocomplete />

<MyTextBox autocomplete={true} />
```

#### 扩展属性
如果已经有了个 props 对象，并且想在 JSX 中传递它，你可以使用 ... 作为扩展操作符来传递整个属性对象。下面两个组件是等效的：
```jsx
function App1() {
  return <Greeting firstName="Ben" lastName="Hector" />;
}

function App2() {
  const props = {firstName: 'Ben', lastName: 'Hector'};
  return <Greeting {...props} />;
}
```

这样做也可能让很多不相关的属性，传递到不需要它们的组件中使代码变得混乱。我们建议你谨慎使用此语法

## 子代
在包含开始和结束标签的 JSX 表达式中，标记之间的内容作为特殊的参数传递：props.children。有几种不同的方法来传递子代：

#### 字符串常量
你可以在开始和结束标签之间放入一个字符串，则 props.children 就是那个字符串。这对于许多内置 HTML 元素很有用。例如：
```jsx
<MyComponent>Hello world!</MyComponent>
```

#### JSX
你可以通过子代嵌入更多的 JSX 元素，这对于嵌套显示组件非常有用：
```jsx
<MyContainer>
  <MyFirstComponent />
  <MySecondComponent />
</MyContainer>
```

#### JavaScript 表达式
```jsx
function Item(props) {
  return <li>{props.message}</li>;
}

function TodoList() {
  const todos = ['finish doc', 'submit pr', 'nag dan to review'];
  return (
    <ul>
      {todos.map((message) => <Item key={message} message={message} />)}
    </ul>
  );
}
```

#### 函数

#### 布尔值、Null 和 Undefined 被忽略
false、null、undefined 和 true 都是有效的子代，但它们不会直接被渲染。下面的表达式是等价的：

```jsx
<div />

<div></div>

<div>{false}</div>

<div>{null}</div>

<div>{undefined}</div>

<div>{true}</div>
```

```jsx
<div>
  {showHeader && <Header />}
  <Content />
</div>
```
