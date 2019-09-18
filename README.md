### 前端移动端代码原则

1. 业务逻辑尽可能往下沉， 放到后台（BFF或者服务层）， 前台尽可能专注在做展示和交互。 
- 比如复杂权限的判断等
### 后端代码原则

1. 查询SQL必须评估表数据量， 加上合适的索引保证检索性能
- 可以通过SQL执行计划帮助优化索引
- 参考SaaS 2.0 巧房SQL规范获取更多关于索引使用的建议
2. 任何功能开发， 都必须对操作的数据数量， 操作频次做预估， 以此为基础做合理设计， 保证功能的性能和系统的稳定性
- 功能开发和测试必须以预估可能的最大量来进行
- 特别是报表类相关功能
- 如果是定时任务， 必须考虑SaaS2支持5000家客户，默认情况下总定时任务时间=5000*每家公司的耗时， 解决方案之一是： 通过发送异步消息提高并发， 避免晚上的定时任务到白天仍没有执行完。
3. 严禁使用ThreadLocal。 
- ThreadLocal使用不当会导致意想不到的数据错乱问题（比如窜公司）。 如果需要使用必须找架构组讨论。
4. 严禁使用静态变量保存用户登陆信息等值，
- 比如把登陆用户信息放在一个静态变量里，需要用的时候从静态变量里取，这样使用在多线程情况下会出现数据错乱的问题。
### 前后端通用代码原则

1. 严禁在循环代码中进行远程调用，
- 远程调用包括但不限于： 数据库， Redis， ES， Restful服务等，循环中执行远程调用会带来严重的性能问题。
2. 访问变量内部属性或者遍历集合， 必须判断变量或者集合是否为空
- 避免出现空指针类异常
3. 所以UI／接口字段都必须有长度／范围限制
- 文字可以校验， 截断等， 数字可以校验等等
- 问题示例： ES 前后都有*号做模糊查询时， 入参过长会导致ES CPU 100%
4. 除法计算必须考虑除数为0的情况
5. 严禁打印日志的时候直接打印整个对象， 只打印必要的指定字段
6. 严禁在代码中使用递归或者使用while(true)类型的语句结构
7. 严禁在代码使用使用id／uuid／DisplayName等于某个值来做条件判断。
- 例如 if（id=100）{...}， if（status='审批通过'）{...}
- 正确的方式是使用code等标识
- 
### 生产环境操作原则：
1. 以下生产环境操作不要在白天工作时间操作

- 更新大批量线上数据
- 数量大的表添加索引（百万级以上的）
- 全量刷公司ES里房客源索引数据
2. 生产环境修复数据的SQL必须经过评审，并由团队Leader确认后方可发申请执行。
- 少量表／字段修改，修改SQL里先备份相关表／字段
- 所有数据修复，都要求需要备份数据库
3. 任何生产环境的代码， 配置等修改， 必须发申请走上线流程
4. 所有上线步骤必须准备好回滚方案，包括但不限于
- 迭代版本里的DDL SQL：添加字段／表的SQL 不需要回滚， 但是改表／字段名类的需要有回滚SQL。
- 迭代版本里的DML SQL： 修改原有表／字段数据的SQL， 执行修改前必须要先备份相关表和字段（DBA不可能备份所有公司数据库）
- 代码 （回滚tag）
- 配置

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
* prettier
* TSLint

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


    git push origin 分支名 --force   git强制提交本地分支覆盖远程分支
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


