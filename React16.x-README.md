# react #
### super
 继承父类，并且this指向子组件本身
 相当于 A.prototype.constructor.call(this, props)

### 单向数据流模式
 不可以在子组件里改变父组件的值，
 如需改变父组件的值，必须通过调用父组件传过来的方法，进行改变
 父组件调用很多次子组件的话，会影响其他组件的值，容易造成冲突。
 优点：较少耦合

### 函数式编程的优点
- 每一个函数代表一个功能或者代表区块渲染。比较清晰，直观
- 对代码的测试有极大的方便，更容易实现前端自动化测试

### setState 是一个异步的方法
*  setState是虚拟DOM操作
*  在React16里面 this.setState有一个回调函数，通过回调函数进行状态改变后的值的获取
  ```js
    this.setState({
        lists:[...this.state.lists,this.input.value]
    },()=>{
        console.log(this.lists.length)
    })
  ```
*  也可以通过async await的方式去获取state变化后的值
  ```js
    add=async()=>{
        await this.setState({
            lists:[...this.state.lists,this.input.value]
        })
        console.log(this.state.lists)
    }
  ```

### 调试工具/插件plugin
- simple react
- React Developer Tools

### 定义传入参数属性
```js
    import PropTypes from 'prop-types'
    A.propTypes={   //注意：这里的propTypes的首字母是小写
        other:PropTypes.string.isRequired,//必传
        item:PropTypes.string,
        index:PropTypes.number
    }
    //假如没有传必传参数 ，那么需要定义默认参数的值
    A.defaultProps={
        other:"李进"
    }
```

### ref 获取真实DOM
```js
    render(
        <input
            onChange={this.changeHandle.bind(this)}
            ref={input=>{this.input=input}}
        />
    )
    changeHandle(e){ //通过ref绑定里此节点，e可传可不传
        console.log(this.input.value) //此时获取的是DOM的值
        console.log(e.target.value) //此时是获取事件的值
    }
```

### 生命周期
- shouldComponentUpdate 
    * 可以解决性能问题，子组件的性能优化，
    ```js
    //接收两个参数，nextPorps,nextStatus
    shouldComponentUpdate(nextProps,nextStatus){
        if(nextProps.item !== this.props.item){//传递过来的与原来的不一样，返回true
            return true //有变化渲染
        }else{
            return false //没变化不渲染
        }
    }
    ```

### axios
 尽量写在 componentDidMount(){} 函数里面


### 动画库
 - npm i -S react-transition-group
 - 自行查看api
    1. CSSTransition
    2. TransitionGroup


### react-router-dom

- npm i react-router-dom
    1. 引入
    ```js
    import {BrowserRouter as Router, Route, Link, Redirect } from 'react-router-dom'

    ```
    2. 使用
    ```js
    /**
    * BrowserRouter 浏览器路由 as 重命名（相当于alias） Router
    * Route 路由组件
    * Link 跳转   
    * Redirect 直接使用功能比较局限 通常使用函数式重定向 this.props.history.replace('/home') like this,如果使用push的方式，会有返回
    */
    import Home from './pages/Home'
    import Mine from './pages/Mine'
    ...
    render(){
        return(
          <Router>
            <Link to="/">首页</Link>
            <Link to="/mine/">我的</Link>
            <Route path="/" exact component={Home} />
            <Route path="/mine/" component={Mine} />
          </Router>  
        )
    }
    ```
    ### 坑
    ```js
    <Route></Route>//中间一定不能有空格，否则会警告，并且不能正确渲染
    ```

    3. exact 精准匹配
    如果不指定，只要符合path规则，则会渲染 即 有 / 就被渲染

- 路由传参
    步骤：设置规则，传递值，接收值，显示内容

- 路由嵌套
  注意大小写问题