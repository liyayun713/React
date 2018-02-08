# Redirects

### skills:
1. Redirect
2. withRouter


### 实例
```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import {
	BrowserRouter as Router,
	Route,
	Link,
	withRouter,
	Redirect
} from 'react-router-dom';

const fakeAuth = {
	isAuthenticated: false,
	authenticate(cb) {
	  	this.isAuthenticated = true
	  	setTimeout(cb, 100) // fake async
	},
	signout(cb) {
	  	this.isAuthenticated = false
	  	setTimeout(cb, 100)
	}
}

const AuthExample = () => (
	<Router>
		<div>
			<AuthButton />
			<ul>
				<li><Link to="/public">Public Page</Link></li>
				<li><Link to="/protected">Protected Page</Link></li>
			</ul>
			<Route path="/public" component={Public}/>
			<Route path="/login" component={Login}/>
			<PrivateRoute path="/protected" component={Protected}/>
		</div>
	</Router>
)

const Public = () => <h3>Public</h3>
const Protected = () => <h3>Protected</h3>

const AuthButton = withRouter(({ history }) => (
	fakeAuth.isAuthenticated
	?
	<div>
		Welcome! <button onClick={() => {
			fakeAuth.signout(() => history.push('/'))
		}}>Sign Out</button>
	</div>
	:
	<p>You are not logged in.</p>
))

const PrivateRoute = ({ component: Component, ...rest }) => (
	<Route {...rest} render={props => {
		console.log(fakeAuth.isAuthenticated);
		console.log(props);
		console.log(rest);
		console.log(...rest);
		return (
			fakeAuth.isAuthenticated
			?
			<Component {...props}/>
			:
			<Redirect to={{
				pathname: '/login',
				state: { from: props.location }
			}} />
		)
	}} />
)

class Login extends React.Component {
	state = {
		redirectToReferrer: false
	}
	login = () => {
		fakeAuth.authenticate(() => {
			this.setState({redirectToReferrer: true})
		})
	}
	render () {
		console.log(this.props);
		console.log(this.props.location.state);
		const { from } = this.props.location.state || { from: { pathname: '/' } }
		const { redirectToReferrer } = this.state
		console.log(from);

		if (redirectToReferrer) {
			return (
				<Redirect to={from} />
			)
		}

		return (
			<div>
				<p>You must log in to view the page at {from.pathname}</p>
				<button onClick={this.login}>Login in</button>
			</div>
		)
	}
}

ReactDOM.render(
	<AuthExample />,
	document.getElementById('app')
)

```
