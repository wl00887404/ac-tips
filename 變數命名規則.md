# 變數命名規則

> 好的變數名稱，要充分表達「他為何會在這裡、它有什麼作用、該怎麼使用它 」。

## 變數用名詞，函數用動詞，陣列使用複數型態

以名詞、動詞區分，  
命名不會重疊，避免意外覆蓋。

```javascript
var students = [];

function getStudent(index) {
  return students[index];
}

function addStudent(student) {
  students.push(student);
}

function removeStudent(index) {
  students.splice(index);
}

var randomIndex = Math.ceil(Math.random() * 10);
var chosenStudent = getStudent(randomIndex);
```

students 為 `名詞`，意謂 `所有學生們` ，  
getStudent 是 `動詞` ，可猜測為 `取得某 index 的學生的動作`，  
addStudent 為 `新增一個學生的動作` ，  
randomIndex 為 `隨機的 index` ，  
chosenStudent 為 `隨機選出來的學生` ，  
就算看不懂程式碼，也可以從命名推測用法。

## 一些常見的錯誤

### 無意義的名稱

```javascript
// bad
var a = "foo";

// ok
for (var i = 0; i < 10; i++) {}
```

避免無意義的變數命名，  
譬如說 `a` 、`b` 、`c` ，  
但在迴圈中 `i` 、 `j` 為常見的寫法，不限於此。

### 無意義的縮寫

```javascript
// bad
var ans; // answer
var cate; // category
var cnt; // count

// ok
var str; // string
var num; // number
var db; // database
```

ans 為 answer 的縮寫，  
但也只少了兩個字母，  
沒有縮寫的必要，不如全寫出保留可讀性。

cate 為 category 的縮寫，  
category 一般縮寫為 `cat.` ，但不能使用 `.` ，  
cate 不好聯想，不推薦使用。

cnt 為 count 的縮寫，  
除了無法理解為什麼要縮寫之外，  
這還是一個無法念出來的字，  
會增加溝通的障礙。

但常用的程式縮寫，不限於此。

### 避免誤導

```javascript
var number = "1";
```

number 暗示這是變數是 `數字` ，  
但是實際上卻是字串。
