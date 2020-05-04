# Binary Search

在完成 `【挑戰題】10 次內猜對` 之後，成功發現了一種簡單的作法：

1. 猜中間那個
2. 如果相等，那就找到了
3. 如果太大，把此數設為上屆，重複 1
4. 如果太小，把此數設為下屆，重複 1

此刻有沒有覺得，這根本沒有在『猜』數字，是在找數字吧！  
正式介紹 `Binary Search 二分搜尋` ，  
Binary Search 是在一個 `已排序` 的陣列做搜尋的最佳解，  
從 1 ~ 100 找一個數字，正好適用 Binary Search，  
其實不只是在 10 次內猜對， Binary Search 只需要 7 次就可以猜對了，  
要證明這點，我們先來觀察從 1 ~ 7 猜中目標，

![0](https://wl00887404.github.io/ac-tips/binary-search/0.png)

從最上面開始走，猜 4 ，  
猜得太小往右走，猜 6 ，  
猜得太大往左走，猜 2 ，  
最好的情境， 4 就猜中了，  
最壞的情境，剛好猜到 1 、 3 、 5 、 7 ，

用同樣的方法把 1 ~ 100 畫出來，  
你會發現 100 最壞的情境是走 7 次，  
每猜一個數字，剩下的搜尋範圍就剩下一半，  
7 不斷 / 2 可以除 3 次， 100 不斷 / 2 可以除 7 次，  
猜 1 ~ n ，最多要走 log<sub>2</sub> n 次，  
電腦科學稱 Binary Search 的時間複雜度是 O(log n) ，

以下為範例程式碼：

```javascript
const answer = Math.floor(Math.random() * 100) + 1;

let left = 1; // 包含
let right = 101; // 不包含
let mid;

while (true) {
  if (left >= right) {
    // 左右界重疊，沒數字猜了
    console.log(`正確答案是 ${answer} ，並不在範圍內 :(`);
    break;
  }

  mid = Math.floor((left + right) / 2);

  if (mid === answer) {
    console.log(`猜到了！答案就是 ${mid}`);
    break;
  }

  if (mid > answer) {
    console.log(`猜 ${mid} ，太大了！`);
    // 下一次範圍為 left （包含） ~ mid （不包含）
    right = mid;
  } else {
    console.log(`猜 ${mid} ，太小了！`);
    // 下一次範圍為 mid + 1 （包含） ~ right （不包含
    left = mid + 1;
  }
}
```
