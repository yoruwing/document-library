面向对象
===

> Create by **jsliang** on **2020-4-26 15:45:42**  
> Recently revised in **2020-04-27 16:31:57**

## <a name="chapter-one" id="chapter-one"></a>一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| <a name="catalog-chapter-two" id="catalog-chapter-two"></a>[二 前言](#chapter-two) |

## <a name="chapter-two" id="chapter-two"></a>二 前言

> [返回目录](#chapter-one)

面向对象（OOP）是一种思维方式

## 面向对象编程思想

* 面向过程：注重解决问题的步骤，分析问题需要的每一步，实现函数依次调用；
* 面向对象：是一种程序设计思想。将数据和处理数据的程序封装到对象中。
* 面向对象特性：抽象、封装、继承、多态。

优点：提高代码的复用性及可维护性。

说了那么多，到底啥意思呢？

举个栗子：

* **jsliang** 去附近的砂锅麻辣烫吃饭。

这就是面向对象，即：

```js
const eat = () => {
  return 'jsliang 去砂锅麻辣烫吃饭';
}
eat();
```

但是，吃饭这个动作，是个正常人都可以做的啊，所以：

```js
const eat = (people) => {
  return `${people} 去砂锅麻辣烫吃饭`;
}
eat('jsliang');
```

这时候，就开始面向对象了，即可以任何人到这家餐厅吃饭。

如果你在工作中，你可能觉得这样还不够完美：我们不一定要吃砂锅麻辣烫啊！也不一定天天吃啊！

```js
const eat = (people, address, time) => {
  return `${people} 去 ${address} 吃 ${time}`;
}
eat('jsliang', '煲仔饭', '午饭');
```

很好，这就是面向过程 -> 面向对象。

在工作中，就是当我们一件事，有很多份代码都使用到的时候，就将其抽取出来（封装）。

为什么要用 **面向对象** 呢，从上面我们可以看出了：为了程序员偷懒。

但是面试的时候你不能这么说啊，这样子你就忽悠不了几句话了，所以来个正经点回答：

* 面向过程

1. 优点：简单明了
2. 缺点：系统较大的时候使用不便，CV 工作量大

* 面向对象

* 优点：方便复用、可迭代性强
* 缺点：单个使用不够方便

## 字面量和构造函数

构造函数：用来构建某一类型的对象 - 对象的实例化

* 对象创建

```js

// 1. 字面量方式
const obj1 = {
  name: '张三',
  age: 20,
  hobby: function() {
    console.log('喜欢玩');
  },
};
console.log(obj1);

// 2. 构造函数
const obj2 = new Object();
obj2.name = '张三';
obj2.age = 20;
obj2.hobby = function() {
  console.log('喜欢玩');
};
console.log(obj2);

// 3. Object.create()
const obj3 = Object.create({
  name: '张三',
  age: 20,
  hobby() {
    console.log('喜欢玩');
  },
});
console.log(obj3);
```

* 对象调用

```js
const obj = {
  name: '张三',
  age: 20,
  hobby: function() {
    console.log('喜欢玩');
  },
};
console.log(obj.name);
console.log(obj['name']);
const str = 'name';
console.log(obj[str]);
```

## 工厂模式

```js
/**
 * @name 01-工厂模式
 * @description 2020-4-26 16:53:40
 */

// const zhangsan = {
//   name: '张三',
//   age: 20,
//   hobby() {
//     console.log('喜欢玩');
//   },
// };
// const lisi = {
//   name: '李四',
//   age: 22,
//   hobby() {
//     console.log('没有爱好');
//   },
// };
// ……王五、赵六……
// 都是同一个模子复制出来的玩意，使用工厂模式

// 工厂模式
function Person(name, age, hobby) {
  const obj = {}; // 添加原料
  obj.name = name;
  obj.age = age;
  obj.hobby = function() {
    console.log(hobby);
  };
  return obj; // 出厂
};

const person1 = new Person('张三', 20, '喜欢玩');
const person2 = new Person('李四', 21, '没有爱好');
console.log(person1);
console.log(person2);
```

## 类的概念

```js
// ES5 类
function Person1() {
  // ...
}
const people1 = new People('123');

// ES6 类
Class Person2() {
  // ...
}
const person2 = new Person('123');
```

## new 运算符

1. 执行函数
2. 自动创建一个空对象
3. 把空对象和 `this` 绑定
4. 如果没有返还，隐式返回 `this`

```js
function Test() {
  // let obj = {}; ——> this

  // ...做一些内容

  // return this
}
new Test();
```

通过这个看工厂模式：

```js
// function Person(name, age, hobby) {
//   const obj = {};
//   obj.name = name;
//   obj.age = age;
//   obj.hobby = function() {
//     console.log(hobby);
//   };
//   return obj;
// };

// 改造
function Person(name, age, hobby) {
  this.name = name;
  this.age = age;
  this.hobby = function() {
    cosnole.log(hobby);
  };
};
const person = new Person('张三', 20, '喜欢玩');
console.log(person); // Person {name: "张三", age: 20, hobby: ƒ}
```

## 构造函数

* 构造函数需要通过 `new` 来调用 `this` 指向实例化对象
* 约定俗成构造函数首字母大写
* 静态属性及方法
  * 静态方法里的 `this`
  * 扩展功能

```js
function Person(name, age, hobby) {
  this.num = 0;
  this.name = name;
  this.age = age;
  this.hobby = function() {
    cosnole.log(hobby);
  };
};

const zhangsan = new Person('张三', 20, '喜欢玩');
zhangsan.num++;
console.log(zhangsan.num); // 1

const lisi = new Person('李四', 20, '喜欢玩');
lisi.num++;
console.log(zhangsan.lisi); // 1
```

每次 `new` 都生成了一个新的对象，那么有没有属于类本身的静态属性和方法呢？

```js
function Person(name, age, hobby) {
  this.name = name;
  this.age = age;
  this.hobby = function() {
    cosnole.log(hobby);
  };
};
// 静态成员
Person.num = 0;

const zhangsan = new Person('张三', 20, '喜欢玩');
Person.num++;
console.log(Person.num); // 1

const lisi = new Person('李四', 20, '喜欢玩');
Person.num++;
console.log(Person.num); // 2
```

* 构造函数性能

```js
function Person(name, age, hobby) {
  this.name = name;
  this.age = age;
  this.hobby = function() {
    cosnole.log(hobby);
  };
};
const zhangsan = new Person('张三', 20, '喜欢玩');
const lisi = new Person('李四', 20, '喜欢玩');
console.log(zhangsan.hobby === lisi.hobby); // false
```

当我们有 100，甚至上千个人，就会开辟 1000 个地址，造成地址损耗。

JavaScript 提供了公共空间存放这些应该存放到相同地址的地方。

## 原型

```js
function Person(name, age, hobby) {
  this.name = name;
  this.age = age;
};
Person.prototype.hobby = function(hobby) {
  cosnole.log(hobby);
};
const zhangsan = new Person('张三', 20, '喜欢玩');
const lisi = new Person('李四', 20, '喜欢玩');
console.log(zhangsan.hobby === lisi.hobby); // true
```

这就是为啥需要 `prototype` 的原因。

```js
function Person(name, age, hobby) {
  this.name = name;
  this.age = age;
};
Person.prototype.hobby = function(hobby) {
  cosnole.log(hobby);
};
const zhangsan = new Person('张三', 20, '喜欢玩');
console.log(zhangsan);
/*
{
  age: 20
  name: "张三"
  __proto__:
    hobby: ƒ ()
    constructor: ƒ Person(name, age, hobby)
    __proto__: Object
}
*/
console.log(zhangsan.__proto__ === Person.prototype); // true
console.log(Person.prototype.constructor === Person); // true
console.log(zhangsan.constructor === Person); // true
```

实例化的对象的 `__proto__` 和原构造函数的 `prototype` 一致：`zhangsan.__proto__ === Person.prototype`。

原型的固有属性：`Person.prototype.constructor === Person`、`zhangsan.constructor === Person`。

可以通过 `constructor` 来判断类型

```js
let str = new String('abc');
console.log(str.constructor === String);
```

## 原型链

对象之间的继承关系，在 JavaScript 中是通过 `prototype` 对象指向父类对象，直到指向 `Object` 对象为止，这样就形成了一个原型指向的链条，称之为原型链。

1. 当访问一个对象的属性和方法时，会先在对象自身上查找属性或方法是否存在，如果存在就使用对象自身的属性和方法。如果不存在就去对象的构造函数中的原型对象中查找。依次类推，直到找到为止。如果在顶层对象中还找不到，则返回 `undefined`。
2. 原型链最顶层为 `Object` 构造函数的 `prototype` 原型对象，给 `Object.prototype` 添加属性或者方法可以被除 `null` 和 `prototype` 之外的所有数据类型对象使用。

```js
// 构造函数
function Foo(name) {
  this.name = name; // 1. 现在构造函数中找
}
// Foo.prototype.name = 'jsliang'; // 2. 在原型对象中找
// Object.prototype.name = 'jsliang'; // 4. 通过原型链查找
const newFoo = new Foo('jsliang');
console.log(newFoo.name);
```

如果没有，则沿着原型链查找；如果有，那就返回最近的。

## call、apply、bind

改变函数内部的 `this` 指向。

* `call(obj, arg1, arg2...)`
  * 参数 1：需要改变的 `this` 指向到 `obj`
  * 参数 2：方法的参数
  * 参数 3：方法的参数
* `apply(obj, [arg1, arg2...])`
  * 参数 1：需要改变的 `this` 指向到 `obj`
  * 参数 2：方法的参数都放到数组中
* `bind(obj)(arg1, arg2...)`
  * 返回的是一个函数，需要执行一遍，即 `bind()()`

> call

```js
function foo(name, age) {
  console.log(this);
  console.log(name);
  console.log(age);
}
const obj = {
  name: '张三',
};
// foo.call(obj, '张三', 20);
// foo.apply(obj, ['张三', 20]);
foo.bind(obj)('张三', 20); // 返回一个函数，需要执行一遍
/*
{
  name: "张三"
  __proto__: Object
}
'张三'
20
*/
```

### 继承

儿子 -> 父亲 -> 爷爷

```js
function Dad(name, age) {
  this.name = name;
  this.age = age;
  this.money = '100000';
}
function Son(son, father) {
  Dad.call(this, father.name, father.age);
  this.name = son.name;
  this.age = son.age;
}
const son = new Son(
  {
    name: '儿子',
    age: 20,
  },
  {
    name: '爸爸',
    age: 99,
  }
);
console.log(son); // Son { name: '儿子', age: 20, money: '100000' }
```

## 原型的继承

```js
function Dad(name, age) {
  this.name = name;
  this.age = age;
  this.money = '100000';
}
Dad.prototye.play = function() {
  console.log('play');
};
function Son(son, father) {
  Dad.call(this, father.name, father.age);
  this.name = son.name;
  this.age = son.age;
}
const son = new Son(
  {
    name: '儿子',
    age: 20,
  },
  {
    name: '爸爸',
    age: 99,
  }
);
console.log(son); // Son { name: '儿子', age: 20, money: '100000' }
// son.play; // 报错
```

可以看到，上面的继承中，我们并没有继承原型的方法。

但是，如果你使用：

```js
Son.prototype === Dad.prototype;
```

那就会导致两者地址相同，即改变一者会触发另一个的改变。

## 传值和传址

众所周知，JavaScript 中有传值和传址一说法。

在这里先简单讲一下 **jsliang** 对传值和传址的理解：

* `String`、`Number` 等是单身汉。假设张三它兜里有钱为 `1`，李四说 “俺也一样”，然后 `李四 = 张三`；接着张三的钱被偷了，这时候李四这二货就回 “俺不一样”。

```js
let zhangsanMoney = 1;
let lisiMoney = zhangsanMoney;

zhangsanMoney = 0; // 被偷了
console.log(lisiMoney === zhangsanMoney); // false
```

* `Array`、`Object` 为家庭。假设张三和李四是一家，金库为 `[1]`，这时候张三挣了 2 块钱，家里金库变成了：`[1, 2]`，李四这二货就会无耻地来一句 “俺也一样”，因为你家就是我家，我家也是 `[1, 2]` 了。

```js
// 一家人的地址相同
let zhangsanMoney = [1];
let lisiMoney = zhangsanMoney;
zhangsanMoney.push(2);

console.log(zhangsanMoney); // [1, 2]
console.log(lisiMoney); // [1, 2]
```

这时候，如果张三受不了李四，要出去打工，那就要更换地址（更换家）。

如果张三拿到第三桶金，那么张三的金库就为：`[1, 2, 3]`，而李四还是：`[1, 2]`

```js
// 一家人的地址相同
let zhangsanMoney = [1];
lisiMoney = zhangsanMoney;
zhangsanMoney.push(2);

// 更换地址
zhangsanMoney = [1, 2, 3];

console.log(zhangsanMoney); // [1, 2, 3]
console.log(lisiMoney); // [1, 2]
```

当然，不排除李四跟着张三跑到同一个地方打工，然后……（感觉 **jsliang** 可以据此写一部小说了，哈哈）

## 深拷贝

看另一篇文章

```js
function deepClone(obj) {
  const newObj = Array.isArray(obj) ? [] : {};
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      if (typeof obj[key] === 'object') {
        newObj[key] = deepClone(obj[key]);
      } else {
        newObj[key] = obj[key];
      }
    }
  }
  return newObj;
}
const obj1 = {
  name: 'jsliang',
  houses: [1, 2, 3, 4],
  like: {
    play: 'game',
    eat: 'food',
  },
  do: function() {
    console.log(123);
  },
};
const obj2 = deepClone(obj1);
console.log(obj2);
/*
{
  name: 'jsliang',
  houses: [ 1, 2, 3, 4 ],
  like: { play: 'game', eat: 'food' },
  do: [Function: do],
}
*/
```

## 组合继承

* 通过深拷贝进行继承

```js
function deepClone(obj) {
  const newObj = Array.isArray(obj) ? [] : {};
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      if (typeof obj[key] === 'object') {
        newObj[key] = deepClone(obj[key]);
      } else {
        newObj[key] = obj[key];
      }
    }
  }
  return newObj;
}

function Dad(name, age) {
  this.name = name;
  this.age = age;
  this.money = '100000';
}
Dad.prototype.play = function() {
  console.log('play1');
};

function Son(name, age) {
  Dad.call(this);
  this.name = name;
  this.age = age;
}
Son.prototype = deepClone(Dad.prototype);
Son.prototype.play = function() {
  console.log('play2');
}

const father = new Dad('父亲', 99);
const son = new Son('儿子', 20);
console.log(father); // { name: '父亲', age: 99, money: '100000' }
console.log(son); // { name: '儿子', age: 20, money: '100000' }
father.play(); // play1
son.play(); // play2
```

* 组合继承

```js
// 更新代码
function Link() {}

function Dad(name, age) {
  this.name = name;
  this.age = age;
  this.money = '100000';
}
Dad.prototype.play = function() {
  console.log('play1');
};

function Son(name, age) {
  Dad.call(this);
  this.name = name;
  this.age = age;
}
// 更新代码
Link.prototype = Dad.prototype;
Son.prototype = new Link();
Son.prototype.constructor = Son;
// 更新代码结束
Son.prototype.play = function() {
  console.log('play2');
}

const father = new Dad('父亲', 99);
const son = new Son('儿子', 20);
console.log(father); // { name: '父亲', age: 99, money: '100000' }
console.log(son); // { name: '儿子', age: 20, money: '100000' }
father.play(); // play1
son.play(); // play2
```

## ES5 -> ES6

```js
// ES5：构造函数 -> 模拟类的概念
function Person(name, age) {
  this.name = name;
  this.age = age;
}
Person.prototype.hobby = function() {
  console.log('爱好');
}

// ES6：类
class Person {
  // 静态属性
  static weight = 170;
  // 私有属性
  #myname = 'jsliang';
  // 构造器属性
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  hobby() {
    console.log('爱好');
  }
}
console.log(typeof Person); // function
const zhangsan = new Person('张三', 20);
zhangsan.hobby(); // '爱好'

// 静态属性调用
console.log(Person.weight); // 170

// 私有属性只能内部调用
console.log(zhangsan.#myname); // Uncaught SyntaxError: Undefined private field undefined: must be declared in an enclosing class
```

## ES6 继承

```js
class Father {
  constructor(age) {
    this.name = '张三';
    this.age = age;
  }
  hobby() {
    console.log('喜欢高尔夫');
  }
}

class Son extends Father {
  constructor(age) {
    // 通过 extends + super 继承
    super(age); // 可以传递参数到父类
    this.height = '178cm';
  }
  hobby() {
    console.log('喜欢篮球');
    super.hobby(); // 也可以继承方法
  }
}
const xiaozhang = new Son(50);
console.log(xiaozhang.name); // 张三
console.log(xiaozhang.age); // 50
xiaozhang.hobby();
// '喜欢篮球'
// 就近原则，加入了 super.hobby() 之后，还会继承父类方法
// '喜欢高尔夫'
```

## ES6 module

* AMD：require.js
* CMD：sea.js
* ES6 模块化：导入、导出

```js
// 两种导出机制

// 导出多个 ——> 通过展开导入
export ... ——> import { ... } from '';

// 导出一个 ——> 自定义变量引入
export default ... ——> import a from '';
````

> index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>module 导入导出</title>
</head>
<body>
  
</body>
<script type="module">
  // 默认不支持 module，需要开启 type="module"
  import Person, { a as c, b } from './module.js';

  const person = new Person('张三', 26);
  console.log(person); // Person {#myname: "jsliang", name: "张三", age: 26}

  // 可以通过 a as c 的形式，来解决命名冲突
  console.log(c); // 10
  console.log(b); // 20
</script>
</html>
```

> module.js

```js
// ES6：类
class Person {
  // 静态属性
  static weight = 170;
  // 私有属性
  #myname = 'jsliang';
  // 构造器属性
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  hobby() {
    console.log('爱好');
  }
}

export default Person;

export const a = 10;
export const b = 20;
```

## ES6 module 按需导入

> index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>module 按需导入</title>
</head>
<body>
  <button class="btn">点我加载</button>
</body>
<script type="module">
  const btn = document.querySelector('.btn');
  btn.onclick = () => {
    import('./module.js').then((res) => {
      console.log(res); // Module {Symbol(Symbol.toStringTag): "Module"}
      /*
        a: (...)
        b: (...)
        default: (...)
        Symbol(Symbol.toStringTag): "Module"
        get a: ƒ ()
        set a: ƒ ()
        get b: ƒ ()
        set b: ƒ ()
        get default: ƒ ()
        set default: ƒ ()
      */
    });
  };

  // 同步加载
  // btn.onclick = async function() {
  //   const res = await import('./module.js');
  //   console.log(res);
  // };
</script>
</html>
```

> index.js

```js
// ES6：类
class Person {
  // 静态属性
  static weight = 170;
  // 私有属性
  #myname = 'jsliang';
  // 构造器属性
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  hobby() {
    console.log('爱好');
  }
}

export default Person;

export const a = 10;
export const b = 20;
```

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">jsliang 的文档库</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/LiangJunrong/document-library" property="cc:attributionName" rel="cc:attributionURL">梁峻荣</a> 采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/LiangJunrong/document-library" rel="dct:source">https://github.com/LiangJunrong/document-library</a>上的作品创作。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="https://creativecommons.org/licenses/by-nc-sa/2.5/cn/" rel="cc:morePermissions">https://creativecommons.org/licenses/by-nc-sa/2.5/cn/</a> 处获得。