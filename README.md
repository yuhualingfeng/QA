# QA
收集技术上遇到的一些问题及解决方案

+ [webpack](webpack.md)
## 问题分类
+ 代码级别。例如拼写错误，变量使用错误等，这种问题可以通过逐步调试解决。
+ 功能实现级别。
    + 功能交互复杂可以通过功能拆解，通用功能封装来处理。
    + 存在技术难点可以通过自我思考，网络求助，借助开源库或工具。

*********
## 对于生成器函数的理解
## react-redux封装了哪些常用的方法？
+ connect()
+ Provider 组件

*********

## React的生命周期函数
1. 挂载
    + constructor()
    + static getDerivedStateFromProps()
    + render()
    + componentDidMount()
2. 更新
    + static getDerivedStateFromProps()
    + shouldComponentUpdate()
    + render()
    + getSnapShotBeforeUpdate()
    + componentDidUpdate()
3. 卸载
    + componentWillUnmount()
4. 错误处理
    + static getDerivedStateFromError()
    + componentDidCatch()

*********



## 常常提到的副作用Effect具体指的什么?
+ 发送网络请求，手动变更 DOM，记录日志,访问浏览器缓存
+ 事件订阅(需要清除的 effect,防止引起内存泄露)

*********
## Redux Toolkit封装了哪些常用方法？
+ configureStore
+ 
## 为什么使用Redux Toolkit ?
+ Redux Toolkit 封装一些方法，让我们更加方便和正确的开发Redux App
+ Redux Toolkit内置了immer,redux-thunk

*********

## 为什么使用immer ?
+ 在生产不可变数据时,避免了过多的使用扩展运算符`...`或者deepCopy.
+ 在生产不可变数据时,提升了性能和减少了不必要的渲染.

*********
## redux-saga封装了哪些常用方法 ?


## redux-saga用途
+ redux saga是一个库，旨在使应用程序的副作用（即数据获取之类的异步事情和访问浏览器缓存之类的不纯事情）更易于管理、更高效地执行、更易于测试，并更好地处理故障。

*********

## redux-thunk用途
+ 通过dispatch function的形式来处理副作用，例如网络请求.

*********

## 常用的Hooks
+ useState
+ useEffect
+ useContext
+ useMemo
+ useCallback
+ useRef

## Hooks的优点
1. 在不编写 class 的情况下使用 state 以及其他的 React 特性
2. 用更简洁的代码实现class相同的功能
3. 更方便的实现代码重用
4. 更纯粹，不再需要在classes,function,hight-order components之间来回切换.

*********

## 对于React.memo的使用与理解
React.memo是一种性能优化的手段,它将对组件的props做前后对比,如果没有发生变化则不会重复渲染.

*********

## 使用flex布局时文字超长影响布局如何处理？
例如子元素的样式为`flex:1;`,只需要加一个`width:0;`既可修复
```css
    .ele{
        flex:1;
        width:0;
    }
```

*********

## React Router如何在不重载页面的情况下刷新当前路由？
先跳转到一个空白页面，然后在空白页面获取需要跳转的路由并执行跳转。
```javascript
import { getQueryString } from '@/common/utils';
import { useEffect } from 'react';
export default function Blank (props){
    useEffect(()=>{
        setTimeout(()=>{
            const path =getQueryString(props.location.search,'path',true);
            props.history.push(decodeURIComponent(path));            
        },200);  
    },[]);

    return (<></>);
}
```

*********

## React Router如何为路由组件传入数据？
平时的写法为：
```html
    <Route exact path='/index' component={Index}></Route>
```
将组件作为children放入即可实现数据传递给组件
```html
    <Route exact path='/index'>
        <Index vin={vin}></Index>
    </Route>
```

*********

## 如何做到webpack打包后配置文件依然可以配置?
*********

## 汉字实体的宽度表示
+ &#12288; 表示一个汉字的宽度
+ &emsp;   表示半个汉字的宽度

*********

## 如何结束一个被占用的端口号?
+ 打开cmd命令窗口，输入命令：netstat -ano | findstr 8080，根据端口号查找对应的PID
+ 根据PID结束对应进程。输入命令taskkill -PID 2188 -F，强制关闭PID为2188的进程。

*********

## IE中的xhr请求存在缓存，如何处理?
+ 在请求参数中添加一个时间戳参数,例如time:Date.now()

*********

## 多内核浏览器(QQ,360)如何设置默认内核？
+ 将下面代码添加到`<head>`标签内
```html
  <meta name="renderer" content="webkit" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta http-equiv="X-UA-Compatible" content="chrome=1" />
```

*********

## 如何终止循环,for...in,for,Array.prototype.forEach?
+ `for,for..in,switch`终止或跳过使用`break,continue`
+ Array.prototype.forEach可以通过抛出异常来终止循环
```javascript
    let arr = [1,2,3,4];
    try{
        arr.forEach((item)=>{
            console.log(item); 
            if(item==2){
                throw new Error('break');
            }
        });    
    }catch(error){

    }
    console.log('end');
```

*********

## React废弃的生命周期
+ componentWillMount
+ componentWillReceiveProps
+ componentWillUpdate

*********

## 如何监测react-router路由变化
```javascript
    this.props.history.listen(route => {
        console.log(route)
    });
```

*********

## react+webpack项目打包后某些图片文件找不到
图片的路径引用分为两种，一种是css中的背景引用，一种是img标签src中引用,由于打包后index.html与css文件不在同一文件加下,所以存在图片找不到的情况,解决方案有一下几种方式
+ 在webpack中使用两个file-loader并分别指定include指向两个图片文件夹,一个用于存放css中的背景引用,一个用于存放img标签src的引用.
+ img标签src中引用直接用字符串指定路径，而不是使用import等方式





