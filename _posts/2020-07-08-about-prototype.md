---
layout: post
title: "关于原型链"
author: yang
categories: [js]
tags: [featured]
---

​		js是一门面向对象的语言，js的所有事物都是对象，数值、字符串、数组、函数等，可以自定义对象，但是早期的时候没有向其他语言一样使用class来定义，是通过prototype原型对象来实现的。之后ES6语言提供了class来定义类，这就相当于语法糖，但是没有prototype灵活。所以现在这个阶段prototype还是很有用的。

## prototype

​		javascript中，每个函数都有一个prototype属性，这个属性指向函数的原型对象。

例如：

```js
function Person(name,age){
    this.name = name;
    this.age = age;
}
var person = new Person();
```



​		每一个javascript对象创建的时候，就会与之关联另一个对象，这个对象就是原型，每一个对象从原型中继承属性，当然这个继承不是真正的继承。

构造函数和示例原型之间的关系可如下图所示：

![img](https://img2018.cnblogs.com/blog/850375/201907/850375-20190708151024134-512558007.png)

## \__proto__

​		每个对象都会有这个属性，叫做\__proto__，这个属性会指向该对象的原型。

![img](https://img2018.cnblogs.com/blog/850375/201907/850375-20190708151322530-1608157973.png)

## constructor

​		每个原型都有一个constructor属性，指向该关联的构造函数。

![img](https://img2018.cnblogs.com/blog/850375/201907/850375-20190708151615691-1017611190.png)

## 原型链

​		每个对象都有  \_\_proto\__ 指向原型对象，原型对象也是对象，也有 \__proto__，直到最上层的object，object.prototype.\_\_proto\_\_为null。

![img](https://img2018.cnblogs.com/blog/850375/201907/850375-20190708153139577-2105652554.png)

## 实例和原型

​		当读取实例的属性时，如果找不到就会查找与对象相关联的原型中的属性，如果还查不到，就去找原型的原型，一直找到最顶层为止。

```js
function Animal(name,age){
    this.name = name;
    this.age = age;
}
Animal.prototype.sex = '女';
var animal = new Animal();
animal.sex = '男'
console.log(animal.sex);//男
delete animal.sex;
console.log(animal.sex);//女

```

​		当执行animal.sex时，会先去animal查找sex属性，这时刚好sex属性为“男”；当删除animal的sex属性时，执行animal.sex，但是animal没有sex属性，这是就会去animal.\__proto__中去找，刚好Animal.prototype中存在sex属性，所以输出。

## 总结

​		\__proto__是原型链查询中实际用到的，它总是指向prototype。

​		prototype是函数独有的，在定义构造函数的自动创建，所有的对象都有\__proto__属性，函数这个特殊对象除了具有\_\_proto\_\_属性,还有一个特有的原型属性prototype。prototype对象有两个默认的属性，constructor属性和\_\_proto\_\_属性。

​		prototype属性可以给函数和对象添加可共享的方法、属性。

​		\_\_proto__是查找某函数或对象的原型链方式。