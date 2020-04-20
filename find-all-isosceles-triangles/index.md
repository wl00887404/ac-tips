# 在三邊之和小於等於 20 的情況下，找出所有的等腰三角形（不含正三角形）組合

因為等腰三角形，必定會有兩邊一樣長，  
以 x 表示兩個等長的邊， y 表示第三邊，  
依題意會得到以下條件：

1. x > 0
   > 三角形邊長一定大於 0
2. y > 0
   > 三角形邊長一定大於 0
3. 2x > y
   > 三角形兩邊之合必定大於第三邊

依據以上條件，做出此圖：

![0](https://wl00887404.github.io/ac-tips/find-all-isosceles-triangles/0.jpg)

另外依據題目需求，得到以下條件：

1. 2x + y <= 20
   > 三邊之合小於等於 20
2. x != y
   > 不含正三角形

得此圖：

![1](https://wl00887404.github.io/ac-tips/find-all-isosceles-triangles/1.jpg)

找出範圍內所有正整數解：

![2](https://wl00887404.github.io/ac-tips/find-all-isosceles-triangles/2.jpg)

列舉所有正整數解，共有兩個方向：

1. 依據 10 > x 來找
   > 因為 2x + y <= 20 ， x 最大值為 9 (x < 10) ，由 (2, 1), (2, 3), ... ,(9, 1), (9, 2) 一一列舉
2. 依據 2x + y = 3, 4, 5 來找
   > 因為 2x + y <= 20 ，表示要找 2x + y = 3, 4, ... , 20 的解，一一列舉

以下為範例程式碼：

實作 1 ：

```javascript
let count = 0;

for (let x = 1; x < 10; x++) {
  for (let y = 1; 2 * x > y && x * 2 + y <= 20; y++) {
    if (x != y) {
      console.log(`發現等腰三角形！三邊長分別為 ${x} ${x} ${y}`);
      count++;
    }
  }
}

console.log(`共找到 ${count} 組等腰三角形`);
```

實作 2 ：

```javascript
let count = 0;

for (let i = 3; i <= 20; i++) {
  let x = 1;

  while (true) {
    let y = i - x * 2;

    if (y < 1) break;

    if (x != y && x * 2 > y) {
      console.log(`發現等腰三角形！三邊長分別為 ${x} ${x} ${y}`);
      count++;
    }

    x++;
  }
}

console.log(`共找到 ${count} 組等腰三角形`);
```
