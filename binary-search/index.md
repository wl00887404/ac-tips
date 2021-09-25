# Binary Search 二分搜尋法

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
猜得太小，表示答案在右邊，往右走，猜 6 ，  
猜得太大，表示答案在左邊，往左走，猜 2 ，  
最好的情境， 4 就猜中了，  
最壞的情境，剛好猜到 1 、 3 、 5 、 7 ，

用同樣的方法把 1 ~ 100 畫出來，  
你會發現 100 最壞的情境是走 7 次，  
每猜一個數字，剩下的搜尋範圍就剩下一半，  
7 不斷除 2 可以除 3 次， 100 不斷除 2 可以除 7 次，  
猜 1 ~ n ，最多要走 log<sub>2</sub> n 次，  
電腦科學稱 Binary Search 的時間複雜度是 O(log n) ，  
如果你對 log 不太熟，請參考下方的 [搜尋次數驗證](#搜尋次數驗證) 。

## 實作

每當 mid 並非目標的時候，將會更新上下界，  
而更新上下屆是否 +1 ，取決於上下界是包含與不包含，
因為 Math.random 的設計是回傳 0 ~ 0.9999999 ，  
通常在會將 left 設計為包含，而 right 設計成不包含，  
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

right 不包含的設計在搜尋 array 時很方便，  
可以直接設定 left = 0; right = array.length ，  
恰好符合 array 的每一個 index ：

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

## 搜尋次數驗證

depth 表示樹的深度，樹的深度同時也是最大搜尋次數，  
像是上述 1 ~ 7 的二分搜尋樹即為 depth = 3 的樹，  
對數不熟可以嘗試一一列出每個 depth ：

- depth 為 1  
  可以容納 1 個節點 ， 也就是小於 2 <sup>1</sup> 個元素，  
  => 小於 2 個元素時，最多只須猜 1 次。
- depth 為 2  
  可以容納 3 (`depth = 1` + 2 <sup>1</sup>) 個節點，也就是小於 2 <sup>2</sup> 個元素，  
  => 小於 4 個元素時，最多只須猜 2 次。
- depth 為 3  
  可以容納 7 (`depth = 2` + 2 <sup>2</sup>) 個節點，也就是小於 2 <sup>3</sup> 個元素，  
   => 小於 8 個元素時，最多只須猜 3 次。
- depth 為 4  
  可以容納 15 (`depth = 3` + 2 <sup>3</sup>) 個節點，也就是小於 2 <sup>4</sup> 個元素，  
  => 小於 16 個元素時，最多只須猜 4 次。
- depth 為 5  
  可以容納 31 (`depth = 4` + 2 <sup>4</sup>) 個節點，也就是小於 2 <sup>5</sup> 個元素，  
  => 小於 32 個元素時，最多只須猜 5 次。
- depth 為 6  
  可以容納 63 (`depth = 5` + 2 <sup>5</sup>) 個節點，也就是小於 2 <sup>6</sup> 個元素，  
  => 小於 64 個元素時，最多只須猜 6 次。
- depth 為 7  
  可以容納 127 (`depth = 6` + 2 <sup>6</sup>) 個節點，也就是小於 2 <sup>7</sup> 個元素，  
  => 小於 128 個元素時，最多只須猜 7 次。
