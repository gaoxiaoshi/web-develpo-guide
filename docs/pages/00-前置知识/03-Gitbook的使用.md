# Gitbook的安装及使用
## 认识Gitbook
GitBook 是一个基于 Node.js 的命令行工具，可使用 Github/Git 和 Markdown 来制作精美的电子书，我们的教程就是通过gitbook和Markdown来编写的，关于Markdown的用法可以看下篇文档。
* [GitBook 官网](https://www.gitbook.com/)
* [GitBook 文档](https://docs.gitbook.com/)

### 安装 GitBook
1. 首先就是安装`nodejs`环境，这里推荐使用v10.21.0版本
```
nvm install v10.21.0
```
2. 安装gitbook
```
npm install gitbook-cli -g
```

### Gitbook 的使用
1. 进入项目文档
```
cd 文档目录
```
2. 创建`book.json`文件
```json
{
    // 电子书名称
    "title": "前端入门宝典-心法篇",
    // 作者
    "author": "Laughing小石头",
    // 书籍描述
    "description": "夯实基础练内功，日后江湖必成功",
    // 书籍语言环境zh-hans表示中文
    "language": "zh-hans",
    // 文档目录
    "root": "docs",
    // 文档插件
    "plugins": [
        // 导航目录折叠插件
        "chapter-fold",
        // 版权页脚插件
        "tbfed-pagefooter"
    ],
    // 插件配置
    "pluginsConfig": {
        "tbfed-pagefooter": {
            "copyright":"Copyright &copy web-develop-guide (2021 - present)"
        }
    }
}
```
3. 初始化书籍
```
gitbook init
```
4. 安装配置中的插件
```
gitbook install
```
5. 在浏览器预览
```
gitbook serve
```