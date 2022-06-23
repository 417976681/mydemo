Git使用教程1---世界上最先进的分布式版本控制系统简介
Git使用教程2---Git的安装与理论基础
Git使用教程3---实战
Git使用教程4---状态
Git使用教程5---回到过去
Git使用教程6---版本对比
Git使用教程7---修改最后一次提交、删除文件和重命名文件
Git使用教程8---创建和切换分支
Git使用教程9---合并和删除分支
Git使用教程10---匿名分支和checkout命令

Git使用教程2---Git的安装与理论基础
一、Git安装
windows安装：进入网站https://git-scm.com/下载安装，然后在cmd命令行配置

> git config --global user.name "FishC_Service"
> git config --global user.email "fishc_service@126.com"
#检查信息是否写入成功
git config --list 
ubuntu配置：apt-get install git

二、理论基础
Git 记录的是什么？


如上，如果每个版本中有文件发生变动，Git 会将整个文件复制并保存起来。这种设计看似会多消耗更多的空间，但在分支管理时却是带来了很多的益处和便利。

三棵树

你的本地仓库有 Git 维护的三棵“树”组成，这是 Git 的核心框架。这三棵树分别是：工作区域、暂存区域和 Git 仓库


工作区域（Working Directory）就是你平时存放项目代码的地方。

暂存区域（Stage）用于临时存放你的改动，事实上它只是一个文件，保存即将提交的文件列表信息。

Git 仓库（Repository）就是安全存放数据的位置，这里边有你提交的所有版本的数据。其中，HEAD 指向最新放入仓库的版本（这第三棵树，确切的说，应该是 Git 仓库中 HEAD 指向的版本）。

Git 的工作流程一般是：

在工作目录中添加、修改文件；

将需要进行版本管理的文件放入暂存区域；

将暂存区域的文件提交到 Git 仓库。

因此，Git 管理的文件有三种状态：已修改（modified）、已暂存（staged）和已提交（committed），依次对应上边的每一个流程。

Git使用教程3---实战
一、初始化Git
在自己方便的盘中新建一个文件夹，这里以MyProject为例，注意路径中不要含有中文字符。打开cmd命令窗口，操作如下：

#初始状态在C盘中，更改路径
C:\Users\lenovo>F:
F:\>
F:\>cd MyProject
F:\MyProject>
#初始化Git项目，成功后创建有一个.git隐藏文件
F:\MyProject>git init
Initialized empty Git repository in F:/MyProject/.git/
#在文件夹MyProject中添加一个文本文件README，md格式指Markdown格式（建议使用Notepad++编辑）
#然后输入以下命令将文件加入暂存区
F:\MyProject>git add README.md
#将文件提交到git仓库（-m表示添加本次提交的说明，强制要求写的）
F:\MyProject>git commit -m "add a readme file"
[master (root-commit) 9e08cf4] add a readme file
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
如何将GItHub上别人的代码“据为己有”？
F:\>Clone>git clone 目标

Git使用教程4---状态
我们怎么知道哪些文件是新添加的，哪些文件已经加入了暂存区域呢？总不能让我们自己拿个本本记下来吧？
当然不，作为世界上最伟大的版本控制系统，你能遇到的囧境，Git 早已有了相应的解决方案。随时随地都可以使用git status查看当前状态

F:\MyProject>git status
On branch master
nothing to commit, working tree clean
On branch master: 我们位于一个叫做“master”的分支里，这是默认的分支
nothing to commit, working directory clean : 说明你的工作目录目前是“干净的”，没有需要提交的文件（意思就是自上次提交后，工作目录中的内容压根儿就没改动过）。

在工作目录中添加LICENSE文件(去掉后缀，用NotePad++打开)：

Copyright (C) <year> <copyright holders>
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

小甲鱼友情提示：MIT 许可证几乎是最宽松的版权约定，一旦你的程序采用，也就意味着别人只要在软件包含上边的版权声明，就可以对你的程序为所欲为了（包括“使用、复制、修改、合并、出版发行、散布、再授权和/或贩售软件及软件的副本”）。

输入git status命令，提示如下：

F:\MyProject>git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        LICENSE(红色)

nothing added to commit but untracked files present (use "git add" to track)
Untracked files 说明存在未跟踪的文件（下边红色的那个）

所谓的“未跟踪”文件，是指那些新添加的并且未被加入到暂存区域或提交的文件。它们处于一个逍遥法外的状态，但你一旦将它们加入暂存区域或提交到 Git 仓库，它们就开始受到 Git 的“跟踪”。

这里圆括号中的英文是 git 给我们的建议：使用 git add <file> 命令将待提交的文件添加到暂存区域。

F:\MyProject>git add LICENSE

F:\MyProject>git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   LICENSE(绿色)
use "git reset HEAD <file>..." to unstage 的意思是“如果你反悔了，你可以使用 git reset HEAD 命令恢复暂存区域”。如果后面接文件名，表示恢复该文件；如果不接文件名，则表示上一次添加的文件。

F:\MyProject>git reset HEAD

F:\MyProject>git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        LICENSE(红色)

nothing added to commit but untracked files present (use "git add" to track)
再次添加到暂存区域，然后执行 git commit -m "add a license file" 命令：

F:\MyProject>git add LICENSE

F:\MyProject>git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   LICENSE


F:\MyProject>git commit -m "add a license file"
[master 9fdf9f4] add a license file
 1 file changed, 7 insertions(+)
 create mode 100644 LICENSE

F:\MyProject>git status
On branch master
nothing to commit, working tree clean
关于修改

突然发现版权那块忘了写上自己的名字了……
打开 LICENSE 文件，将 Copyright (C) <year> <copyright holders> 改为 Copyright (C) 2016 FishC，保存……

执行 git status 命令：

F:\MyProject>git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   LICENSE(红色)

no changes added to commit (use "git add" and/or "git commit -a")
由于你对工作目录的文件进行了修改，导致这个文件和暂存区域的对应文件不匹配了，所以 Git 又给你提出两条建议：

使用 git add 命令将工作目录的新版本覆盖暂存区域的旧版本，然后准备提交
使用 git checkout 命令将暂存区域的旧版本覆盖工作目录的新版本（危险操作：相当于丢弃工作目录的修改）
还有一种情况我们没分析，大家先把新版本的文件覆盖掉暂存区域的旧版本：

F:\MyProject>git add LICENSE

F:\MyProject>git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   LICENSE(绿色)
然后我们打开 LICENSE 文件，将 FishC 改为 FishC.com，保存……

F:\MyProject>git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   LICENSE(绿色)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   LICENSE(红色)
这次情况是：被绿的 LICENSE 说明文件存放在暂存区域（待提交），同时红色的 LICENSE 说明文件还在工作目录等待添加到暂存区域。

这种情况你应该意识到这里存在两个不同版本的 LICENSE 文件，这时如果你直接执行 commit 命令，那么提交的是暂存区域的版本（FishC），如果你希望提交工作目录的新版本（FishC.com），那么你需要先执行 add 命令覆盖暂存区域，然后再提交……

一步到位

从工作目录一步添加到仓库：git commit -am “说明”

F:\MyProject>git commit -am "change the license file"
-a的意思是add。

git log 查看历史操作记录

Git使用教程5---回到过去
有关回退的命令有两个：reset 和 checkout


先执行git log命令，将此时的Git仓库可视化


三棵树的情况：


回滚快照
注：快照即提交的版本，每个版本我们称之为一个快照。

现在我们利用 reset 命令回滚快照，并看看 Git 仓库和三棵树分别发生了什么。

执行 git reset HEAD~ 命令：

注：HEAD 表示最新提交的快照，而 HEAD~ 表示 HEAD 的上一个快照，HEAD~~表示上上个快照，如果表示上10个快照，则可以用HEAD ~10

此时我们的快找回滚到了第二棵数（暂存区域）


第一次执行reset后Git仓库
第一次执行reset后三棵树
git reset HEAD~ 命令其实是 git reset --mixed HEAD~ 的缩写， --mixed 选项是默认的。

默认
git reset HEAD~ 命令其实影响了两棵树：首先是移动 HEAD 的指向，将其指向上一个快照（HEAD~）；然后再将该位置的快照回滚到暂存区域。
--soft选项
git reset --soft HEAD~ 命令就相当于只移动 HEAD 的指向，但并不会将快照回滚到暂存区域。相当于撤消了上一次的提交（commit）。一不小心提交了，后悔了，那么你就执行 git reset --soft HEAD~ 命令即可（此时执行 git log 命令，也不会再看到已经撤消了的那个提交）。
--hard选项
reset 不仅移动 HEAD 的指向，将快照回滚动到暂存区域，它还将暂存区域的文件还原到工作目录。

回滚指定快照
reset 不仅可以回滚指定快照，还可以回滚个别文件。

命令格式为： git reset 快照 文件名/路径

这样，它就会将忽略移动 HEAD 的指向这一步（因为你只是回滚快照的部分内容，并不是整个快照，所以 HEAD 的指向不应该发生改变），直接将指定快照的指定文件回滚到暂存区域。

不仅可以往回滚，还可以往前滚！
这里需要强调的是：reset 不仅是一个“复古”的命令，它不仅可以回到过去，还可以去到“未来”。

唯一的一个前提条件是：你需要知道指定快照的 ID 号。

那如果不小心把命令窗口关了不记得ID号怎么办？
命令：git reflog
Git记录的每一次操作的版本ID号

Git使用教程6---版本对比
目的：对比版本之间有哪些不同

准备工作
创建一个叫做 MyProject2 的新文件夹作为本次演示的项目，初始化 Git
创建一个 game.py 的文本，将下边代码拷贝进去：
import random

print('------------------我爱鱼C工作室------------------')
secret = random.randint(1,10)
temp = input("不妨猜一下小甲鱼现在心里想的是哪个数字：")
guess = int(temp)

while guess != secret:
    temp = input("哎呀，猜错了，请重新输入吧：")
    guess = int(temp)
    if guess == secret:
        print("卧槽，你是小甲鱼心里的蛔虫吗？！")
        print("哼，猜中了也没有奖励！")
    else:
        if guess > secret:
            print("大了，大了~~~")
        else:
            print("小了，小了~~~")
            
print("游戏结束，不玩啦^_^")
再创建一个 README.md 文件，写清楚这是一个课后作业的项目：

课后作业：文字游戏

执行 git add README.md game.py 命令将文件添加到暂存区域，接着执行 git commit -m "猜数字游戏" 提交项目的第一个快照
更改代码如下：
import random

print('------------------我爱鱼C工作室------------------')

times = 3
secret = random.randint(1,10)
guess = 0

print("不妨猜一下小甲鱼现在心里想的是哪个数字：", end=" ")

while (guess != secret) and (times > 0):
    temp = input()
    guess = int(temp)
    times = times - 1 # 用户每输入一次，可用机会就-1
    if guess == secret:
        print("哇哦，你是小甲鱼心里的蛔虫吗？！")
        print("哼，猜中了也没有奖励！")
    else:
        if guess > secret:
            print("哥，大了大了~~~")
        else:
            print("嘿，小了，小了~~~")
        if times > 0:
            print("再试一次吧：", end=" ")
        else:
            print("机会用光咯T_T")
            
print("游戏结束，不玩啦^_^")
更改README文件

《零基础入门学习Python》第004讲
课后作业：文字游戏

比较暂存区域与工作目录
直接执行 git diff 命令是比较暂存区域与工作目录的文件内容：

这里可能出现一个问题，直接执行的结果出现中文乱码。在cmd界面的冒号：后面输入q退出，使用Notepad++打开README文件，点击编码→转为UTF-8编码。（旧版本中选择UTF-8（无BOM），新版中的UTF-8默认为无BOM）重新执行git diff发现还是不行！怎么肥四？？在本菜查遍各网站论坛之后，终于找到了解决方法
执行以下三条命令(别问我明明是四条为啥说三条...)

git config --global i18n.commitencoding utf-8
git config --global i18n.logoutputencoding utf-8

export LESSCHARSET=utf-8 ## linux bash配置环境变量
set LESSCHARSET=utf-8 #windows配置环境变量
哈哈哈，终于搞定了！

现在来解释一下上面每一行的含义：
第一行：diff --git a/README.md b/README.md
表示对比的是存放在暂存区域的 README.md 和工作目录的 README.md
第二行：index 7966837..472a180 100644
表示对应文件的 ID 分别是 7966837 和 472a180，左边暂存区域，后边当前目录。最后的 100644 是指定文件的类型和权限
第三行：--- a/README.md
--- 表示该文件是旧文件（存放在暂存区域）
第四行：+++ b/README.md
+++ 表示该文件是新文件（存放在工作区域）
第五行：@@ -1 +1,2 @@
以 @@ 开头和结束，中间的“-”表示旧文件，“+”表示新文件，后边的数字表示“开始行号，显示行数”
第六、七行：

这是将两个文件合并显示的结果，前边有个 + 的绿色的那一行说明是新文件独有的，浅灰色的则是两个文件所共有的内容。所以，+1,2 表示新文件在合并显示中从第 1 行开始，显示 2 行。那为啥 -1 后边没有显示的行数？因为在合并显示的结果中，旧文件已经完全包含在新文件中了（也就是旧文件没有自己“独有的”内容）。
第八行：\ No newline at end of file
这是 Git 出于善意的提醒：文件不是以换行符结束。为什么会有这样多此一举的提醒呢？仔细推敲下你就会明白了：diff 将两个文件合并打印，到达最后一个字符的时候，无论文件中是否存在换行符，diff 都需要打印一个换行符！为啥？为了好看呗！！所以如果你的文件最后一个字符不是以换行符结尾，但 diff 又自行添加了一个换行符，所以它觉得有义务提醒你它这么做了！
最后的（:）是什么？
意思是窗口太小，没办法显示全部，正在等待命令（Vim编程知识）
移动命令
j、k：向下移动一行/向上移动一行
f、b：向下翻页/向上翻页
d、u：向下翻半页/向上翻半页
跳转命令
g、G：跳转到第一行/跳转到最后一行
先输入数字（如3），再输入g，表示跳转到该行（如第3行）
搜索命令
输入斜杠（/）或问号（?）,后面接搜索关键字
区别：斜杠（/）表示从当前位置向下搜索，问号（?）表示从当前位置向上搜索。
接着输入 n 表示顺着当前的搜索方向快速跳转到下个匹配的位置，大写的 N 则是与当前搜索方向相反。
退出和帮助
在点点（:）后边输入 q，表示退出 diff；输入 h 表示进入帮助界面，你会看到很多命令和功能，输入 q 可以退出帮助界面。

比较两个历史快照
我们执行 git commit -am "添加功能：玩家只有三次机会" 命令，添加并提交工作目录中的所有文件。执行 git log 命令，可以看到现在 Git 仓库中已经有两个快照了：


执行 git diff 6e26975 ed3708c 命令，即可比较 Git 仓库中两个快照的差异：

Git仓库中目前两个快照的差异
比较当前工作目录和 Git 仓库中的快照
我们稍微改动一下 README.md 文件的内容：


目前我们的 Git 仓库应该是：


三棵树是这样：


比较之前版本的快照与当前工作目录内容
输入 git diff ed3708c 命令即可

比较当前版本快照与当前工作目录内容
输入 git diff HEAD 命令即可

比较Git仓库与暂存区域
执行 git add README.md 命令，将第三版的 README.md 文件添加到暂存区域。
然后三棵树就是这样了：


如果希望比较最新提交的快照和暂存区域的文件，只需要执行 git diff --cached 命令；当然也可以指定其他快照，就是需要多写上一个 ID 值，即git diff --cached ID号。

哈哈哈，很乱有木有，其实就是这三棵树之间的相互比较，最后奉上终极奥义图：


Git使用教程7---修改最后一次提交、删除文件和重命名文件
问题出现：
Situation One：版本刚一提交（commit）到仓库，突然想起漏掉两个文件还没有添加（add）
Situation Two：版本刚一提交（commit）到仓库，突然想起版本说明写得不够全面，无法彰显你本次修改的重大意义……

由于使用reset命令过于繁琐，需要提交一个新的版本，这里可以使用带 --amend 选项的 commit 命令，（即git commit --amend）Git 会“更正”最近的一次提交。由于这里没有-m说明，会进入以下页面：


这个界面其实只是让你编辑提交说明而已。如果不需要修改，可以连续按下两个大写Z来退出，或者按下（:）再输入q!退出，Git会保留旧的提交说明。如果需要提交说明又不想用这么繁琐的方式，输入git commit --ammend -m “新的提交说明” 即可。

删除文件
问题一：不小心删除文件怎么办？
现在从工作目录中手动删除 README.md 文件，然后执行 git status 命令：


提醒使用 checkout 命令可以将暂存区域的文件恢复到工作目录：


文件就会重新返回。
问题二：那么如何彻底删除一个文件呢？
假如你不小心把小黄图下载到了工作目录，然后又不小心提交到了 Git 仓库：

执行 git rm yellow.jpg 命令：


此时工作目录中的小黄图（yellow.jpg）已经被删除……
但执行 git status 命令，你仍然发现 Git 还不肯松手：


意思是说它在仓库的快照中发现有个叫 yellow 的东西，但似乎在暂存区域和当前目录不见了！

此时可以执行 git reset --soft HEAD~ 命令将快照回滚到上一个位置，然后重新提交，Git 就不会再提小黄图的事儿了：


注意：rm 命令删除的只是工作目录和暂存区域的文件（即取消跟踪，在下次提交时不纳入版本管理）

问题三：我在工作目录中增加一个 test.py 文件，然后执行 git add test.py 命令将其添加到暂存区域，此时我修改 test.py 文件的内容，那么暂存区域和工作目录就是两个不同的 test.py 文件了，此时如果我执行 git rm test.py 命令，Git 会下意识地阻止我，这是怎么办？



因为两个不同内容的同名文件，谁知道你是不是搞清楚了都要删掉？还是提醒一下好，别等一下出错了又要赖机器……
根据提示，执行 git rm -f test.py 命令就可以把两个都删除。

问题四：我只想删除暂存区域的文件，保留工作目录的，应该怎么操作？
执行 git rm --cached 文件名 命令。

重命名文件
直接在工作目录重命名文件，执行git status出现错误：


正确的姿势应该是：

git mv 旧文件名 新文件名

注：Windows 使用 ren 命令修改文件名，Linux 是使用 mv 命令

教程6彩蛋
如何让Git 识别某些格式的文件，然后自主不跟踪它们？
比如工作目录中有三个文件1.temp、2.temp 和 3.temp，我们不希望后缀名为 temp 的文件被追踪，可是每次执行git status都会出现：


解决办法：在工作目录创建一个名为 .gitignore 的文件。

然后你发现 Windows 压根儿不允许你在文件管理器中创建以点（.）开头的文件。windows需要在命令行窗口创建（.）开头的文件。执行 echo *.temp > .gitignore 命令，创建一个 .gitignore 文件，并让 Git 忽略所有 .temp 后缀的文件：



好了，Git 已经忽略了所有的 *.temp 文件（你还可以把 .gitignore 文件也一并忽略）。

Git使用教程7---创建和切换分支
分支是什么？
假设你的大项目已经上线了（有上百万人在使用），过了一段时间你突然觉得应该添加一些新的功能，但是为了保险起见，你肯定不能在当前项目上直接进行开发，这时候你就有创建分支的需要了。


对于其它版本控制系统而言，创建分支常常需要完全创建一个源代码目录的副本，项目越大，耗费的时间就越多；而 Git 由于每一个结点都已经是一个完整的项目，所以只需要创建多一个“指针”（像 master）指向分支开始的位置即可。

创建分支
来到之前创建的项目MyProject2，


目前仓库的状态如下：


执行git status查看状态：


可以看到 README.md 文件被修改并添加到暂存区域（还没有提交），所以当前三棵树应该是这样：


创建分支，使用 git branch 分支名 命令：


没有任何提示说明分支创建成功（一般也不会失败啦，除非创建了同名的分支会提醒你一下），此时可以执行 git log --decorate 命令查看：

如果希望以“精简版”的方式显示，可以加上一个 --oneline 选项（即 git log --decorate --oneline），这样就只用一行来显示一个快照记录。


可以看到最新的快照后边多了一个 (HEAD -> master, feature)

它的意思是：目前有两个分支，一个是主分支（master），一个是刚才我们创建的新分支（feature），然后 HEAD 指针仍然指向默认的 master 分支。

所以目前仓库中的快照应该是这样：



切换分支
现在我们需要将工作环境切换到新创建的分支（feature）上，使用的就是之前我们欲言又止的 checkout 命令。执行 git checkout feature 命令：


这样 HEAD 指针就指向 feature 分支了：



现在我们进行一次提交（暂存区域还有一个更改的文件没有提交呢）：


现在仓库中的快照应该是酱紫（提交的快照由当前HEAD指针指向的分支来管理）：


然后我们将 HEAD 指针切回 master 分支：


细心的朋友会发现上一次对 README.md 文件的修改已经荡然无存了，这是因为我们的工作目录已经回到 master 分支的状态中：


现在对 README.md 文件进行修改（随便改改），然后执行 git commit -m "再次修改说明文件"：


目前仓库中的快照应该变成了酱紫：


执行 git log --oneline --decorate --graph --all 命令：

--graph 选项表示让 Git 绘制分支图，--all 表示显示所有分支


Git使用教程9---合并和删除分支
合并分支
当一个子分支的使命完结之后，它就应该回归到主分支中去。


合并分支我们使用 merge 命令，执行 git merge feature 命令，将 feature 分支合并到 HEAD 所在的分支（master）上：


从 Git 提示的内容来看，我们知道这次的合并并没有成功，Git 说：

合并 README.md 文件的时候出现冲突。

所以自动合并失败；请修改冲突的内容并重新提交快照。

意思是说现在你需要先解决冲突的问题，Git 才能进行合并操作。所谓冲突，无非就是像两个分支中存在同名但内容却不同的文件，Git 不知道你要舍弃哪一个或保留哪一个，所以需要你自己来决定。
此时执行 git status 命令也会显示需要你解决的冲突：


然后 Git 会在有冲突的文件中加入一些标记，不信你打开 README.md 文件看看：


以“=======”为界，上到“<<<<<<< HEAD”的内容表示当前分支，下到“>>>>>>> feature”表示待合并的 feature 分支，之间的内容就是冲突的地方。

现在我们将 README.md 统一修改（去掉 <<<<<<< HEAD 等内容）
保存文件，然后提交快照：


执行 git log --decorate --all --graph --oneline 命令，可以看到此时的分支已经自动合并了:


当然，如果不存在冲突，就不用搞这么多了……举个例子：
执行 git checkout -b feature2 命令（相当于 git branch feature2 和 git checkout feature2 两个命令的合体）：


在工作目录随便创建一个文本文件（feature2.txt）并提交快照：


执行 git log --decorate --all --graph --oneline 命令：


可以看到，feature2 分支比 master 分支快了一步。现在我们切换回 master 分支，并将 feature2 分支合并进来：


这次 Git 只显示了 Fast-forward（快进）这词儿，这是因为 feature2 这个分支的父结点是 master 分支，所以 Git 只需要简单移动 master 的指向即可。

执行 git log --decorate --all --graph --oneline 命令：


删除分支
删除分支，使用 git branch -d 分支名 命令：


执行 git log --decorate --all --graph --oneline 命令：


由于 Git 的分支原理实际上只是通过一个指针记载，所以创建和删除分支都几乎是瞬间完成。

注意：如果试图删除未合并的分支，Git 会提示你“该分支未完全合并，如果你确定要删除，请使用 git branch -D 分支名 命令。

彩蛋：Git的两种合并方式 --- Fast-forward 和 Three-way merge
Fast-forward
所谓的 Fast-forward 就是当待合并的分支位于目标分支的直接上游时，Git 只需把目标分支的指针直接移动即可实现合并。

比如下面图片中 master 分支是位于 feature2 分支的直接上游：


将 feature2 分支合并到 master 分支，只需要移动 master 的指针即可：


Three-way merge
如果待合并的两个分支不在同一条线上，那么进行合并就需要解决一个根本的问题 —— 冲突！

为何两个分支在同一条线上就不会冲突呢？

因为 Git 的快照是按时间顺序提交的，所以在同一条线上的两个快照，它们是有先后顺序的，尽管两者可能出现同名文件不同内容，Git 会认为这是“改变”而不是“冲突”。

举个例子：


合并 C3 和 C4 得到 C5，但 C5 应该如何处理“冲突”呢？

SVN 会把问题抛给用户，让用户自行解决；Git 则显得更为高明，它会找到第三个快照，然后综合三者特点自动解决冲突。

那第三个快照应该如何决定呢？

没错，应该找两者的共同“祖先”作为参照物，一比较就知道两个分支都干了些什么。

图片中 C3 和 C4 的共同祖先是 C1，可以看到 C3 和 C4 分别增加了 test2.py 和 test1.py 两个文件。因为对比之后发现三者并没有冲突，所以 C5 应该是三者的合体，即同时拥有 common.py、test1.py 和 test2.py 三个文件。

另外，值得一提的是，Git 这种合并方式也适用于同名文件的不同更改。

举个例子：


这里 C3 和 C4 都只有一个文件（test.txt），但是内容却不一样。如果这样合并，你猜 Git 会不会报“冲突”？

答案是不会的！

因为 Git 找到它们的共同祖先 C1，可以看到 C3 和 C4 都是在 C1 的基础上进行添加（C4 在第 2 行添加了“I”，C3 在第 4 行增加了“FishC”，C1 第 3 行的“love”是它们共同拥有的），同时在每一行并没有产生冲突的地方，所以自动合并后的 C5 是这样的：

# test.txt
I
love
FishC
注意：如果 Git 检测到同一行有不同的内容，还是会报冲突并让你自行决定谁去谁留的！

Git使用教程10---匿名分支和checkout命令
匿名分支
创建一个新的文件夹（MyProject3），然后初始化 git。依次创建三个文件并提交（每创建一个文件提交一次）：


上一节课我们讲的是使用 branch 命令创建一个分支，然后使用 checkout 命令切换分支。

如果在没创建分支的情况下执行 checkout 命令，会有怎样的事情发生呢？

我们不妨试试看，执行 git checkout HEAD~ 命令：


当前的 HEAD 指针处于分离状态，你可以环顾四周，做一些实验性修改并提交它们，并且你可以在这个状态中丢弃任何你所做的提交，而不影响任何分支，做法是执行 checkout 命令切换回别的分支。

如果你希望创建一个新分支，并保持你所做创建的提交，你可以（现在或稍后）通过使用带有 -b 选项的 checkout 命令实现。例如：

git checkout -b <new-branch-name>

HEAD 指针当前指向 52861cf... 2.txt

你使用了 checkout 命令但没有指定分支名，所以 Git 帮你创建了一个匿名分支，OK，既然是匿名，那么当你切换到别的分支时，这个匿名分支中的所有提交都会被丢弃掉（因为你都没给人家命名，反正以后都找不回了，不丢了干啥？）。因此，你可以利用匿名分支来做做实验什么的，反正不会有负面影响。

来，我们试试，在工作目录中创建一个 4.txt（你会发现 3.txt 不见了，这是因为 checkout 将环境切换到上一次提交了），然后提交


执行 git log --decorate --all --graph --oneline 命令


可以看到有两个分支，但 HEAD 所在的分支并没有名字（匿名分支），那现在我们把 HEAD 切回 master 分支：


警告：你残留一个没有连接任何分支的提交：

178d909 4.txt

如果你想通过创建一个分支来连接它，这将是一个好时机，请执行：

git branch <new-branch-name> 178d909

已经切换到 'master' 分支

现在再来查看提交日志，可以看到匿名分支已经荡然无存：


再论checkout
事实上呢，checkout 命令有两种功能：

从历史快照（或者暂存区域）中拷贝文件到工作目录
切换分支
从历史快照（或者暂存区域）中拷贝文件到工作目录

当给定某个文件名时，Git 会从指定的提交中拷贝文件到暂存区域和工作目录。比如执行 git checkout HEAD~ README.md 命令会将上一个快照中的 README.md 文件复制到工作目录和暂存区域中：


如果命令中没有指定具体的快照 ID，则将从暂存区域恢复指定文件到工作目录（git checkout README.md）：


有些朋友可能会问：“上次看你在文件名的前边有加两个横杆（--），这次怎么就没有了呢？”

问得好，Git 提醒你写成 git checkout -- README.md 的形式，那是为了预防你恰好有一个分支叫做 README.md，那么它就搞不懂你要恢复文件还是切换分支了，所以约定两个横杆（--）后边跟的是文件名。

反过来说，如果你确保你没有一个叫做 README.md 的分支，你直接写 git checkout README.md 也是妥妥的没问题啦

切换分支
首先我们知道 Git 的分支其实就是添加一个指向快照的指针，其次我们还知道切换分支除了修改 HEAD 指针的指向，还会改变暂存区域和工作目录的内容。

所以执行 git checkout 373c0 命令，Git 主要就是做了下边这两件事（当然事实上 Git 还做了更多）：


那回过头来，如果我们只想恢复指定的文件/路径，那么我们只需要指定具体的文件，Git 就会忽略第一步修改 HEAD 指向的操作，这不正跟之前讲 reset 命令的时候一样吗？

checkout 命令和 reset 命令的区别
恢复文件

checkout 命令和 reset 命令都可以用于恢复指定快照的指定文件，并且它们都不会改变 HEAD 指针的指向。

下面开始划重点：

它们的区别是 reset 命令只将指定文件恢复到暂存区域（--mixed），而 checkout 命令是同时覆盖暂存区域和工作目录。

注意：也许你试图使用 git reset --hard HEAD~ README.md 命令让 reset 同时覆盖工作目录，但 Git 会告诉你这是徒劳（此时 reset 不允许使用 --soft 或 --hard 选项）。

这样看来，在恢复文件方面，reset 命令要比 checkout 命令更安全一些。

恢复快照

reset 命令是用来“回到过去”的，根据选项的不同，reset 命令将移动 HEAD 指针（--soft） -> 覆盖暂存区域（--mixed，默认）-> 覆盖工作目录（--hard）。

checkout 命令虽说是用于切换分支，但前面你也看到了，它事实上也是通过移动 HEAD 指针和覆盖暂存区域、工作目录来实现的。

那问题来了：它们有什么区别呢？

下面开始划重点：

第一个区别是，对于 reset --hard 命令来说，checkout 命令更安全。因为 checkout 命令在切换分支前会先检查一下当前的工作状态，如果不是“clean”的话，Git 不会允许你这样做；而 reset --hard 命令则是直接覆盖所有数据。

另一个区别是如何更新 HEAD 指向，reset 命令会移动 HEAD 所在分支的指向，而 checkout 命令只会移动 HEAD 自身来指向另一个分支。

看文字你肯定懵，我们举例说明。

来，大家先把刚才的例子改成下边这样：


执行 git checkout feature 命令：


可以看到只是 HEAD 指针跑到 feature 分支那儿去了。

好，我们执行 git checkout master 命令将其切回。

现在执行 git reset --hard feature 命令：


彩蛋
通常情况下，Git 会尽可能地尝试使用 Fast-forward 方式来合并分支，因为这样效率非常高，只有在万不得已的时候才使用三方合并（Three-way merge）

但是，有时候 Fast-forward 的方式却很容易让我们忽略了分支的存在！

举个例子，比如下面这样：


如果我们把“feature”分支删除，就会直接丢掉分支的信息：


根本就不知道有个分支存在过……

可有时候我们确实希望保留分支的信息，应该怎么办呢？

只需要在 merge 的时候使用 --no-ff 选项即可告诉 Git 不要使用 Fast-forward 方式合并分支。

这样 Git 就会乖乖地使用三方合并（Three-way merge）：


OK，这样就算删掉了“feature”分支，我们仍然可以很容易看出有个分支曾经存在过：
