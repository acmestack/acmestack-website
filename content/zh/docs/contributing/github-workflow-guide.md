---
title: "GitHub 工作流程指南"
description: "GitHub 工作流程指南"
lead: "GitHub 工作流程指南"
date: 2020-11-12T13:26:54+01:00
lastmod: 2020-11-12T13:26:54+01:00
draft: false
images: []
menu:
  docs:
    parent: "contributing"
weight: 44
toc: true
---

## 1. 从云端 Fork

1. 打开 https://github.com/acmestack
2. 选中一个项目
2. 单击 `Fork` 按钮 (右上角) 建立一个基于云端的fork.

## 2. Clone fork 到本地

> 根据 Go语言的 [工作区说明](https://golang.org/doc/code.html#Workspaces), 根据以下命令将克隆下来的项目代码放在您的 GOPATH 上。

  ```sh
  git clone git@github.com:<your_name>/{project-name}.git
  ```

## 3. 设置远程仓库以同步更新

  ```sh
  git remote add upstream https://github.com/acmestack/{project-name}.git
  ```

### 保持分支同步

您将需要定期从`upstream`仓库中获取变更来保持您的工作分支同步。请注意，根据您使用的仓库，默认分支可能叫做“main”而不是“master”。

确保您的本地仓库位于您的工作分支上并运行以下命令以使其保持同步：

```sh
git fetch upstream
git rebase upstream/master
```

请不要使用 `git pull` 而不是以上的 `fetch` 和
`rebase`. 由于 `git pull`  执行合并，它会创建合并提交。这些使提交历史变得混乱，违反了提交应该是人们易于理解和有用的原则（见下文）。

您也可以考虑通过 `git config branch.autoSetupRebase always` 更改您的`.git/config` 文件，以更改 `git pull` 的行为，或其他非合并选项，例如 `git pull --rebase`

## 4. 创建一个工作分支

>以下适用于任何一个新 issue.

让您的本地master分支更新到最新状态。请注意，根据您使用的存储库，默认分支可能称为“main”而不是“master”。

```sh
cd $working_dir/{project-name}
git fetch upstream
git checkout master
git rebase upstream/master
```

### 选择或创建一个 issue

创建您的新分支.

```sh
git checkout -b issue-id
```

您现在可以在 issue-id`分支上编辑文件

## 5. 提交您的变更

您可能希望定期提交您的变更。您可能会返回并多次编辑、构建和测试。在这样的几个循环之后，你可能会[修改你之前的提交](https://www.w3schools.com/git/git_amend.asp).

```sh
git commit
```

## 6. 推送到 GitHub

当您的更改准备好review时，将您的工作分支推送到 GitHub 上的 fork仓库

```sh
git push -f <your_name> issue-id
```

## 7. 创建一个Pull Request

1. 打开您的 fork `https://github.com/<your_name>/{project-name}`
2. 单击`issue-id` 分支旁边的 **Compare & Pull Request** 按钮 。
3. 查看pull request [流程](../pull-requests)以获取更多详细信息和建议。

如果您有`upstream` 写入权限，请不要使用 GitHub UI 创建 PR，因为 GitHub 将在主仓库中创建 PR 分支，而不是在您的 fork 中。

### 获得代码审查

一旦您的pull request 被打开，它将被分配给一个或多个审阅者。这些审阅者将进行彻底的代码审查，寻找正确性、错误、改进机会、文档和注释以及样式

将审阅评论所做的更改提交到您 fork 上的同一分支。 小的 PR 很容易审查。非常大的 PR 很难审查。

### 压缩提交

审核后，通过压缩提交来准备 PR 以进行合并。

审查后留在分支上的所有提交都应代表有意义的里程碑或工作单元。使用提交来增加开发和审查过程的清晰度。

在合并 PR 之前，压缩以下类型的提交：

- Fixes/review feedback
- Typos
- Merges and rebases
- Work in progress

如果可以的话，旨在让 PR 中的每个提交都独立编译和通过测试，但这不是必需的。特别是，必须删除`merge` 提交，因为它们不会通过测试。

要压缩您的提交，请执行 [interactive rebase](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History):

1. 检查您的 git 分支:

  ```
  git status
  ```

  输出应该与此类似：

  ```
  On branch your-contribution
  Your branch is up to date with 'origin/your-contribution'.
  ```

2. 使用特定的提交哈希开始一个interactive rebase, 或使用从您上次提交开始倒数 `HEAD~<n>`, 其中 `<n>`表示要包含在 rebase.

  ```
  git rebase -i HEAD~3
  ```

  输出应该与此类似：

  ```
  pick 2ebe926 Original commit
  pick 31f33e9 Address feedback
  pick b0315fe Second unit of work

  # Rebase 7c34fc9..b0315ff onto 7c34fc9 (3 commands)
  #
  # Commands:
  # p, pick <commit> = use commit
  # r, reword <commit> = use commit, but edit the commit message
  # e, edit <commit> = use commit, but stop for amending
  # s, squash <commit> = use commit, but meld into previous commit
  # f, fixup <commit> = like "squash", but discard this commit's log message

  ...

  ```

3. 使用命令行文本编辑器将单词`pick`更改为`squash`来压缩您想要压缩的提交，然后保存更改并继续 rebase：

```sh
pick 2ebe926 Original commit
squash 31f33e9 Address feedback
pick b0315fe Second unit of work

...

```

  保存更改后的输出应如下所示：

  ```sh
  [detached HEAD 61fdded] Second unit of work
   Date: Thu Mar 5 19:01:32 2020 +0100
   2 files changed, 15 insertions(+), 1 deletion(-)

   ...

  Successfully rebased and updated refs/heads/master.
  ```

4. 强制将您的更改推送到远程分支：

```sh
git push --force
```

对于诸如自动文档格式化之类的大规模自动化修复，对工具的更改使用一个或多个提交，并使用最后一次提交来整体应用修复。这使得审查更容易。

## 8. 合并提交

一旦你收到审查和批准，你的提交就会被压缩，你的 PR 就可以合并了

在 Reviewer 和 Approver 都批准 PR 后，合并会自动发生。如果你还没有压缩你的提交，他们可能会在批准 PR 之前要求你这样做。

## 9. 还原提交

如果您希望还原提交，请使用以下说明。

如果您拥有upstream写入权限, 请不要使用 GitHub UI 中的 `Revert`按钮来创建 PR，因为 GitHub 将在主仓库库中而不是在您的 fork 中创建 PR 分支。


- 创建一个分支并将其与upstream同步。请注意，根据您使用的仓库，默认分支可能称为“main”而不是“master”。

  ```sh
  # create a branch
  git checkout -b myrevert

  # sync the branch with upstream
  git fetch upstream
  git rebase upstream/master
  ```

- 如果您希望恢复的提交是*merge commit*，请使用以下命令：

  ```sh
  # SHA is the hash of the merge commit you wish to revert
  git revert -m 1 <SHA>
  ```

- 如果是 *single commit*, 使用以下命令:

  ```sh
  # SHA is the hash of the single commit you wish to revert
  git revert <SHA>
  ```

- 这将创建一个新的提交来还原更改。 推送该新提交到您的远程仓库。
  ```sh
  git push <your_remote_name> myrevert
  ```

- 最后, 用这个分支创建一个[ Pull Request](#7-create-a-pull-request) 。

## 10. Commit 信息模板

[commit message guidelines](../pull-requests#commit-message-guidelines)

1. Specify the type of commit:
   - feat: The new feature you're adding to a particular application
   - fix: A bug fix
   - style: Feature and updates related to styling
   - refactor: Refactoring a specific section of the codebase
   - test: Everything related to testing
   - docs: Everything related to documentation
   - chore: Regular code maintenance.[ You can also use emojis to represent commit types]
2. Separate the subject from the body with a blank line
3. Your commit message should not contain any whitespace errors
4. Remove unnecessary punctuation marks
5. Do not end the subject line with a period
6. Capitalize the subject line and each paragraph
7. Use the imperative mood in the subject line
8. Use the body to explain what changes you have made and why you made them.
9. Do not assume the reviewer understands what the original problem was, ensure you add it.
10. Do not think your code is self-explanatory
11. Follow the commit convention defined by your team
