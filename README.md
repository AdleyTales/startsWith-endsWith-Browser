# startsWith 和 endsWith函数的兼容写法



### 前言

为什么要写这个东西，因为在实际工作中碰到了这个问题。ie11以下都没有这两个方法。所以js中用到会报错。

使用babel编译ES6+的语法，但是发现  `startsWith`  和 `endsWith` 并没有给我编译。所以只能自己写兼容了。

当然写法也是很简单，只是一个小细节值得记录下来，之前从没写过正则的变量拼接的写法。



### 介绍一下这两个字符串方法

- startsWith 字符串新增方法 判断所传的参数是否在当前这个字符串的开始位置 是返回true 不是返回false
- endsWith   判断所传的参数是否在当前这个字符串的结束位置 是返回true 不是返回false



example：

```js

var str = 'abcdef';

if(str.startsWith('abc')){
   alert(true); //满足条件  省去写正则的写法
}

```



### 兼容写法

- 这里主要注意的点是：正则可以字符串拼接 变量。

```js

if (!String.prototype.startsWith) {
    String.prototype.startsWith = function(str) {
      var reg = new RegExp('^'+str,'gim');
      return reg.test(this);
    }
  }

 
if(!String.prototype.endsWith){
  String.prototype.endsWith = function(str) {
    var reg = new RegExp(str+'$','gim');
    return reg.test(this);
  }
}

```



