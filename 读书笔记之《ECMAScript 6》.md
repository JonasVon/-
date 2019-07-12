## 一、两个关键字 let 和 const

### （一）let 关键字

#### 1. 基本用法

​	`ES6` 新增了 `let` 关键字，用于声明变量。它的用法类似于 `var`，但是所声明的变量，只在 `let` 命令所在的代码块内有效，这是 `let` 与 `var` 最根本的区别。示例：

```js
{
    let a = 10;
    var b = 1;
}

a //在声明的代码块外访问a,报错
b //1
```

`for` 循环的计算器就非常实用使用 `let` 命令：

```js
for(let i = 0;i < 10;i++){
    //...
}
console.log(i);//报错
```

这是很显然的结果了，如果改为 `var` ，上面的结果就是10。其实我们更应该倾向于前者的结果，因为变量 i 只是作为循环的计数器，在循环外一般都不会使用，所以在外面无法访问时一种合乎逻辑的现象！但是，如果使用了 `var` 声明，那么就相当于多了一个全局变量 i ，固然在外面也能访问了，这就污染了全局环境了。

上面只是一种优势，再来看一个示例：

```js
let a = [];
for(var i = 0;i < 10;i++){
    a[i] = function(){
        console.log(i);
    }
}
a[6]();//输出的结果是：10 为何不是6呢？
```

上面的代码中，变量 i 是 `var` 声明的，在全局作用域内有效，所以全局只有一个变量 i。每次循环变量 i 的值都会发生改变，而循环内被赋给数组 a 的函数内部的 i 指向的就是全局的 i 。也就是说，所有数组 a 的成员里面的i，指向的都是同一个 i ，导致在运行时输出的是最后一轮的 i 的值。如果使用 `let` 声明 i ，那么输出的结果为 6。

```js
let a = [];
for(let i = 0;i < 10;i++){
    a[i] = function(){
        console.log(i);
    }
}
a[6]();//输出的结果是：6
```

上面的代码中，变量 i 是 `let` 声明的，当前的 i 只在本轮循环有效，也就是说，每次循环的 i 是一个新的变量。

#### 2. let 不存在变量提升现象

​	`let` 声明的变量不会存在变量提升现象，这也是 `let` 与 `var` 不同的一点。其实，按照正常的编辑习惯以及逻辑，变量应该在声明语句之后才使用，这也无形的规范了开发者的编码风格与方式。示例：

```js 
console.log(a);//输出 undefined，注意，此处并不会报错
var a = 1;

console.log(b);//报错，b is not defined
let b = 2;
```

#### 3. 临时死区

在一个块级作用域中，如果同时存在 `let` 声明的变量 a ，和外部（上一级作用域或全局作用域）的变量 a 同名，则在 `let` 声明之前，变量 a 是没有存在的意义的，这个区域称为临时死区。示例：

```js 
var a = 1;//哪怕此处改为let，也是同样的结果
if(true){
    a = 2;//报错，a is not defined  此处就是临时死区
    let a;
}
```

#### 4. 顶层对象的属性

这是很容易被忽略的一个点，在全局环境中，如果使用关键字 `var` 或者不使用任何关键字直接定义一个变量，那么这个变量其实会作为全局对象的属性；然而，如果使用 `let` 定义的变量，则不会出现该现象。示例：

```js
var a = 1;
window.a //1

let b = 1;
window.b //undefined
```

### （二）const 关键字

​	书上是这么来介绍 `const` 的 —— “用于声明一个只读常量”，好像有点对，也好像有点什么不妥。所以我说说自己的理解吧。我认为，`const` 是用于声明一个保存指定某个指针（栈内存保存某个堆内存的引用地址值）的变量。这么来解读这句话：

- 因为指针不能改变，所以**必须在初始化变量的时候就同时赋值，声明和赋值不能分开。**
- 一旦初始化，变量保存的值不能修改。

注意误区：

`const` 定义的变量保存的值不能改变，而不是这个变量引用的某个堆内存中的对象不能改变！！

`const` 不一定用于定义常量，也可以保存一些能预测未来不会改变的数据，比如从服务器端获取的数据，因为这往往是一个对象或数组，并且不会让这个变量去引用其他地址。

另外，`const` 跟 `let` 类似的有块级作用域。

---

## 二、解构赋值

​	`ES6` 允许按照一定模式，从可迭代对象（例如对象、数组、字符串或集合）中提取值，对变量进行赋值，这被称为解构赋值。如果被解构的数据不是可迭代对象，那么会报错！！

### （一）对象的解构赋值

​	**对象的解构赋值，就是从一个已知对象中取出某些特定的值，然后将这些值分别赋给某些对应的变量。**示例：

```js
//已知有这么个对象
let obj = {name:"jonas",age:18}
//对这个对象进行解构赋值
let {name,age} = obj //结果就是变量name保存了字符串jonas，变量age保存了数值18
//还可以使用默认值
let {name="jonas",age} = obj //默认值表示如果对象中没有这个属性，则使用默认值；否则使用对象中的值
//可以将静态对象的方法赋值给变量，比如，将Math中的三角函数方法赋值给三个变量
let {sin,cos,tan} = Math

```

总结：

- **对象的解构赋值是根据对象的属性名去匹配的，也就是说，变量名必须与对象中的某个属性名进行匹配，否则返回 `undefined` 。**
- 对象的解构赋值可以使用默认值，一旦对象中不存在对应的属性，则使用默认值；否则使用对象中的值。

### （二）数组的解构赋值

​	数组的解构赋值与对象的解构赋值不同的是，数组是通过索引（位置）来赋值的。示例：

```js
let [a,b,c] = [1,2,3]
```

注意：左侧包含 `a,b,c` 三个变量的不是数组，只是声明了三个变量而已，然后按照对应的位置将数组中的值赋值过去。其他使用跟对象一致，都可以指定默认值。

### （三）字符串的解构赋值

​	字符串被认为是一个字符数组，所以本质上还是数组。不同的是，解构一个字符串会将每一个字符提取出来，然后赋值给变量。

---

## 三、字符串的扩展

### （一）字符串的遍历器接口

​	`ES6` 为字符串添加了遍历器接口，使得字符串可以被遍历。示例：

```js
for(let str of "jonas"){
    console.log(str);
}
```

### （二）字符串新增的方法

- `includes(str)` —— 字符串是否包含子字符串 `str` ，返回布尔值。
- `startsWith(str)` —— 字符串是否以 `str` 开头，返回布尔值。
- `endsWith(str)` —— 字符串是否以 `str` 结尾，返回布尔值。
- `repeat(int)` —— 重复生成字符串 `int` 次，返回一个新的字符串。
- `trimStart()` —— 清空字符串头部空格。
- `trimEnd()` —— 清空字符串尾部空格。
- `matchAll()` —— 返回一个正则表达式在当前字符串的所有匹配。

---

## 四、数值的扩展

### （一）检测方法

​	`ES6` 在 `Number` 对象上，提供了 `Number.isFinite()` 和 `Number.isNaN()` 两个方法分别用于检测数值是否有限和数值是否为 `NaN`。

- `Number.isFinite(num)` —— 检测数值 `num` 是否有限，返回布尔值。当数值为 `Infinity` 或其他数据类型时，返回 `false`。
- `Number.isNaN(num)` —— 检测数值 `num` 是否为 `NaN` ，返回布尔值。
- `Number.isInteger(num)` —— 检测数值 `num` 是否为整数，返回布尔值。注意：5 跟 5.0 都被视为整数。

### （二）提取数值方法

​	`ES6` 将两个全局方法 `parseInt()` 和 `parseFloat()` 移植到 `Numer` 对象上，用于提取字符串中的整型数值和浮点型数据。注意：只有以数值开头的字符串才能够被提取，一旦出现其他非数字的字符，则会被中断并返回结果。

- `Number.parseInt(str)` —— 提取整型数值
- `Number.parseFloat(str)` —— 提取浮点型数值

### （三）Math 对象的扩展

​	`ES6` 在 `Math` 对象上扩展了 17 个静态方法，部分方法如下：

- `Math.trunc(num)` —— 去除数值 `num` 的小数部分，返回整数部分；对于非数值而言，会将非数值转换为数值，再提取整数部分返回；对于空值或无法截取整数的值，返回 `NaN` 。
- `Math.sign(num)` —— 判断 `num` 是正数，负数，还是零。对于非数值，先做类型转换。 
  - 参数为整数，返回 `+1`
  - 参数为负数，返回 `-1`
  - 参数为 0，返回 0
  - 参数为 -0 ，返回 -0
  - 其他值，返回 `NaN`

- `Math.cbrt(num)` —— 计算一个数的立方根；非数值会做类型转换，不合法值返回 `NaN`

---

## 五、对象的扩展

### （一）简写属性

​	如果对象的属性名和属性值一致，则可以省略属性值。比如：

```js
let name = "jonas"
let obj = {name};//等价于 let obj = {name:name}
```

对于函数，同样适用：

```js
let foo = function(){
    console.log("hello js");
}
let obj = {foo};
```

除此以外，在一个对象中定义一个函数还可以这么来写：

```js
let obj = {
    foo(){ //省略了function关键字，省略了属性名
        console.log("hello js");
    }
}
```

### （二）对象的描述器

​	对象的每个属性都有一个描述对象 `Descriptor`，用来控制该属性的行为。通过 `Object.getOwnPropertyDescriptor(obj,propertyName)` 可以获取该属性的描述对象。示例：

```js
let obj = {name:"jonas"}
console.log(Object.getOwnPropertyDescriptor(obj,"name"))
```

输出结果：

configurable: true

enumerable: true

value: "jonas"

writable: true

描述对象的 `enumerable` 属性，称为 可枚举性，如果该属性为 `false` ，就表示以下操作会忽略当前属性：

- `for...in` 循环：只遍历对象自身的和继承的可枚举的属性
- `Object.keys()` ：返回对象自身的所有可枚举属性名
- `JSON.stringfly()` ：只处理可枚举属性
- `Object.assign()` ：只拷贝对象自身的可枚举属性

`value` 属性表示该属性对应的值。

`writeable` 属性表示该属性是否可写。

`configurable` 属性表示该属性是否可配置。

### （三）遍历对象中的属性

#### 1. `for...in` 

`for...in` 循环遍历对象自身和继承的可枚举属性。

#### 2. `Object.keys(obj)`

`Object.keys(obj)` 返回一个数组，包含对象自身的（不含继承）所有可枚举属性名。

#### 3. `Object.getOwnPropertyNames(obj)`

`Object.getOwnPropertyNames(obj)` 返回一个数组，包含对象自身的所有属性。

#### 4. `Reflect.ownKeys(obj)`

`Reflect.ownKeys(obj)` 返回一个数组，包含对象自身的所有键名。

### （四）对象新增的方法

- `Object.is(obj1,obj2)` —— 用于判断两个对象是否相等，与全等运算符基本一致。
- `Object.assign(target,source1,source2)` —— 用于对象的合并，将源对象 `source` 的所有可枚举属性，复制到目标对象 `target` 上，注意：该方法为浅拷贝。（补充：如果需要深拷贝，则可以考虑 `JSON` 两次转换）

---

## 六、数组的扩展

- `Array.from(obj)` —— 用于将可迭代对象 `obj` 转换为数组，常用于转换类数组。
- `Array.of(...args)` —— 用于将一组值转换为一个数组
- `Array.prototype.includes(obj)` —— 数组的实例方法，检测数组中是否包含 `obj` ，返回布尔值。

---

## 七、**`Promise` （重要）

### （一）概述

​	`Promise` 是异步编程的一种解决方案。所谓 `promise` ，从语法上看是一个对象，里面保存着未来某个时候才会结束的事件的结果。`promise` 对象又以下两个特点：

- **对象的状态不受外界影响。**`promise` 对象代表一个异步操作，有三种状态：`pending`、`fulfilled` 和 `rejected` 。只有异步操作的结果才可以决定当前是具体哪种状态，任何其他操作都无法改变这个状态。这也是它被称为 `promise` 的原因。

- **状态一旦改变，就不会再变，任何时候都可以得到这个结果。**`promise` 对象的状态改变只有两种可能：

  - 从 `pending` 变成 `fulfilled`
  - 从 `pending` 变成 `rejected`

  一旦以上任一种情况发生了，状态就凝固了，不会再改变，会一直保持这个结果，这时就称为 `resolved` 。

### （二）基本使用

​	`ES6` 规定， `Promise` 对象是一个构造函数，用来生成 `promise` 实例。示例：

```js
const promise = new Promise(function(resolve,reject){
    //一般是发送异步请求
    if(/*异步操作成功*/){
       resolve();
	}else{//异步操作失败
       reject();
    }
});
```

`Promise` 构造函数接受一个函数作为参数，该函数的两个参数分别是 `resolve` 和 `reject` 。它们是两个函数，由解释引擎提供，不用自己部署。

`resolve()` 的作用是，将 `Promise` 对象的状态从 `pending` 变成 `resolved` ，在异步操作成功时调用，并将异步操作的结果作为参数传递出去。

`reject()` 的作用是，将 `Promise` 对象的状态从 `pending` 变成 `rejected` ，在异步操作失败时调用，并将异步操作报出的错误作为参数传递出去。

`promise` 实例生成后，可以通过 `then()` 分别指定 `resolved` 状态和 `rejected` 状态的回调函数。示例：

```js
promise.then(function(response){
    //success
},function(error){
    //error
});
```

`then()` 可以接受两个回调函数作为参数。第一个回调函数是 `promise` 对象的状态变成 `resolved` 时调用，第二个回调函数是 `promise` 对象的状态变成 `rejected` 时调用。第二个参数非必须。

### （三）`Promise.prototype.then()`

​	`Promise` 实例具有 `then()` ，也就是说，`then()` 是定义在原型对象上的。它的作用是为了 `Promise` 实例添加状态改变时的回调函数。上面提到过，`then()`第一个参数是 `resolved` 状态的回调函数，第二个参数是 `rejected` 状态的回调函数。

​	`then()` 返回的是一个新的 `promise` 实例，因此可以采用链式写法。采用链式的 `then`，可以指定一组按照次序调用的回调函数。

### （四）`Promise.prototype.catch()`

​	`Promise.prototype.catch()` 是 `Promise.prototype.then(null,rejection)` 或 `Promise.prototype.then(undefined,rejection)` 的别名，用于指定发生错误时的回调函数。示例：

```js
promise.then(function(response){
    //success
}).catch(error){
    //error
}
```

### （五）`Promise.prototype.finally()`

​	不管 `Promise` 对象最后状态如何，都会执行的操作。示例：

```js
promise.then(function(response){
    //success
}).catch(error){
    //error
}.finall(){
    
}
```

---

## 八、遍历器 Iterator

### （一）`Iterator` 的概念

​	遍历器是一种机制，一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 `Iterator` 接口，就可以完成遍历操作。它的作用主要体现为以下三个方面：

- 为各种数据结构提供一个统一的、简便的访问接口
- 使得数据结构的成员能够按某种次序排列
- 为 `for...of` 循环消费

`Iterator` 的遍历过程是这样的：

1. 创建一个指针对象，指向当前数据结构的起始位置。也就说，遍历器对象本质上就是一个指针对象。
2. 第一次调用指针对象的 `next()`，可以将指针指向数据结构的第一个成员。
3. 第二次调用指针对象的 `next()`，指针就指向数据结构的第二个成员。
4. 不断地调用 `next()`，直到它指向数据结构的结束位置。

每次调用 `next()` ，都会返回数据结构的当前成员的信息。具体的说，就是返回一个包含 `value` 和 `done` 两个属性的对象。其中，`value` 属性表示当前成员的值，`done` 属性是一个布尔值，表示遍历是否结束。

### （二）默认的 `Iterator` 接口

​	上面说到 `Iterator` 接口的作用之一就是提供了一种统一的访问机制，即 `for...of` 循环。当使用 `for...of` 循环遍历某种数据结构时，该循环会自动去寻找 `Iterator` 接口。

​	`ES6` 规定，默认的 `Iterator` 接口部署在数据结构的 `Symbol.iterator` 属性，也就是说，一个数据结构只要具有 `Symbol.iterator` 属性，就可以认为是可遍历的。`Symbol.iterator` 属性本身是一个函数，就是当前数据结构默认的遍历器生成函数。执行这个函数，就会返回一个遍历器。原生具备 `Iterator` 接口的数据结构如下：

- `Array`
- `Map` （`ES6` 新增的一种结构）
- `Set` （`ES6` 新增的一种结构）
- `String`
- `TypeArray`
- 函数中的 `arguments` 对象
- `NodeList` 对象

示例：

```js
let arr = [1,2,3,4,5]
let iter = arr[Symbol.iterator]();//注意：Symbol.iterator是一个变量，必须通过方括号的方式取，不能通过点属性名的方式！
iter.next() //{value:1,done:false}
iter.next() //{value:2,done:false}
```

​	对象（指普通的对象 `Object`）之所以没有默认部署 `Iterator` 接口，是因为对象中的属性是没有顺序的。本质上，遍历器是一种线性处理，对于任何非线性的数据结构，部署遍历器接口就等于部署一种线性转换。不过，`ES6` 提供了一种键值对的数据结构 `Map` 就部署了。

### （三）使用遍历器的场合

​	有些场合会默认调用 `Iterator` 接口（即`Symbol.iterator` 方法）：

- 对数组和 `Set` 解构赋值，会默认调用 `Symbol.iterator`
- 扩展运算符
- `for...of` 循环

---

## 九、Generator 函数

​	`Generator` 函数是 `ES6` 提供的一种异步编程解决方案，本质上是函数，但语法行为与普通的函数却完全不同。可以将 `Generator` 函数理解为一个状态机，封装了多个内部状态。**执行 `Generator` 函数会返回一个遍历器对象。**形式上，`Generator` 函数是一个普通的函数，但有两个特征：**① `function` 关键字与函数名之间有一个星号；② 函数体内部使用 `yield` 表达式，定义不同的内部状态。**示例：

```js
function* helloWorldGenerator(){
    yield "hello";
    yield "world";
    return "ending"
}
let hw = helloWorldGenerator();
```

上面的这段代码定义了一个 `Generator` 函数，它的内部有两个 `yield` 表达式，即该函数有三个状态：`hello、world、return` 。从上面可以看出，`Generator` 函数的调用方法与普通函数一样，也是在函数名后面加上一对圆括号。不同的是，**调用 `Generator` 函数后，函数体代码不会立马执行，返回的也不是函数运行的结果，而是一个指向内部状态的指针对象，也就是一个遍历器对象。**如果需要获取函数的状态，必须调用遍历器的 `next()`，使得指针移向下一个状态。也就是说，每次调用 `next()`，内部指针就从函数头部或上一次停下来的地方开始执行，直到遇到下一个 `yield` 表达式或 `return` 语句。换言之，`Generator` 函数是分段执行的，`yield` 表达式是暂停执行的标记，而 `next()` 可以恢复执行。 

---

## 十、`Proxy`

### （一）概述

​	`Proxy` 用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种元程序，即对编程语言进行编程。`Proxy` 可以理解为一个 “拦截器” ，外界对该对象的访问之前都必须经过这个拦截器，因此提供了一种机制，可以对外界的访问进行过滤和改写。示例：

```js	
var obj = new Proxy({}, {
  get: function (target, key, receiver) {
    console.log(`getting ${key}!`);
    return Reflect.get(target, key, receiver);
  },
  set: function (target, key, value, receiver) {
    console.log(`setting ${key}!`);
    return Reflect.set(target, key, value, receiver);
  }
});
```

上面这段代码对一个空对象进行了拦截，重新定义了属性的读取（`get`）和设置（`set`）行为。对设置了拦截行为的对象 `obj` 进行读写操作，结果如下：

```js
obj.count = 1
//  setting count!
++obj.count
//  getting count!
//  setting count!
//  2
```

这里说明，`Proxy` 实际上重载了点运算符，即用自己的定义覆盖了语言的原始定义。

`ES6` 原生提供 `Proxy` 构造函数，用来生成 `proxy` 实例：

```js
let proxy = new Proxy(target,handler);
```

`Proxy` 对象的所有用法，都是上面这种形式，不同的是 `handler` 参数的写法。其中，`new Proxy()` 表示生成一个 `proxy` 实例，`target` 参数表示所要拦截的目标对象，`handler` 参数也是一个对象，用来定制拦截行为。下面是另一个拦截读取属性行为的例子：

```js
var proxy = new Proxy({}, {
  get: function(target, property) {
    return 35;
  }
});

proxy.time // 35
proxy.name // 35
proxy.title // 35
```

上面代码中，作为构造函数，`Proxy`接受两个参数。第一个参数是所要代理的目标对象；第二个参数是一个配置对象，对于每个被代理的操作，需要提供一个对应的处理函数，该函数将拦截对应的操作。比如，上面代码中，配置对象提供了一个 `get` 方法，用来拦截对目标对象属性的访问请求。`get` 方法的两个参数分别是目标对象和所要访问的属性，可以发现，由于拦截函数总是返回35，所以访问任何属性都得到35。

### （二）配置对象

下面是 `Proxy` 支持的拦截操作：

- `get(target,propKey,receiver)`：拦截对象属性的读取，比如，`obj.a` 或 `obj[a]`
- `set(target,propKey,value,receiver)`：拦截对象属性的设置，比如，`obj.a = 'a'` 或 `obj[a] = 'a'`
- `has(target, propKey)`：拦截 `propKey in proxy` 的操作，返回一个布尔值。
- `deleteProperty(target, propKey)`：拦截 `delete proxy[propKey]` 的操作，返回一个布尔值。
- `ownKeys(target)`：拦截 `Object.getOwnPropertyNames(proxy)`、`Object.getOwnPropertySymbols(proxy)`、`Object.keys(proxy)`、`for...in` 循环，返回一个数组。该方法返回目标对象所有自身的属性的属性名，而 `Object.keys()` 的返回结果仅包括目标对象自身的可遍历属性。
- `getOwnPropertyDescriptor(target, propKey)`：拦截 `Object.getOwnPropertyDescriptor(proxy, propKey)`，返回属性的描述对象。
- `defineProperty(target, propKey, propDesc)`：拦截 `Object.defineProperty(proxy, propKey, propDesc）`、`Object.defineProperties(proxy, propDescs)`，返回一个布尔值。