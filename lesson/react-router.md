# React-Router
### 基本用法
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
### exact
精确匹配

### NavLink
1. import {NavLink} from 'react-router-dom';
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
2. NavLink的常用选项
* activeClassName 激活状态

### 404设置和跳转
* Switch组件
* Redirect

```jsx
ReactDOM.render(
    <Router>
        <div>
            <NavBar />
            <Switch>
                <Route path="/" component={RouterA} exact />
                <Route path="/b" component={RouterB} />
                <Route path="/c" component={RouterC} />
                <Redirect from="/redirect" to="/b" />
                {/* 找不到跳到Error，在最下面 */}
                <Route component={Error} />
            </Switch>
        </div>
    </Router>,
    document.getElementById('app')
)
```

### 路由传值
NavLink 上传入值
```jsx
<NavLink to="/c/008/Tony Li" activeClassName="active-state">C 路由</NavLink> ||&nbsp;
```

Router中的Route上定义
```jsx
<Route path="/c/:id/:name" component={RouterC} />
```

组件中取值
```jsx
<div>
    <div>Router C</div>
    <div>ID: {this.props.match.params.id}</div>
    <div>Name: {this.props.match.params.name}</div>
</div>
```

### Router中的属性
* basename 层级（功能划分时可以使用）
* forceRefresh 强制刷新 true or false （路由效果不起作用，）

### 路由模式
5种路由模式

1. BrowserRouter 默认
2. HashRouter （刷新可以找到路径）
3. MemoryRouter 内存路由模式，地址栏不跳转
4. NativeRouter 原生，React-Native使用
5. StaticRouter 静态路由，SSR使用

### prompt用法

