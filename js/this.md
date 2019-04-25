# this
> 在全局环境中this等于window，而当函数被作为某个对象的方法调用时this则指向这个对象。不够匿名函数的执行环境具有**全局性**this通常指向window。
---

####先看一段代码：
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

> 这段代码的我们只看结尾那段:
> #### obj.getNameFun()()
> * obj.getNameFun()：**函数被作为某个对象的方法调用时this则指向这个对象，由此得知getNameFun()函数无论是在**严格模式**or**非严格模式**中this都是指向obj对象**
>  * obj.getNameFun()()
>  ###### 我们将代码改写一下:
  
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
    const wrapperFun = obj.getNameFun();
    wrapperFun();
  ```
  
>   **非严格模式**：在非严格模式下obj的getNameFun()函数其实返回的匿名函数的**this**实际是指向全局的window的<br>
>   **严格模式**：严格模式下getNameFun()函数返回的匿名函数的this为undefined
