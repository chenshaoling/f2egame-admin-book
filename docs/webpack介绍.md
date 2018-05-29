# webpack介绍

### 什么是WebPack

WebPack可以看做是模块打包机：它做的事情是，分析你的项目结构，找到JavaScript模块以及其它的一些浏览器不能直接运行的拓展语言（Scss，TypeScript等），并将其转换和打包为合适的格式供浏览器使用。

### 使用WebPack

Webpack的工作方式是：把你的项目当做一个整体，通过一个给定的主文件（如：index.js），Webpack将从这个文件开始找到你的项目的所有依赖文件，使用loaders处理它们，最后打包为一个（或多个）浏览器可识别的JavaScript文件。
我们项目的webpack配置文件webpack.config.js,主要配置如下：

入口和输出
```javascript
    entry: './src/main.js', //唯一入口文件
    output: {
        path: path.resolve(__dirname, './dist'), //打包后的文件存放的地方，__dirname：node.js中的一个全局变量，它指向当前执行脚本所在的目录
        publicPath: '/', //生产模式下替换内嵌到css、html文件里的url值,比如图片url
        filename: 'js/build.js' //打包后输出文件的文件名
    },
```

编译规则,使用loaders处理文件：
```javascript
rules: [{ //编译html
        test: /\.html$/,
        use: [{
            loader: 'html-loader',
            options: {
                minimize: true
            }
        }]
    }]
```

使用插件处理任务，比如分离html
```javascript
new HtmlWebpackPlugin({ //抽出html
    filename: 'index.html',
    template: __dirname + '/src/index.html',
    inject: true,
    minify: {
        collapseWhitespace: false,
        removeAttributeQuotes: false
    }
})
```
生成source-map
```javascript
devtool: '#source-map' //生成Source Maps（使调试更容易）

```
开启本地服务器
```javascript
devServer: {
    contentBase: __dirname + '/dist', //本地服务器所加载的页面所在的目录
    historyApiFallback: true, //不跳转
    noInfo: true,
    overlay: true,
    disableHostCheck: true
}
```

更多详细的配置，请查看webpack.config.js