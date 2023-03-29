# 常用命令清单

| **操作命令**                                      | 描述                      |
| --------------------------------------------- | ----------------------- |
| **分支**                                        | ​                       |
| `git branch`                                  | 列出全部本地分支                |
| `git branch -a`                               | 列出全部本地与远程分支             |
| `git checkout -b <branch_name>`               | 创建本地新分支并切换为当前分支         |
| `git checkout <branch_name>`                  | 切换本地已有分支为当前分支           |
| `git push origin <branch_name>`               | 推送分支到远程                 |
| `git branch -m <new_name>`                    | 重命名当前分支                 |
| `git branch -d <branch_name>`                 | 删除本地分支                  |
| `git push origin :<branch_name>`              | 删除远程分支                  |
| **历史**                                        | ​                       |
| `git log --oneline`                           | 显示所有提交（单行模式：仅哈希值与提交信息）  |
| `git log -2`                                  | 显示最近 N 条提交              |
| `git log -p -2`                               | 显示最近 N 条提交，并显示相应修改      |
| `git diff`                                    | 显示当前工作区与上次提交版本的区别       |
| `git diff <myfile>`                           | 显示某个文件与上次提交版本的区别        |
| `git blame <myfile>`                          | 显示某个文件被「谁」在什么时候修改过      |
| `git remote show origin`                      | 显示远程分支与本地分支的跟踪关系        |
| **清理**                                        | ​                       |
| `git clean -f`                                | 删除全部未跟踪的文件              |
| `git clean -df`                               | 删除全部未跟踪的文件和文件夹          |
| `git checkout -- .`                           | 重置本地全部更改                |
| `git reset HEAD <myfile>`                     | 移除缓冲区中的某个文件             |
| `git reset $(git merge-base master feaure/x)` | 把 MR 的分支的合并记录移除，压缩为一条提交 |
| **标签**                                        | ​                       |
| `git tag`                                     | 列出全部标签                  |
| `git tag -a <tag_name> -m "tag message"`      | 创建新标签                   |
| `git push --tags`                             | 推送全部标签到远程               |
| **暂存**                                        | ​                       |
| `git stash save "<stash name>" && git stash`  | 暂存工作区全部改动               |
| `git stash list`                              | 列出全部暂存                  |
| `git stash pop`                               | 恢复最新暂存到工作区              |
| **配置**                                        | ​                       |
| `git config -l`                               | 列出当前已有配置                |
| `git config --local -l`                       | 列出当前仓库配置                |
| `git config --global -l`                      | 列出全局配置                  |
| `git config --system -l`                      | 列出系统配置                  |
| `git config --global user.name <username>`    | 设置用户名                   |
| `git config --global user.email <email>`      | 设置用户邮箱                  |
| **同步上游**                                      | ​                       |
| `git fetch upstream`                          | 获取上游分支及提交               |
| `git checkout master`                         | 切换本地 `master` 分支        |
| `git merge upstream/master`                   | 合并上游更改到本地 `master` 分支   |
| **工作空间**                                      | ​                       |
| `git worktree add <path> <branch>`            | 添加工作空间                  |
| `git worktree list`                           | 列出全部工作空间                |
| `git worktree prune`                          | 清理工作空间                  |
