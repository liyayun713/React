# AJAX
React 组件的数据可以通过 componentDidMount 方法中的 Ajax 来获取，当从服务端获取数据库可以将数据存储在 state 中，再用 this.setState 方法重新渲染 UI。

当使用异步加载数据时，在组件卸载前使用 componentWillUnmount 来取消未完成的请求。

```jsx
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8" />
  <title>菜鸟教程 React 实例</title>
  <script src="https://cdn.bootcss.com/react/15.4.2/react.min.js"></script>
  <script src="https://cdn.bootcss.com/react/15.4.2/react-dom.min.js"></script>
  <script src="https://cdn.bootcss.com/babel-standalone/6.22.1/babel.min.js"></script>
  <script src="https://cdn.bootcss.com/jquery/2.1.4/jquery.min.js"></script>
</head>
<body>
  <div id="example"></div>
  <script type="text/babel">
      var UserGist = React.createClass({
        getInitialState: function() {
          return {
            username: '',
            lastGistUrl: ''
          };
        },

        componentDidMount: function() {
          this.serverRequest = $.get(this.props.source, function (result) {
            var lastGist = result[0];
            this.setState({
              username: lastGist.owner.login,
              lastGistUrl: lastGist.html_url
            });
          }.bind(this));
        },

        componentWillUnmount: function() {
          this.serverRequest.abort();
        },

        render: function() {
          return (
            <div>
              {this.state.username} 用户最新的 Gist 共享地址：
              <a href={this.state.lastGistUrl}>{this.state.lastGistUrl}</a>
            </div>
          );
        }
      });

      ReactDOM.render(
        <UserGist source="https://api.github.com/users/octocat/gists" />,
        document.getElementById('example')
      );
  </script>
</body>
</html>
```
