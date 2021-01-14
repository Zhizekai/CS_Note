# redux
> 英文文档: https://redux.js.org/
> 中文文档: http://www.redux.org.cn/
> Github: https://github.com/reactjs/redux

&emsp;&emsp;写使用介绍时候纠结应该先从哪讲起，最后决定按照redux官方文档的顺序说起，按照组件发起action，action dispatch（分发）操作对象到store，store把之前的state状态和action的操作对象一起给到reducer，reducer返回新的state到组件这个过程说起。

## 原理
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210109165321766.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)

## action
组件发起action和得到数据：
```javascript

import {createIncrementAction,createDecrementAction,createIncrementAsyncAction} from "../redux/actions";
import store from "../redux/store";

// 一堆代码

//奇数再加
    incrementIfOdd = () => {
        const {value} = this.selectNumber;
        const count = store.getState(); //reducer 返回的就是一个数字不需要解构赋值
        if (count % 2 !== 0) {
            // this.setState({count: count + value * 1});
            store.dispatch(createDecrementAction(value*1))
        }
    };
    //异步加
    incrementAsync = () => {
        const {value} = this.selectNumber;
        const count = store.getState();
        store.dispatch(createIncrementAsyncAction(value*1,1000))
        // setTimeout(() => {
        //     // this.setState({count: count + value * 1});
        //     store.dispatch(createIncrementAsyncAction(value*1))
        // }, 500);
    };
```

在action.js里返回一个**操作对象**，这个操作对象包含**操作类型**和**要处理的数据** ：

```javascript
/**
 * 异步函数必须依赖redux-thunk
 * @param data
 * @param time
 */
export const createIncrementAsyncAction = (data,time) => {
    console.log(data,time);
    //异步函数就是返回一个函数
    return () => {
        setTimeout(() => {
            store.dispatch(createIncrementAction(data))
        },time);

        console.log("继续执行下去了");
    }
};


export const createAddPersonAction = (data) => {
    console.log(data);
    const {username,userAge} = data;
    let userData = {id:uuid(),name:username,age:userAge};

    return {type:actionTypes.ADD_PERSON,userData};
};
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210108211525622.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
## reducer
&emsp;&emsp;操作对象和preState（之前的状态）都被传入reducer里，reducer按照操作类型更新preState，这个reducer必须是纯函数（HOC），就是不能改动preState，因为直接改动preState并不会让store更新状态，store是按照state的地址来判断是否更新，直接更新state并不会改变他的地址，store就不会认为它更新了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210108211806475.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
reducer处理完就返回新的数据到store当中

## store
&emsp;&emsp;现在从最复杂的情况说起，就是目前有两个reducer，两个reducer分别给不同的组件维护数据，两个reducer返回的数据都放在一个store里，两个reducer对应的组件都有分别的action。

store接受两个reducer，然后把它们结合起来，合成一个大的对象放在store里：

```javascript
import { createStore ,applyMiddleware,combineReducers} from 'redux'
import {countReducer,personReducer} from './reducers'
import thunk from "redux-thunk"; //异步函数要用的中间件


//传入的对象就是redux总状态对象
const allReducer = combineReducers({
    he:countReducer,
    rens:personReducer
})


let store = createStore(allReducer,applyMiddleware(thunk));
export default store;
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210108192737198.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
&emsp;&emsp;上面的he和rens是两个reducer的key，也是两部分组件对应的store中不同部分的数据的key，因为两个reducer当中返回的新数据就是两部分组件分别对应的store中的数据

## 组件调用
&emsp;&emsp;store再把数据返回到组件当中，组件使用store.getState()，获取store中的全部状态，如果想获取属于该组件的一部分状态可以再从中拆解。

