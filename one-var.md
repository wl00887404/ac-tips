# 一行宣告一個變數

```javascript
// good
var foo;
var bar;

// bad
var foo, bar;
```

單行宣告是合法的語法，  
但單行宣告會造成很多 `快捷鍵無法使用` ，很不方便。

舉例來說，  
<kbd>Ctrl</kbd> + <kbd>/</kbd> ，整行註解，  
<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>k</kbd> ，整行刪除，  
另外在沒有選取的情況下，  
<kbd>Ctrl</kbd> + <kbd>C</kbd> ，整行複製，  
<kbd>Ctrl</kbd> + <kbd>x</kbd> ，整行剪下，  
真的很不方便。

另外，在 [anirbnb](https://github.com/airbnb/javascript#variables--one-const) 、 [google](https://google.github.io/styleguide/jsguide.html#features-one-variable-per-declaration) 的 style guide 皆有 follow 這條規則。
