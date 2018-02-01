# 性能优化
> 更新UI时，React在内部使用几种巧妙的技术来最小化DOM操作的数量。对许多应用来说，使用React不需要做太多的优化工作就可以快速创建用户界面。除此之外，还有一些优化React应用性能的办法。

## 使用生产版本

## 使用Chrome Timeline归档组件
![](https://doc.react-china.org/static/react-perf-chrome-timeline-64d522b74fb585f1abada9801f85fa9d-dcc89.png)

## 避免重复渲染
React在渲染出的UI内部建立和维护了一个内层的实现方式，它包括了从组件返回的React元素。**这种实现方式使得React避免了一些不必要的创建和关联DOM节点，因为这样做可能比直接操作JavaScript对象更慢一些。有时它被称之为“虚拟DOM”**，但是它其实和React Native的工作方式是一样的。

当一个组件的props或者state改变时，React通过比较新返回的元素和之前渲染的元素来决定是否有必要更新实际的DOM。当他们不相等时，React会更新DOM。

在一些情况下，你的组件可以通过重写这个生命周期函数shouldComponentUpdate来提升速度， 它是在重新渲染过程开始前触发的。 这个函数默认返回true，可使React执行更新：

```jsx
shouldComponentUpdate(nextProps, nextState) {
  return true;
}
```

如果你知道在某些情况下你的组件不需要更新，你可以在shouldComponentUpdate内返回false来跳过整个渲染进程，该进程包括了对该组件和之后的内容调用render()指令。

## shouldComponentUpdate应用

## 不会突变的数据的力量

## 使用不可突变的数据结构
