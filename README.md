# QA
收集技术上遇到的一些问题及解决方案
+ [webpack](webpack.md)

### 如何结束一个被占用的端口号?
+ 打开cmd命令窗口，输入命令：netstat -ano | findstr 8080，根据端口号查找对应的PID
+ 根据PID结束对应进程。输入命令taskkill -PID 2188 -F，强制关闭PID为2188的进程。

### IE中的xhr请求存在缓存，如何处理?
+ 在请求参数中添加一个时间戳参数,例如time:Date.now()
### 多内核浏览器(QQ,360)如何设置默认内核？
+ 将下面代码添加到`<head>`标签内
```html
  <meta name="renderer" content="webkit" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta http-equiv="X-UA-Compatible" content="chrome=1" />
```
### 如何终止循环,for...in,for,Array.prototype.forEach?
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
### React废弃的生命周期
+ componentWillMount
+ componentWillReceiveProps
+ componentWillUpdate


### 如何监测react-router路由变化
```javascript
    this.props.history.listen(route => {
        console.log(route)
    });
```


### react+webpack项目打包后某些图片文件找不到
图片的路径引用分为两种，一种是css中的背景引用，一种是img标签src中引用,由于打包后index.html与css文件不在同一文件加下,所以存在图片找不到的情况,解决方案有一下几种方式
+ 在webpack中使用两个file-loader并分别指定include指向两个图片文件夹,一个用于存放css中的背景引用,一个用于存放img标签src的引用.
+ img标签src中引用直接用字符串指定路径，而不是使用import等方式




