![1589804898999](D:\document\vue\1589804898999.png)

### 实现响应式



```js


class KVue {
  constructor(options) {
    this.$options = options
    this.$data = options.data
    // 响应化
    this.observe(this.$data)
  }

  // 递归遍历，使传递进来的对象响应化
  observe(value) {
    if (!value || typeof value !== 'object') {
      return
    }
    // 遍历
    Object.keys(value).forEach(key => {
      // 对key做响应式处理
      this.defineReactive(value, key, value[key])
      this.proxyData(key)
    })
  }

  // 在vue根上定义属性代理data中的数据
  // app.test 代替app.$data.test
  proxyData(key) {
    Object.defineProperty(this, key, {
      get() {
        return this.$data[key]
      },
      set(newVal) {
        this.$data[key] = newVal
      }
    })
  }

  defineReactive(obj, key, val) {

    // 递归
    this.observe(val)

    Object.defineProperty(obj, key, {
      get() {
        return val
      },
      set(newVal) {
        if (newVal !== val) {
          val = newVal
          console.log(`${key}属性更新了`)
        }
      }
    })
  }

}
```

### 测试响应式

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <script src="./kvue.js"></script>
  <script>
    const app = new KVue({
      data: {
        test: 'I am tian',
        foo: {
          bar: 'bar'
        }
      }
    })
    app.$data.test = 'hello world'
    app.$data.foo.bar = 'god'
    app.test = 'hello world2'
    app.foo.bar = 'god2'
  </script>
</body>
</html>
```

### $set

通过上线的代码可以看出，为什么不在data中的数据，不支持响应化。因为没经过observe 遍历data。所以通过$set重新让原本不在data中的数据响应化