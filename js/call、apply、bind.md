> [this](https://github.com/Linbiiiin/web-mark/blob/master/js/this.md)有关this的介绍
# apply、bind、call
> 它们都可以用来改变this的指向，其中call()和apply的方法类似，区别在于传参方式，call()方法接受参数列表(a1, a2, a3,...)，apply()方法接受参数是一个参数数组([a1, a2, a3, ...])。
## apply
  * 介绍
    > apply()方法接受一个给定的this，和一个参数数组。
    * 语法
      > fun.apply(this, [args]);
    * 参数
      * `this`<br>可选，fun函数运行时使用的this，注意：**在非严格模式下当this为null或undefined时将会自动指向全局对象**
      * `args`<br>可选，一个数组或者类数组对象，其中的数组元素将作为单独的参数传给fun函数。
    * 返回值
      调用有指定this值和参数的函数的结果。
 * 使用
 
 <br>
 `合并两个数组`
  ```js
   var arr1 = [1, 2, 3];
   var arr2 = [4, 5, 6];
   arr1.push.apply(arr1, arr2);
   console.log(arr1); // [1, 2, 3, 4, 5, 6];
  ```
  
 <br>
  `查询一个数组中的最大值与最小值`
  ```js
   const number = [45, 1, 15, 60];
   const max = Math.max.apply(null, number);
   const min = Math.min.apply(null, number);
   console.log(max); // 60
   console.log(min); // 1
   ```
  > **注意：正常情况下上面这么做是没有问题的，但是如果你的传参超出了apply()方法的限制就会有风险(比方说上万个参数)，不同javascript引擎有不同的限制（JavaScript 核心中已经做了硬编码[参数个数限制在65536](https://bugs.webkit.org/show_bug.cgi?id=80797)）这个限制可能会导致参数‘丢失’比方说某个引擎限制了方法参数最多传入10个（只是假设）而传入的参数个数为11个甚至更多，那么真正通过参数传入函数内部的参数就只有10个而已，并不是一个完整的参数列表**。
如果你的参数数组可能非常大，那么推荐你最好将参数数组做切块处理：

```js
// 摘自javascript|MDN
function minOfArray(arr) {
  var min = Infinity;
  var QUANTUM = 32768;

  for (var i = 0, len = arr.length; i < len; i += QUANTUM) {
    var submin = Math.min.apply(null, arr.slice(i, Math.min(i + QUANTUM, len)));
    min = Math.min(submin, min);
  }

  return min;
}

var min = minOfArray([5, 6, 2, 3, 7]);
```

---
## bind
 * 介绍
   > bind()方法是创建一个新的函数，在调用时设置this，并在调用新函数时将给定参数列表作为原函数的参数序列的前若干项。
   * 语法
     fun.bind(this, a1, a2, a3, ...);
   * 参数
     * `this`<br>调用绑定函数时作为this参数传递给目标函数。如果使用new运算符构造绑定函数，则忽略该值。当使用bind在setTimeout中创建一个函数（作为回调提供）时，作为thisArg传递的任何原始值都将转换为object。如果bind函数的参数列表为空，执行作用域的this将被视为新函数的thisArg。
     * `a1, a2, ...`<br>当目标函数被调用时，预先添加到绑定函数的参数列表中的参数 
   * 返回值
     返回一个原函数的拷贝，并且拥有指定this和初始参数。
   * 使用
   ```js
   ```
## call
 * 介绍
    call()方法使用一个指定this和指定的若干参数来调用一个函数。
   > bind()方法是创建一个新的函数，在调用时设置this
   * 语法
     > fun.call(this, a1, a2, a3, ...)
   * 参数
     * `this`<br>在 fun 函数运行时指定的 this 值。需要注意的是，指定的 this 值并不一定是该函数执行时真正的 this 值，如果这个函数在非严格模式下运行，则指定为 null 和 undefined 的 this 值会自动指向全局对象（浏览器中就是 window 对象），同时值为原始值（数字，字符串，布尔值）的 this 会指向该原始值的自动包装对象。
     * `a1, a2, ...`<br>指定的参数列表。
   * 返回参数
     使用调用者提供的 this 值和参数调用该函数的返回值。若该方法没有返回值，则返回 undefined。
   * 使用
   ```js
   ```
