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
