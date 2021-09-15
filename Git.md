## Git

### 一、本地初始化

**1.1**

> 命令：git init

> 效果：
>
> 

注意：.git 目录中存放的是本地库相关的子目录和文件，不要删除，也不要胡乱修改

**1.2设置签名**

> **形式**
>
> 用户名：
>
> Email地址：
>
> 作用：区分不同开发人员的身份
>
> 辨析：这里设置的签名和登录的远程库（代码托管中心）的账号、密码没有任何关系
>
> 命令
>
> * 项目级别/仓库级别：仅在本地仓库范围内有效
>   * git config user.name username(自定义)
>   * git config user.email emailname(自定义)
>   * 信息保存位置， ./.git/config
> * 系统用户级别：登录当前操作系统的用户范围
>   * git config --global user.name username(自定义)
>   * git config --global user.email emailname(自定义,例：xxxxx@qq.com)
> * 级别优先级：
>   * 就近原则：项目级别优先于系统用户级别，二者都有时采用项目级别的签名
>   * 如果只有系统级别的签名，就以系统用户级别的签名
>   * 二者都没有不允许

### 二、Git命令

> ```text
> git add filename （把文件加到暂存区） 工作区--》暂存区
> git restore --staged （把文件移出暂存区）
> git rm --cached filename
> git status （查看git目录状态）
> git commit filename (提交文件到本地库，需要进vim编辑器写信息)
> git commit -m "commit message" filename (提交文件到本地库，不需要进vim编辑器写信息)
> git log (查看版本记录)空格：向下翻页    b:向上翻页    q:退出
> git log --pretty=oneline (以简洁的方式显示)
> git log --oneline (以简洁+哈希取部分显示)
> git reflog (HEAD@移动到当前版本需要多少布)
> ```
>
> 工作区（写代码）-->git add-->暂存区（临时存储）-->git commit-->本地库（历史版本）

### 三、前进后退(版本切换)

> **基于索引**
>
> ```text
> git reset --hard 版本索引值
> ```
>
> **基于^符号**：只能后退
>
> ```text
> git reset --hard HEAD^ (回退一步)  一个^退一步
> ```
>
> **基于~符号**：只能后退
>
> ```text
> git reset --hard HEAD~n (回退n步)
> ```

> **reset命令的三个参数对比**
>
> ```text
> --soft参数    （仅仅在本地库移动HEAD指针）
> --mixed参数    （在本地库移动HEAD指针；重置暂存区）
> --hard参数    （在本地库移动HEAD指针；重置暂存区；重置工作区）
> ```

### 四、文件操作

> **文件找回**
>
> ```text
> 前提：删除前，文件存在时的状态提交到了本地仓库
> 操作：git reset --hard 版本索引值
> 		删除操作已经提交到本地库：指针位置指向历史记录
> 		删除操作尚未提交到本地库：指针位置使用HEAD
> ```

> **文件比较**
>
> ```text
> git diff filename
> 将工作区中的文件和暂存区进行比较
> git diff 历史版本  filename
> 将工作区中的文件和本地库历史记录进行比较（不指定文件名则比较所有文件）
> ```

### 五、分支管理

> ```text
> git branch -v (查看现有分支)
> git branch 分支name (创建分支)
> git checkout 分支name (切换分支)
> ```

> **合并分支**
>
> * 第一步：切换到接受修改的分支（被合并，增加新内容）
>
>   ```text
>   git checkout 分支name (切换分支)
>   ```
>
>   
>
> * 第二步：执行merge命令
>
>   ```text
>   git merge 分支name
>   ```

**解决冲突**

> **冲突表现**
>
> ```text
> <<<<<<<<<
> 
> =========
> 
> >>>>>>>>>
> ```
>
> **冲突解决**
>
> ```text
> 修改文件直到满意
> git add filename
> git commit (不能带文件名，需日志)
> ```

## Git+Github

> **创建Github账号**
>
> ```text
> https://git.com
> ```
>
> 登录账号

> 创建第一个远程库Git+
>
> 登录进去后点头像右边“+”符号
>
> 选择new repository(可能需要验证邮箱)
>
> 填写repository name 
>
> public或private看自己意愿选择
>
> 点击最下创建

> **本地库推送远程库**
>
> **别名**
>
> ```text
> git remote -v (查看别名)
> git remote add NewName OldName (设置别名)
> 例：git remote add origin https://github.com/xxxxxxxxxxx/xxxx.git
> ```
>
> **推送**
>
> ```
> git push NewFilename 分支名 
> 例：git push origin master
> 填写github账号密码
> 等待一下。。。
> Bug:  guthup拒绝了老版本git那种弹窗验证方式 (弹框登录，推送不了就更新git)
> ```

> 刷新github仓库查看文件

> **克隆**
>
> ```text
> git clone 仓库地址
> 克隆效果：
> 完整地把远程库下载到本地
> 创建远程地址别名
> 初始化本地库
> ```

> **邀请成员**
>
> 远程仓库页面
>
> Settings-->Collaborators-->输入邀请人账号
>
> 负责链接，发送给邀请人

> SSH  Git连接GitHub
>
> ```
> ssh-keygen -t rsa -C Github的注册邮箱
> cd .ssh/
> ```
>
> 