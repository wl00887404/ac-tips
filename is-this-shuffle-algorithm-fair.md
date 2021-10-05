# 這個洗牌演算法是公平的嗎？

## 怎麼樣的洗牌演算法是公平？

一個公平的演算法，在洗牌之後每一種組合出現的機率應該相等，  
舉例來說，當 `shuffle([1, 2, 3])` 以下組合出現的機率應該相等：

- [1, 2, 3]
- [1, 3, 2]
- [2, 3, 1]
- [2, 1, 3]
- [3, 0, 1]
- [3, 1, 0]

其中 `[0, 1, 2]` 特別重要，  
一個公平的洗牌演算法洗完的結果，是有可能跟原本相同。

## 如何檢驗洗牌演算法是否公平？

就與擲骰子相同，每面出現的機率是 1 / 6 ，  
擲連續擲 600 次，最終結果每個數字應該在 100 上下，  
就用這個邏輯，我們來檢驗 Math.random ：

```javascript
// 隨機產生 1 ~ 6 的數字
const rollADice = () => Math.floor(Math.random() * 6) + 1;

const frequency = {};

for (let i = 0; i < 600; i++) {
  const result = rollADice();

  if (frequency[result] === undefined) {
    frequency[result] = 0;
  }

  frequency[result]++;
}

console.table(frequency);
```

執行結果：

| 數值 | 出現次數 |
| ---- | -------- |
| 1    | 107      |
| 2    | 98       |
| 3    | 96       |
| 4    | 96       |
| 5    | 100      |
| 6    | 103      |

## 一個不公平的洗牌演算法

使用 array.sort + Math.random 洗牌，  
雖然是可以成功洗牌，但卻是是不公平的，  
可以參考此 [hackmd](https://hackmd.io/@sysprog/S1jR0mHfN) 證明，但在此我們直接以重複執行檢驗：

```javascript
const shuffle = array => {
  /**
   * sort 需要傳入一個 function
   * 此 function 會傳入陣列中兩個元素 a 、 b 做比較
   *
   * 當此 function 回傳小於 0 時，
   * a 會排在 b 前面，即為 [a, b]
   *
   * 當此 function 回傳大於 0 時
   * a 會排在 b 後面，即為 [b, a]
   *
   * 所以隨機傳入 -0.5 ~ 0.49999 讓他隨機排序
   */
  return array.sort(() => Math.random() - 0.5);
};

const frequency = {};

for (let i = 0; i < 600; i++) {
  // 在此直接將 shuffle 完的結果
  // 轉換成字串，作為 frequency 的 key
  const result = shuffle([1, 2, 3]).join(' ');

  if (frequency[result] === undefined) {
    frequency[result] = 0;
  }

  frequency[result]++;
}

console.table(frequency);
```

執行結果：

| 數值  | 出現次數 |
| ----- | -------- |
| 1 2 3 | 231      |
| 1 3 2 | 36       |
| 2 1 3 | 69       |
| 2 3 1 | 47       |
| 3 1 2 | 42       |
| 3 2 1 | 175      |

可以觀察到 `[1, 2, 3]` 與 `[3, 2, 1]` 非常容易被選中，  
想當然爾這不是個公平的洗牌方法。

## Fisher–Yates 演算法

直接複製課文的演算法，依樣畫葫蘆：

```javascript
const shuffle = array => {
  for (let index = array.length - 1; index > 0; index--) {
    const randomIndex = Math.floor(Math.random() * (index + 1));
    const temp = array[index];
    array[index] = array[randomIndex];
    array[randomIndex] = temp;
  }

  return array;
};

const frequency = {};

for (let i = 0; i < 600; i++) {
  const result = shuffle([1, 2, 3]).join(' ');

  if (frequency[result] === undefined) {
    frequency[result] = 0;
  }

  frequency[result]++;
}

console.table(frequency);
```

執行結果：

| 數值  | 出現次數 |
| ----- | -------- |
| 1 2 3 | 106      |
| 1 3 2 | 95       |
| 2 1 3 | 104      |
| 2 3 1 | 104      |
| 3 1 2 | 101      |
| 3 2 1 | 90       |

所以有結果出現次數十分相近，真棒！

## 承 Fisher–Yates 演算法， random 有可能與 index 相同，這樣沒問題嗎？

在 Fisher-Yates 演算法， randomIndex 的寫法為：

```javascript
const randomIndex = Math.floor(Math.random() * (index + 1));
```

randomIndex 與 index 是有可能出現一樣的數字的：

```javascript
// $_ 表示前一次的執行結果
Math.random()     // 0 <= result < 1
$_ * (index + 1)  // 0 <= result < (index + 1)
Math.floor($_)    // 0 <= result < (index + 1)
                  // 等同於 0 <= result <= index
```

如果 randomIndex 剛好全等於 index ，那不就沒有洗到牌嗎？  
是不是應該以 index 取代 index + 1 ，讓 randomIndex 不可能等於 index ，

答案當然是否定的，  
因為一個公平的洗牌演算法，是可能會出現是原本的組合的，  
如果只是想避免洗牌完的結果與原本相同，那這更是失敗的寫法，  
不過先讓當然我們以同樣的方式驗證：

```javascript
const shuffle = array => {
  for (let index = array.length - 1; index > 0; index--) {
    const randomIndex = Math.floor(Math.random() * index);
    const temp = array[index];
    array[index] = array[randomIndex];
    array[randomIndex] = temp;
  }

  return array;
};

const frequency = {};

for (let i = 0; i < 600; i++) {
  const result = shuffle([1, 2, 3]).join(' ');

  if (frequency[result] === undefined) {
    frequency[result] = 0;
  }

  frequency[result]++;
}

console.table(frequency);
```

執行結果：

| 數值  | 出現次數 |
| ----- | -------- |
| 2 3 1 | 294      |
| 3 1 2 | 306      |

原本應該出現 6 種組合，意外的只剩下 2 種，

重新檢視這寫法的執行結果，  
第一次迴圈會從 index 為 2 進行洗牌時，  
randomIndex 可能為 0 、 1 ，也就是拿 3 與 1 、 2 進行交換，  
此時的陣列為 `[3, 2, 1]` 或 `[1, 3, 2]` ，  
第二次以 index 為 1 進行洗牌，只能與 index 為 0 進行交換，  
註定結果為 `[2, 3, 1]` 或 `[1, 3, 2]` ，

這樣的寫法不只會讓 `[1, 2, 3]` 消失，也會意外讓其他組合消失，  
如果真的希望洗完牌不會出現原本的組合，  
應該出現此結果時就再進行一次洗牌：

```javascript
const shuffle = array => {
  // 複製原本的 array
  const clone = array.concat();
  const isEqual = () => {
    for (let i = 0; i < array.length; i++) {
      if (array[i] !== clone[i]) {
        return false;
      }
    }

    return true;
  };

  while (true) {
    for (let index = array.length - 1; index > 0; index--) {
      const randomIndex = Math.floor(Math.random() * (index + 1));
      const temp = array[index];
      array[index] = array[randomIndex];
      array[randomIndex] = temp;
    }

    // 如果 array 與 clone 不同就結束洗牌
    if (!isEqual(array, clone)) break;
  }

  return array;
};

const frequency = {};

for (let i = 0; i < 600; i++) {
  const result = shuffle([1, 2, 3]).join(' ');

  if (frequency[result] === undefined) {
    frequency[result] = 0;
  }

  frequency[result]++;
}

console.table(frequency);
```

執行結果：

| 數值  | 出現次數 |
| ----- | -------- |
| 1 3 2 | 117      |
| 2 1 3 | 125      |
| 2 3 1 | 111      |
| 3 1 2 | 129      |
| 3 2 1 | 118      |

如此出現次數分佈才會比較理想。
