# React.js Notes
## React Router
1. npm i --save react-router react-router-dom
2. import {BrowserRouter as Router , Route} from 'react-router-dom';
3. 设计路由
```jsx
ReactDOM.render(
    <Router>
        <div>
            <Route exact path="/" component={Jspang} />
            <Route path="/Jspangb" component={Jspangb} />
            <Route path="/Jspangc" component={Jspangc} />
        </div>
    </Router>,
    document.getElementById("app")
);
```
4. exact
5. import {NavLink} from 'react-router-dom';
```jsx
// nav.js
const NavBar = () =>(
    <div>
        <div>
            <NavLink exact to='/'>Jspanga</NavLink> |&nbsp;
            <NavLink to='/Jspangb'>Jspangb</NavLink> |&nbsp;
            <NavLink to='/Jspangc'>Jspangc</NavLink>
        </div>
    </div>
)
export default NavBar;
```
6. NavLink的常用选项
7. 404设置和跳转
8. 路由传值
9. Router中的属性和路由模式
10. prompt用法

## 构建项目
1. create-react-app脚手架
2. generator-react-webpack（基于yeoman）
2. 手动配置webpack

## React 高级指引
1. [深入JSX](https://github.com/liyayun713/React/blob/master/lesson/senior-jsx.md)
2. 使用 PropTypes 检查类型
3. 静态类型检查（建议使用 Flow 或者 TypeScript 来替代 PropTypes。）
4. [Refs & DOM](https://github.com/liyayun713/React/blob/master/lesson/refs-dom.md)
5. [非受控组件](https://github.com/liyayun713/React/blob/master/lesson/uncontrolled-components.md)
6. [性能优化](https://github.com/liyayun713/React/blob/master/lesson/performance-optimization.md)
7. [不使用ES6](https://github.com/liyayun713/React/blob/master/lesson/without-es6.md)
8. [不使用JSX](https://github.com/liyayun713/React/blob/master/lesson/without-jsx.md)
9. [协调（Reconciliation）](https://github.com/liyayun713/React/blob/master/lesson/reconciliation.md)

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
![](https://github.com/bailicangdu/pxq/blob/master/screenshot/react-lifecycle.png)

**组件在初始化时会触发5个钩子函数：**

  **1、getDefaultProps()**

> 设置默认的props，也可以用dufaultProps设置组件的默认属性。

  **2、getInitialState()**

> 在使用es6的class语法时是没有这个钩子函数的，可以直接在constructor中定义this.state。此时可以访问this.props。

  **3、componentWillMount()**

> 组件初始化时只调用，以后组件更新不调用，整个生命周期只调用一次，此时可以修改state。

  **4、 render()**

> react最重要的步骤，创建虚拟dom，进行diff算法，更新dom树都在此进行。此时就不能更改state了。

  **5、componentDidMount()**

> 组件渲染之后调用，可以通过this.getDOMNode()获取和操作dom节点，只调用一次。

**在更新时也会触发5个钩子函数：**

  **6、componentWillReceivePorps(nextProps)**

> 组件初始化时不调用，组件接受新的props时调用。

  **7、shouldComponentUpdate(nextProps, nextState)**

> react性能优化非常重要的一环。组件接受新的state或者props时调用，我们可以设置在此对比前后两个props和state是否相同，如果相同则返回false阻止更新，因为相同的属性状态一定会生成相同的dom树，这样就不需要创造新的dom树和旧的dom树进行diff算法对比，节省大量性能，尤其是在dom结构复杂的时候。不过调用this.forceUpdate会跳过此步骤。

  **8、componentWillUpdate(nextProps, nextState)**

> 组件初始化时不调用，只有在组件将要更新时才调用，此时可以修改state

  **9、render()**

> 不多说

  **10、componentDidUpdate()**

> 组件初始化时不调用，组件更新完成后调用，此时可以获取dom节点。

还有一个卸载钩子函数

  **11、componentWillUnmount()**

> 组件将要卸载时调用，一些事件监听和定时器需要在此时清除。

以上可以看出来react总共有10个周期函数（render重复一次），这个10个函数可以满足我们所有对组件操作的需求，利用的好可以提高开发效率和组件性能。

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
React 具有强大的组合模型，我们建议使用组合而不是继承来复用组件之间的代码。

在 Facebook 网站上，我们的 React 使用了数以千计的组件，然而却还未发现任何需要推荐你使用继承的情况。

属性和组合为你提供了以清晰和安全的方式自定义组件的样式和行为所需的所有灵活性。请记住，组件可以接受任意元素，包括基本数据类型、React 元素或函数。

如果要在组件之间复用 UI 无关的功能，我们建议将其提取到单独的 JavaScript 模块中。这样可以在不对组件进行扩展的前提下导入并使用该函数、对象或类。

### React 理念

### React 的 diff 算法
当组件更新的时候，react会创建一个新的虚拟dom树并且会和之前储存的dom树进行比较，这个比较多过程就用到了diff算法，所以组件初始化的时候是用不到的。react提出了一种假设，相同的节点具有类似的结构，而不同的节点具有不同的结构。在这种假设之上进行逐层的比较，如果发现对应的节点是不同的，那就直接删除旧的节点以及它所包含的所有子节点然后替换成新的节点。如果是相同的节点，则只进行属性的更改。

对于`列表`的diff算法稍有不同，因为列表通常具有相同的结构，在对列表节点进行删除，插入，排序的时候，单个节点的整体操作远比一个个对比一个个替换要好得多，所以在创建列表的时候需要设置 `key` 值，这样react才能分清谁是谁。当然不写key值也可以，但这样通常会报出警告，通知我们加上key值以提高react的性能。

### React-Router 路由
当页面比较多时，项目就会变得越来越大，尤其对于单页面应用来说，初次渲染的速度就会很慢，这时候就需要`按需加载`，只有切换到页面的时候才去加载对应的js文件。react配合webpack进行按需加载的方法很简单，Route的component改为getComponent，组件用require.ensure的方式获取，并在webpack中配置chunkFilename。

```jsx
const chooseProducts = (location, cb) => {
    require.ensure([], require => {
        cb(null, require('../Component/chooseProducts').default)
    },'chooseProducts')
}

const helpCenter = (location, cb) => {
    require.ensure([], require => {
        cb(null, require('../Component/helpCenter').default)
    },'helpCenter')
}

const saleRecord = (location, cb) => {
    require.ensure([], require => {
        cb(null, require('../Component/saleRecord').default)
    },'saleRecord')
}

const RouteConfig = (
    <Router history={history}>
        <Route path="/" component={Roots}>
            <IndexRoute component={index} />//首页
            <Route path="index" component={index} />
            <Route path="helpCenter" getComponent={helpCenter} />//帮助中心
            <Route path="saleRecord" getComponent={saleRecord} />//销售记录
            <Redirect from='*' to='/'  />
        </Route>
    </Router>
);
```

### 组件通信
1. react推崇的是单向数据流，自上而下进行数据的传递，但是由下而上或者不在一条数据流上的组件之间的通信就会变的复杂。解决通信问题的方法很多，**如果只是父子级关系，父级可以将一个回调函数当作属性传递给子级，子级可以直接调用函数从而和父级通信。**

2. 组件层级嵌套到比较深，可以使用上下文 **getChildContext** 来传递信息，这样在不需要将函数一层层往下传，任何一层的子级都可以通过this.context直接访问。

3. 兄弟关系的组件之间无法直接通信，它们只能利用同一层的上级作为中转站。而如果兄弟组件都是最高层的组件，为了能够让它们进行通信，必须在它们外层再套一层组件，这个外层的组件起着保存数据，传递信息的作用，这其实就是 **redux** 所做的事情。

4. 组件之间的信息还可以通过全局事件来传递。不同页面可以通过参数传递数据，下个页面可以用location.param来获取。其实react本身很简单，难的在于如何优雅高效的实现组件之间数据的交流。

### React-Redux

首先，redux并不是必须的，它的作用相当于在顶层组件之上又加了一个组件，作用是进行逻辑运算、储存数据和实现组件尤其是顶层组件的通信。如果组件之间的交流不多，逻辑不复杂，只是单纯的进行视图的渲染，这时候用回调，context就行，没必要用redux，用了反而影响开发速度。但是如果组件交流特别频繁，逻辑很复杂，那redux的优势就特别明显了。我第一次做react项目的时候并没有用redux，所有的逻辑都是在组件内部实现，当时为了实现一个逻辑比较复杂的购物车，洋洋洒洒居然写了800多行代码，回头一看我自己都不知道写的是啥，画面太感人。

先简单说一下redux和react是怎么配合的。react-redux提供了connect和Provider两个好基友，它们一个将组件与redux关联起来，一个将store传给组件。组件通过dispatch发出action，store根据action的type属性调用对应的reducer并传入state和这个action，reducer对state进行处理并返回一个新的state放入store，connect监听到store发生变化，调用setState更新组件，此时组件的props也就跟着变化。

流程是这个样子的：

![](https://github.com/bailicangdu/pxq/blob/master/screenshot/simple_redux.jpg)
