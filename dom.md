# DOM

參考 [樹狀結構與 DOM 節點](https://lighthouse.alphacamp.co/courses/40/units/5674) 。

## Node Type

- 元素節點 element node  
  &lt;img /&gt; 、 &lt;div&gt;&lt;/div&gt; ... ，HTML 標籤。
- 文字節點 text node  
  &lt;div&gt;text&lt;/div&gt; 中間的 text ，在 HTML 標籤之間的純文字。
- comment node  
  &lt;!--comment--&gt; ，註解標籤。

## NodeList vs HTMLCollection

- HTMLCollection
  只有 element node 。
- NodeList
  除了 element node 以外，還會有 text node 、 comment node 。
  
特別注意，在 [地雷：看不見的空白文字節點](https://lighthouse.alphacamp.co/courses/40/units/5679) 中有解釋到，  
 #text ，也就是 text node ，  
正是 element node 後方的換行，  
所以 NodeList 才會 #text 與 li 互相間隔。

NodeList 是允許有其他種的 node ，並不是一定有，  
CSS Selector 並沒有能夠抓 text node 的 selector ，  
可以把 NodeList 當成是 HTMLCollection 的宇集，  
另外 NodeList 是固定的，只要一 query 出來就不會變了，  
而 HTMLCollection 是動態的，內容更新也跟著更新，可以參考 [這裡](https://codepen.io/wl00887404/pen/ZEbjXNr?editors=1010) 。

## innerHTML vs innerText vs textContent

### textContent

所有 node 都有這個屬性，值是原本的內容（不包含 html tag ）。

### innerHTML

但只有 element node 才有這個屬性，值是原本的內容（包含 html tag ）。

### innerText

但只有 element node 才有這個屬性，在界面中看起來的樣子。

範例程式碼請參考 [這裡](https://codepen.io/wl00887404/pen/zYvLEdp?editors=1010) 。
