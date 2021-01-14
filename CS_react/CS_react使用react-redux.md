# react使用react-redux

> &emsp;&emsp;之前研究了react，redux，react-redux，redux-thunk，其中数据流解决方案是redux和react-redux，当中react-thunk只是一个处理异步任务的中间件，它就像是一个插件。
> &emsp;&emsp;按理来说应该是先熟悉redux，然后再使用react-redux。react-redux是redux的官方绑定库，说白了就是为了方便react使用redux而设计的类库。而本文是面向开发时速查的，所以认定读者已经熟悉react和redux，直接跳跃的介绍react-redux的使用。如果不熟悉的读者可以查看我之前介绍redux的文章。
> &emsp;&emsp;react-redux 中文文档：https://www.redux.org.cn/docs/react-redux/

## 1. 安装
```bash
yarn add react-redux
```
按理来说安装react-redux时候它应该是会自动安装redux的

## 2. 原理
&emsp;&emsp;这是react-redux官方的概念图：
![react-redux](https://img-blog.csdnimg.cn/20210109102543278.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
&emsp;&emsp;我认为react-redux的容器组件和UI组件根本就是虚的概念，更应该说是容器组件就是一个父组件，UI组件就是一个子组件，父组件和redux交互，从redux获取数据到自己的组件（父组件）里，父组件再通过组件通信传递数据到子组件里，子组件不与redux做直接的交互。
&emsp;&emsp;举个例子就像列表里列表框和列表子项的关系，一个列表就一个列表框，列表框从redux获取列表数据，再通过map函数渲染很多列表子项。列表框就是这个父组件，列表子项就是那个子组件，按照react-redux的说法就是列表框就是容器组件，列表子项就是UI组件。
## 3. 使用介绍
&emsp;&emsp;react-redux就是提供了几个API简化了react操作redux的难度，本文重点描述这个API
### 1. Provider 
最原始在最外层函数里组件传入 store，这样才能在组件里拿到store
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210107214500580.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
组件里的store：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210107215519670.png)
&emsp;&emsp;现在不用手动传入store，使用Provider 包裹组件让所有组件都能拿到state，并且它会自动设置监听，一旦有组件的state改变就重新渲染。
```html
<Provider store={store}>
  <App />
</Provider>
```
### 2. connect 
&emsp;&emsp;在组件里面用`connect()()`连接组件和store容器，这两个括号意思是要被调用两次，第一次设置参数，第二次传入组件。也就是第一个括号设置参数，第二个括号传入要连接的组件，也就是当前组件，它会接收第一个括号传进去的参数，所以很简单没必要详细说明。重点说第一个括号里两个参数`mapStateToprops` 和 `mapDispatchToProps`。

```javascript
import {createIncrementAction, createDecrementAction,createIncrementAsyncAction} from "../../redux/actions";
import {connect} from 'react-redux'; //连接UI组件和容器组件的东西

//////////
// 此处一堆代码
///////////


/**
 * connect 起到了subscribe的作用，监听状态
 */
export default connect(
    //state 就是redux的总状态
    state => ({count:state.he,renshu:state.rens.length}),
    {createIncrementAction, createDecrementAction, createIncrementAsyncAction}
)(CountContainer);
```
#### mapStateToprops
>&emsp;&emsp;将外部的数据（即state对象）转换为UI组件的标签属性

&emsp;&emsp;第一个()里的第一个参数 `state`，`state`这个参数接收的是`store`里面全部的状态，是一个大的状态，一个大的对象，也是这两个reducer的返回数据集合。 rens 就是store里那个`reducer`的`key`，也就是这个组件对应的那一部分的数据的`key`，`state.rens`就是拿到这个组件对应的reducer返回的数据，`{users:state.rens}` 是把它包装成对象传入第二个括号传入的组件的props当中，在被传入的组件当中可以用`this.props`看得到被传入的数据。
#### mapDispatchToProps
>&emsp;&emsp;将分发action的函数转换为UI组件的标签属性

&emsp;&emsp;第一个括号里第二个参数是action的集合，{}里可以传入很多action，这些action也都被传入第二个括号当中传入的组件当中，一般第二个括号传入的都是当前的组件，所以state和action也都传入当前组件当中。以下就把第二个括号当中传入的组件称作当前组件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210108202245948.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)

### 3. 组件里调用

上面mapStateToprops和mapDispatchToProps给当前组件传入的参数在当前组件里用 `this.props` 就能看见，**调用的时候必须要用this.props调用**，因为需要让react-redux帮忙dispatch。




