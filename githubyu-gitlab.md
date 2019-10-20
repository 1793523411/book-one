## gitHub和gitLab
如果我们熟悉服务器的话，我们完全可以将上述的步骤在我们的远程服务器上进行操作，然后再做一些登录权限的设置，就可非常完美的搭建一个共享服务器了。其实为了更好的管理我们的仓库，一些第三方机构开发出了Web版仓库管理程序，通过Web界面形式管理仓库。
gitHub关于它的名气与意义，大家可以自行查阅，我们这里介绍它的使用
1、注册账号并完善资料
自行注册略过
2、创建共享仓库

3、填写仓库资料

4、共享仓库

远程地址特别长，我们可以给他起一个别名
`git remote add origin git@github.com:Botue/repo.git`
这样origin 就代表 `git@github.com:Botue/repo.git`
当我们通过git clone 从共享仓库获内容时，会自动帮我们添加origin到对应的仓库地址，例如：`git clone git@github.com:Botue/repo.git `会自动添加origin 对应 `git@github.com:Botue/repo.git`
5、生成密钥
`ssh-keygen -t rsa `然后一路回车，这里会在当前用户生成了一个.ssh的文件夹

将id_rsa.pub公钥的内容复制
打开gitHub的个人中心

打到SSH keys

到此我们便可以通过gitHub 提供的Web界面来管理我们的仓库了。
我们发现通过gitHub管理仓库实在是太方便了，可是只能免费使用公开仓库，自已公司的代码当然不能公开了，可是私有仓库又是需要交“保护费”的，无耐国人还是比较喜欢免费的，网络界总是有很多雷峰的，比如gitLab!!!
gitLab也是一个可以通过Web界面管理仓库的网站程序，我们可以把它架设到公司自已的服务器上，实现仓库私有化，这也是大部分公司通常采用的方法，其使用方法与gitHub十分相似。
我将闲置电脑配置成了一台服务器，上面架设了gitLab程序，我们接下来的练习全部会在gitLab上进行演示。
省略很多内容.....
## 命令汇总
```
git config配置本地仓库
常用git config --global user.name、git config --global user.email
git config --list查看配置详情
git init 初始一个仓库，添加--bare可以初始化一个共享（裸）仓库
git status 可以查看当前仓库的状态
git add“文件” 将工作区中的文件添加到暂存区中，其中file可是一个单独的文件，也可以是一个目录、“*”、-A
git commit -m '备注信息' 将暂存区的文件，提交到本地仓库
git log 可以查看本地仓库的提交历史
git branch查看分支
git branch“分支名称” 创建一个新的分支
git checkout“分支名称” 切换分支
git checkout -b deeveloper 创健并切到developer分支
git merge“分支名称” 合并分支
git branch -d “分支名称” 删除分支
git clone “仓库地址”获取已有仓库的副本
git push origin “本地分支名称:远程分支名称”将本地分支推送至远程仓库（不写冒号默认名字为分支名字），
git push origin hotfix（通常的写法）相当于
git push origin hotfix:hotfix
git push origin hotfix:newfeature
本地仓库分支名称和远程仓库分支名称一样的情况下可以简写成一个，即git push “仓库地址” “分支名称”，如果远程仓库没有对应分支，将会自动创建
git remote add “主机名称” “远程仓库地址”添加远程主机，即给远程主机起个别名，方便使用
git remote 可以查看已添加的远程主机
git remote show “主机名称”可以查看远程主机的信息
```
## Git注意事项

没错，Git非常强大！
但是，如果我们的分支不加以规范管理，也有可能适得其反！
1、不要有太多的树杈（子分支）
2、要有一个“稳定分支”，即master分支不要轻意被修改
3、要有一个开发分支（developer），保证master分支的稳定性
4、所有的功能分支（feature）从developer创建
5、所有功能开发完成后新建发布分支（release）





## 冲突解决
Gitlab有grope，用于团队开发，可对开发者分配角色
假如两个开发同时改到同一文件的同一段内容会发生什么事情呢？
这时就会就会产生冲突了，当冲突产生后，需要开发者进行协商确认冲突的原因，然后将冲突代码删除重新提交就可以了。
有一个会叫你先pull在push避免同时push出错（即先pull检查一下同时在push的内容）
## Git高级
熟悉掌握以上操作，基本上是可以满足日常开的需要的，但是在解决一些特殊问题时，就又需要我们能够掌握更多的命令。
### gitignore忽略文件
在项目根目录下创建一个.gitignore文件，可以将不希望提交的罗列在这个文件里，如项目的配置文件、node_modules等
https://github.com/github/gitignore
### 比较差异
当内容被修改，我们无法确定修改哪些内容时，可以通过git diff来进行差异比较。
git difftool 比较的是工作区和暂存的差异
git difftool “SHA”比较与特定提交的差异
git difftool “SHA”“SHA”比较某两次提交的差异
git difftool 分支名称 比较与某个分支的差异
2、回滚（撤销）操作

HEAD 默认指向当前分支的“末端”，即最后的一次提交，但是我们通过git reset 可以改变HEAD的指向。
看情况解释（稍微复杂一些，理解就好）
1、git reset
--hard 工作区会变、历史(HEAD)会变， 暂存区也变
--soft 只会变历史(HEAD)
--mixed（默认是这个选项）历史(HEAD)会变、暂存区也变，工作区不变
2、git checkout
git checkout SHA -- "某个文件"，代表只是从SHA这个版中取出特定的文件，
和git reset 是有区别的，reset 重写了历史，checkout 则没有。
### 更新仓库
在项目开发过程中，经常性的会遇到远程（共享）仓库和本地仓库不一致，我们可以通过git fetch 命令来更新本地仓库，使本地仓库和远程（共享）仓库保持一致。
`git fetch  “远程主机”`
或者
`git fetch “远程主机” “分支名称”`
我们要注意的是，利用git fetch 获取的更新会保存在本地仓库中，但是并没有体现到我们的工作目录中，需要我们再次利用git merge来将对应的分支合并（融合）到特定分支。如下
`git pull origin` 某个分支， 上操作相当于下面两步
`git fetch `
`git merge origin/某个分支`
问题：如何查看远程主机上总共有多少个分支？
`git branch -a `便可以查看所有(本地+远程仓库)分支了

3.10其它
删除远程分支`git push origin --delete 分支名称`
删除远程分支`git push origin :分支名称`