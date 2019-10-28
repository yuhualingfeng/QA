# QA
收集技术上遇到的一些问题及解决方案
+ [webpack](webpack.md)

### IE中的xhr请求存在缓存，如何处理?
+ 在请求参数中添加一个时间戳参数,例如time:Date.now()
### 多内核浏览器(QQ,360)如何设置默认内核？
+ 将一下代码添加到`<head>`标签内
```html
  <meta name="renderer" content="webkit" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta http-equiv="X-UA-Compatible" content="chrome=1" />
```
### 如何终止循环,for...in,for,Array.prototype.forEach?
+ `for,for..in,switch`终止或调过使用`break,continue`
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




