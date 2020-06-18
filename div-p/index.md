# div vs p

p 是 paragraph ，paragraph 底下只有文字，
也就是 p 底下只能包含 inline 元素（ img 、 span 、 a ...） ，
如果底下有 block 元素（ div 、 p 、ul ）都是不合法的，
像是這樣：

```html
<p>
  <p>foo</p>
</p>

<p>
  <div>bar</div>
</p>

<p>
  <ul>
     <li>apple</li>
     <li>banana</li>
     <li>cat</li>
  </ul>
</p>
```

這些錯誤會被瀏覽器自動修正，
當然結果並不如原本預期，以下是修正結果：

![fixed](https://wl00887404.github.io/ac-tips/div-p/fixed.png)

```html
<p></p>
<p>foo</p>
<p></p>

<p></p>
<div>bar</div>
<p></p>

<p></p>
<ul>
  <li>apple</li>
  <li>banana</li>
  <li>cat</li>
</ul>
<p></p>
```

如果改用 div 就不會有任何問題，

總而言之：

- div  
  division ，純粹的容器，想放什麼在裡面都可以。
- p  
  paragraph ，段落，體內只容許 inline 元素。
