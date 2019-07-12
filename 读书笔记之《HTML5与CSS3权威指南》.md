## 一、HTML5与HTML4的区别

---

### （一）新增的属性

- **表单相关的属性**
  - 自动获得焦点：可以对 `input(type=text)、select、textarea、button` 元素指定 `autofocus` 属性。
  - 输入框提示：可以对 `input(type=text)、textarea` 元素指定 `pleaceholder` 属性。
  -  表单声明：可以对 `input、output、select、textarea、button、fieldset` 指定 `form` 属性，声明它属于哪个表单，然后将其放置在页面上的任何位置，而不是表单之内。
  - 输入框非空校验：可以对 `input(type=text)、textarea` 元素指定 `required` 属性。该属性表示在用户提交的时候进行检查，检查该元素内一定要有输入内容。（但一般不要这么做）
  -  `input` 新增属性：`autocomplete,min,max,multiple,pattern,step`。同时还有一个新的 `list` 元素与 `datalist` 元素配合使用。`datalist` 元素与 `autocomplete` 属性配合使用。 `multiple` 属性允许在上传文件时一次上传多个文件。

- **链接相关的属性**
  - 为 a 元素添加了 `media、downolad、ping` 属性，其中，`media` 属性规定目标 `URL` 是什么类型的媒介。`download` 属性用于让用户下载目标链接所指向的资源，而不是直接打开该目标链接。
  - 为 `link` 元素增加了新属性 `sizes` 。该属性可以与 `icon` 元素结合使用，该属性指定关联图标（icon元素）的大小。
  - 为 `base` 元素增加了 `target` 属性。

- **全局属性**

  所谓全局属性，就是指所有元素都可以使用的属性。

  - `hidden` 属性 —— 元素是否可见。

- **其他属性**
  - 为 `script` 元素增加 `async` 属性，定义脚本是否异步执行。
  - 为 `style` 元素增加 `scoped` 属性，用来规定样式的作用范围，比如只对页面上某个树起作用。

---

### （二）新增的元素

- `article` —— 代表文档、页面或应用程序中独立的、完整的、可以独立被外部引用的内容。它可以是一篇博客或文章、一篇论坛帖子、一段用户评论等。在 `article` 内通常还有自己的标题（用 `header` 描述）。
- `section` —— 用来对网站或应用程序页面上的内容进行分块，一个 `section` 元素通常由内容及标题组成。强调的分块或分段。
- `nav` —— 可以用来作为页面导航的链接组。里面的元素还可以像以往那样 `ul>li` 。
- `aside` —— 用来表示当前页面或文章的附属信息部分，它可以包含与当前页面或主要内容相关的引用、侧栏、广告等。
- `header` —— 头部，可以是整个页面的头部，也可以是某块区域的头部。
- `footer` —— 尾部，可以是整个页面的尾部，也可以是某块区域的尾部。
- `main` —— 表示网页中的主要内容，一个网页只能放一个 `main` 元素，而且不能放在 `article,aside,footer,header,nav` 里面，不能包含网站LOGO，版权信息、公共搜索等内容。

---

### （三）多媒体API

- **视频播放**

  在 `HTML5` 中新增了元素 `video` 来播放网络上的视频或电影，只要浏览器支持 `HTML5` ，那么就不需要再使用第三方插件了。用法：

  ```html
  <video width="640" height="360" src="test.mp4">
  	您的浏览器不支持video元素
  </video>
  ```

  用法很简单，只要设定好元素的宽高，并把视频的地址给元素的 `src` 属性就可以了。

- **音频播放**

  在 `HTML5` 中新增了元素 `audio` 用于播放网络上的音频。

  ```html
  <audio src="test.mp3" >
  	您的浏览器不支持audio元素
  </audio>
  ```

- **公共属性**
  - `src` —— 上面就提到过了，用于引入资源。
  - `autoplay` —— 指定资源是否在页面加载完成后自动播放，直接在标签上加上该属性表示自动播放。
  - `preload` —— 指定资源是否预加载。如果使用预加载，浏览器会预先缓存视频或音频数据，这样可以加快播放速度，因为播放时数据已经缓冲好了。该属性有三个可选值：`none,metadata,auto` ，默认值为 `auto` 。`none` 表示不进行预加载；`metadata` 表示只预加载媒体的元数据（媒体字节数、第一帧、播放列表、持续时间等）；`auto` 表示预加载全部视频或音频。
  - `poster` —— 这是 `video` 特有的属性，表示视频不可用时，可以使用该元素向用户展示一个图片。
  - `loop` —— 是否循环播放视频或音频。
  - `controls` —— 是否为视频或音频添加浏览器自带的播放用的控制条。

- **公共方法**
  - `play` —— 使用该方法来播放媒体，自动将元素的 `paused` 属性的值变为 `false` 。
  - `pause` —— 使用该方法来暂停播放，自动将元素的 `paused` 属性改为 `true` 。
  - `load` —— 使用该方法重新载入媒体进行播放。

---

## 二、History API

在 `HTML5` 中，新增了一个 `History API`，该 `API` 以一种新的、革命性的方式来切换浏览器中所需显示网页的 `URL` 地址。它其实是一个 `window.history` 对象相关的 `API` 。

- `window.history.back()` —— 返回或后退。
- `window.history.forward()` —— 前进
- `window.history.go()` —— 去往某个 `URL`

---

## 三、本地存储

在 `HTML5` 中的一个非常重要的功能就是在客户端保存数据的 `Web Storage` 。具体的说，它分为两种：

- `sessionStorage` —— 将数据保存在 `session` 对象中，所谓 `session` ，是指用户在浏览某个网站时，从进入网站到浏览器关闭所经过的这段时间，也就是用户浏览这个网站所花费的时间。`session` 对象可以用来保存这段时间内所要求保存的任何数据。
- `localStorage` —— 将数据保存在客户端本地的硬件设备（通常指硬盘）中，即使浏览器关闭了，该数据仍然存在，下次打开浏览器访问时仍然可以继续使用。以上两者的区别在于，`sessionStorage` 为临时保存，而 `localStorage` 为永久保存。

常用的操作方法：

- `sessionStorage` 
  - 保存数据的方法：`sessionStorage.setItem(key,value)` 或 `sessionStorage.key=value`
  - 读取数据的方法：`sessionStorage.getItem(key)` 或 `sessionStorage.key`

- `localStorage` 
  - 保存数据的方法：`localStorage.setItem(key,value)` 或 `localStorage.key=value`
  - 读取数据的方法：`localStorage.getItem(key)` 或 `localStorage.key`
  - 总记录数：`localStorage.length`
  - 清空：`localStorage.clear()`

