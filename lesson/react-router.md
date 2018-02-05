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

### Router中的属性和路由模式

### prompt用法
