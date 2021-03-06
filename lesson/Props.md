# Props
state 和 props 主要的区别在于 **props 是不可变的**，而 **state 可以根据与用户交互来改变**。这就是为什么有些容器组件需要定义 state 来更新和修改数据。 而子组件只能通过 props 来传递数据。

### 使用 props


```jsx
<body>
  <div id="demo"></div>
  <script type="text/babel">
    var PropsDemo = React.createClass({
      render: function () {
        return {
          <div>{this.props.name}</div>
        };
      }
    })

    ReactDOM.render(
      <PropsDemo name="Hello World!"/>,
      document.getElementById('demo')
    )
  </script>
</body>
```

### 默认 props
可以通过 getDefaultProps() 方法为 props 设置默认值

```jsx
<body>
  <div id="demo"></div>
  <script type="text/babel">
    var PropsDemo = React.createClass({
      getDefaultProps: function () {
        return {
          name: 'getDefaultProps'
        };
      },
      render: function () {
        return {
          <div>{this.props.name}</div>
        };
      }
    })

    ReactDOM.render(
      <PropsDemo />,
      document.getElementById('demo')
    )
  </script>
</body>
```

### State 和 Props
我们可以在父组件中设置 state， 并通过在子组件上使用 props 将其传递到子组件上。在 render 函数中, 我们设置 name 和 site 来获取父组件传递过来的数据。

```jsx
var Father = React.createClass({
  getInitialState: function () {
    return {
      name: 'Tony Li',
      url: 'github.com/liyayun713'
    };
  },
  render: function () {
    return {
      <div>
        <Childone name={this.state.name} />
        <Childtwo url={this.state.url} />
      </div>
    };
  }
})

var Childone = React.createClass({
  render: function () {
    <h1>{this.props.name}</h1>
  }
})

var Childtwo = React.createClass({
  render: function () {
    <a href={this.props.url}>{this.props.url}</a>
  }
})

ReactDOM.render(
  <Father />,
  document.getElementById('example')
)
```

### props 验证
Props 验证使用 propTypes，它可以保证我们的应用组件被正确使用，React.PropTypes 提供很多验证器 (validator) 来验证传入数据是否有效。当向 props 传入无效数据时，JavaScript 控制台会抛出警告。

以下实例创建一个 Mytitle 组件，**属性 title 是必须的且是字符串，非字符串类型会自动转换为字符串**

```jsx
var title = "菜鸟教程";
// var title = 123;
var MyTitle = React.createClass({
  propTypes: {
    title: React.PropTypes.string.isRequired,
  },
  render: function() {
     return <h1> {this.props.title} </h1>;
   }
});
ReactDOM.render(
    <MyTitle title={title} />,
    document.getElementById('example')
);
```

更多验证器说明如下：

```jsx
React.createClass({
  propTypes: {
    // 可以声明 prop 为指定的 JS 基本数据类型，默认情况，这些数据是可选的
   optionalArray: React.PropTypes.array,
    optionalBool: React.PropTypes.bool,
    optionalFunc: React.PropTypes.func,
    optionalNumber: React.PropTypes.number,
    optionalObject: React.PropTypes.object,
    optionalString: React.PropTypes.string,
 
    // 可以被渲染的对象 numbers, strings, elements 或 array
    optionalNode: React.PropTypes.node,
 
    //  React 元素
    optionalElement: React.PropTypes.element,
 
    // 用 JS 的 instanceof 操作符声明 prop 为类的实例。
    optionalMessage: React.PropTypes.instanceOf(Message),
 
    // 用 enum 来限制 prop 只接受指定的值。
    optionalEnum: React.PropTypes.oneOf(['News', 'Photos']),
 
    // 可以是多个对象类型中的一个
    optionalUnion: React.PropTypes.oneOfType([
      React.PropTypes.string,
      React.PropTypes.number,
      React.PropTypes.instanceOf(Message)
    ]),
 
    // 指定类型组成的数组
    optionalArrayOf: React.PropTypes.arrayOf(React.PropTypes.number),
 
    // 指定类型的属性构成的对象
    optionalObjectOf: React.PropTypes.objectOf(React.PropTypes.number),
 
    // 特定 shape 参数的对象
    optionalObjectWithShape: React.PropTypes.shape({
      color: React.PropTypes.string,
      fontSize: React.PropTypes.number
    }),
 
    // 任意类型加上 `isRequired` 来使 prop 不可空。
    requiredFunc: React.PropTypes.func.isRequired,
 
    // 不可空的任意类型
    requiredAny: React.PropTypes.any.isRequired,
 
    // 自定义验证器。如果验证失败需要返回一个 Error 对象。不要直接使用 `console.warn` 或抛异常，因为这样 `oneOfType` 会失效。
    customProp: function(props, propName, componentName) {
      if (!/matchme/.test(props[propName])) {
        return new Error('Validation failed!');
      }
    }
  },
  /* ... */
});
```
