## 使用MKDOCS构建个人博客

如果电脑里有python，执行

```
pip install mkdocs
```

### 构建项目

```
mkdocs new mkdocs-site
```



同样的，添加.github\workflows\PublishMySite.yml

```
mkdir .github
cd .github
mkdir workflows
cd workflows
vim PublishMySite.yml
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

- 不创建user仓库，需要静态网站时新建多个project

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
git init
git add .
$ git commit -m "init"
```



第一条命令中记得更换为自己的项目仓库

```
git remote add origin git@github.com:Yang-Xijie/mkdocs-site.git
git branch -M main
git push -u origin main
```



GitHub > Repository > Settings > Pages > Branch > gh-pages > Click Save



## 附录

[Git国内的下载源](https://registry.npmmirror.com/binary.html?path=git-for-windows/)





