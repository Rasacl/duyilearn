# 组件与事件绑定

本章包含以下内容：

- *React* 中的组件
- 为组件绑定事件
- *this* 的指向
- 向事件处理函数传参



## *React* 中的组件

在 *React* 中，可以使用类的方式来声明一个组件。

```js
class 类名 extends React.Component{
  render(){
    return (
    	// 一段 JSX
    )
  }
}
```



除了类组件，*React* 中还支持使用函数来创建组件，同样需要返回一段 *JSX*，来表示这个组件的 *UI* 是什么样的。

```js
function 组件名(){
  return (
  	// 一段 JSX
  );
}
```

**早期**的函数组件被称之为无状态组件，一般仅仅用来做纯 *UI* 的展示，里面不会有复杂的逻辑。

但是从 *React 16.8* 推出 *Hooks* 后，现在更多的是使用函数组件了。

这不仅仅是语法的改变，同时也代表着整个 *React* 编程思想的一种转变。



## 为组件绑定事件

在 *React* 中绑定事件的写法如下：

```react
<button onClick={activateLasers}>Activate Lasers</button>
```

在 *React* 中无法通过 *return false* 来阻止默认行为，所以只有使用 *e.preventDefault* 的方式来阻止默认行为。

```react
function Form() {
  function handleSubmit(e) {
    e.preventDefault();
    console.log('You clicked submit.');
  }

  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">Submit</button>
    </form>
  );
}
```

如果是类组件，那么事件处理函数写作一个类方法。

```react
class Welcome extends React.Component {
  // 事件处理函数
  eventHandler(e){
    window.alert('Hello');
    e.preventDefault();
  }
  
  render() {
    return (
      <a href="https://www.baidu.com/" onClick={this.eventHandler}>this is a test</a>
    );
  }
}
```

在 *React* 的事件处理函数中所传入的事件对象，是一个合成事件对象。

*React* 也提供了访问原生事件对象的方式。如下：

```react
eventHandler(e){
    e.nativeEvent // 原生事件对象
}
```



## *this* 的指向

由于 *JS* 中 *this* 的特殊性，事件处理函数中的 *this* 并不会指向当前的组件，这就需要我们自行对 *this* 进行指向的修正。

这里介绍 *3* 种解决方式：

- 将事件处理函数修改为箭头函数
- 将事件绑定修改为箭头函数
- 使用 *bind* 方法来强制绑定 *this* 的指向



## 向事件处理程序传参

另外还有一个非常重要的问题，就是如何向事件处理函数传递参数。

如果要传递参数，可以使用下面的两种方式来进行传参：

- 通过 *bind* 方法在绑定 *this* 指向时向事件处理函数进行传参
- 绑定事件时，通过书写箭头函数的形式来传参
