# Git 

| Git 术语 | 通俗解释 |
|---------|----------|
| Git|本地的版本控制工具，记录代码每一次修改，可回退、对比、分支开发 |
|GitHub / GitLab |远程代码托管平台，把本地 Git 仓库同步到云端，方便协作、备份 |
仓库（Repository）|	存放项目代码 + 所有修改历史的文件夹，本地一个、远程一个
工作区（Working Directory）|	你在编辑器里写代码的文件夹，就是当前正在编辑文件的地方
暂存区（Staging Area）|	提交前的 “缓冲带”，用来挑选要提交的修改（对应 git add）
本地仓库（Local Repository）|	Git 在本地存的版本历史，git commit 后就永久存到这里
远程仓库（Remote Repository）	|GitHub/GitLab 上的仓库，git push 推上去，git pull 拉下来
提交（Commit）|	一次版本快照，必须写提交信息，相当于给代码拍一张带备注的照片
分支（Branch）|	独立的开发线，默认主分支叫 main（旧版叫 master），开分支不影响主代码
合并（Merge）|	把一个分支的代码合并到另一个分支（比如把开发分支合到主分支）
克隆（Clone）|	把远程仓库完整复制到本地（git clone）


### 一、仓库初始化与配置
| 命令 | 作用  |	说明 |
|---------|----------|---------|
git init|	初始化本地 Git 仓库	|在当前文件夹创建 .git 目录，开启版本控制|
git clone <仓库地址> |	克隆远程仓库到本地	|完整复制远程仓库（含所有历史），如 git clone https://github.com/xxx/xxx.git
git config --global user.name "你的名字"|	配置全局用户名	|所有仓库通用，用于标识提交者
git config --global user.email "你的邮箱"|	配置全局邮箱	|必须和 GitHub/GitLab 注册邮箱一致
git config --list	|查看所有配置	|检查用户名、邮箱等配置是否正确 

### 二、日常提交流程（核心必用）
#### 1 查看状态
命令	|作用
|---------|----------|
git status|	查看工作区 / 暂存区状态，显示修改、新增、待提交文件
git diff	|查看工作区未暂存的修改内容
git diff --cached	|查看暂存区已 add 但未 commit 的修改
#### 2 暂存与提交
命令|	作用|	说明|
|---------|----------|---------|
git add <文件名>	|把指定文件加入暂存区|	如 git add git_learn.md
git add .	|把当前目录所有修改 / 新增文件加入暂存区|	最常用，快速暂存所有变更
git commit -m "提交说明"	|提交暂存区到本地仓库|	必须写清晰的提交信息，如 feat: 新增Git学习笔记
git commit -am "提交说明"	|跳过 add，直接提交所有已跟踪文件的修改|	仅适用于已被 Git 跟踪的文件，新增文件需先 add
git restore --staged <文件名>	|取消暂存指定文件|	把文件从暂存区退回工作区

### 三、分支与合并
命令	|作用	|说明
|---------|----------|---------|
git branch	|查看本地所有分支	|当前分支会标 *
git branch <分支名>	|新建分支	|如 git branch feature/login
git checkout <分支名>	|切换分支|	如 git checkout main 切回主分支
git checkout -b <分支名>	|新建 + 切换分支|	一步完成，最常用
git merge <分支名>	|合并指定分支到当前分支	|如在 main 分支执行 git merge feature/login
git branch -d <分支名>	|删除已合并的分支	|未合并分支用 -D 强制删除
git branch -a	|查看所有分支（含远程）	|查看远程仓库的分支

### 四、远程仓库操作（push/pull）
命令	|作用	|说明
|---------|----------|---------|
git remote -v	|查看远程仓库地址	|确认远程仓库是否配置正确
git remote add origin <仓库地址>|	关联远程仓库|	把本地仓库和远程仓库绑定
git push origin <分支名>	|把本地分支推送到远程|	如 git push origin main
git push -u origin <分支名>	|首次推送，绑定远程分支|	后续直接 git push 即可
git pull origin <分支名>	|拉取远程分支最新代码到本地|	协作时先 pull 再 push，避免冲突
git fetch origin	|拉取远程所有分支更新，但不合并|	安全查看远程变更，再手动 merge

### 五、版本回退与撤销
命令	|作用	|说明
|---------|----------|---------|
git log	|查看提交历史	|按时间倒序显示所有 commit
git log --oneline	|精简查看提交历史|	只显示 commit 哈希和提交信息，最常用
git reset --hard <commit哈希>	|回退到指定 commit|	危险操作：会丢弃回退点之后的所有修改
git reset --soft <commit哈希>|	回退 commit，保留修改到暂存区|	撤销提交但不丢代码
git checkout -- <文件名>	|撤销工作区文件的修改|	把文件恢复到上一次 commit 的状态
git revert <commit哈希>|	撤销指定 commit 的修改|	安全回退，会生成新的 commit，不影响历史

### 六、其他实用命令
命令 |	作用	
|---------|----------|
git stash	|暂存当前工作区修改	切换分支前临时保存未提交的代码
git stash pop|	恢复暂存的修改	把 stash 的代码恢复到工作区
git gc --aggressive|	清理 Git 缓存，优化仓库	解决仓库过大、提交卡顿问题
git rm --cached <文件名>	|从 Git 跟踪中删除文件，保留本地文件	误 add 大文件时用
git tag <版本号>	|打标签	如 git tag v1.0.0，用于版本发布

### 七、新手避坑指南
1. *提交前必做：* 先 git status 确认变更，再 git add、git commit，避免误提交。
2. *协作必做：* push 前先 git pull，避免代码冲突。
3. *回退谨慎：* git reset --hard 会永久丢失代码，仅在本地未 push 时使用。
4. *提交信息规范：* 用 feat:（新功能）、fix:（修复 bug）、docs:（文档）等前缀，方便追溯。