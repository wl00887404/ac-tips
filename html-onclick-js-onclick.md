# HTML onclick vs JavaScript onclick

在 HTML 的 onclick 值 assign 的是文字，  
但 JavaScript assign 的是 function ，  
像是這樣：

```HTML
<button
  id="button1"
  onclick="function foo(){ console.log(1) }"
>button1</button>

<button id="button2">button2</button>
<script>
  button2.onclick = function bar() {
    console.log(2);
  };
</script>
```

點擊 #button1 ，什麼也沒發生，  
點擊 #button2 ，會正確的印出 2 ，  
如果你試著 console.log(button1.onclick) 會發現：

```javascript
console.log(button1.onclick);
/**
 * 輸出結果：
 *   ƒ onclick(event) {
 *   function foo(){ console.log(1) }
 *   }
 */
```

HTML 的 onclick 運作原理，相當於直接把文字當程式碼執行，
JS 則是實際執行 assign 的 callback 。
