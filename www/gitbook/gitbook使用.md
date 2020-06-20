### gitbook的使用

GitBook 是一个基于 Node.js 的命令行工具，支持 Markdown 和 AsciiDoc 两种语法格式，可以输出 HTML、PDF、eBook 等格式的电子书。

#### 安装

+ 安装`nodeJS`，因为 GitBook 是基于 Node.js，所以我们首先需要安装 Node.js

  ```javascript
  node -v // 查看版本及是否安装成功
  ```

  

+ 安装`gitbook-cli`

  ```js
  npm install gitbook-cli -g
  gitbook -V // 查看版本及是否安装成功
  ```

  

+ 初始化项目 

  ```javascript
  gitbook init
  // 执行完后，你会看到多了两个文件 —— [README.md](http://readme.md/) 和 [SUMMARY.md](http://summary.md/)
  // [README.md](http://readme.md/) —— 书籍的介绍写在这个文件里
  // [SUMMARY.md](http://summary.md/) —— 书籍的目录结构在这里配置
  ```

#### 预览与打包

+ 方式一：启动一个本地服务

  ```javascript
  gitbook serve // gitbook 会启动一个 4000 端口用于预览。
  ```

+ 方式二：打包为一个.html静态文件，配置后可以直接访问预览

  ```javascript
  gitbook build
  gitbook build --gitbook=2.0.1 // 生成时指定gitbook的版本, 本地没有会先下载
  ```

#### 命令

+ `gitbook-cli` 和 `gitbook` 是两个软件
+ `gitbook-cli` 会将下载的 gitbook 的不同版本放到 `~/.gitbook`中, 可以通过设置`GITBOOK_DIR`环境变量来指定另外的文件夹

**列出gitbook所有的命令**

```javascript
gitbook help
```

**输出gitbook-cli的帮助信息**

```javascript
gitbook --help
```

**生成静态网页**

```bash
gitbook build
```

**本地运行服务器**

```bash
gitbook serve
```

**生成时指定gitbook的版本, 本地没有会先下载**

```javsa
gitbook build --gitbook=2.0.1
```

**列出本地所有的gitbook版本**

```bash
gitbook ls
```

**列出远程可用的gitbook版本**

```bash
gitbook ls-remote
```

**安装对应的gitbook版本**

```bash
gitbook fetch 标签/版本号
```

**更新到gitbook的最新版本**

```bash
gitbook update
```

**卸载对应的gitbook版本**

```bash
gitbook uninstall 2.0.1
```

**指定log的级别**

```bash
gitbook build --log=debug
```

**输出错误信息**

```bash
gitbook builid --debug
```

#### 配置

+ 配置目录文件`Summary.md`

  ```
  # Summary
  * [Introduction](README.md)
  * [目录1](part1/README.md)
      * [1.1](part1/writing.md)
      * [1.2](part1/gitbook.md)
  * [目录2](part2/README.md)
      * [2.1](part2/feedback_please.md)
      * [2.2](part2/better_tools.md)
  ```

  - 我们通过使用 `标题` 或者 `水平分割线` 标志将 GitBook 分为几个不同的部分

    ```
    # Summary
    
    ### Part I
    
    * [Introduction](README.md)
    * [Writing is nice](part1/writing.md)
    * [GitBook is nice](part1/gitbook.md)
    
    ### Part II
    
    * [We love feedback](part2/feedback_please.md)
    * [Better tools for authors](part2/better_tools.md)
    
    ---- // 分割线
    
    * [Last part without title](part3/title.md)
    ```

    

+ 目录根目录下新建`book.json`并配置相关属性，存放配置信息

```javascript
// book.json
{
    "title" : "Gitbook Use", // 设置书本的标题
    "author" : "zhangjikai", // 作者的相关信息
	"description" : "描述", // 描述
    "language" : "zh-hans", // Gitbook使用的语言, 版本2.6.4中可选的语言如下
        // en, ar, bn, cs, de, en, es, fa, fi, fr, he, it, ja, ko, no, pl, pt, ro, ru, sv, uk, vi, zh-hans, zh-tw
    "gitbook" : "3.2.2", // 指定使用的gitbook版本
    "gitbook" : ">=3.0.0",
    "root": ".", // 指定存放 GitBook 文件（除了 book.json）的根目录
    "links" : { // 在左侧导航栏添加链接信息
        "sidebar" : {
            "Home" : "xx.com"
        }
    },     
    "styles": { // 自定义页面样式， 默认情况下各generator对应的css文件
        "website": "styles/website.css",
        "ebook": "styles/ebook.css",
        "pdf": "styles/pdf.css",
        "mobi": "styles/mobi.css",
        "epub": "styles/epub.css"
    },
 // 例如使<h1> <h2>标签有下边框， 可以在website.css中设置
    //h1 , h2{
    //	border-bottom: 1px solid #EFEAEA;
	//}
    "plugins": [ // 配置使用的插件
        "disqus"
    ],
    //添加新插件之后需要运行gitbook install来安装新的插件
   /* Gitbook默认带有5个插件：
        highlight
        search
        sharing
        font-settings
        livereload
    */
    // 如果要去除自带的插件， 可以在插件名称前面加-
   /*
   "plugins": [
    	"-search"
	]
	*/
    "pluginsConfig": { // 配置插件的属性
        "fontsettings": {
            "theme": "sepia",
            "family": "serif",
            "size":  1
        }
    },
    // structure 见如下表格
    // 指定 Readme、Summary、Glossary 和 Languages 对应的文件名，下面是这几个文件对应变量以及默认值：
}

```

|                       |                                                |
| :-------------------- | :--------------------------------------------- |
| 变量                  | 含义和默认值                                   |
| `structure.readme`    | `Readme file name (defaults to README.md)`     |
| `structure.summary`   | `Summary file name (defaults to SUMMARY.md)`   |
| `structure.glossary`  | `Glossary file name (defaults to GLOSSARY.md)` |
| `structure.languages` |                                                |

#### 插件

`book.json` 配置，配置后需要使用命令`gitbook install ./`

​	

|插件名    |描述 |
| :---- | :---- |
|hide-element |隐藏元素|
|back-to-top-button|回到顶部|
| chapter-fold|导航目录折叠 |
|code| 复制代码  |
| splitter |侧边栏宽度可调节|
| search-pro | 高级搜索 |
| insert-logo  |   插入logo   |
| custom-favicon     |修改标题栏图标|
|pageview-count|阅读量计数|
|tbfed-pagefooter |页面添加页脚  |
|sharing-plus|分享当前页面|

1、`hide-element` 隐藏元素

```
{
    "plugins": [
        "hide-element"
    ],
    "pluginsConfig": {
        "hide-element": {
            "elements": [".gitbook-link"]
        }
    }
}
```

2、`back-to-top-button` 回到顶部

```
{
    "plugins": [
         "back-to-top-button"
    ]
}
```

3、`chapter-fold` 导航目录折叠

```
{
    "plugins": ["chapter-fold"]
}
```

4、`code` 复制代码

```
{
    "plugins" : [ "code" ]
}
```

5、`splitter `侧边栏宽度可调节

```
{
    "plugins": [
        "splitter"
    ]
}
```

6、`search-pro `高级搜索

```
{
    "plugins": [
          "-lunr", 
          "-search", 
          "search-pro"
    ]
}
```

7、`insert-logo` 插入logo

```
{
    "plugins": [ "insert-logo" ]
    "pluginsConfig": {
      "insert-logo": {
        "url": "images/logo.png",
        "style": "background: none; max-height: 30px; min-height: 30px"
      }
    }
}
```

8、`custom-favicon` 修改标题栏图标

注意只支持`ico`后缀的图片，并且只支持本地图片，不支持网络图片链接。

```
{
    "plugins" : ["custom-favicon"],
    "pluginsConfig" : {
        "favicon": "icon/favicon.ico"
    }
}
```

9、`pageview-count` 阅读量计数

记录每个文章页面被访问的次数。

```
{
  "plugins": [ "pageview-count"]
}
```

10、`tbfed-pagefooter` 页面添加页脚

在每个文章下面标注版权信息和文章时间

```
{
    "plugins": [
       "tbfed-pagefooter"
    ],
    "pluginsConfig": {
        "tbfed-pagefooter": {
            "copyright":"Copyright &copy 2020",
            "modify_label": "该文章修订时间：",
            "modify_format": "YYYY-MM-DD HH:mm:ss"
        }
    }
}
```

11、`popup `弹出大图

点击可以在新窗口展示图片。

```
{
  "plugins": [ "popup" ]
}
```

12、`sharing-plus` 分享当前页面

**gitbook`默认只有`Facebook、Google+、Twiter、Weibo、Instapaper**

插件可以有更多分享方式，也可以关闭指定分享方式。

```
{
    "plugins": ["-sharing", "sharing-plus"],
    "pluginsConfig": {
        "sharing": {
             "douban": true,
             "facebook": true,
             "google": true,
             "pocket": true,
             "qq": true,
             "qzone": true,
             "twitter": true,
             "weibo": true,
          "all": [
               "douban", "facebook", "google", "instapaper", "linkedin","twitter", "weibo", 
               "messenger","qq", "qzone","viber","whatsapp"
           ]
       }
    }
}
```

