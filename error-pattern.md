# 錯誤處理

## undefined

JS 是弱型別語言，  
也就是有時候會因為 undefined 而發生錯誤，

```javascript
const dog = {
  name: "Lucky",
  age: 5
};

console.log(
  dog.name, // Lucky
  dog.friends, // undefined
  dog.friends[0] // Uncaught TypeError: Cannot read property '0' of undefined
);
```

發生錯誤的原因 dog.friends 為 undefined，  
而 undefined 並沒有 0 這個屬性，

```javascript
console.log(
  dog.name, // Lucky
  dog.friends, // undefined
  dog.friends && dog.friends[0] // undefined
);
```

利用 `undefined &&` ，  
JS 會在回傳 undefined ，並停止執行 && 後的程式碼，  
同理，也可以用來處來 `default value` ，

``` javascript
console.log(
  dog.name, // Lucky
  dog.friends, // undefined
  dog.friends && dog.friends[0] || "George" // George
)
```

`undefined || defaultValue` 是在 JS 中，  
非常常見的處理 default value 的寫法，相當實用。