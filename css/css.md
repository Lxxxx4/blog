##### 文字颜色渐变

https://codepen.io/lxxxx4/pen/MWjRmaN

```html
<div class="fill-text">hello world</div>
<style>
.fill-text {
  color: bule;
  background-image: -webkit-linear-gradient(bottom,red,#fd8403,#ff0);
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
}
</style>
```

