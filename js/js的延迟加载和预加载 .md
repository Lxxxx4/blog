### 延迟加载(懒加载)

> 原理：当数据真正被需要的时候才加载。
>
> 目的：减少无所谓的性能开销。

#### 实现延迟加载的集中方法

- > 将`<script>`标签放在`<body>`之后

  等浏览器进行完渲染后再执行js，目的是提升用户体验。

  原理：浏览器的js引擎和渲染引擎都是在主线程中，其中一个执行必定会导致另一个挂起。

- > defer属性

  带有defer属性的脚本将会延迟到解析完`</html>`之后执行，且所有的defer脚本都是按顺序执行的。

- > async属性

  带有async属性，加载和渲染后续文档元素的过程和脚本的**加载与执行**并行进行。

- > 动态创建dom的形式加载脚本

  添加一个事件监听器onload，等到页面加载完成时动态加载脚本。

- > 使用setTimeout延迟方法的加载时间

  ​	

### 预加载

> 原理：提前加载图片，当需要时直接从本地缓存中渲染。
>
> 目的：牺牲能来换取用户体验。

#### 实现预加载的集中方法

- css实现

  通过css的background属性将需要加载的图片预加载到屏幕外的背景上。等真正需要时，就可以直接从本地缓存中获取。

  ```css
  #preload-01 { background: url(http://domain.tld/image-01.png) no-repeat -9999px -9999px; }
  ```

- js预加载图片

  ```js
  // 预加载图片而不插入到文档中
  function preloader() {
      if (document.images) {
          var img1 = new Image();
          var img2 = new Image();
          var img3 = new Image();
          img1.src = "http://domain.tld/path/to/image-001.gif";
          img2.src = "http://domain.tld/path/to/image-002.gif";
          img3.src = "http://domain.tld/path/to/image-003.gif";
      }
  }
  ```

- 通过ajax来预加载js，css等资源

  ```JS
  window.onload = function() {
    	//  1000 毫秒的超时是为了防止脚本挂起，而导致正常页面出现功能问题。
      setTimeout(function() {
          // XHR to request a JS and a CSS
          var xhr = new XMLHttpRequest();
          xhr.open('GET', 'http://domain.tld/preload.js');
          xhr.send('');
          xhr = new XMLHttpRequest();
          xhr.open('GET', 'http://domain.tld/preload.css');
          xhr.send('');
          // preload image
          new Image().src = "http://domain.tld/preload.png";
      }, 1000);
  };
  ```

  