# React 表单与事件
### 1、一个简单的实例
在实例中我们设置了输入框 input 值 value = {this.state.data}。在输入框值发生变化时我们可以更新 state。我们可以使用 onChange 事件来监听 input 的变化，并修改 state。

```jsx
var HelloMessage = React.createClass({
  getInitialState: function() {
    return {
      value: 'Hello Runoob!'
    };
  },
  handleChange: function(event) {
    this.setState({
      value: event.target.value
    });
  },
  render: function() {
    var value = this.state.value;
    return <div>
              <input type="text" value={value} onChange={this.handleChange} /> 
              <h4>{value}</h4>
           </div>;
  }
});
ReactDOM.render(
  <HelloMessage />,
  document.getElementById('example')
);
```

### 2、在子组件上使用表单
onChange 方法将触发 state 的更新并将更新的值传递到子组件的输入框的 value 上来重新渲染界面。

你需要在父组件通过创建事件句柄 (handleChange) ，并作为 prop (updateStateProp) 传递到你的子组件上。

```jsx
var Content = React.createClass({
  render: function() {
    return  <div>
              <input type="text" value={this.props.myDataProp} onChange={this.props.updateStateProp} /> 
              <h4>{this.props.myDataProp}</h4>
            </div>;
  }
});
var HelloMessage = React.createClass({
  getInitialState: function() {
    return {
      value: 'Hello Runoob!'
    };
  },
  handleChange: function(event) {
    this.setState({
      value: event.target.value
    });
  },
  render: function() {
    var value = this.state.value;
    return <div>
             <Content myDataProp={value} updateStateProp={this.handleChange}></Content>
           </div>;
  }
});
ReactDOM.render(
  <HelloMessage />,
  document.getElementById('example')
);
```

当你需要从子组件中更新父组件的 state 时，你需要在父组件通过创建事件句柄 (handleChange) ，并作为 prop (updateStateProp) 传递到你的子组件上。实例如下：

#### updateStateProp 相当于 vue 中的 $emit，父组件监听变化调用回调函数
