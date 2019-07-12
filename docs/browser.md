# 浏览器相关的问题
- IE9 不支持 flex 布局
- create-react-app 提供的 react-app-polyfill 只是对某些 ES6 的 API 做了兼容，所以用 @babel/polyfill 替代了 react-app-polyfill
- dev 环境不支持 IE9：在 IE9 上打开 dev 环境发现了很多问题，不仅有 webpack-dev-server 存在的兼容性问题，还有一些其它第三方库存在的兼容性问题，主要有以下问题（因为问题太多所以最后我放弃了IE9下的dev环境）：
    - 首先是 bundle.js 文件里报 const map 未定义是因为 webpack-dev-server 从 2.7.1 后不支持 IE9
    - 如果是 vendor.js 文件里报 setPrototypeOf 未定义是因为 create-react-app 引入的 react-dev-utils/webpackHotDevClient 文件里面有一个 chalk 的包使用了这个 ES6 的方法，而 @babel/polyfill 的编译是基于__proto__，而 IE9 并不支持__proto__，所 以@babel/polyfill 无效
- 调试的时候保证是 IE9 的标准模式
- 线上的项目无法在 IE9 上打开的原因：IE9 默认采用的文档模式是 IE7。解决方案：加入`<meta http-equiv="X-UA-Compatible" content="IE=edge">`，注意顺序：
    >The X-UA-Compatible header is not case sensitive; however, it must appear in the header of the webpage (the HEAD section) before all other elements except for the title element and other meta elements.
- IE9 Spin 元素包裹的内容无法点击 原因：Spin 设置的 css 属性 pointer-events 不兼容IE9。解决方案：升级 antd
- IE9 设置 img height 为百分比并不能像chrome浏览器里一样按比例缩放，只能设置 width
- IE9 上 css 样式没有浏览器前缀导致样式错误，原因 autoprefixer 对应的 browserslist 没写对没能将 IE9 包含进去
- 默认使用 webkit 内核：`<meta name="renderer" content="webkit" />` 