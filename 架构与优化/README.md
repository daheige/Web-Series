# Web 应用的架构与优化

# 性能调优

从桌面浏览器到移动互联网的时代，用户体验毫无疑问都是重中之重，而 Web 页面的性能则是整体体验的基础。所谓高性能的网站，直观来说，即是用户能够快速打开页面展示网页内容，并能流畅的浏览网页，同时尽可能地降低页面资源占用。移动端的硬件条件，网络条件相对于桌面端，会复杂的多，设备类型多样，硬件配置参差不齐，分辨率碎片化，网络状况在移动过程中稳定性，速率都会变化，而对于一个页面到达用户的终端展示，会经过，用户发起请求，服务端接受请求，服务端处理请求，返回响应内容，在用户终端的浏览器展示内容，用户操作页面发起其他页面时间，而这个过程中任何一个环节的延迟都会造成性能瓶颈，降低用户继续访问的可能性，所以我们在服务器端，浏览器端，网络加载，多个方面做了一系列的优化工作。

![](https://i.postimg.cc/Hxsn6grJ/Web-Tuning-Web.png)

In 2019, the dominant costs of processing scripts are now download and CPU execution time. User interaction can be delayed if the browser’s main thread is busy executing JavaScript, so optimizing bottlenecks with script execution time and network can be impactful.

随着应用复杂度的不断增加，我们发现脚本解析与处理的瓶颈在于脚本的下载与 CPU 执行这两个阶段：而当 CPU 忙于执行 JavaScript 的时候，自然会难以及时响应用户的操作，从而造成卡顿的感觉。因此，这个阶段我们优化的重点就是网络下载以及脚本执行。

- 对于降低下载时间，保持JavaScript包的小巧，特别是对于移动设备。 小型捆绑包可提高下载速度，降低内存使用率并降低CPU成本。避免只有一个大捆; 如果捆绑超过~50-100 kB，则将其拆分为单独的较小捆。通过 HTTP/2 多路复用，可以同时传输多个请求和响应消息，从而减少额外请求的开销。在移动设备上，你会希望运输更少，特别是因为网络速度，但也保持低内存使用率。

- 对于脚本执行效率的优化，避免长期任务可以使主线程保持忙碌，并可以推断出页面交互的时间。 下载后，脚本执行时间现在是主要成本。避免使用大型内联脚本（因为它们仍然在主线程上进行了解析和编译）。 一个好的经验法则是：如果脚本超过1 kB，请避免内联（也因为1 kB是代码缓存为外部脚本启动时）。

总的优化策略会从[资源请求与缓存、关键渲染路径、图片优化、脚本解析与执行、页面布局与渲染策略、交互与动画、移动端优化、PWA]()等几个角度进行考虑。

# 链接

- https://zhuanlan.zhihu.com/p/66398148
