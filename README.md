# 初试 nuxt.js 之心得体会
> 最近刚忙完公司 M 站的建设。由于公司站点大都属于广告性质的，对 SEO 的要求很高，于是就想到了服务器端渲染；由于之前使用或 vue ，所以就选了 nuxt.js 。这东西和 next.js 是师出同门，只不过 next.js 是 react 的服务器端渲染框架。

先解释下什么是服务器端渲染（ssr：server side rendering）。
现在常规的页面往往都是单页（spa）应用，浏览器先向服务器端请求加载一段 html，这段 html 往往很简单，主要作用是用来引入 css 和 js 文件，并作为数据的插入点。真正的内容数据是在解析 js 之后通过 js 中发出的请求加载的。
所以，这样的站点往往刚刚打开是会出现短暂的白屏（因为没有内容，也没有样式）；并且对 SEO也不太友好（因为一般的搜索引擎只会加载HTML，而不会去异步加载并解析 js，所以这时候搜索引擎就看不到你真正的内容数据了，SEO自然就不会太好。在浏览器的 sources 面板或者终端工具通过 curl 命令请求的内容大概就是搜索引擎能看到的东西。）

而 ssr 就是在服务器端那里完成数据和模板的拼接组装成 html 输出给浏览器（这里的渲染并发浏览渲染出页面那样，只是拼装而已，本质还是一堆字符串），这样浏览器和搜索引擎获取的内容是相同的（包括数据）；另外由于浏览器获取的是完整的 HTML 所以就可以拿来直接渲染显示给用户，所以白屏基本可以忽略不计。所以 ssr 就和访问一般的静态页面看起来差不多，只不过可以随时更新数据而不用去改源码。

一图胜千言，上图：

既然 ssr 这么好，为什么 spa 还那么流行呢？但凡一个事物都有其适用性和两面性。现阶段而言，ssr 比较适合对 SEO 要求比较高的，而 spa 则适合对 SEO 没什么要求的，涉及到用户个人状态的站点，比如网页聊天工具等。
就 ssr 的两面性而言，正如热力学第一定律，能量的总量是不变的只不过从一个地方转移到另一个地方。而 HTML 总是要拼接的，页面总是要渲染的。ssr 就是将HTML 的拼接工作转移到了服务器端，每个用户访问一遍，服务器都要去渲染一次，一旦短时间有大量用户请求，这对服务器的压力可想而知。但是问题就是用来解决的，有问题肯定有办法解决。

服务器端的压力主要有两点，一是频繁的 HTML 拼接导致 CPU 使用率过高，二是拼接的 HTML 和一些相关数据文件遗留在内存中导致内存使用量居高不下。


nuxt的特点

服务器端渲染的常见问题及解决办法

项目总结