# 先宣告，後使用

JavaScript 變數有 hoisting 特性， 見 [MDN](https://developer.mozilla.org/zh-TW/docs/Glossary/Hoisting) 。

```javascript
console.log(foo); // undefined
var foo = "bar";
```

這段程式碼等價於，

```javascript
var foo;
console.log(foo);
foo = "bar";
```

如此的執行結果並不直觀，  
所以 `變數使用前一律要宣告` ，以避免此情況。

遵守 `先宣告，後使用` 的另一個優點是，  
在閱讀他人程式碼時比較方便，  
只要看到沒看過的變數、函數時，往上找就對了。

另外 JavaScript 在處理函數時，  
一樣有 hoisting 特性，

```javascript
console.log(foo()); // bar

function foo() {
  return "bar";
}
```

雖然函數是能正常運作的，  
但還是建議遵守 `先宣告，後使用` 。
