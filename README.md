### 开发工具
* 推荐使用VSCode来进行前端项目的开发。

* VSCode推荐插件列表

* Auto Close Tag
* Auto Rename Tag
* Beautify
* Document This
* ESLint
* Git Lens
* JavaScript(ES6) code snippets
* Path Autocomplete
* Path Intellisense
* React-Native/React/Redux snippets for es6/es7
* stylelint
* vscode-fileheader
* vscode-icons

* 基本配置

```js
    {
    "editor.fontSize": 16,
    "fileheader.Author": "你的名字",
    "fileheader.tpl": "/*\r\n * @Author: {author} \r\n * @since: {createTime} \r\n */",
    "fileheader.LastModifiedBy": "你的名字",
    "git.confirmSync": false,
    "git.enableSmartCommit": true,
    "editor.formatOnSave": false,
    "eslint.autoFixOnSave": false,
    "eslint.options": {
        "extensions": [
            ".jsx",
            ".js",
            ".vue"
        ]
    },
    "eslint.validate": [
        "javascript",
        "javascriptreact",
        "vue",
        "vue-html"
    ],
    "extensions.ignoreRecommendations": true,
    "workbench.colorTheme": "Monokai",
    "files.exclude": {
        "**/.git": true,
        "**/.svn": true,
        "**/.hg": true,
        "**/CVS": true,
        "**/node_modules": true,
        "**/.DS_Store": true
    },
    "beautify.config": {
        "selector_separator_newline": true,
        "space_in_paren": true
    },
    "vsicons.dontShowNewVersionMessage": true,
    "docthis.includeDescriptionTag": true,
    "docthis.inferTypesFromNames": true,
    "workbench.startupEditor": "newUntitledFile",
    "typescript.validate.enable": false,
    "typescript.format.enable": false,
    "javascript.validate.enable": false,
 
    "gitlens.advanced.messages": {
        "suppressCommitHasNoPreviousCommitWarning": false,
        "suppressCommitNotFoundWarning": false,
        "suppressFileNotUnderSourceControlWarning": false,
        "suppressGitVersionWarning": false,
        "suppressLineUncommittedWarning": false,
        "suppressNoRepositoryWarning": false,
        "suppressUpdateNotice": false,
        "suppressWelcomeNotice": true
    },
    "explorer.confirmDelete": false
}
```

### 前端GIT规范

* GIT的常用操作

```js
    git pull	拉取并合并代码	fetch，diff和merge的语法糖，由于会自动执行merge，很容易导致冲突了也没注意到，不推荐
    git fetch origin xxx	拉取远端代码但不合并	推荐
    git merge origin/xxx	合并代码到当前分支	推荐
    git state -s	查看有变动的文件列表	
    git branch	查看所有本地分支
    git branch -a	查看本地和远程分支	
    git branch -d xxx	删除本地xxx分支	必须不在xxx分支上才能删除
    git checkout xxx	切换到xxx分支上	xxx分支必须存在
    git checkout -b xxx	新建xxx本地分支并切换到xxx分支上	xxx分支必须不存在
    git checkout -b xxx origin/xxxx	新建远端分支为origin/xxxx的xxx本地分支并切换到xxx分支上	xxx分支必须不存在
    git add .	提交所有本地工作区的改动到本地暂存区	
    git commit -m '注释'	提交本地暂存区到对应本地分支上	
    git push	将本地分支上的代码推送到远端分支上	
    git log	查看当前分支上的commit记录	
    git reset --hard xxxx	回复本地版本到xxxx（git log查到的commit记录hash号）


    补充：
    git log    查看当前分支上的commit记录，git log后按q退出
    git reflog      查看命令历史，以便确定要回到未来的哪个版本
    HEAD       表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^
    git reset --hard HEAD^   回退到上一个版本
    git checkout -- .\src\page\product\index.jsx     撤销工作区修改
    git reset HEAD .\src\page\product\index.jsx      撤销暂存区修改
    git merge dev          合并指定分支到当前分支
    git branch -D feature-vulcan      -D强制删除
    如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。


    分支策略
    master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
    干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
    每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。
```

### 前端基础文档

* MDN Web 技术文档
* ECMAScript 6入门
* React 中文文档 css88
* React 中文文档 doc-china
* Redux 中文文档
* Redux 使用教程
* React Router 使用教程
* less 中文文档
* Vue
* Ant Design
* Ant Design 19大期间专用镜像
* ECharts
* iconfont


