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

### GIT规范

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

    git checkout -b dbg_lichen_star
    git push origin dbg_lichen_star:dbg_lichen_star
    把新建的本地分支push到远程服务器，远程分支与本地分支同名（当然可以随意起名）：
    git push origin --delete dbg_lichen_star
    删除远程分支


    git stash    储存到本地
    git stash list    查看储藏的东西
    git stash apply   将储存的东西拿出来，不删除储存的内容      如果不指定，则取出最近的一次
    git stash pop   将储存的东西拿出来，删除储存的内容
    git stash apply stash@{2}    将指定的内容，取出来

```

* 分支管理
```js
    分支管理
    master（主分支，永远是可用的、稳定的、可直接发布的版本，不能直接在该分支上开发）
    develop（开发主分支，代码永远是最新，该分支只做只合并操作，不能直接在该分支上开发）
    feature-xxx（功能开发分支，在develop上创建分支，以自己开发功能模块命名，功能测试正常后合并到develop分支）
    hotfix-xxx（紧急bug修改分支，项目上线之后可以会遇到一些环境问题需要紧急修复）
```

* commit规范
```js
    feat: 新特性
    fix: 修改问题
    refactor: 代码重构
    docs: 文档修改
    style: 代码格式修改, 注意不是 css 修改
    test: 测试用例修改
    chore: 其他修改, 比如构建流程, 依赖管理.
```

### Linux命令
```js
    tar                   //用来压缩和解压文件。tar本身不具有压缩功能。他是调用压缩功能实现的 
    tar -czvf test.tar.gz a.c   //压缩 a.c文件为test.tar.gz
    tar -xzvf test.tar.gz       //解压文件

    rm                  //除一个文件或者目录。
    rm x.txt            //删除文件
    rm -r dist          //删除文件夹
    rm  -r  *           //删除当前目录下的所有文件    
    rm -rf  dist             //删除文件夹，不逐一确认 


    scp    //scp是 secure copy的缩写, scp是linux系统下基于ssh登陆进行安全的远程文件拷贝命令。
    scp dist  root@10.2.101.123:~   //拷贝到远程服务器     
    ssh root@10.2.101.123           //ssh方式登陆远程服务器·

    mkdir test     //创建文件夹
    touch index.html   //创建文件
```


