# 避免巢狀

![hadouken](https://ithelp.ithome.com.tw/upload/images/20171221/20065504RIRldpL7Fs.jpg)

巢狀的程式碼不方便閱讀、維護，  
平時在開發時，應該盡力避免巢狀，

## 利用變數

```javascript
const pricesMap = {
  foo: 10,
  bar: 20
};

const items = ["foo", "foo", "bar"];

let sum = 0;
for (let i = 0; i < items.length; i++) {
  sum += pricesMap[items[i]];
}
```

`pricesMap[items[i]]` 就有點太巢，  
在閱讀時相當不方便，

```javascript
let sum = 0;
for (let i = 0; i < items.length; i++) {
  const item = items[i];
  sum += pricesMap[item];
}

let sum = 0;
for (const item of items) {
  sum += priceMap[item];
}
```

將 `key 另外取出` ，或 `以 for...of 取代` ，  
這樣的程式碼，相對好閱讀很多。

## 利用 return 、 break

另外常有情境為 `確認為某些特定情況則執行` ，  
譬如說在帳號密碼正確時，執行某些程式，

```javascript
function login(account, password) {
  if (account === "foo" && password === "bar") {
    // do something
  }
}
```

內部的程式碼會越來越巢，
此時可以善用 return ，

```javascript
function login(account, password) {
  if (account !== "foo" || password !== "bar") { return; }
  // do something
}
```

在看到第一行 return ，  
暗示若不符合條件，以後的程式碼不會執行，  
可讀性更高，更方便 debug，  

另外以一個費氏數列為例，

```javascript
function fib(x) {
  if (x === 0) {
    return 0;
  } else if (x === 1) {
    return 1;
  } else {
    return fib(x - 1) + fib(x - 2);
  }
}
```

因為 return 後不會繼續執行，  
else 的部份都可以省略不寫，  
同理也可以應用在 break 上。
