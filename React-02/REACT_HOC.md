# React高阶组件

* 装饰器模式

```js
function hello() {
  console.log('hello YueYue');
}

function WrapperHello(fn) {
  return function () {
    console.log('before hello');
    fn()
    console.log('after hello');
  }
}
hello = WrapperHello(hello)
hello()
```

### React使用

* 高阶组件属性代理

```js
function WrapperHello(Comp) {
  class WrapComp extends React.Component{
    render(){
      return (
        <div>
         <p>这是HOC高阶组件特有元素</p>
         <Camp {...this.props}></Camp>
        </div>
      )
    }
  }
  return WrapComp
}

class Hello extends React.component {
  render(){
    return(<h2>hello YueYue</h2>)
  }
}

hello = WrapperHello(Hello)
```

* HOC，给出的组件外面包装一层

  * 属性代理
  * 反向继承:渲染劫持

* 高阶组件反向继承

##### HOC组件hoc.js

```js
export function WrapperHello(Comp) {
  class WrapComp extends Comp {
    componentDidMount(){
      console.log('高阶组件新增的生命周期，加载完成');
    }
    render(){
      return <Comp></Comp>
    }
  }
  return WrapComp
}
```

##### 被HOC包裹的组件

```js
//正常写法
class Hello extends React.component {
  render(){
    return(<h2>hello YueYue</h2>)
  }
}
Hello = WrapperHello(Hello)
//简写
@WrapperHello
class Hello extends React.component {
  render(){
    return(<h2>hello YueYue</h2>)
  }
}
```



