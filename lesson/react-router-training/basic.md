# Basic

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import {BrowserRouter as Router, Route, Link} from 'react-router-dom';

const BasicExample = () => (
	<Router>
		<div>
			<ul>
				<li><Link to="/">Component A</Link></li>
				<li><Link to="/b">Component B</Link></li>
				<li><Link to="/c">Component C</Link></li>
			</ul>
			<hr/>
			<Route exact path="/" component={ComponentA} />
			<Route path="/b" component={ComponentB} />
			<Route path="/c" component={ComponentC} />
		</div>
	</Router>
)

const ComponentA = () => (
	<div>im component A</div>
)

const ComponentB = () => (
	<div>im component B</div>
)

const ComponentC = ({ match }) => (
	<div>
		<h3>component C</h3>
		<ul>
			<li>
				<Link to={`${match.url}/c1`}>im component C1</Link>
			</li>
			<li>
				<Link to={`${match.url}/c2`}>im component C2</Link>
			</li>
			<li>
				<Link to={`${match.url}/c3`}>im component C3</Link>
			</li>
		</ul>
		<Route path={`${match.url}/:key`} component={ComponentCC} />
		<Route exact path={match.url} render={() => (
			<h3>Please choose child component</h3>
		)} />
	</div>
)

const ComponentCC = ({ match }) => (
	<div>
		<h3>{match.params.key}</h3>
	</div>
)

ReactDOM.render(
	<BasicExample />,
	document.getElementById('app')
)

```
