# 组件生命周期
组件的生命周期可分成三个状态：
* Mounting：已插入真实 DOM
* Updating：正在被重新渲染
* Unmounting：已移出真实 DOM

生命周期的方法有：
* componentWillMount: 在渲染前调用，在客户端也在服务端。

* componentDidMount: 在第一次渲染后调用，只在客户端。之后组件已经生成了对应的DOM结构，可以通过 this.getDOMNode() 来进行访问。 如果你想和其他JavaScript框架一起使用，可以在这个方法中调用 setTimeout, setInterval 或者发送 AJAX 请求等操作(防止异部操作阻塞UI)。

* componentWillReceiveProps: 在组件接收到一个新的prop时被调用。这个方法在初始化render时不会被调用。

* shouldComponentUpdate: 返回一个布尔值。在组件接收到新的props或者state时被调用。在初始化时或者使用forceUpdate时不被调用。可以在你确认不需要更新组件时使用。

* componentWillUpdate: 在组件接收到新的props或者state但还没有render时被调用。在初始化时不会被调用。

* componentDidUpdate: 在组件完成更新后立即调用。在初始化时不会被调用。

* componentWillUnmount: 在组件从 DOM 中移除的时候立刻被调用。

以下实例在 Hello 组件加载以后，通过 componentDidMount 方法设置一个定时器，每隔100毫秒重新设置组件的透明度，并重新渲染：

```jsx
var Hello = React.createClass({
  getInitialState: function () {
    return {
      opacity: 1.0
    };
  },
 
  componentDidMount: function () {
    this.timer = setInterval(function () {
      var opacity = this.state.opacity;
      opacity -= .05;
      if (opacity < 0.1) {
        opacity = 1.0;
      }
      this.setState({
        opacity: opacity
      });
    }.bind(this), 100);
  },
 
  render: function () {
    return (
      <div style={{opacity: this.state.opacity}}>
        Hello {this.props.name}
      </div>
    );
  }
});
 
ReactDOM.render(
  <Hello name="world"/>,
  document.body
);
```

以下实例初始化 state ， setNewNumber 用于更新 state。所有生命周期在 Content 组件中。

```jsx
var Button = React.createClass({
  getInitialState: function() {
    return {
      data:0
    };
  },
  setNewNumber: function() {
    this.setState({data: this.state.data + 1})
  },
  render: function () {
    return (
       <div>
          <button onClick = {this.setNewNumber}>INCREMENT</button>
          <Content myNumber = {this.state.data}></Content>
       </div>
    );
  }
})
var Content = React.createClass({
  componentWillMount:function() {
      console.log('Component WILL MOUNT!')
  },
  componentDidMount:function() {
       console.log('Component DID MOUNT!')
  },
  componentWillReceiveProps:function(newProps) {
        console.log('Component WILL RECEIVE PROPS!')
  },
  shouldComponentUpdate:function(newProps, newState) {
        return true;
  },
  componentWillUpdate:function(nextProps, nextState) {
        console.log('Component WILL UPDATE!');
  },
  componentDidUpdate:function(prevProps, prevState) {
        console.log('Component DID UPDATE!')
  },
  componentWillUnmount:function() {
         console.log('Component WILL UNMOUNT!')
  },
 
  render: function () {
    return (
      <div>
        <h3>{this.props.myNumber}</h3>
      </div>
    );
  }
});
ReactDOM.render(
   <div>
      <Button />
   </div>,
  document.getElementById('example')
);
```
