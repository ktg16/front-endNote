参考: https://juejin.cn/post/6844903476661583880#heading-10

该文章写的非常全面,在此记录一下一些 不是很了解的地方

## 不同的router使用相同的component

![router-view.png](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2017/5/3/ed2de15673673276b00e205c042048e4~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)

当创建和编辑的页面使用的是同一个component,默认情况下当这两个页面切换时并不会触发vue的created或者mounted钩子，后来发现其实可以简单的在 router-view上加上一个唯一的key，来保证路由切换时都会重新渲染触发钩子了。这样简单的多了。

```
<router-view :key="key"></router-view>

computed: {
    key() {
        return this.$route.name !== undefined? this.$route.name + +new Date(): this.$route + +new Date()
    }
 }
```

