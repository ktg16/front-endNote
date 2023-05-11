# 博客

博客来源：

github 飞鸟的个人博客

博客技术点：

## 1.ahooks(有时间去研究一下源码)

## 2.marked与hljs的使用

marked：https://marked.js.org/ 建议使用

使用marked将传递的数据封装一下, 需要设置代码高亮的一些css（MarkDown文件看完就明白）

hljs(高亮代码):https://highlightjs.readthedocs.io/en/latest/api.html#configure

配置前需要一个操作

```
// 将代码配置上class前缀
hljs.configure({
    classPrefix: 'hljs-',
    languages: ['CSS', 'HTML', 'JavaScript', 'TypeScript', 'Markdown']
  });
 // 引入 hljs.custom.scss  配置代码块中的样式
```

## 3.使用腾讯云cloudbase开发实现（React文件夹内）

文档：https://docs.cloudbase.net/api-reference/webv2/database#orderby

## 4.主题的切换

使用redux

## 5.classNames 可以使用多个className 

# 后台

## 1.权限的设置(相比于vue简易)

https://juejin.cn/post/6844903902995824654