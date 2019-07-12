## 一、灵活的语言 —— JavaScript

### （一）需求

​	书中通过引入一个常见的需求：验证表单功能来介绍 `js` 。具体：验证用户名、邮箱、密码。

然后小白就很兴奋的写了三个函数：

```js
function checkName(){
    //验证姓名
}
function checkEmail(){
    //验证邮箱
}
function checkPassword(){
    //验证密码
}
```

从功能上看着貌似没啥不妥，通过调用三个函数去验证表单而已。但是，这样的定义污染了全局环境，然而，小白通过同事的提示将三个函数收编在一个对象中：

```js
let checkObject = {
    checkName(){
        //验证姓名
    },
    checkEmail(){
        //验证邮箱
    },
    checkPassword(){
        //验证密码
    }
}
```

这样一来，在全局中只定义了一个变量，然后通过对象来调用方法就能实现功能了，比如：`checkObject.checkName()`。

但是，问题又来了，如果需要验证多个表单项，那么就得写多个上面这样的表达式；而且，上面这种方式并不符合面向对象编程。

### （二）解决方案

```js
function CheckObject(){}
CheckObject.prototype.checkName = function(){
    return this;
}
CheckObject.prototype.checkEmail = function(){
    return this;
}
CheckObject.prototype.checkPassword = function(){
    return this;
}
```

通过上面这种方式就可以链式调用，并且符合面向对象风格。

```js
let check = new CheckObject();
check.checkName().checkEmail().checkPassword();//一行代码解决
```

---

## 二、创建型设计模式

### （一）简单工厂模式

