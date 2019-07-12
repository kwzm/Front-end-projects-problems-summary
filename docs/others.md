# 其它
[问题] textarea 里面输入带换行的文本在详情页里面没有体现出来  
[原因及方案] 1、替换'/r/n'为`<br/>`，2、定义`white-space: pre-wrap`  

[问题] 生产环境下出现样式覆盖的问题，因为动态加载导致，比如先访问 a 页面，加载 a.css，然后访问 b 页面，引入 b.css，b.css 后引入所以如果有重名的 class，就会覆盖 a.css 里面的样式  
[原因及方案] 解决方案通过修改 css 来解决

[问题] 新的页面会记录之前页面的滚动位置  
[原因及方案]  因为滚动的样式定义在 route 外，所以 route 对应的组件即便卸载页不会影响外面的滚动条的位置，解决方案：[https://react-router.docschina.org/web/guides/scroll-restoration](https://react-router.docschina.org/web/guides/scroll-restoration)

[问题] hash 路由无法用 hash 锚点，可以用 scrollIntoView 方法，但是在某些场景下会有问题，比如你设置了 header，你想让要显示的元素在 header 下方显示，但是由于 scrollIntoView 是根据浏览器视窗去滚动的所以它会忽略 header 这时你滚动的元素的一部分就可能被 header 遮挡  [原因及方案] 所以我自己封装了一个 react 组件[react-anchor-without-hasn](https://github.com/kwzm/react-anchor-without-hash)，可以定义滚动的 offset 

[问题] 搜索优化：一般我们对于用户输入搜索都会采用 debounce 进行优化减少服务端请求，但是假如用户输入的比较慢两次输入的字符在你设置的延迟时间之外，比如延迟间隔 500 你输入第一个字符 'k' 后隔了 500 再输入 'w' 这时会发送两条请求，我们知道 http 请求的响应时长不是固定的，如果第一次请求的响应时长比第二次请求的响应时长长就有可能发送第一次搜索结果覆盖第二次的搜索结果，这样就会给用户造成困扰。  
[原因及方案]解决方法就是设置一个数组，存储每次请求的 cancel 函数(这块需要根据自己采用的 ajax 库)，在每次请求之前先判断数组是否为空，如果不为空则先依次调用数组里面的 cancel 方法终止之前的请求，再发送请求 

[问题] iconfont symbol 模式下有些字体无法修改 color  
[原因及方案] [https://www.cnblogs.com/jopny/p/9454785.html](https://www.cnblogs.com/jopny/p/9454785.html)