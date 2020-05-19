# Vue工作机制

## 初始化

在new Vue()之后。Vue会调用进行初始化，会初始化生命周期、事件、props、methods、data、couputed与watch等。其中最重要的是通过Object.defineProperty设置setter与getter，用来实现【响应式】以及【依赖收集】

![1558340758374](D:\document\vue\1558340758374.png)

简化版：

![1558340952072](D:\document\vue\1558340952072.png)

