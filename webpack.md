### react中的图片应该如何引入?
假如我们直接在`img`标签的src属性中直接写入图片路径，webpack不会对其进行打包处理。  
正确的处理方式为：
+ 首先需要在webpack的配置文件中使用`file-loader`,`file-loader`一般用于处理图片及字体文件.
+ 在`img`标签的src中通过require来引入文件
```javascript
    <img src={require('../imgs/common/user_icon.png')}/>
```

