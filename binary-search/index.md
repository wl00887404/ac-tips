# Binary Search

在完成 `【挑戰題】10 次內猜對` 之後，成功發現了一種簡單的作法：

1. 猜中間那個
2. 如果相等，那就找到了
3. 如果太大，把此數設為上界，重複 1
4. 如果太小，把此數設為下界，重複 1

此刻有沒有覺得，這根本沒有在「猜」數字，是在找數字吧！  
這種從中間開使搜尋，每次都可以縮小一半的範圍的搜尋法，  
正是 `Binary Search 二分搜尋法` ，

Binary Search 是在一個搜尋 `已排序的陣列` 的最佳作法，  
從 1 ~ 100 找一個數字，正好適用 Binary Search 。

## 為什麼 Binary Search 很快

從 1 ~ 100 猜對數字， 其實並不需要 10 次，  
Binary Search 只需要 7 次就可以猜對了，  
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
7 不斷除 2 可以除 3 次， 100 不斷除 2 可以除 7 次，  
猜 1 ~ n ，最多要走 log<sub>2</sub> n 次，  
電腦科學稱 Binary Search 的時間複雜度是 除## 實作

每當 mid 並非目標的時候，將會更新上下界，  
而更新上下屆是否 +1 ，取決於上下界是包含與不包含，  
通常在會將 left 設計為包含，而 right 設計成不包含，  
right 不包含的設計在搜尋 array 時很方便，  
可以直接設定 left = 0; right = array.length ，  
恰好符合 array 的每一個 index ，

以下為範例程式碼：

```javascript
const answer = Math.floor(Math.random() * 100) + 1;

let left = 1; // 包含
let right = 101; // 不包含

while (true) {
  let mid = Math.floor((left + right) / 2);

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
    // 下一次範圍為 mid + 1 （包含） ~ right （不包含）
    left = mid + 1;
  }
}
```

在已排序的陣列中做搜尋：

```javascript
const array = [1, 4, 7, 9, 13];
const target = 9;

let left = 0;
let right = array.length;

while (true) {
  let mid = Math.floor((left + right) / 2);

  if (left >= right) {
    console.log(`array 中沒有 ${target}`);
    break;
  }

  if (array[mid] === target) {
    console.log(`找到了！ array[${mid}] 就是 ${target}`);
    break;
  }

  if (array[mid] > target) {
    right = mid;
  } else {
    left = mid + 1;
  }
}
```
