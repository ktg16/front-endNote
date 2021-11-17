webpack 环境

1.安装webpack  选择对应环境

2.配置html模板

这里可能有的朋友会认为我们打包js文件名称不是一直是固定的嘛(output.js)？这样每次就不用改动引入文件名称了呀？实际上我们日常开发中往往会这样配置:

`module.exports = {`
    `// 省略其他配置`
    `output: {`
      `filename: '[name].[hash:8].js',      // 打包后的文件名称`
      `path: path.resolve(__dirname,'../dist')  // 打包后的目录`
    `}`
`}`

需要html-webpack-plugin 不需要手动修改引入js文件的名称



babel转义js文件 将es6/7/8转换为es5