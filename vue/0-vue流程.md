vue对data对象递归遍历，遍历的时候做响应式，响应式是通过defineProperty来实现的。对每个data中的key都关联一个Dep对象（Dep对象是管理Watcher的），并且在getter中添加依赖收集，把当前watcher对象添加到dep中去，记录一下变量的使用，在setter方法中调用dep的notify方法，通知watcher调用update方法去改变UI。Watcher是在模板编译的时候创建的，发现{{}}就添加一个watcher



![1589813272007](D:\document\vue\1589813272007.png)



![1589813622239](D:\document\vue\1589813622239.png)



vue1的时候每个key都会加watcher，粒度太小，所以会内存溢出

vue2的时候是给每个组件加watcher，粒度变大了，但又不能改变一个变量，就更新整个组件，所以就出现了虚拟dom以及diff算法