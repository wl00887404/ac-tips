# 不要使用 Number()

如果傳入參數為 `字串` ，  
建議使用 `parseInt` 與 `parseFloat` ，  
Number() 較不直觀，

```javascript
Number(); // 0
Number(""); // 0
Number(null); // 0
Number("150cm"); // NaN

parseInt(); // NaN
parseInt(""); // NaN
parseInt(null); // NaN
parseInt("150cm"); // 150
```

在字串解析上，  
未輸入的情境， Number() 會輸出 0 ，  
150cm 的輸入也無法解析出 150 ，  
不符合一般的預期，

另外 parseInt 也可以用來轉換其他進位，

```javascript
parseInt("100", 10); // 100
parseInt("100", 2); // 4
parseInt("100", 8); // 64
parseInt("100", 16); // 256
```

第二個參數預設為 10 ，也就是轉換成十進位，  
為了可讀性，建議把兩個參數完整寫出來。
