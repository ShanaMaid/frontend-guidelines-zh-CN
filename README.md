# frontend-guidelines-zh-CN(前端指南汉化)
前端指南汉化

## 写在前面的话
本文原文是一篇来自Github上[@bendc](https://github.com/bendc/)的6,539星的文章,在此声明，原作者保有所有权利，本文仅供技术探讨学习。

作者:[@bendc](https://github.com/bendc/)

原文:[https://github.com/bendc/frontend-guidelines](https://github.com/bendc/frontend-guidelines)。

译者:[ShanaMaid](https://github.com/shanamaid)

译文:[https://github.com/ShanaMaid/frontend-guidelines-zh-CN/](https://github.com/ShanaMaid/frontend-guidelines-zh-CN/)

喜欢得话不妨给我一个`star`?

-------------转载请注明原作者以及译者和出处，请务必保留以上信息-------------



## frontend-guidelines(前端指南)
### HTML
#### Semantics(语义化)
> HTML5 provides us with lots of semantic elements aimed to describe precisely the content. Make sure you benefit from its rich vocabulary.

HTML5为我们提供了大量的语义化元素，目的在于帮助我们更准确地描述网页的内容。确保你自己从这些丰富的语义化元素中受益。

```
<!-- bad -->
<div id="main">
  <div class="article">
    <div class="header">
      <h1>Blog post</h1>
      <p>Published: <span>21st Feb, 2015</span></p>
    </div>
    <p>…</p>
  </div>
</div>

<!-- good -->
<main>
  <article>
    <header>
      <h1>Blog post</h1>
      <p>Published: <time datetime="2015-02-21">21st Feb, 2015</time></p>
    </header>
    <p>…</p>
  </article>
</main>
```


>Make sure you understand the semantics of the elements you're using. It's worse to use a semantic element in a wrong way than staying neutral.

在你使用这些元素时，请务必保证你理解了它们的语义。以错误地方式去使用一个语义化元素远比按照原来的写法更加糟糕。

```
<!-- bad -->
<h1>
  <figure>
    <img alt=Company src=logo.png>
  </figure>
</h1>

<!-- good -->
<h1>
  <img alt=Company src=logo.png>
</h1>
```

#### Brevity(简洁)
> Keep your code terse. Forget about your old XHTML habits.

请保持代码的简洁性，忘掉你那些关于XHTML的老旧写法与习惯吧
```
<!-- bad -->
<!doctype html>
<html lang=en>
  <head>
    <meta http-equiv=Content-Type content="text/html; charset=utf-8" />
    <title>Contact</title>
    <link rel=stylesheet href=style.css type=text/css />
  </head>
  <body>
    <h1>Contact me</h1>
    <label>
      Email address:
      <input type=email placeholder=you@email.com required=required />
    </label>
    <script src=main.js type=text/javascript></script>
  </body>
</html>

<!-- good -->
<!doctype html>
<html lang=en>
  <meta charset=utf-8>
  <title>Contact</title>
  <link rel=stylesheet href=style.css>

  <h1>Contact me</h1>
  <label>
    Email address:
    <input type=email placeholder=you@email.com required>
  </label>
  <script src=main.js></script>
</html>
```

#### Accessibility(可访问性)
> Accessibility shouldn't be an afterthought. You don't have to be a WCAG expert to improve your website, you can start immediately by fixing the little things that make a huge difference, such as:
* learning to use the alt attribute properly
* making sure your links and buttons are marked as such (no <div class=button> atrocities)
* not relying exclusively on colors to communicate information
* explicitly labelling form controls

网页的可访问性不应该在网站开发完后再进行考虑，也并非要成为[(WCAG(Web内容无障碍指南)专家](http://baike.baidu.com/link?url=y1Ip0Tcqi2GSvVZ2FdtY8evH66xslyaLWU8Z87NQYKy5qlct0eKq826BqHBsc1xF5-0pHHeGwyhouuLj2pATe_)才能优化你的网站，你可以立刻开始，通过完善一些小的细节，它们可以给你的网站带来很大的变化，比如：
* 学会正确地使用`alt`属性
* 保证你的所有链接和按钮不要被这样标记，`<div class=button> `
* 在信息的交互上不要单一依赖颜色上的交流
* 明确地用label对表单进行管理控制

```
<!-- bad -->
<h1><img alt="Logo" src="logo.png"></h1>

<!-- good -->
<h1><img alt="My Company, Inc." src="logo.png"></h1>
```

#### Language(语言)
> While defining the language and character encoding is optional, it's recommended to always declare both at document level, even if they're specified in your HTTP headers. Favor UTF-8 over any other character encoding.

虽然语言和字符编码的定义是可选的，但还建议都在文档层进行声明，即使他们都在你的HTTP报文头部中已经确定。在任何字符编码中如果支持`utf-8`，推荐使用`utf-8`。

```
<!-- bad -->
<!doctype html>
<title>Hello, world.</title>

<!-- good -->
<!doctype html>
<html lang=en>
  <meta charset=utf-8>
  <title>Hello, world.</title>
</html>
```

#### Performance(性能)
> Unless there's a valid reason for loading your scripts before your content, don't block the rendering of your page. If your style sheet is heavy, isolate the styles that are absolutely required initially and defer the loading of the secondary declarations in a separate style sheet. Two HTTP requests is significantly slower than one, but the perception of speed is the most important factor.

除非有必要的原因，否则不要再你的网页前面加载script文件，因为它会阻止你网页的渲染。如果你的css样式文件太大，请将必需的样式分离出来，将次要的样式放在另外一个css文件中进行延迟的二次加载。虽然两个HTTP请求比一个明显变慢，但相比而言网页实际加载速度来说，感官上的快慢感受更加重要。

```
<!-- bad -->
<!doctype html>
<meta charset=utf-8>
<script src=analytics.js></script>
<title>Hello, world.</title>
<p>...</p>

<!-- good -->
<!doctype html>
<meta charset=utf-8>
<title>Hello, world.</title>
<p>...</p>
<script src=analytics.js></script>
```

### CSS
#### Semicolons(分号)
> While the semicolon is technically a separator in CSS, always treat it as a terminator.

虽然在CSS中分号被视作一个分隔号，但请始终将它视作终结号。
```
/* bad */
div {
  color: red
}

/* good */
div {
  color: red;
}
```

#### Box model(盒子模型)
> The box model should ideally be the same for the entire document. A global * { box-sizing: border-box; } is fine, but don't change the default box model on specific elements if you can avoid it.

对于整个文档来说，理论上来说盒子模型应该是相同的，全局设置盒子模型(`* { box-sizing: border-box; }`)是很好的。如果可以的话，请不要改变特定元素的默认盒子模型。

```
/* bad */
div {
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
}

/* good */
div {
  padding: 10px;
}
```

#### Flow(文档流)
> Don't change the default behavior of an element if you can avoid it. Keep elements in the natural document flow as much as you can. For example, removing the white-space below an image shouldn't make you change its default display:

如果可以的话，请不要改变一个元素的默认表现行为。尽可能地保留原生文档流中元素的默认行为。例如，删除一个图像下面的`white-space`不会让你改变它的默认表现行为：
```
/* bad */
img {
  display: block;
}

/* good */
img {
  vertical-align: middle;
}
```
> Similarly, don't take an element off the flow if you can avoid it.

同样的，如果可以的话，请不要让元素脱离文档流。
```
/* bad */
div {
  width: 100px;
  position: absolute;
  right: 0;
}

/* good */
div {
  width: 100px;
  margin-left: auto;
}
```

#### Positioning(定位)
> There are many ways to position elements in CSS but try to restrict yourself to the properties/values below. By order of preference:

在CSS中有许多种定位元素的方法，但是对于定位属性值的使用上尽量严格要求你自己按照以下使用顺序：

```
display: block;
display: flex;
position: relative;
position: sticky;
position: absolute;
position: fixed;
```

#### Selectors(选择器)
> Minimize selectors tightly coupled to the DOM. Consider adding a class to the elements you want to match when your selector exceeds 3 structural pseudo-classes, descendant or sibling combinators.

请将选择器与`DOM`节点尽量紧密的联系在一起(耦合)。如果你想为某个元素添加样式的时候你的选择器超过了三层结构的伪类、后代或者兄弟选择器，请考虑直接添加一个`class`。

```
/* bad */
div:first-of-type :last-child > p ~ *

/* good */
div:first-of-type .info
```
> Avoid overloading your selectors when you don't need to.

如果你不需要，请不要重载你的选择器。
```
img[src$=svg], ul > li:first-child {
  opacity: 0;
}

/* good */
[src$=svg], ul > :first-child {
  opacity: 0;
}
```
#### Specificity(特异化)
> Don't make values and selectors hard to override. Minimize the use of id's and avoid !important.

不要让属性值和选择器变得难以重写，尽量减少`id`的使用和避免`!important`。

```
/* bad */
.bar {
  color: green !important;
}
.foo {
  color: red;
}

/* good */
.foo.bar {
  color: green;
}
.foo {
  color: red;
}
```

#### Overriding(复写)
> Overriding styles makes selectors and debugging harder. Avoid it when possible.

复写样式会使得选择器和调试变得困难，尽可能避免这样做。

```
/* bad */
li {
  visibility: hidden;
}
li:first-child {
  visibility: visible;
}

/* good */
li + li {
  visibility: hidden;
}
```

#### Inheritance(继承)
> Don't duplicate style declarations that can be inherited.

不要对可以继承的样式声明进行重复声明。

```
/* bad */
div h1, div p {
  text-shadow: 0 1px 0 #fff;
}

/* good */
div {
  text-shadow: 0 1px 0 #fff;
}
```

#### Brevity(简洁性)
> Keep your code terse. Use shorthand properties and avoid using multiple properties when it's not needed.

请保持代码的简洁性。尽量使用简写属性，当没有必要的时候应当避免使用多个属性。

```
/* bad */
div {
  transition: all 1s;
  top: 50%;
  margin-top: -10px;
  padding-top: 5px;
  padding-right: 10px;
  padding-bottom: 20px;
  padding-left: 10px;
}

/* good */
div {
  transition: 1s;
  top: calc(50% - 10px);
  padding: 5px 10px 20px;
}
```

#### Language(语言)
> Prefer English over math.

相对于数学表达式更提倡使用英语，能使用英语表达的，尽量别使用数学表达式。
```
/* bad */
:nth-child(2n + 1) {
  transform: rotate(360deg);
}

/* good */
:nth-child(odd) {
  transform: rotate(1turn);
}
```

#### Vendor prefixes(浏览器属性前缀)
> Kill obsolete vendor prefixes aggressively. If you need to use them, insert them before the standard property.

强烈建议抛弃那些已经过时的浏览器属性前缀。如果你需要使用他们，请在标准属性前面插入它们。
```
/* bad */
div {
  transform: scale(2);
  -webkit-transform: scale(2);
  -moz-transform: scale(2);
  -ms-transform: scale(2);
  transition: 1s;
  -webkit-transition: 1s;
  -moz-transition: 1s;
  -ms-transition: 1s;
}

/* good */
div {
  -webkit-transform: scale(2);
  transform: scale(2);
  transition: 1s;
}
```

#### Animations(动画)
> Favor transitions over animations. Avoid animating other properties than `opacity` and `transform`.

相对于`animations`来说更提倡使用`transitions`。除了 `opacity` 和 `transform`，`animate`过程中请避免使用其它属性。

```
/* bad */
div:hover {
  animation: move 1s forwards;
}
@keyframes move {
  100% {
    margin-left: 100px;
  }
}

/* good */
div:hover {
  transition: 1s;
  transform: translateX(100px);
}
```

#### Units(单位)
> Use unitless values when you can. Favor rem if you use relative units. Prefer seconds over milliseconds.

当你能够使用无单位值的时候，你最能能够这样做。如果你需要使用相对单位，推荐`rem`。
相对于毫秒来说，推荐使用秒。

```
/* bad */
div {
  margin: 0px;
  font-size: .9em;
  line-height: 22px;
  transition: 500ms;
}

/* good */
div {
  margin: 0;
  font-size: .9rem;
  line-height: 1.5;
  transition: .5s;
}
```

#### Colors(颜色)
> If you need transparency, use rgba. Otherwise, always use the hexadecimal format.

如果你需要使用透明度，请使用`rgba`。否则，请使用十六进制的形式。

```
/* bad */
div {
  color: hsl(103, 54%, 43%);
}

/* good */
div {
  color: #5a3;
}
```

#### Drawing(图片绘制)
> Avoid HTTP requests when the resources are easily replicable with CSS.

如果一个图形资源你你能用css轻松绘制出来进行代替，那么请不要使用`HTTP`请求。
注:  white-circle   白圈
```
/* bad */
div::before {
  content: url(white-circle.svg);
}

/* good */
div::before {
  content: "";
  display: block;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #fff;
}
```

#### Hacks(css hack技巧)
> Don't use them.

不要使用他们。
```
/* bad */
div {
  // position: relative;
  transform: translateZ(0);
}

/* good */
div {
  /* position: relative; */
  will-change: transform;
}
```

### JavaScript
#### Performance(性能)
> Favor readability, correctness and expressiveness over performance. JavaScript will basically never be your performance bottleneck. Optimize things like image compression, network access and DOM reflows instead. If you remember just one guideline from this document, choose this one.

基于性能的基础上，需要考虑代码可读性、正确性和表现性。`JavaScript`从根本上来说绝对不会成为你性能上的瓶颈。优化一些事物，例如图片压缩、网络介入以及`DOM`回流。如果在这篇文档中你只想记住这一个指导方针，那就就记住这个吧。

```
// bad (albeit way faster)
const arr = [1, 2, 3, 4];
const len = arr.length;
var i = -1;
var result = [];
while (++i < len) {
  var n = arr[i];
  if (n % 2 > 0) continue;
  result.push(n * n);
}

// good
const arr = [1, 2, 3, 4];
const isEven = n => n % 2 == 0;
const square = n => n * n;

const result = arr.filter(isEven).map(square);
```

#### Statelessness(无状态)
> Try to keep your functions pure. All functions should ideally produce no side-effects, use no outside data and return new objects instead of mutating existing ones.

请尽量保持你函数的纯洁性。所有的函数理想状态下都应该无副作用，请不要使用外部数据，同时返回的应该是一个新的对象而不是改变已有的。

```
// bad
const merge = (target, ...sources) => Object.assign(target, ...sources);
merge({ foo: "foo" }, { bar: "bar" }); // => { foo: "foo", bar: "bar" }

// good
const merge = (...sources) => Object.assign({}, ...sources);
merge({ foo: "foo" }, { bar: "bar" }); // => { foo: "foo", bar: "bar" }
```

#### Natives(原生)
> Rely on native methods as much as possible.

尽可能地使用JavaScript的原生方法。

```
// bad
const toArray = obj => [].slice.call(obj);

// good
const toArray = (() =>
  Array.from ? Array.from : obj => [].slice.call(obj)
)();
```

#### Coercion(类型隐式转换)
> Embrace implicit coercion when it makes sense. Avoid it otherwise. Don't cargo-cult.

当类型隐式转换是有意义的时候，请放心的使用它。如果没有意义，就别使用它。不要盲目地迷权威！

```
// bad
if (x === undefined || x === null) { ... }

// good
if (x == undefined) { ... }
```

#### Loops(循环)
> Don't use loops as they force you to use mutable objects. Rely on array.prototype methods.

当你不得不使用易变的对象的时候，不要使用循环。请考虑使用` array.prototype `方法，即数组原生方法。

```
// bad
const sum = arr => {
  var sum = 0;
  var i = -1;
  for (;arr[++i];) {
    sum += arr[i];
  }
  return sum;
};

sum([1, 2, 3]); // => 6

// good
const sum = arr =>
  arr.reduce((x, y) => x + y);

sum([1, 2, 3]); // => 6
```

> If you can't, or if using array.prototype methods is arguably abusive, use recursion.

如果你不想使用数组方法，或者说你觉得使用数组方法令你很不爽，那么你可以考虑使用递归。
```
// bad
const createDivs = howMany => {
  while (howMany--) {
    document.body.insertAdjacentHTML("beforeend", "<div></div>");
  }
};
createDivs(5);

// bad
const createDivs = howMany =>
  [...Array(howMany)].forEach(() =>
    document.body.insertAdjacentHTML("beforeend", "<div></div>")
  );
createDivs(5);

// good
const createDivs = howMany => {
  if (!howMany) return;
  document.body.insertAdjacentHTML("beforeend", "<div></div>");
  return createDivs(howMany - 1);
};
createDivs(5);
```

> Here's a [generic loop function](https://gist.github.com/bendc/6cb2db4a44ec30208e86) making recursion easier to use.

这里是一个[通用的循环函数](https://gist.github.com/bendc/6cb2db4a44ec30208e86)，它使得递归使用起来更加容易。

#### Arguments(arguments内置对象)
> Forget about the arguments object. The rest parameter is always a better option because:
 * it's named, so it gives you a better idea of the arguments the function is expecting
 * it's a real array, which makes it easier to use.
 
 请忘了`arguments`对象。额外的参数总会是一个较好的选择，因为：
 * 它已经被命名了，所以它能让你在实现函数的功能上有一个更好的期望，能够为你提供理想的参数。
 * 它是一个数组，会让你使用起来更加方面
 
 #### Apply
> forget about apply(). Use the spread operator instead.

请忘记关于`apply()`的一切，使用操作符去代替。

```
const greet = (first, last) => `Hi ${first} ${last}`;
const person = ["John", "Doe"];

// bad
greet.apply(null, person);

// good
greet(...person);
```

#### Bind
> Don't bind() when there's a more idiomatic approach.

当你有一个更合理的方法的时候，不要使用`bind()`。

```
// bad
["foo", "bar"].forEach(func.bind(this));

// good
["foo", "bar"].forEach(func, this);
```

```
// bad
const person = {
  first: "John",
  last: "Doe",
  greet() {
    const full = function() {
      return `${this.first} ${this.last}`;
    }.bind(this);
    return `Hello ${full()}`;
  }
}

// good
const person = {
  first: "John",
  last: "Doe",
  greet() {
    const full = () => `${this.first} ${this.last}`;
    return `Hello ${full()}`;
  }
}
```

#### Higher-order functions(高阶函数)
> Avoid nesting functions when you don't have to.

当你不是必须使用嵌套函数的时候，请避免它。

```
// bad
[1, 2, 3].map(num => String(num));

// good
[1, 2, 3].map(String);
```

#### Composition(组合函数)
> Avoid multiple nested function calls. Use composition instead.

请避免使用多层嵌套函数调用，使用组合函数去替代。

```
const plus1 = a => a + 1;
const mult2 = a => a * 2;

// bad
mult2(plus1(5)); // => 12

// good
const pipeline = (...funcs) => val => funcs.reduce((a, b) => b(a), val);
const addThenMult = pipeline(plus1, mult2);
addThenMult(5); // => 12
```

#### Caching(缓存)
>  Cache feature tests, large data structures and any expensive operation.

缓存功能测试，大数据结构以及任何高性能损耗的操作。

```
// bad
const contains = (arr, value) =>
  Array.prototype.includes
    ? arr.includes(value)
    : arr.some(el => el === value);
contains(["foo", "bar"], "baz"); // => false

// good
const contains = (() =>
  Array.prototype.includes
    ? (arr, value) => arr.includes(value)
    : (arr, value) => arr.some(el => el === value)
)();
contains(["foo", "bar"], "baz"); // => false
```

#### Variables(变量)
> Favor const over let and let over var.

推荐定义变量使用的优先级顺序，`const` > `let` > `var`。
```
// bad
var me = new Map();
me.set("name", "Ben").set("country", "Belgium");

// good
const me = new Map();
me.set("name", "Ben").set("country", "Belgium");
```

#### Conditions(条件语句)
> Favor IIFE's and return statements over if, else if, else and switch statements.

推荐使用`匿名执行函数`返回语句，代替 `if`,`else if`,`else`,`switch` 语句。

```
// bad
var grade;
if (result < 50)
  grade = "bad";
else if (result < 90)
  grade = "good";
else
  grade = "excellent";

// good
const grade = (() => {
  if (result < 50)
    return "bad";
  if (result < 90)
    return "good";
  return "excellent";
})();
```

#### Object iteration(对象迭代)
> Avoid for...in when you can.

如果可以的话，请不要使用 `for...in`。
```
const shared = { foo: "foo" };
const obj = Object.create(shared, {
  bar: {
    value: "bar",
    enumerable: true
  }
});

// bad
for (var prop in obj) {
  if (obj.hasOwnProperty(prop))
    console.log(prop);
}

// good
Object.keys(obj).forEach(prop => console.log(prop));
```

#### Objects as Maps
> While objects have legitimate use cases, maps are usually a better, more powerful choice. When in doubt, use a Map.

当对象有合理的用例时，`maps`是一个更棒更高效的选择。当有疑问时，请使用`map`!

```
// bad
const me = {
  name: "Ben",
  age: 30
};
var meSize = Object.keys(me).length;
meSize; // => 2
me.country = "Belgium";
meSize++;
meSize; // => 3

// good
const me = new Map();
me.set("name", "Ben");
me.set("age", 30);
me.size; // => 2
me.set("country", "Belgium");
me.size; // => 3
```

#### Curry(柯里化)
> Currying is a powerful but foreign paradigm for many developers. Don't abuse it as its appropriate use cases are fairly unusual.

柯里化的功能是很强大，但是对于很多开发者来说它是陌生的。不要滥用它，但适当地使用还是非常有用的。

```
// bad
const sum = a => b => a + b;
sum(5)(3); // => 8

// good
const sum = (a, b) => a + b;
sum(5, 3); // => 8
```

#### Readability(可读性)
> Don't obfuscate the intent of your code by using seemingly smart tricks.

不要试图通过一些看似聪明的小技巧来模糊混淆你代码本身的真实目的。

```
// bad
foo || doSomething();

// good
if (!foo) doSomething();
```
```
// bad
void function() { /* IIFE */ }();

// good
(function() { /* IIFE */ }());
```
```
// bad
const n = ~~3.14;

// good
const n = Math.floor(3.14);
```
#### Code reuse(代码复用)
> Don't be afraid of creating lots of small, highly composable and reusable functions.

不要害怕创建了大量的小的，高组合型和可复用性的涵涵素。

```
// bad
arr[arr.length - 1];

// good
const first = arr => arr[0];
const last = arr => first(arr.slice(-1));
last(arr);
```
```
// bad
const product = (a, b) => a * b;
const triple = n => n * 3;

// good
const product = (a, b) => a * b;
const triple = product.bind(null, 3);
```

#### Dependencies(依赖性)
> Minimize dependencies. Third-party is code you don't know. Don't load an entire library for just a couple of methods easily replicable:

降低代码的依赖性。因为第三方的代码库是你完全不知道的。不要为了几个简单的很容易被复制的方法去加载整个库。

```
// bad
var _ = require("underscore");
_.compact(["foo", 0]));
_.unique(["foo", "foo"]);
_.union(["foo"], ["bar"], ["foo"]);

// good
const compact = arr => arr.filter(el => el);
const unique = arr => [...Set(arr)];
const union = (...arr) => unique([].concat(...arr));

compact(["foo", 0]);
unique(["foo", "foo"]);
union(["foo"], ["bar"], ["foo"]);
```

## License 
see [MIT LICENSE](./LICENSE) for details

## 补充
翻译存在不足之处欢迎各位PR进行补充修改，欢迎邮箱联系，uestczeng@gmail.com

## 鸣谢
[@xiyuanyuan](https://github.com/xiyuanyuan)


