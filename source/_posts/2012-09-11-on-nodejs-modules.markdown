---
layout: post
title: "On NodeJs Modules"
date: 2012-09-11 10:18
comments: true
categories: [NodeJs, Module]
---

对于Node的初学者来说，可能对模块化方面比较模糊，网上的资料比较分散，在此总结一下。


## require 和 exports

个人感觉客户端js的最大缺点就是模块化难，原因有二：

1. JavaScript没有类的概念，虽然可以用一些方法来模拟类，但是远没有直接用`class`定义来得直接，针对这个缺点，可以用**CoffeeScript**来替代，但在下一篇文章会说说如何用JavaScript来模拟类。
2. JavaScript没有包含文件的功能，这就导致了必须自己来组织文件的顺序，从而在`index.html`里面按顺序把包含的`.js`文件一一列出。当然还有其他的方式，但是原理还是如此。使用工具的话推荐[RequireJs](https://github.com/jrburke/requirejs)以及[browserify](https://github.com/substack/node-browserify)，但使用起来依然不是那么方便。

为此，在Node里面就方便很多了，其默认将各个文件看作是各个独立的**Module**，即在一个文件里面定义的变量，函数都不为其他文件所见，下面举个简单的例子。比如在文件`add.js`如下：

``` javascript
// add.js
var file_name = 'add.js';
var add = function(a, b) { return a + b; }
```

那么在别的文件是不能访问`file_name`这个变量以及`add`这个函数的，如果要在别的文件里面使用它们，那么就必须先把它们**暴露**到这一个文件模块的外部，可以用如下的方式：

``` javascript
// add.js
var file_name = 'add.js';
var add = function(a, b) { return a + b; }

exports.file_name = file_name;
exports.add = add;
```

这样，我们就可以在别的文件使用这些变量了，在`use.js`里面使用方式如下：

``` javascript 
// use.js
var add_file = require('./add');

console.log(add_file.file_name); // output => add.js
console.log(add_file.add(3, 4)); // output => 7
```

由此可以看出，在`add.js`里面，我们把需要暴露的变量绑定到`exports`对象上面，然后真正返回出去的实际上是`exports`对象，在`use.js`里面调用`require`语句的时候，返回出来的`exports`对象被`add_file`变量接住了，所以就可以使用那些本来绑定在`exports`对象上面的变量了。


## exports 和 module.exports

既然`exports`是这样的一个对象，那么我们也可以这样进行绑定，比如`person.js`如下：

``` javascript 
// person.js
var Person = function(name, age) {
    this.name = name;
    this.age  = age;
}

Person.prototype = {
    introduce: function() {
        console.log('I am ' + this.name + '.');
        console.log('I am ' + this.age + ' years old.');
    }
}

module.exports = Person;
// exports = Person; DOES NOT WORK!
```

然后在`class.js`里面调用：

``` javascript
// class.js
var Person = require('./person');

var class = [
    new Person('Tom'  , 13),
    new Person('Jim'  , 12),
    new Person('Mary' , 12)
];

class.map(function(person) {
    person.introduce();
});

/**
 * output:
 * I am Tom. I am 13 years old.
 * I am Jim. I am 12 years old.
 * I am Han meimei. I am 13 years old.
 */
```

可以看出，这个时候把`Person`作为整个模块的输出，那么`exports`和`module.exports`有什么区别呢？**实际上，`exports`只是`module.exports`的一个helper，`exports`的作用在于收集需要暴露的变量，并将其包装为一个对象交给`module.exports`进行输出，所以`exports = Person`没有任何效果，`Person`没有绑定到`exports`。**既然这样，写的时候就必须注意了，因为`exports`最后会交给`module.exports`进行输出，所以如果这两者同时存在，绑定到`exports`的变量会被`module.exports`的值所覆盖，即：

``` javascript
module.exports = Person;
exports.something = 9; // `something` is blocked.
```


## 模块化组织

明白了上面所说的以后，进行模块化组织就很方便了，看看如下的文件结构：

    └─┬─ lib
      │   ├── add.js
      │   ├── sub.js
      │   └── math.js
      └─ use.js

个文件如下：

``` javascript
// add.js
var add = function(a, b) {
    return a + b;
}
module.exports = add;

// sub.js
var sub = function(a, b) {
    return a - b;
}
module.exports = add;

// math.js
module.exports = {
    add: require('./add'),
    sub: require('./sub'),
}

// use.js
var math = require('./lib/math');

console.log(math.add(3, 4)); // output =>  7
console.log(math.sub(3, 4)); // output => -1 
```
