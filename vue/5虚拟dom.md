# 1虚拟dom是什么

使用js对象来描述dom

操作 DOM 慢，js运行效率高。我们可以将DOM对比操作放在JS层，提高效率。
 因为DOM操作的执行速度远不如Javascript的运算速度快，因此，把大量的DOM操作搬运到Javascript中，运用patching算法来计算出真正需要更新的节点，最大限度地减少DOM操作，从而显著提高性能。

总结：Vue.js通过编译将模版转换成渲染函数(render)，执行渲染函数就可以得到一个虚拟节点树(虚拟DOM)，虚拟节点树(虚拟DOM)提供虚拟节点vnode和对新旧两个vnode进行比对并根据比对结果进行DOM操作来更新视图，达到减少对DOM的目的，从而减少浏览器的开销，提高渲染速度，改善用户体验。

一个组件都会调用$mount，一个组件就会创建一个watcher，vue中watcher与组件是一一对应的。组件中data有很多key,在vue1中每个key都会创建一个watcher，这样会造成内存溢出。到了vue2之后每个组件创建一个watcher。

![1591267506580](D:\ztGithub\vue-markdown\vue\1591267506580.png)

到了vue2中，因为一个watcher管理一个组件中data所有的key，所以就需要diff算法，进行新旧两次虚拟dom的比较，这是diff的必要性。

__patch__方法 深度优先，同层比较。从根节点开始，如果有孩子，则比较孩子节点，这是深度优先。同层比较，是每次只比较新旧虚拟dom中同层的节点

深度优先是递归操作，同层



# 2虚拟dom如何新建

