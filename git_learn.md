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
