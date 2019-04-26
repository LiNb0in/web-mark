# this
> 在全局环境中this等于window，而当函数被作为某个对象的方法调用时this则指向这个对象。不够匿名函数的执行环境具有**全局性**this通常指向window。
---

#### 先看一段代码：
```js
  const name = 'window';
  
  const obj = {
    name: 'obj',
    getNameFun: function () {
      return function () {
        return this.name;
      }
    }
  };
console.log(obj.getNameFun()()); // "window"(在非严格模式下)
```

> 我们只看结尾那段:
> #### obj.getNameFun()()
> * 可以分成两部分
>   * obj.getNameFun()：
>     * **函数被作为某个对象的方法调用时this则指向这个对象，由此得知getNameFun()函数无论是在**严格模式**or**非严格模式**中this都是指向obj对象**
>   * obj.getNameFun()():
  
  ```js
    // 我们将代码改写一下
    const name = 'window';
    const obj = {
      name: 'obj',
      getNameFun: function () {
        return function () {
          return this.name;
        }
      }
    }; 
    const wrapperFun = obj.getNameFun();
    wrapperFun(); // 可以看到getNameFun()函数的匿名函数其实是在全局执行的，所以this(在非严格模式下)自然指向window
  ```
  
>   **非严格模式**：在非严格模式下obj的getNameFun()函数返回的匿名函数**this**实际是指向全局window<br

>   **严格模式**：严格模式下匿名函数与在全局中直接执行的普通函数，无法直接获取全局变量中window的this，都为undefined


#### 块级作用域
> **块级作用域**：函数执行时**活动对象**所在的作用域链就是一个块级作用域
* 来看一段代码:
```js
  function consoleNumber (number) {
    const arr = [];
    for(var i=0; i<number; i+=1) {
      arr[i] = function () {
        return i;
      }
    }
    console.log(i);
    return arr;
  }
```
这个函数会返回一个数组，表面上来看每个数组项返回的应该都是自己对应的索引值。然而实际上，每个函数都返回10，
