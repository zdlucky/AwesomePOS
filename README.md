# AwesomePOS

> A Vue 2.X Project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).


# 整个项目从 0 -> 1 -> 可视（部署到 GitHub Pages）的简单记录：

1. 安装 node（要求：8.9+；推荐：8.11.0+，如：8.11.2）、npm（推荐：6.1.0+）/cnpm（设置淘宝镜像）

2. 全局安装 vue-cli （已安装，则跳过）：`npm install vue-cli -g`
3. 初始化 Vue 项目：`vue init webpack AwesomePos`
4. 接下来当然是 运用所学 按需开发 啦~
5. 开发完毕，项目打包，优化上线（**即，修改 `config/index.js` 文件**）：<br>
1、`npm run dev` 自动打开浏览器：`autoOpenBrowser: true` （初始化完成即可配置）<br>
2、更改 `npm run build` 文件存储目录：`dist -> docs` （适应 GitHub Pages 部署要求）<br>
3、改绝对路径为相对路径， 并 去除 `*.map` 文件的打包：
``` js -> config/index.js
    build: {
        // 打包(生产)目录 设置成 docs ,纯粹为了能部署在 GitHub Pages 上面，
        // GitHub Pages 要求为 docs 目录，dist不识别。
        index: path.resolve(__dirname, '../docs/index.html'),
        assetsRoot: path.resolve(__dirname, '../docs'),

        assetsPublicPath: './', // 改绝对路径为相对路径
        productionSourceMap: false // 去除 *.map 文件的打包，减小生产包体积，加快打包速度
    }
```
6. 至此开发及配置完毕，准备上传 GitHub 仓库，在 GitHub 上新建一个空的 repo ，即，不要勾选 `Initialize this repository with a README` （即不自动生成 README.md 文件），新建空仓库完成后，会看到一个向导页，大概就是说，教你如何上传代码到 GitHub 仓库了
7. 初始化本地Git仓库 -> 暂存 -> 提交，然后与 远程 GitHub 仓库配对（注意：使用SSH方式，否则每次 `push` 需要输入GitHub用户名、密码，挺烦），具体参考这篇文章即可，全都有（包括：初始化一直到成功推送到远程GitHub仓库踩的坑、SSH KEY生成及配置等等。。。）<br>
[【GitHub SSH keys & Permission denied (publickey)】windows下github 出现Permission denied (publickey).解决方法 - 青春阳光 - 博客园](https://www.cnblogs.com/lxwphp/p/7884757.html)
8. 至此代码更新完毕，只要设置一下 GitHub Pages 的源就行了<br>
`repo Settings -> GitHub Pages -> Source中有 /docs 的分支`