# URL-Parameters
```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import {
	BrowserRouter as Router,
	Route,
	Link
} from 'react-router-dom';

const ParamsExample = () => (
	<Router>
		<div>
			<ul>
				<li><Link to="/A">A</Link></li>
				<li><Link to="/B">B</Link></li>
				<li><Link to="/C">C</Link></li>
				<li><Link to="/D">D</Link></li>
				<li><Link to="/E">E</Link></li>
			</ul>
			<Route path="/:id" component={Child}/>
		</div>
	</Router>
)

const Child = ({ match }) => (
	<div>{match.params.id}</div>
)

ReactDOM.render(
	<ParamsExample />,
	document.getElementById('app')
)
```
