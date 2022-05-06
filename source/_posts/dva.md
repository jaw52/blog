---
title: dva
tags:
- umi
- 第三方库
- 工程化
categories: 
- 前端
- umi
---
# dva

#### Model

dva 通过 `model `的概念把一个领域的模型管理起来，包含同步更新 `state `的 `reducers`，处理异步逻辑的 `effects`。

#### Reducer

`reducers` 等同于 `redux `里的 `reducer`，接收 `action`，同步更新 `state`

``` js
export default {
  namespace: 'products',
  state: [],
  reducers: {
    'delete'(state, { payload: id }) {
      //state为当前状态值，函数返回最新的状态值
      return state.filter(item => item.id !== id);
    },
  },
};
```

*   `namespace` 表示在全局 `state `上的 `key`，必须不同

*   `state` 是初始值，`Model `的状态数据，通常表现为一个 javascript 对象

#### Effect

Effect在我们的应用中，最常见的就是异步操作，`Effects` 的最终流向是通过 `Reducers` 改变 `State`

``` js
export default {
  namespace: 'todos',
  effects: {
    *addRemote({ payload: todo }, { put, call, select }) {
      // 这边的 state 来源于全局的 state，select 方法提供获取全局 state 的能力，也就是说，在这边如果你有需要其他 model 的数据，则完全可以通过 state.modelName 来获取
      const todos = yield select(state => state.todos); 
      //call 用于调用异步逻辑，支持 promise 。
      yield call(addTodo, todo);
      //put 用于触发 action 。这边需要注意的是，action 所调用的 reducer 或 effects 来源于本 model 那么在 type 中不需要声明命名空间，如果需要触发其他非本 model 的方法，则需要在 type 中声明命名空间，如 yield put({ type: 'namespace/fuc', payload: xxx });
      yield put({ type: 'add', payload: todo }); 
    },
  },
};
```

#### Action

Action 是一个普通 javascript 对象，它是改变model中 `State `的唯一途径。

``` js
dispatch({
  type: 'user/add', // 如果在 model 外调用，需要添加 namespace
  payload: {}, // 需要传递的信息
});
```

`dipatch `可以看作是触发这个行为的方式，而 `Reducer `则是描述如何改变数据的

## connect

dva 提供了 `connect `方法。如果你熟悉 `redux`，这个 `connect `就是 `react-redux` 的 `connect `。

### 类组件

使用`connect`连接

#### 方式一

``` js
import React from "react";
import {Component} from 'react';
import { connect } from "dva"; //从dva中导入connect
 
class Counter extends Component {
    constructor(props){
        super(props)
    }  
    render (){
        return (
            <div>
                 <p> this.props.example.initText</p> //如这里就获取到了上面定义的initText数据了
            </div>
        )
    }
}
 
export default connect (({example})=>({example}))(Counter) //通过这种方式来把model层的数据传递到当前组件了，默认这面的也是example属性，通过this.props.example可以获取到model（example.js）中state的数据了
```

#### 方式二

``` js
import React from "react";
import {Component} from 'react';
import { connect } from "dva"; //从dva中导入connect
 
@connect(({example})=>({example}))
class Counter extends Component {
    constructor(props){
        super(props)
    }  
    render (){
        return (
            <div>
                 <p> this.props.example.initText</p> //如这里就获取到了上面定义的initText数据了
            </div>
        )
    }
}
```

### 函数式组件

``` js
import { useSelector, useDispatch，useStore } from 'umi';

const Index = () => {
  //获取dva中products全局存放的state
   const state = useSelector(state => state.products) 

  const dispatch = useDispatch()
  
  //改变dva中products全局存放的state
  const deleteHandler = async (id) => {
    
    dispatch({
      type:'products/delete',
      payload:{id}
    })
  };
  
  //略
  return <>
  
  </>
}
export default Index

```
