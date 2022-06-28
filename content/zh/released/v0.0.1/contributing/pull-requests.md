---
title: "Pull Request 流程"
description: "该文档解释了向 AcmeStack 项目及其关联的子仓库提交Pull Request的过程和最佳实践。
它应该作为所有贡献者的参考，对新的和不经常提交的人尤其有用。"
lead: "该文档解释了向 AcmeStack 项目及其关联的子仓库提交Pull Request的过程和最佳实践。
它应该作为所有贡献者的参考，对新的和不经常提交的人尤其有用。"
date: 2020-10-06T08:49:31+00:00
lastmod: 2020-10-06T08:49:31+00:00
draft: false
images: []
menu:
  docs:
    parent: "contributing"
weight: 66
toc: true
---

# 在您提交 Pull Request之前

本指南适用于已经提交Pull Request的贡献者。

首次贡献者应前往[贡献者指南](../guide) 开始，[贡献者指南](../guide)也适用于**所有开发者**。

**确保您的pull request符合我们的最佳实践。
其中包括以下项目规范， 提出小的pull requests, 并且有足够的注释. 详情参阅文档末尾 [Best Practices for Faster Reviews](#best-practices-for-faster-reviews) 。**

## 本地运行并且验证

您可以在提交pull request之前运行这些本地验证，以预测持续集成的通过或失败。

# Pull Request提交流程

合并pull request需要在pull request自动合并之前完成以下步骤。

- [创建一个pull request](https://help.github.com/articles/about-pull-requests/)
- 对于首次贡献者签署 [Contributor License Agreement](../contributor-license-agreement)
- 通过所有 e2e 测试
- 获得审查者和代码所有者的所有必要批准

##标记未完成的 Pull Requests

如果您想在Pull Requests完成之前征求审查，您应该保留您的pull request，以确保 Tide 不会标记并尝试合并它。
有两种方法可以实现这一点：

1. 您可以添加 `/hold` 或 `/hold cancel` 注释
2. 您可以在您的pull request添加或移除 `WIP` 或 `[WIP]` 前缀

我们将在您使用`do-not-merge/hold`注释处添加或删除标签并在 `do-not-merge/work-in-progress` 您编辑标题时添加和删除标签。
当任一标签存在时，您的pull request将不会被考虑合并。

## Pull Requests 和发布周期

如果一个pull request已经被审核但是hold或者未批准的状态, 这可能是由于当前阶段在发布周期中。
在朝着可能影响其他开发的特定功能或目标努力时，我们可能会冻结他们自己的代码库。
D、在此期间，您的pull request可能会在其发布工作完成时保持未合并状态。

如果您觉得您的pull request处于这种状态，请联系我们进行澄清。

## e2e 测试如何工作

端到端测试会将状态结果发布到 pull request.

# 为什么我的pull request会被关闭?

超过 90 天的pull request将被关闭。
对于具有正在审查或正在等待其他相关pull request的pull request，可以进行例外处理。
关闭的pull requests很容易重新创建, 关闭随后需要重新打开的pull request会丢失少许工作。
我们希望将运行中的pull request总数限制为

- 维护一个干净的项目
- 删除由于底层代码随时间变化而难以rebase的旧pull requests
- 鼓励代码效率

# 为什么我的pull requests没有得到审核?

有几个因素会影响您的pull requests等待审核的时间。

如果这是里程碑的最后几周，我们需要减少用户流失并保持稳定。

或者，它可能与最佳实践有关。
一个常见问题是pull requests太大导致无法审查。
假设您已经接触了 39 个文件并进行了 8657 次插入。
当你的准审阅者准备审查时，他们会被吓跑——这个pull requests需要 4 个小时来审查，而他们现在没有 4 个小时。
只要他们有更多的空闲时间，他们就会稍后再做（哈！）。

下一节将详细介绍最佳实践，包括如何避免过长的pull requests。

但是，如果你已经遵循了最佳实践，但仍然没有得到任何 pull request被合并，那么你可以采取一些措施来推动这个过程：

- 确保您的pull request具有指定的审阅者（GitHub 中的受让人）。如果没有，请回复pull request评论 `/assign @username` ，要求分配审阅者。

- 在pull request评论上 ping 受让人（@username），并询问他们何时可以进行审查。

- 通过电子邮件 Ping 受让人（我们中的许多人都有公开的电子邮件地址）。

- 如果您已经修复了审核中的所有问题，但您还没有收到回复，您应该在评论流中 ping 受让人，并使用“请再看一次”(`PTAL`) 或类似的评论，表明您已准备好进行另一次审核。

继续阅读以了解有关如何通过遵循最佳实践获得更快审核的更多信息。

# 更快审核的最佳实践

节的大部分内容并不限定于AcmeStack社区，但是当您提出pull request时，最好记住这些最佳实践。

例如您刚刚对如何使 AcmeStack 变得更好有了个好主意。
我们暂时称这个主意为Feature-X.
Feature-X 甚至没有那么复杂。
您对如何实现它有一个很好的想法。
你开始去实施它，一路上修复了一堆东西。
您发送了 pull request - 这非常的棒！
等啊等～
一个星期过去了，没有人审核它。
最后，有人提供了一些评论，您可以修复并等待更多审查。你继续等着。
又过一两个星期。这太可怕了

让我们谈谈最佳实践，以便您的pull request得到快速审查。

## 熟悉项目规范

[代码规范](../coding-conventions)

## KISS, YAGNI, MVP, etc.

有时我们需要互相提醒软件设计的核心原则——大道至简、你不需要的不要、最小可行产品等等
添加一个“因为我们以后可能需要它”的功能与发布的软件是对立的。
添加您现在需要的东西并（理想情况下）为您以后可能需要的东西留出空间 - 但现在不要实施它们。

## 越小越好：小的提交, 小的Pull Requests

小的提交和小的Pull Requests比大的更容易得到审查，并且更有可能是正确的。

注意力是稀缺资源。
如果你的 pull request 需要 60 分钟来审查，那么审查者对细节的关注在最后 30 分钟就没有第一次那么敏锐了。
如果它需要审阅者持续大量的时间，它可能根本不会得到审阅。

## 分解提交

在逻辑断点将您的pull request分解为多个提交。

进行一系列离散的提交是表达一个想法的演变或构成一个单一功能的不同想法的一种强有力的方式。
努力将逻辑上不同的想法分组到单独的提交中。

例如，如果您发现 Feature-X 需要一些预分解来适应，请提交执行该预分解的提交。然后为 Feature-X 准备一个新的提交。

在提交的数量进行权衡。
一个有 25 个提交的pull request审查仍然非常麻烦，所以请使用您的最佳判断。

## 分解 Pull Requests

或者，回到我们的预分解示例，您还可以创建一个新分支，在那里进行预分解并为此发送pull request。
如果您可以从pull request中提取全部想法并将其作为pull request发送，则可以避免不断rebase的痛苦问题。

AcmeStack 是一个快速发展的代码库 - 通过您的小请求尽快锁定您的更改，并使合并成为其他人的问题。

多个小的pull request通常比多个提交更好。不要担心我们会收到大量的pull request。
不要担心我们会收到大量的pull request。我们宁愿有 100 个小而明显的pull request，而不是 10 个不可审查的单体。

我们希望每个pull request都单独有用，因此请根据您的最佳判断来判断pull request与提交的区别。

根据经验，如果您的pull request与 Feature-X 直接相关而不是其他任何东西，那么它可能应该是 Feature-X pull request的一部分。
如果你能解释为什么你在做看似无用的工作（“我保证，它使 Feature-X 的变化更容易”）我们可能会接受它。
如果您可以想象有人独立于 Feature-X 找到价值，请将其作为pull request尝试。
（不要在提交描述中通过 `#` 链接pull request，因为 GitHub 会创建大量垃圾邮件。相反，请通过您的提交所在的pull request引用其他pull request。）

## 为修复和通用功能打开不同的pull request

**将与您的功能无关的更改放入不同的pull request中。**

通常，在您实现 Feature-X 时，您会发现不好的评论、糟糕的函数名称、糟糕的结构、弱类型安全等。

你绝对应该解决这些问题（或者至少是文件问题）——但不是在与你的功能相同的pull request中。否则，您的差异将有太多变化，您的审阅者会以大局为重。

**寻找机会提取通用功能。**

例如，如果您发现自己接触了很多模块，请考虑您在包之间引入的依赖关系。
你正在做的一些事情可以变得更通用，并从 Feature-X 包中移出和移出吗？
您是否需要使用其他无关包中的函数或类型？
如果有，请推广！我们有托管更多通用代码的地方。

同样地，如果Feature-X在形式上类似于上个月签入的Feature-W，并且你从Feature-W中复制了一些棘手的东西，那么考虑将核心逻辑预先分解出来，并在Feature-W和Feature-X中使用它。
（请在自己的提交或pull request中这样做。）

## 注释十分重要

在你的代码中，如果有人可能不明白你为什么做某事（或者你以后不记得为什么），请添加注释。许多代码审查的评论都是关于这个没有注释的问题。

如果您认为我们可以跟进一些非常明显的事情，请添加 TODO。

阅读 [GoDoc](https://blog.golang.org/godoc-documenting-go-code) 遵循注释通用规范。

## 测试

没有什么比开始审查时发现测试不充分或根本没有更令人沮丧的了。
很少有pull request可以管代码而不管测试。

如果您不知道如何测试 Feature-X，请询问我们！
我们很乐意帮助您设计易于测试的东西或建议适当的测试用例。

## 压缩

您的审阅者终于向您发送了有关 Feature-X 的反馈。

做了相关的修复，并且还未压缩。
将它们放入新的提交中，然后重新推送。
这样，您的审阅者可以自己查看新提交，这比重新开始要快得多。

为了更易读的记录，我们可能仍会在最后要求您清理提交，但在被问到之前不要这样做：通常是在pull request被标记为 `LGTM` 的地方。

每个提交都应该有一个好的标题行（<70 个字符），并包含一个额外的描述段落，更详细地描述预期的更改。

有关详细信息，请参阅 [压缩提交](../github-workflow-guide#压缩提交).

**一般压缩指南：**

- Sausage => 压缩

当有多个提交以修复原始提交中的错误时，请执行压缩，解决审阅者的反馈等。
其实我们只想看到最终状态，以及整个pull request的提交信息。

- 图层 => 不要压缩

当有分层的独立更改以实现单个目标时，不要压缩。
例如，编写代码munger可能是一次提交，应用它可能是另一次提交，添加预提交检查可能是第三次提交。
有人可能会争辩说它们应该是单独的pull request，但实际上没有办法在没有看到它应用的情况下测试/审查 munger，并且需要进行预提交检查以确保 munged 输出不会立即过时。

**注意**:您也可以要求您的审阅者将 `tide/merge-method-squash` 标签添加到您的 PR（这可以由审阅者通过发出命令来完成：`/label tide/merge-method-squash`), 这将让机器人负责压缩作为此 PR 一部分的所有提交，并且不会导致删除 `LGTM` 标签（如果已应用）或重新运行 CI 测试。

## 提交信息指南

PR 评论不会出现在提交历史记录中。
提交及其提交信息是 PR 中所做更改的“永久记录”，它们的提交消息应准确描述所做的内容和原因。

提交信息由两部分组成;主体和正文。

主体是提交信息的第一行，并且通常是小的或微不足道的更改所需的唯一部分。
这些可以用“一行代码”来完成，使用`“git commit -m”`或`“——message”`标志，但前提是必须用这几个字来完整地描述什么，特别是为什么。

提交消息主体是当你运行`git commit`时，没有`-m `标志的那部分文本，它会打开提交消息进行编辑
在您的 [首选编辑].
输入一些进一步的澄清句子对于您的审核和后期整体项目维护来说是一种有效的时间投资。

```bash
This is the commit message subject

Any text here is the commit message body
Some text
Some more text
...

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch example
# Changes to be committed:
#   ...
#
```

使用下面的这些指南来帮助制作格式正确的提交信息。
这些很大程度上归功于 [Chris Beams], [Tim Pope],
[Scott Chacon] 和 [Ben Straub]之前的工作。

- [Try to keep the subject line to 50 characters or less; do not exceed 72 characters](#try-to-keep-the-subject-line-to-50-characters-or-less-do-not-exceed-72-characters)
- [The first word in the commit message subject should be capitalized unless it starts with a lowercase symbol or other identifier](#the-first-word-in-the-commit-message-subject-should-be-capitalized-unless-it-starts-with-a-lowercase-symbol-or-other-identifier)
- [Do not end the commit message subject with a period](#do-not-end-the-commit-message-subject-with-a-period)
- [Use imperative mood in your commit message subject](#use-imperative-mood-in-your-commit-message-subject)
- [Add a single blank line before the commit message body](#add-a-single-blank-line-before-the-commit-message-body)
- [Wrap the commit message body at 72 characters](#wrap-the-commit-message-body-at-72-characters)
- [Do not use GitHub keywords or (@)mentions within your commit message](#do-not-use-github-keywords-or-mentions-within-your-commit-message)
- [Use the commit message body to explain the _what_ and _why_ of the commit](#use-the-commit-message-body-to-explain-the-what-and-why-of-the-commit)

<!-- omit in toc -->
### 主体最好少于50个字符;最多不超过72个字符

提交信息主题的 50 个字符限制以内，以使提交信息摘要尽可能简洁。它应该足以描述正在做的事情。

72 个字符的硬限制是与最大正文大小保持一致。
当我们使用` git log `查看存储库的历史记录时 git 将用额外的空格填充正文文本。
Wrapping 将宽度包装为 72 个字符可确保正文文本居中并在 80 列终端上轻松查看。

<!-- omit in toc -->
#### 提供补充上下文

您可以通过在您的提交消息前加上您的 PR 影响的 [kind] 或 [area] 来提供具有更少字符的补充上下文
这些是 AcmeStack 社区的其他成员会理解的常用标签。

**示例:**

- `cleanup: remove unused portion of script foo`
- `deprecation: add notice for bar feature removal in future release`
- `etcd: update default server to 3.4.7`

在进一步扩展提交信息正文中的内容和原因之前，这些可以作为一个很好的主体。

<!-- omit in toc -->
### 提交信息的主体中的第一个单词应大写，除非它以小写符号或其他标识符开头

提交信息主体就像一个缩写句子。
第一个单词应该大写，除信息以符号、首字母缩略词或其他标识符（例如 [kind] 或 [area]）开始，而这些标识符通常是小写的。

<!-- omit in toc -->
### 不以句号结束提交信息主体

这主要是为了节省空间，但也有助于使主体行尽可能短和简洁。

<!-- omit in toc -->
### 在提交信息主体中体现紧迫感

紧迫感可以被认为是“发出命令”;它是一个**现在时态**的陈述，明确地描述正在做的事情。

#### 正确示例:

- Fix x error in y
- Add foo to bar
- Revert commit "baz"
- Update pull request guidelines

**错误示例**

- Fixed x error in y
- Added foo to bar
- Reverting bad commit "baz"
- Updating the pull request guidelines
- Fixing more things

[Chris Beams] 关于形成命令式提交主体的一般准则是它应该完成这句话：

```bash
If applied, this commit will <your subject line here>
```

**例如:**

- _If applied, this commit will_ **Fix x error in y**
- _If applied, this commit will_ **Add foo to bar**
- _If applied, this commit will_ **Revert commit "baz"**
- _If applied, this commit will_ **Update the pull request guidelines**

<!-- omit in toc -->
### 在提交信息正文之前添加一个空行

Git 使用空行来确定提交信息的哪个部分是主体和正文。空行前面的文字是主体，后面的文字是正文。
空行前面的文字是主体，后面的文字是正文。

<!-- omit in toc -->
### 将提交信息正文包装为 72 个字符

git 的默认列宽是 80 个字符。
在查看 git 日志时，Git 将在信息正文的文本中额外填充 4 个空格。
这将为您留下 76 个可用的文本空间，但是文本将是“不平衡的”。
为了使文本居中以便更好地查看，另一侧人为地填充了相同数量的空格，从而每行有 72 个可用字符。
将它们视为 word doc 中的页边空白。

<!-- omit in toc -->
### 不要在提交信息中使用 GitHub 关键字或 (@)

<!-- omit in toc -->
#### GitHub 关键字

在您的提交信息中使用 [GitHub 关键字] 后面跟上 `#<issue 标号>` 引用将自动将 `do-not-merge/invalid-commit-message`
签应用于您的 PR，以防止它被合并。

[GitHub 关键字] 在 PR 中关闭问题被认为是一个方便的项目，但在提交信息中使用时可能会产生意想不到的副作用；经常关闭他们不应该关闭的东西。

**被屏蔽的关键字:**

- close
- closes
- closed
- fix
- fixes
- fixed
- resolve
- resolves
- resolved

<!-- omit in toc -->
#### (@)艾特

提交信息中的(@)将向该用户发送通知，并且每次更新 PR 时都会不断这样做。

<!-- omit in toc -->
### 使用提信息正文来解释提交的内容和原因

提交及其提交信息是 PR 中所做更改的“永久记录”。
描述某事发生变化的原因以及它可能产生的影响。
您正在为您的审阅者和下一个必须接触您的代码的人提供上下文。

如果某些东西正在解决错误，或者是为了响应特定问题，您可以链接到它作为信息正文本身的参考。
在追踪未来的错误或回归时，这些类型的面包屑变得必不可少，并进一步帮助解释提交的“原因”。

**补充资源:**

- [How to Write a Git Commit Message - Chris Beams](https://chris.beams.io/posts/git-commit/)
- [Distributed Git - Contributing to a Project (Commit Guidelines)](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project)
- [What’s with the 50/72 rule? - Preslav Rachev](https://preslav.me/2015/02/21/what-s-with-the-50-72-rule/)
- [A Note About Git Commit Messages - Tim Pope](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Writing good commit messages a practical guide](https://www.freecodecamp.org/news/writing-good-commit-messages-a-practical-guide/)

## 可以回滚

有时候审核的人也会犯错。
可以回滚审阅者要求的更改。
如果您有充分的理由以某种方式做某事，那么您绝对可以就所请求更改的优点进行辩论。
审稿人和被审稿人都应该努力以礼貌和尊重的方式讨论这些问题。

你可能会被否决，但你也可能占上风。我们都是很通情达理的人。

开源项目的另一个现象（任何人都可以对任何问题发表评论）——你的pull request得到了很多人的评论，以至于很难理解。
在这种情况下，您可以询问主要审阅者（受让人）是否希望您派生一个新的pull request以清除所有评论。
您不必解决每个想发表评论的人提出的每个问题，但您应该用解释来回答合理的评论。

## 常识和礼貌

没有任何文件可以代替常识和良好的品味。使用您的最佳判断，同时考虑如何使您的工作更容易审查。
如果你做这些事情，你的pull request将会以更快的被合并。

## 微不足道的的改动

每个传入的 Pull Request 都需要审查、检查然后合并。

虽然自动化对此有所帮助，但每项贡献也都有工程成本。因此，如果您不进行多余的编辑和修复，而是专注于对整个文件进行审查，我们将不胜感激。

如果你发现一个语法或拼写错误，很可能在该文件中有更多，你可以通过检查格式，检查损坏的链接，修复错误，然后提交所有修复一次文件，真正使你的Pull Request计数。

**值得思考的问题**

- 文件可以进一步改进吗？
- 微不足道的编辑是否大大提高了内容的质量？

## 其他参考

- [Chris Beams](https://chris.beams.io)
- [Tim Pope](https://tpo.pe)
- [Scott Chacon](https://scottchacon.com)
- [Ben Straub](https://ben.straub.cc/)
- [preferred editor](https://help.github.com/en/github/using-git/associating-text-editors-with-git)
- [imperative mood](https://www.grammar-monster.com/glossary/imperative_mood.htm)
- [GitHub keywords](https://help.github.com/articles/closing-issues-using-keywords)
