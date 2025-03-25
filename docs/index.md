```

```





## mdbook

[入门 - MkDocs](https://www.mkdocs.org/getting-started/)

### 1.前往mdbook下载构建工具

[发布 ·rust-lang/mdBook](https://github.com/rust-lang/mdBook/releases)

### 2.使用mdbook.exe构建

```cmd
mdbook.exe init ./mybook
```

### 3.结构说明

```
mybook/
├── book
├── book.toml
└── src
    ├── chapter_1.md
    └── SUMMARY.md
```

book.toml : **配置文件**，可以配置每篇文章最上面统一标题、路径、作者等信息。

src 文件夹: 新增的 Markdown文章都要放到 src 目录下。

SUMMARY.md : **所有文章的目录**，新增的 Markdown文章都需要在这里面配置。

book 文件夹: mdBook 启动后会自动生成一些 html 文件在里面。

### 4.编写文章以及启动

​	1.在src目录下编写md文章

​	2。在SUMMARY.md中配置你的文章

### 5.导出html文件

```
mdbook.exe build {location}
```

ps : location为导出的位置，需要自己修改。

```
mdbook.exe serve {location}
```

启动时它会先执行构建命令，然后开启 3000 端口，启动成功后，你就可以浏览器访问 `http://localhost:3000`，便可本地看到效果了。



## mkdocs

如果电脑里有python，执行pip install mkdocs拉取

### 构建项目

```
mkdocs new mkdocs-site
```



同样的，添加.github\workflows\PublishMySite.yml

```
$ mkdir .github
$ cd .github
$ mkdir workflows
$ cd workflows
$ vim PublishMySite.yml
```



```yml
name: publish site
on: # 在什么时候触发工作流
  push: # 在从本地main分支被push到GitHub仓库时
    branches:
      - main
  pull_request: # 在main分支合并别人提的pr时
    branches:
      - main
jobs: # 工作流的具体内容
  deploy:
    runs-on: ubuntu-latest # 创建一个新的云端虚拟机 使用最新Ubuntu系统
    steps:
      - uses: actions/checkout@v2 # 先checkout到main分支
      - uses: actions/setup-python@v2 # 再安装Python3和相关环境
        with:
          python-version: 3.x
      - run: pip install mkdocs-material # 使用pip包管理工具安装mkdocs-material
      - run: mkdocs gh-deploy --force # 使用mkdocs-material部署gh-pages分支
```



### 项目结构

```
├── .github
│   ├── .DS_Store
│   └── workflows
│       └── PublishMySite.yml
├── docs
│   └── index.md
└── mkdocs.yml
```



### mkdocs-material

```
pip install mkdocs-material
```



Add the following lines to :`mkdocs.yml`

```
theme:
  name: material
```



## 部署

### 在githubPage中部署


这里一定要注意：个人用户只有两种 GitHub Pages 网站的类型：一种是 `user`(用户)，一种是`project`(项目)。

`user`类型的网址只能对应唯一的用户，而且仓库的名字必须为 `<username>.github.io`，对应的网址为 `http(s)://<username>.github.io`。

`project`类型的仓库则可以新建很多，只要仓库的名字不为 `<username>.github.io` 即可，对应的网址为 `http(s)://<username>.github.io/<repository>`。

根据这两种类型，建站可以有两种策略：

- 只创建一个user仓库

  ```
  <username>.github.io
  ```

  ，所有的文章都放在这个仓库中。

  - 优点：只有一个仓库维护方便
  - 缺点：你的个人账户再新建`project`类型的仓库大概率会与这个user仓库冲突。但我感觉一般对于个人来说 一个仓库也完全够用。

- 不创建user仓库，需要静态网站时新建多个

  ```
  project
  ```

  类型的仓库

  - 优点：仓库不限量 仓库之间互不冲突 可以使用不同的框架
  - 缺点：多个仓库维护困难

选择哪种仁者见仁智者见智吧

[GitHub Pages - 杨希杰的个人网站](https://yang-xijie.github.io/BLOG/Markdown/github-pages/)



GitHub > Repository > Settings > Actions > General >

- Actions permissions: Allow all actions and reusable workflows
- Workflow permissions: Read and write permissions
- Click Save



在github项目中给予Workflows的权限



push项目到github上



```
$ git init
$ git add .
$ git commit -m "init"
```



第一条命令中记得更换为自己的项目仓库

```
$ git remote add origin git@github.com:Yang-Xijie/mkdocs-site.git
$ git branch -M main
$ git push -u origin main
```



GitHub > Repository > Settings > Pages > Branch > gh-pages > Click Save



done!





## 附录

[Git国内的下载源](https://registry.npmmirror.com/binary.html?path=git-for-windows/)

