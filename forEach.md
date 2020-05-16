# forEach 原理講解

先來宣告一個 function ：

```javascript
function add(x, y) {
  return x + y;
}

console.log(add(1, 1));
```

add 是一個很簡單的 function ，  
功能就是將傳入的兩個變數相加，  
function 其實跟物件一樣，可以有一些屬性，  
而且可以 assign 給其他變數，  
像是這樣：

```javascript
/**
 * 只有寫 function 的名子
 * 不在後面加上括號
 * 就可以把 function 當作物件使用
 */

console.log(add.name); // function 的名子
console.log(add.length); // function 要傳入的參數數量
console.log(add.toString()); // function 宣告時的程式碼

/**
 * log 的結果：
 *   add
 *   2
 *   function add(x, y) {
 *     return x + y;
 *   }
 */

// 呼叫 add 時才加上括號
console.log(add(2, 2)); // 4

const foo = add; // 把 function 賦值給其他變數

// 此時的 foo 就像 add 的別名
// foo === add 會是 true
// 被呼叫時也有一樣的效果
console.log(foo === add); // true
console.log(foo(2, 2)); // 4
```

同樣的 function 也可以作為參數傳入其他的 function ，  
這樣的 function 有很大的靈活性，  
作為參數的 function 通常稱為 callback ，  
以 setTimeout 作為舉例，  
setTimeout 的功能是延遲幾秒鐘後再執行 callback，  
使用 setTimeout 時要傳入兩個參數：

- callback
  被延遲執行的 function 。
- timeout
  延遲的秒數，單位是 milliseconds 。

```javascript
function sayHello() {
  console.log('Hello!');
}

// sayHello 作為參數傳入 setTimeout
setTimeout(sayHello, 5000);

/**
 * 五秒後的 log 結果：
 *   hello
 */
```

當然，我們自己寫的 function ，  
也可以試著用 function 作為參數，

```javascript
// callback 會是一個 function
function sayHelloAndThen(callback) {
  console.log('Hello!');
  // 在 console.log 後呼叫 callback
  callback();
}

function Introduce() {
  console.log("I'm Max.");
}

// 將 Introduce 作為 callback 傳入 sayHelloAndThen
sayHelloAndThen(Introduce);

/**
 * log 結果：
 *   Hello!
 *   I'm Max.
 */
```

如果上述的都懂了，那我們可以來實作 forEach 看看，  
forEach 的功用就是跑過整個 array ，  
可以說是 callback 版本的 for...in + foo...of ，  
forEach 有兩個參數：

- array
  要跑的 array
- callback
  每次迴圈都會執行的 function

其中 callback 會以三個參數呼叫：

- element
  這次迴圈的 array[index]
- index
  這次迴圈 index
- array
  跟 forEach 第一參數一樣的 array

```javascript
function forEach(array, callback) {
  // 用 for 跑過 array
  for (let index = 0; index < array.length; index++) {
    const element = array[index];

    callback(element, index, array);
  }
}

function sayMyName(name) {
  console.log(name);
}

const names = ['Max', 'Jackson', 'Callie'];

forEach(names, sayMyName);
/**
 * log 的結果：
 *   Max
 *   Jackson
 *   Callie
 */
```

上段程式碼完全等價於這段：

```javascript
for (let index = 0; index < names.length; index++) {
  const name = names[index];

  sayMyName(name, index, names);
}
```

因為 sayMyName 會依序接到三個參數，  
分別是 element 、 index 、 array ，  
因為是照順序傳的，所以 sayMyName 第一個參數叫什麼都是可以的，  
原生的 forEach 寫法也是相同的：

```javascript
forEach(names, sayMyName);

names.forEach(sayMyName);
```

在範例中， sayMyName 只有用 element 的參數，  
如果需要用到 index ，只需要加上第二個參數即可：

```javascript
function sayMyName2(name, index) {
  console.log(`${index + 1}. ${name}`);
}

names.forEach(sayMyName2);

/**
 * log 的結果：
 *   1. Max
 *   2. Jackson
 *   3. Callie
 */
```

如果 callback 只要使用一次，  
也可以作為寫在參數，不用另外宣告，  
上段程式碼完全等價於這段：

```javascript
names.forEach(function (name, index) {
  console.log(`${index + 1}. ${name}`);
});
```
