# 用 map 、 join 取代 forEach

## Before

```javascript
const fruits = ["頻果", "香蕉", "橘子", "檸檬", "西瓜"];

function render() {
  let result = "<ul>";

  fruits.forEach(fruit => {
    result += `<li>${fruit}</li>`;
  });

  return result + "</ul>";
}
```

## After

```javascript
const fruits = ["頻果", "香蕉", "橘子", "檸檬", "西瓜"];

function render() {
  const lis = fruits
    .map(fruit => {
      return `<li>${fruit}</li>`;
    })
    .join("");

  return `<ul>${lis}</ul>`;
}
```
