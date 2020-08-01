---
title: hexo快速搭建个人博客
---

## hexo起步
```shell
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```

### 修改默认配置
`_config.yml`文件
```yml
language: zh-CN
```

## 主题

### 搜索
1. GitHub搜索关键字`hexo-theme`
2. Sort:Most stars

示例主题：[probberechts/hexo-theme-cactus](https://github.com/probberechts/hexo-theme-cactus)

### 安装

安装到`themes`文件夹下
```shell
git clone https://github.com/probberechts/hexo-theme-cactus.git themes/cactus
```
**注意：删除主题默认.git配置文件，把主题和博客项目合并成一个项目**

### 配置
`_config.yml`文件
```yml
theme: cactus
```

## 部署

**方式一：** `https://[username].github.io`
  
*仓库名必须为`[username].github.io`*
*打包产物`master`分支*

**方式二：** `https://[username].github.io/[repo]`

*可以自定义仓库名*
*打包产物`gh-pages`分支*

***

1. 初始化当前项目
```shell
git init
```

2. 添加远程的git地址
```shell
git remote add origin git@github.com:yiyulong/yiyulong.github.io.git
```

3. 安装`hexo-deployer-git`依赖
```shell
yarn add hexo-deployer-git
```

4. 配置`_config.yml`
```yml
deploy:
  type: git
  repo: git@github.com:yiyulong/yiyulong.github.io.git
  branch: master
```

4. 运行
```shell
npm run deploy
```
或
```shell
hexo deploy
```

***

### 源代码提交到其它分支

* 新建`myblog`分支
* 提交源代码

***

### 自动打包部署

*项目根目录下*
```
.github/workflows/deploy.yml
```

```yml
name: Build and Deploy
on: [push]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout 🛎️
        uses: actions/checkout@v2 # If you're using actions/checkout@v2 you must set persist-credentials to false in most cases for the deployment to work correctly.
        with:
          persist-credentials: false

      - name: Install and Build 🔧 # This example project is built using npm and outputs the result to the 'build' folder. Replace with the commands required to build your project, or remove this step entirely if your site is pre-built.
        run: |
          npm install
          npm run build
        env:
          CI: false

      - name: Deploy 🚀
        uses: JamesIves/github-pages-deploy-action@releases/v3
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          BRANCH: master # The branch the action should deploy to.
          FOLDER: public # The folder the action should deploy.
```

## 在线编辑

```html
<a href="https://github.com/yiyulong/yiyulong.github.io/edit/myblog/source/<%- page.source %>" target="_blank">编辑</a>
```


