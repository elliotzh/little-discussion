将当前 worktree 分支同步到 main 的最新状态，如有冲突则给出解决方案。

## 前置检查

1. 运行 `git worktree list` 确认当前处于 worktree（非主 worktree）中
2. 如果当前在主 worktree 上，告知用户"已在 main 分支，无需 rebase"并结束

## 第一步：保存当前工作

1. 运行 `git status` 检查是否有未提交的改动（含未暂存、已暂存、未追踪文件）
2. 如果有改动：
   - 运行 `git stash --include-untracked` 暂存所有改动
   - 记住已执行 stash，后续需要恢复

## 第二步：执行 rebase

1. 运行 `git fetch origin` 获取最新远程状态
2. 运行 `git rebase main`
3. 如果 rebase 成功（无冲突），跳到第四步

## 第三步：处理冲突

如果 rebase 产生冲突：

1. 运行 `git diff --name-only --diff-filter=U` 列出所有冲突文件
2. 收集冲突相关的 commit message 以理解改动意图：
   - 运行 `git log --oneline main..REBASE_HEAD` 查看当前分支上正在被 rebase 的 commit
   - 运行 `git log --oneline REBASE_HEAD..main` 查看 main 上的新 commit
   - 对于每个冲突文件，可进一步运行 `git log --oneline main..REBASE_HEAD -- <文件>` 和 `git log --oneline REBASE_HEAD..main -- <文件>` 查看该文件相关的 commit
3. 对每个冲突文件：
   - 读取文件内容，找到所有冲突标记（`<<<<<<<`、`=======`、`>>>>>>>`）
   - 结合 commit message 和文件内容，分析冲突双方的意图：
     - **当前分支（HEAD）的改动**：做了什么、为什么（引用相关 commit message）
     - **main 的改动**：做了什么、为什么（引用相关 commit message）
   - 给出解决方案（resolve proposal），说明推荐如何合并及理由
3. 汇总所有冲突文件的解决方案，格式如下：

```
### 冲突文件：[文件路径]

**当前分支的改动：** ...
**main 的改动：** ...
**推荐解决方案：** ...
**理由：** ...
```

4. 使用 AskUserQuestion 询问用户：
   - 选项 1：按推荐方案自动解决
   - 选项 2：放弃 rebase（执行 `git rebase --abort`）

5. 如果用户选择自动解决：
   - 按方案编辑每个冲突文件，移除所有冲突标记
   - 对每个已解决的文件运行 `git add <文件>`
   - 运行 `git rebase --continue`
   - 如果后续 commit 又产生新冲突，重复本步骤
   - 全部解决后，进入第四步

6. 如果用户选择放弃：
   - 运行 `git rebase --abort`
   - 如果第一步执行了 stash，运行 `git stash pop` 恢复改动
   - 告知用户已恢复到 rebase 前的状态，结束流程

## 第四步：恢复工作区

1. 如果第一步执行了 stash，运行 `git stash pop` 恢复改动
2. 如果 stash pop 产生冲突，按第三步相同的方式分析并给出解决方案
3. 运行 `git status` 展示最终状态
4. 告知用户同步完成
