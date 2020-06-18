# 錯誤處理

## undefined, null

> Uncaught TypeError: Cannot read property 'name' of undefined
> Uncaught TypeError: Cannot read property 'name' of null

以中文理解，即為某個變數是 undefined 或是 null ，  
所以沒有辦法 (undefined | null).property ，
像是以下程式碼：

```javascript
const dog = {
  name: 'Lucky',
  age: 5,
};

console.log(
  dog.name, // Lucky
  dog.friend, // undefined
  dog.friend.name, // Uncaught TypeError: Cannot read property 'name' of undefined
);
```

發生錯誤的原因 dog.friends 為 undefined，  
而 undefined 並沒有 0 這個屬性，
可以利用 `undefined &&` 解決這個 bug ，  
JS 會在回傳 undefined ，並停止執行 && 後的程式碼，

```javascript
console.log(
  dog.name, // Lucky
  dog.friend, // undefined
  dog.friend && dog.friend.name, // undefined
);
```

同理，也可以用來 `||` 處理來 `default value` ，  
`undefined || defaultValue` 是在 JS 中，  
非常常見的處理 default value 的寫法，相當實用，

```javascript
console.log(
  dog.name, // Lucky
  dog.friend, // undefined
  (dog.friend && dog.friend.name) || 'George', // George
);
```

抑或是新語法 `?.` 與 `??` ，

```javascript
console.log(
  dog.name, // Lucky
  dog.friend, // undefined
  dog.friend?.name ?? 'George', // George
);
```
