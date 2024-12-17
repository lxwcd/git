git 学习  
      
# 学习资源  
> 初步了解 git：[廖雪峰 Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)  
> github 官方文档：[GitHub Docs](https://docs.github.com/en/get-started/quickstart/set-up-git)  
> git 命令官方文档：[git](https://git-scm.com/docs/)  
> git book：[Pro Git book](https://git-scm.com/book/en/v2)  
> [Learn Git Branching](https://learngitbranching.js.org/?locale=zh_CN) 
> [Git 教程 - Rebase](https://www.delftstack.com/zh/tutorial/git/git-rebase/) 
      
# git 介绍
> [Git - What is Git?](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F) 

1. **Git 的基本概念**：
   - Git 与其他版本控制系统（如 CVS、Subversion 或 Perforce）的主要区别在于它如何存储数据。Git 将数据视为一系列文件系统快照，而不是基于文件的变更列表（delta-based）。

2. **快照而非差异**：
   - Git 在每次提交时，都会保存项目文件的当前状态的快照。如果文件未更改，Git 只存储对先前相同文件的链接，而不是文件本身。这种方法使得 Git 更像是一个带有强大工具的迷你文件系统。

3. **几乎每个操作都是本地的**：
   - Git 的大多数操作只需要本地文件和资源，不需要网络上的其他计算机的信息。这意味着即使在没有网络连接的情况下，你也可以进行大多数操作，如查看项目历史或提交更改。

4. **Git 的完整性**：
   - Git 在存储之前会对所有内容进行校验和检查，并通过校验和引用这些内容。Git 使用 SHA-1 哈希来确保文件或目录结构的完整性。这意味着任何文件或目录的内容更改都会被 Git 检测到。

5. **Git 通常只添加数据**：
   - 在 Git 中执行的操作几乎都是向 Git 数据库中添加数据。提交到 Git 的快照很难丢失，特别是如果你定期将数据库推送到其他仓库。

6. **三种状态**：
   - Git 有三个主要的状态：已修改（modified）、已暂存（staged）和已提交（committed）。文件可以处于这三个状态之一。
   - **工作目录**：项目的单个检出版本。
   - **暂存区**：存储下一次提交的信息的文件。
   - **Git 目录**：存储项目的元数据和对象数据库。

7. **基本 Git 工作流程**：
   - 修改工作目录中的文件。
   - 选择性地暂存那些你希望成为下一次提交一部分的更改。
   - 执行提交，将暂存区中的文件状态永久存储到 Git 目录中。

# 安装 git  
## linux 安装  
> [安装 Git](https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496)  
      
## Windows 安装  
官网下载地址：[Download for Windows](https://git-scm.com/download/win)  
      
# Git config 配置Git  
> [Git Config](https://www.gitkraken.com/learn/git/git-config)  
> [配置 git config](https://tsejx.github.io/devops-guidebook/code/git/config/)  
> [Git - git-config Documentation](https://git-scm.com/docs/git-config) 

## system level
`git config --system` 是一个用于设置系统级 Git 配置的命令选项。系统级配置影响当前操作系统上的所有 Git 用户和仓库。

### 作用范围

- **系统级配置**：`--system` 选项用于设置对所有用户和所有仓库都有效的配置。这些配置通常用于定义整个系统范围内的默认行为。
- **影响所有用户**：与 `--global` 配置（仅影响当前用户）不同，`--system` 配置对所有用户都有效。

### 配置文件位置

- **配置文件**：系统级配置通常存储在 `/etc/gitconfig` 文件中。这个文件包含了适用于整个系统的 Git 配置。
- **可修改性**：只有具有适当权限（通常是 root 权限）的用户才能修改系统级配置文件。

### 使用场景

- **全局默认设置**：当你想要为整个系统设置统一的 Git 配置时（例如，统一的用户名、电子邮件地址或别名），使用 `--system` 是合适的。
- **多用户环境**：在多用户环境中，`--system` 配置确保所有用户都遵循相同的 Git 行为和规则。

### 示例命令

- **设置系统级配置**：
  ```bash
  sudo git config --system user.email "system@example.com"
  ```
  这个命令会将 `user.email` 配置设置为 `system@example.com`，适用于所有用户和所有仓库。

- **查看系统级配置**：
  ```bash
  git config --system --get user.email
  ```
  这个命令会显示系统级配置中设置的 `user.email` 值。

### 注意事项

- **权限要求**：修改系统级配置通常需要 root 权限，因此你可能需要使用 `sudo` 来执行这些命令。
- **谨慎使用**：由于系统级配置影响所有用户和仓库，因此在修改这些配置时要格外小心。确保你了解每个配置选项的作用，以避免意外的行为。
- **优先级**：如果同一配置选项在多个层级（系统、全局、本地）中设置，Git 会根据优先级选择使用哪个值。通常，本地配置（`--local`）优先级最高，其次是全局配置（`--global`），最后是系统配置（`--system`）。

通过使用 `git config --system`，你可以为整个系统设置统一的 Git 配置，确保所有用户和仓库都遵循相同的规则和行为。这种方法在管理多用户环境或确保一致性时非常有用。

## global and local level
`git config --local` 和 `git config --global` 是 Git 配置命令的两个选项，它们用于指定配置的范围。这两个选项的主要区别在于它们应用配置的层级和影响范围。下面详细解释这两个选项的区别：

### `git config --local`

- **作用范围**：`--local` 选项用于设置特定 Git 仓库的配置。这些配置仅适用于当前仓库，不会影响其他仓库或全局 Git 配置。
- **配置文件位置**：使用 `--local` 时，配置信息存储在当前仓库的 `.git/config` 文件中。每个 Git 仓库都有自己的 `.git` 目录，其中包含该仓库的配置文件。
- **使用场景**：当你想要为特定项目设置特定的配置选项时（例如，特定的合并策略或分支名称），使用 `--local` 是合适的。这样，这些设置不会干扰其他项目或全局设置。
- **示例命令**：
  ```bash
  git config --local user.email "local@example.com"
  ```
  这个命令会将 `user.email` 配置设置为 `local@example.com`，但仅适用于当前仓库。

### `git config --global`

- **作用范围**：`--global` 选项用于设置全局 Git 配置。这些配置适用于当前用户的所有 Git 仓库。
- **配置文件位置**：使用 `--global` 时，配置信息存储在用户的主目录下的 `.gitconfig` 文件中（例如，`~/.gitconfig`）。这个文件包含了适用于所有仓库的全局配置。
- **使用场景**：当你想要为所有项目设置统一的配置选项时（例如，全局的用户名或编辑器），使用 `--global` 是合适的。这样，你不需要在每个项目中重复设置相同的配置。
- **示例命令**：
  ```bash
  git config --global user.email "global@example.com"
  ```
  这个命令会将 `user.email` 配置设置为 `global@example.com`，适用于当前用户的所有仓库。

### 总结

- **`--local`**：特定于单个仓库的配置，存储在 `.git/config` 中。
- **`--global`**：特定于用户的全局配置，存储在 `~/.gitconfig` 中。

## 查看全局配置信息  
```bash  
git config --global --list  
```  

## 修改配置文件的路径
修改 Git 配置文件的路径通常涉及到更改 Git 查找配置文件的位置。Git 配置文件有三个主要层级：系统级（system）、全局级（global）和项目级（local）。每个层级的配置文件路径可以通过环境变量或 Git 命令进行修改。

### 1. 修改全局配置文件路径

全局配置文件默认位于用户的主目录下，名为 `.gitconfig`。可以通过设置环境变量 `GIT_CONFIG_GLOBAL` 来修改全局配置文件的路径。

- **临时修改**（当前终端会话有效）：
  ```bash
  export GIT_CONFIG_GLOBAL=/path/to/your/global/config
  ```

- **永久修改**（对所有终端会话有效）：
  将上述 `export` 命令添加到你的 shell 配置文件中（如 `~/.bashrc`、`~/.zshrc` 等），然后重新加载配置文件：
  ```bash
  echo 'export GIT_CONFIG_GLOBAL=/path/to/your/global/config' >> ~/.bashrc
  source ~/.bashrc
  ```

### 2. 修改系统配置文件路径
> [bash 配置文件介绍](https://github.com/lxwcd/linux/blob/main/notes/shell学习笔记.md#bash-环境配置文件的用途说明) 

系统配置文件默认位于 `/etc/gitconfig`。你可以通过设置环境变量 `GIT_CONFIG_SYSTEM` 来修改系统配置文件的路径。

- **临时修改**：
  ```bash
  export GIT_CONFIG_SYSTEM=/path/to/your/system/config
  ```

- **永久修改**：
  将上述 `export` 命令添加到你的 shell 配置文件中，然后重新加载配置文件：
  ```bash
  echo 'export GIT_CONFIG_SYSTEM=/path/to/your/system/config' >> ~/.bashrc
  source ~/.bashrc
  ```

### 3. 修改项目配置文件路径

项目配置文件位于每个 Git 仓库的 `.git/config` 文件中。如果你想为特定项目指定不同的配置文件路径，可以使用 `git config` 命令的 `--file` 选项。

- **指定配置文件**：
  ```bash
  git config --file /path/to/your/project/config --get core.editor
  ```

### 注意事项
- 确保新的配置文件路径是可访问的，并且 Git 有权限读取和写入这些文件。

      
## 设置用户名和电子邮件  
```bash  
root@ubuntu2204c12:~# git config --global user.name "name"  
root@ubuntu2204c12:~# git config --global user.email "email@163.com"  
```  

## 设置初始默认分支名
```bash
sudo git config --system init.defaultBranch main
```

## 配置换行符
- **Unix/Linux/Mac** 使用 LF（Line Feed，`\n`）作为换行符。
- **Windows** 使用 CRLF（Carriage Return + Line Feed，`\r\n`）作为换行符。

由于这些差异，当开发者在不同操作系统之间协作时，可能会遇到换行符不一致的问题。Git 提供了 `core.autocrlf` 和 `core.safecrlf` 配置选项来帮助处理这些问题。

这些设置的主要目的是在不同操作系统之间协作时，确保文件的换行符保持一致，从而避免因换行符不一致导致的合并冲突和其他问题。

### 对于 Unix/Mac 用户：

1. **`git config --global core.autocrlf input`**：
   - 这个配置使得当文件从工作目录添加到索引（即暂存区）时，Git 会将 CRLF 转换为 LF。
   - 当文件从索引检出(checkout)到工作目录时，Git 不会进行任何转换。
   - 这样可以确保在 Unix/Mac 系统上，文件总是以 LF 结尾。

这种设置通常用于 Unix 和 Mac 系统，因为这些系统默认使用 LF 作为换行符。通过这种方式，可以确保在这些系统上工作的开发者不会因为换行符问题而遇到麻烦。

2. **`git config --global core.safecrlf true`**：
   - 这个配置选项启用了一个安全检查，以确保在转换过程中不会损坏文件。
   - 如果 Git 检测到转换可能会导致文件内容变化（例如，文件中包含混合的换行符），它会拒绝转换并报错。

### 对于 Windows 用户：

1. **`git config --global core.autocrlf true`**：
   - 这个配置使得当文件从索引检出到工作目录时，Git 会将 LF 转换为 CRLF。
   - 当文件从工作目录添加到索引时，Git 会将 CRLF 转换为 LF。
   - 这样可以确保在 Windows 系统上，文件在工作目录中以 CRLF 结尾，而在仓库中以 LF 结尾。

2. **`git config --global core.safecrlf true`**：
   - 与 Unix/Mac 用户的配置相同，这个选项启用了一个安全检查，以确保在转换过程中不会损坏文件。

## git 配置代理  
> [git设置、查看、取消代理](https://blog.csdn.net/qq_43331089/article/details/129637569)  
      
- 如 windows 中安装 clash for windows，可查看其端口，例如 7890  
      
### Windows 中安装的 git 设置代理  
在 git 设置代理：  
```git  
git config --global http.https://github.com.proxy socks5://127.0.0.1:7890  
```  
      
配置完查看：  
```git  
$ git config --global --list  
http.https://github.com.proxy=socks5://127.0.0.1:7890  
```  

### vmware 虚拟机中安装的 git 设置代理  
> [vmware Ubuntu虚拟机设置代理](https://blog.csdn.net/qq_36383272/article/details/116307665)  
      
```bash  
git config --global http.proxy http://192.168.0.119:7890  
git config --global https.proxy https://192.168.0.119:7890  
```  
      
上面的地址 `192.168.0.119` 为宿主机的 ip 地址，端口 `7890` 为代理端口  

## 显示配置项的来源
```cpp
git config --global --list --show-origin
```
`git config --show-origin` 是一个非常有用的命令，它允许你查看 Git 配置项及其来源文件。这个命令可以帮助你理解每个配置项是从哪个配置文件中读取的。

- **显示配置来源**：`--show-origin` 选项用于显示每个配置项的来源，即配置项是从哪个文件中读取的。这包括文件路径、标准输入、blob 或命令行等来源。

- **调试配置问题**：当你不确定某个配置项是从哪个文件中读取时，使用 `--show-origin` 可以帮助你找到答案。
- **查看配置文件路径**：通过显示配置项的来源，你可以快速找到相关的配置文件路径。

1. **查看所有配置及其来源**：
   ```bash
   git config --list --show-origin
   ```
   这个命令会列出所有 Git 配置项及其来源文件路径。

2. **查看特定配置项的来源**：
   ```bash
   git config --show-origin --get <key>
   ```
   这个命令用于获取指定键的配置值以及它们所在的配置文件路径。

      
# Git 存储数据方式  
> [Git Internals Part 2: How does Git store your data?](https://www.developernation.net/blog/git-internals-how-does-git-store-your-data)  
> [1.3 Getting Started - What is Git?](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F#what_is_git_section)  
> [Commits are snapshots, not diffs](https://github.blog/2020-12-17-commits-are-snapshots-not-diffs/)  
> [BASIC SNAPSHOTTING](http://git.github.io/git-reference/basic/)  
> [What is a git "Snapshot"?](https://stackoverflow.com/questions/4964099/what-is-a-git-snapshot)  
> [Is the git storage model wasteful?](https://stackoverflow.com/questions/7321360/is-the-git-storage-model-wasteful)  
> [Are Git's pack files deltas rather than snapshots?](https://stackoverflow.com/questions/5176225/are-gits-pack-files-deltas-rather-than-snapshots)  
> [Git Internals - Packfiles](https://git-scm.com/book/en/v2/Git-Internals-Packfiles)  
      
      
- In git, commits are snapshots, not diffs  
      
# 文件的两种状态 - tracked and untracked
> [Git - Recording Changes to the Repository](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository) 

## tracked file
Tracked files are files that were in the last snapshot, as well as any newly staged files; they can be unmodified, modified, or staged. In short, tracked files are files that Git knows about.

## untracked file
Tracked files are files that were in the last snapshot, as well as any newly staged files; they can be unmodified, modified, or staged. In short, tracked files are files that Git knows about.
      
# git clone 克隆仓库到新目录  
如果远程仓库地址为：https://github.com/lxwcd/learnVim.git，直接用 git clone url 会将远程仓库克隆到当前目录  
当前目录下会包含远程仓库的目录

如果不想远程仓库的目录，只将目录内的文件克隆到本地当前目录下，则如下：
```bash     
git clone https://github.com/lxwcd/cpp.git .
```
      
将远程仓库克隆到指定目录并且修改仓库名字为 `new_folder`：  
```bash  
git clone https://github.com/lxwcd/learnVim.git /usr/local/src/new_folder  
```  
      
也可以指定多级目录，如果不存在，则自动创建  
```bash  
git clone https://github.com/lxwcd/learnVim.git /usr/local/src/1/2/3/new_folder  
```  

# git init 初始化仓库
> [Git - git-init Documentation](https://git-scm.com/docs/git-init) 

`git init` 是 Git 中用于初始化新仓库的命令。它将一个现有的目录转换为 Git 仓库，使其可以进行版本控制。

1. **创建新的 Git 仓库**：`git init` 在当前目录中创建一个新的 `.git` 目录，该目录包含所有必要的 Git 仓库文件。
2. **初始化仓库结构**：命令会初始化仓库的基本结构，包括配置文件、对象数据库、引用等。

## 使用场景

- **开始新项目**：当你开始一个新项目并希望使用 Git 进行版本控制时，`git init` 是第一步。
- **将现有项目转换为 Git 仓库**：如果你有一个未使用 Git 版本控制的现有项目，`git init` 可以将其转换为 Git 仓库。

## 基本使用

- **初始化当前目录**：
  ```bash
  git init
  ```
  这个命令将当前目录初始化为一个 Git 仓库。

- **初始化指定目录**：
  ```bash
  git init <directory>
  ```
  这个命令将指定目录初始化为一个 Git 仓库。如果目录不存在，Git 会尝试创建它。

## 选项

- **`--bare`**：创建一个裸仓库（bare repository），这种仓库没有工作目录，通常用于服务器上的中央仓库。
  ```bash
  git init --bare
  ```

- **`--template=<template_directory>`**：指定一个模板目录，Git 将从该目录复制文件到新仓库的 `.git` 目录。
  ```bash
  git init --template=/path/to/template
  ```

- **`--separate-git-dir=<git_dir>`**：将 Git 仓库目录（`.git`）与工作目录分开，指定一个单独的路径来存储 Git 仓库文件。
  ```bash
  git init --separate-git-dir=/path/to/gitdir
  ```

## 结果

执行 `git init` 后，当前目录（或指定目录）将包含一个新的 `.git` 目录，其中包含以下内容：

- **`HEAD`**：指向当前分支的引用。
- **`config`**：仓库的配置文件。
- **`objects`**：存储 Git 对象的目录。
- **`refs`**：存储分支和标签引用的目录。

## 后续步骤

初始化仓库后，你可以开始使用 Git 进行版本控制：

1. **添加文件**：使用 `git add` 将文件添加到暂存区。
2. **首次提交**：使用 `git commit` 创建初始提交。
3. **添加远程仓库**：使用 `git remote add` 添加远程仓库，以便与他人协作。

## 注意事项

- **空目录**：`git init` 通常在空目录中执行，但也可以在非空目录中执行，Git 会将目录中的文件视为未跟踪文件。
- **裸仓库**：裸仓库不包含工作目录，通常用于集中式版本控制。

## 裸仓库
想象一下，你有一个 Git 仓库，里面有很多文件和文件夹，这些文件和文件夹是你项目的实际内容。在普通的 Git 仓库中，这些文件和文件夹是可见的，并且你可以直接编辑它们。这种仓库被称为“非裸仓库”或“常规仓库”。

现在，想象一下一个只有 Git 版本控制数据（如提交历史、分支信息等），但没有任何实际项目文件的仓库。这种仓库就是“裸仓库”。它只包含 `.git` 目录，而没有工作目录（即没有你项目的文件和文件夹）。

1. **没有工作目录**：裸仓库没有工作目录，这意味着你不能在裸仓库中直接查看或编辑文件。

2. **只包含版本控制数据**：裸仓库只包含版本控制数据（如提交、分支、标签等），这些数据都存储在 `.git` 目录中。

3. **用于远程仓库**：裸仓库通常用作远程仓库，用于集中式版本控制和协作。开发者可以将本地更改推送到裸仓库，或者从裸仓库拉取更改到本地。

### 为什么使用裸仓库？

- **集中式协作**：裸仓库作为中央仓库，允许多个开发者协作。每个开发者可以克隆中央裸仓库，进行本地开发，然后将更改推送到中央仓库。
- **存储效率**：由于不包含工作目录，裸仓库通常比常规仓库更小，因为它们只存储版本控制的元数据，而不存储实际的工作文件。
- **安全性**：裸仓库不允许直接在服务器上修改文件，这可以防止未经授权的更改。

### 创建裸仓库

你可以使用以下命令创建一个裸仓库：

```bash
git init --bare myproject.git
```

这将创建一个名为 `myproject.git` 的目录，其中包含一个裸仓库。

### 使用裸仓库

- **推送和拉取**：开发者可以将本地更改推送到裸仓库，或者从裸仓库拉取更改到本地。
- **克隆裸仓库**：如果你想从裸仓库开始本地开发，需要克隆裸仓库以创建一个包含工作目录的常规仓库。

# git status 检查文件状态
> [Git - git-status Documentation](https://git-scm.com/docs/git-status) 

`git status` 是 Git 中一个非常常用的命令，用于显示当前仓库的状态。这个命令提供了关于工作目录和暂存区的详细信息，帮助用户了解哪些文件被修改、哪些文件已暂存、哪些文件尚未跟踪等。以下是对 `git status` 命令的详细讲解：

1. **显示工作目录的状态**：`git status` 显示当前工作目录中的文件状态，包括已修改、已暂存、未跟踪的文件。
2. **显示分支信息**：命令输出当前分支的名称，以及与远程分支的同步状态。
3. **显示暂存区的状态**：显示已暂存的文件，这些文件将在下次提交时被包含。

## 输出内容
运行 `git status` 命令后，输出内容通常包括以下几个部分：

1. **分支状态**：
   - 显示当前分支的名称。
   - 如果当前分支与远程分支有差异，会显示分支是领先、落后还是分叉的状态。

2. **工作目录状态**：
   - **已修改（Modified）**：列出已修改但尚未暂存的文件。
   - **已暂存（Staged）**：列出已暂存的文件，这些文件将在下次提交时被提交。
   - **未跟踪（Untracked）**：列出尚未被 Git 跟踪的文件。

3. **暂存区状态**：
   - 显示暂存区中的文件列表，这些文件准备在下次提交时被提交。

4. **提交建议**：
   - 根据当前状态，`git status` 可能会提供提交建议，如使用 `git add` 暂存文件或使用 `git commit` 提交更改。

## 使用示例

- **基本使用**：
  ```bash
  git status
  ```
  这个命令显示当前仓库的状态。

- **简洁模式**：
  ```bash
  git status --short
  ```
  或者简写为：
  ```bash
  git status -s
  ```
  这个命令以简洁的格式显示状态，通常用于快速查看文件状态。

## 注意事项

- **查看详细信息**：如果你想查看更详细的信息，可以使用 `git status --verbose` 或 `git status -vv`。
- **忽略文件**：`git status` 会显示未跟踪的文件，但你可以通过 `.gitignore` 文件指定要忽略的文件模式。
- **分支同步**：`git status` 显示的分支同步状态基于远程分支的最新已知状态，可能需要 `git fetch` 来更新。

# Ignoring files
> [Git - gitignore Documentation](https://git-scm.com/docs/gitignore) 
> [GitHub - github/gitignore: A collection of useful .gitignore templates](https://github.com/github/gitignore) 

`.gitignore` 是一个在 Git 仓库中使用的特殊文件，用于指定 Git 应该忽略的文件和目录。这个文件帮助你防止不小心提交不需要版本控制的文件，比如编译产物、日志文件、个人配置文件等。

不影响已被跟踪的文件。

可以写到多个位置，如果忽略文件只针对本地仓库，将忽略的文件放到 `$GIT_DIR/info/exclude` 中，即仓库根目录的 `.git` 目录中。

## 作用

- **指定忽略规则**：`.gitignore` 文件包含一系列的模式（pattern），用于匹配文件和目录路径。Git 会根据这些模式决定哪些文件不需要版本控制。
- **保持仓库清洁**：通过忽略不必要的文件，`.gitignore` 帮助保持仓库的清洁和组织。

## 文件位置

- **项目根目录**：通常，`.gitignore` 文件位于 Git 仓库的根目录。
- **多个 `.gitignore` 文件**：可以在子目录中创建 `.gitignore` 文件，这些文件会影响其所在目录及其子目录。

## 忽略规则

- **模式匹配**：`.gitignore` 文件中的每一行都是一个模式，用于匹配文件路径。模式可以使用通配符，如 `*`、`?`、`[` 和 `]`。
- **注释和空行**：以 `#` 开头的行被视为注释，空行会被忽略。

## 常用模式

- `*`：匹配任意数量的字符。
- `?`：匹配任意单个字符。
- `[abc]`：匹配括号内的任意字符（在这个例子中是 `a`、`b` 或 `c`）。
- `**`：匹配任意数量的目录层级。

### 双星号 `**`
1. **双星号（`**`）在模式匹配中的特殊含义：**
   - 当双星号（`**`）出现在模式中，并且与完整路径名进行匹配时，它们具有特殊的含义。

2. **双星号后跟斜杠（`/`）表示在所有目录中匹配：**
   - 如果模式以双星号（`**`）开始，并且后面紧跟着一个斜杠（`/`），这意味着在所有目录中进行匹配。例如，`**/foo`会匹配任何地方的文件或目录`foo`，这与模式`foo`相同。`**/foo/bar`会匹配任何直接位于目录`foo`下的文件或目录`bar`。

3. **斜杠后跟双星号（`/**`）表示匹配目录内的所有内容：**
   - 如果模式以斜杠（`/`）开始，后面紧跟着双星号（`/**`），这意味着匹配目录内的所有内容。例如，`abc/**`会匹配`abc`目录内的所有文件，相对于`.gitignore`文件的位置，匹配深度是无限的。

4. **斜杠后跟双星号再跟斜杠表示匹配零个或多个目录：**
   - 如果模式中包含斜杠（`/`）后跟双星号（`**`），然后再跟一个斜杠（`/`），这意味着匹配零个或多个目录。例如，`a/**/b`会匹配`a/b`、`a/x/b`、`a/x/y/b`等。

5. **其他连续的星号被视为普通星号，并根据之前的规则进行匹配：**
   - 如果模式中出现其他连续的星号（`*`），它们将被视为普通的星号，并根据之前提到的规则进行匹配。

### 忽略文件夹
`folder` 和 `folder/` 都会忽略该目录下的子目录

## 示例内容

```bash
# 忽略所有 .log 文件
*.log

# 忽略 build 目录
build/

# 忽略所有 .tmp 文件，但不忽略子目录中的 .tmp 文件
*.tmp
!*.subdir/*.tmp

# 忽略 node_modules 目录
node_modules/

# 忽略 .env 文件
.env

# 忽略所有 .DS_Store 文件
.DS_Store
```

## 特殊规则

- **排除特定文件**：使用感叹号 `!` 可以排除特定的文件或模式，使其不被忽略。
- **目录分隔符**：如果模式以 `/` 结尾，表示匹配的是目录。

## 应用 `.gitignore` 规则

- **现有文件**：如果文件已经被跟踪（即已经提交过），那么即使后来在 `.gitignore` 中添加了匹配的规则，这些文件仍然会被跟踪。要停止跟踪这些文件，需要先从仓库中删除它们。
- **新文件**：对于尚未被跟踪的文件，`.gitignore` 规则会立即生效。

## 生成 `.gitignore` 文件

- **手动创建**：你可以手动创建 `.gitignore` 文件并编辑它。
- **使用模板**：许多项目和编程语言有通用的 `.gitignore` 模板，你可以从这些模板开始，然后根据需要进行调整。

## 工具和资源

- **`.gitignore` 模板**：GitHub 提供了许多预定义的 `.gitignore` 模板，你可以根据你的项目类型选择合适的模板。
- **在线生成器**：有些在线工具可以帮助你生成 `.gitignore` 文件，例如 `gitignore.io`。

# git diff 查看文件差异
> [Git - git-diff Documentation](https://git-scm.com/docs/git-diff)   

`git diff` 是 Git 中用于显示文件差异的命令。它可以帮助你查看自上次提交以来文件发生了哪些更改，或者比较不同分支、标签或提交之间的差异。

1. **显示未暂存的更改**：`git diff` 默认显示自上次提交以来未暂存的更改。
2. **比较暂存区与提交**：可以查看已暂存的更改与上次提交的差异。
3. **比较不同提交**：可以比较任意两个提交之间的差异。
4. **比较分支**：可以比较不同分支或标签之间的差异。

## 基本使用

- **查看未暂存的更改**：
  ```bash
  git diff
  ```
  这个命令显示自上次提交以来未暂存的更改。

- **查看已暂存的更改**：
  ```bash
  git diff --cached
  ```
  或者
  ```bash
  git diff --staged
  ```
  这些命令显示已暂存的更改与上次提交的差异。

- **比较两个提交**：
  ```bash
  git diff <commit1> <commit2>
  ```
  这个命令比较两个提交之间的差异。

- **比较分支**：
  ```bash
  git diff <branch1> <branch2>
  ```
  这个命令比较两个分支之间的差异。

## 选项

- **`--cached` 或 `--staged`**：显示已暂存的更改。
- **`--stat`**：显示差异的统计信息，而不是详细内容。
- **`--summary`**：显示差异的简要总结。
- **`--check`**：检查潜在的提交问题，如尾随空格。
- **`--color`**：以颜色显示差异。
- **`-w` 或 `--ignore-all-space`**：忽略空白差异。
- **`-b` 或 `--ignore-space-at-eol`**：忽略行尾空白。
- **`--word-diff`**：以单词为单位显示差异。

## 输出格式

`git diff` 的输出格式通常包括：

- **差异标记**：`+` 表示新增的行，`-` 表示删除的行。
- **文件名**：显示发生差异的文件名。
- **行号**：显示差异行的行号。
- **差异内容**：显示具体的差异内容。

## 使用示例

- **查看特定文件的差异**：
  ```bash
  git diff <file>
  ```

- **比较分支与当前工作目录**：
  ```bash
  git diff <branch>
  ```
  这个命令比较指定分支与当前工作目录的差异。

- **比较标签**：
  ```bash
  git diff <tag1> <tag2>
  ```
  这个命令比较两个标签之间的差异。

### 注意事项

- **未跟踪的文件**：`git diff` 不显示未跟踪的文件。要查看这些文件，请使用 `git status`。
- **合并冲突**：在合并冲突时，`git diff` 可以帮助你查看冲突的详细内容。
- **差异工具**：你可以使用外部差异工具（如 `meld`、`kdiff3` 等）来查看差异，通过配置 Git 使用这些工具。

通过使用 `git diff`，你可以详细查看文件的更改内容，这在代码审查、调试和提交前检查时非常有用。它是一个强大的工具，可以帮助你理解和管理代码的更改。


# git add 
> [Git - git-add Documentation](https://git-scm.com/docs/git-add) 

`git add` 是 Git 中用于将文件更改添加到暂存区（staging area）的命令。暂存区是一个准备下次提交的文件列表。

## 主要功能

1. **暂存文件更改**：`git add` 将文件的更改标记为暂存，这意味着这些更改将在下次 `git commit` 时被提交。
2. **添加新文件**：对于未跟踪的文件（新文件），`git add` 会将其添加到暂存区，使其成为 Git 仓库的一部分。
3. **更新已跟踪文件**：对于已跟踪的文件，`git add` 会将文件的最新更改添加到暂存区。

## 使用场景

- **准备提交**：当你完成一些更改并准备提交时，使用 `git add` 将这些更改添加到暂存区。
- **选择性暂存**：如果你有多个更改，可以选择性地暂存部分更改，以便分批次提交。

## 基本使用

- **暂存单个文件**：
  ```bash
  git add <file>
  ```
  这个命令将指定文件的更改添加到暂存区。

- **暂存多个文件**：
  ```bash
  git add <file1> <file2> ...
  ```
  这个命令将多个文件的更改添加到暂存区。

- **暂存所有更改**：
  ```bash
  git add .
  ```
  或者
  ```bash
  git add --all
  ```
  这些命令将所有更改（包括新文件和修改的文件）添加到暂存区。

## 选项

- **`-A` 或 `--all`**：暂存所有更改，包括新文件和删除的文件。
- **`-u`**：仅暂存已跟踪文件的更改，不包括新文件。
- **`-p`**：交互式地选择要暂存的更改。
- **`-i`**：启动交互式暂存模式，允许你选择要暂存的更改。
- **`-N` 或 `--intent-to-add`**：标记新文件为暂存状态，但不实际添加内容。

## 交互式暂存

使用 `git add -i` 或 `git add --interactive` 可以进入交互式暂存模式，这允许你逐个选择要暂存的更改。这个模式特别有用，当你有多个更改但只想提交其中一部分时。

## 注意事项

- **暂存区状态**：使用 `git status` 可以查看暂存区的状态，了解哪些文件已被暂存。
- **撤销暂存**：如果你想要撤销暂存的文件，可以使用 `git reset <file>`。
- **未跟踪文件**：`git add` 会将未跟踪的文件添加到暂存区，使其成为仓库的一部分。
- **文件模式**：`git add` 会保留文件的模式（如执行权限），因此在提交时文件模式也会被记录。

## 查看可 add 的文件
`git add -n` 或 `--dry-run` 是一个 Git 命令选项，用于模拟 `git add` 操作而不实际将文件添加到暂存区。这个选项非常有用，因为它允许你查看哪些文件会被添加到暂存区，从而避免意外添加不需要的文件。

- **模拟添加操作**：`-n` 选项用于模拟 `git add` 命令的行为。它不会实际将文件添加到暂存区，而是显示哪些文件将被添加。
- **查看影响**：使用这个选项可以帮助你了解执行 `git add` 命令时哪些文件会被影响，从而避免意外添加不需要的文件。

### 使用场景

- **检查待添加文件**：当你想要确认哪些文件将被添加到暂存区时，可以使用 `git add -n` 进行检查。
- **避免错误**：在执行实际的 `git add` 操作之前，使用 `git add -n` 可以帮助你避免将错误的文件添加到暂存区。

### 示例命令

假设有一些修改过的文件和新文件，你想要查看哪些文件会被 `git add` 添加到暂存区：

```bash
git add -n .
```

这个命令会列出当前目录及其子目录中所有会被添加的文件，但不会实际将它们添加到暂存区。

### 输出解释

- **输出内容**：命令的输出会显示所有即将被添加到暂存区的文件的路径。这与实际执行 `git add` 时的输出相同，但不会改变暂存区的状态。
- **理解输出**：通过查看输出，你可以确认是否有任何意外的文件被包含在内，或者是否有任何需要的文件被遗漏。

### 注意事项

- **不影响工作目录**：使用 `-n` 选项不会改变工作目录或暂存区的状态。
- **结合其他选项使用**：你可以结合其他 `git add` 选项使用 `-n`，例如 `git add -A -n` 来查看所有将被添加的文件。


# git commit
> [Git - git-commit Documentation](https://git-scm.com/docs/git-commit) 

`git commit` 是 Git 中用于记录更改的命令。它将暂存区中的更改保存到本地仓库的历史记录中。

## 主要功能

1. **记录更改**：`git commit` 将暂存区中的更改保存为一个新的提交（commit），并记录更改的内容和时间。
2. **更新项目历史**：每次提交都会更新项目的提交历史，形成一个版本记录。
3. **要求提交信息**：执行提交时，Git 会要求你提供一个提交信息，以描述所做的更改。

## 使用场景

- **保存工作进度**：当你完成一部分工作并希望保存当前进度时，可以使用 `git commit`。
- **版本控制**：通过提交，你可以创建项目的不同版本，便于后续的版本比较和回退。
- **协作开发**：在团队协作中，提交是共享和讨论更改的基本单位。

## 基本使用

- **指定提交信息**：
  ```bash
  git commit -m "Commit message"
  ```
  使用 `-m` 选项可以直接在命令行中指定提交信息。

- **提交所有更改**：
  ```bash
  git commit -a -m
  ```
  使用 `-a` 选项会自动将所有已跟踪文件的更改添加到暂存区并提交，但不包括新文件。

## 选项

- **`-m`**：指定提交信息。
- **`-a` 或 `--all`**：自动暂存所有已跟踪文件的更改并提交。
- **`--amend`**：修改最后一次提交。这允许你更改最近一次提交的信息或内容。
- **`-C <commit>`**：使用指定提交的信息作为当前提交的信息。
- **`--dry-run`**：模拟提交操作，显示将要提交的内容，但不实际创建提交。

## 钩子脚本

- **`prepare-commit-msg`**：在编辑提交信息之前运行。
- **`commit-msg`**：在提交信息被接受但提交尚未完成时运行。
- **`post-commit`**：在提交完成后运行。

## 注意事项

- **暂存区内容**：`git commit` 只提交暂存区中的内容。确保你已经使用 `git add` 将需要的更改添加到暂存区。
- **空提交**：如果你尝试提交但暂存区中没有更改，Git 会提示你没有内容要提交。
- **提交历史**：提交历史记录了项目的更改，是团队协作和版本控制的基础。
      
      
- `git rm file`  
- `git commit -m "delete file"`  
- `git push origin <remote repo>`  

# git rm 删除文件
> [Git - git-rm Documentation](https://git-scm.com/docs/git-rm) 
> [How to Delete a File or a Directory from a Git Repository](https://www.w3docs.com/snippets/git/how-to-delete-a-file-from-a-git-repository.html)  

`git rm` 是 Git 中用于删除文件的命令。它不仅从工作目录中删除文件，还从暂存区和 Git 仓库中删除文件。

1. **删除文件**：`git rm` 用于删除工作目录中的文件，并将此删除操作添加到暂存区。
2. **更新暂存区**：删除操作会被记录在暂存区中，以便在下次提交时更新仓库。
3. **可选的提交**：虽然 `git rm` 将删除操作添加到暂存区，但它不会自动提交更改。你需要使用 `git commit` 来提交这些更改。

## 使用场景

- **移除不再需要的文件**：当你需要从项目中删除文件，并确保这些更改被版本控制时，可以使用 `git rm`。
- **清理仓库**：在重构或清理项目时，`git rm` 可以帮助你移除旧文件或不再使用的文件。

## 基本使用

- **删除单个文件**：
  ```bash
  git rm <file>
  ```
  这个命令将指定文件从工作目录和暂存区中删除。

- **删除多个文件**：
  ```bash
  git rm <file1> <file2> ...
  ```
  这个命令将多个文件从工作目录和暂存区中删除。

- **删除目录**：
  ```bash
  git rm -r <directory>
  ```
  使用 `-r` 选项可以递归地删除目录及其内容。

## 选项

- **`-r` 或 `--recursive`**：递归地删除目录及其内容。
- **`-f` 或 `--force`**：强制删除文件，即使它们已经被修改但尚未暂存。
- **`-n` 或 `--dry-run`**：模拟删除操作，显示将要删除的文件，但不实际删除。
- **`-v` 或 `--verbose`**：在删除文件时显示详细信息。

## git rm --cached 保留文件到工作目录
`git rm --cached` 是一个 Git 命令，用于从 Git 版本控制中删除文件，但保留在本地工作目录中。以下是该命令的详细讲解：

1. **从版本控制中移除文件**：
   - `git rm --cached` 将文件从 Git 的索引（也称为暂存区）中移除，这意味着该文件将不再被 Git 跟踪和管理。

2. **保留本地文件**：
   - 与普通的 `git rm` 命令不同，`--cached` 选项使得 Git 只是从版本控制中移除文件，而不会从你的本地工作目录中删除实际的文件。

3. **用途**：
   - 这个命令常用于以下几种情况：
     - 不想跟踪特定的文件或文件夹，例如大型数据文件、自动生成的文件或者敏感信息。
     - 已经误将不应该被版本控制的文件添加到了 Git 中，需要将其从版本控制中移除。
     - 调整 `.gitignore` 文件，使得新的忽略规则生效。有时候，即使你在 `.gitignore` 中添加了规则，已经追踪的文件依然会被提交。在这种情况下，你需要先使用 `git rm --cached` 移除这些文件，然后再提交更改。

- **删除单个文件**：
  ```bash
  git rm --cached <file>
  ```
  这个命令将指定文件从 Git 的索引中删除，但保留在本地文件系统中。

- **删除目录及其内容**：
  ```bash
  git rm --cached -r <directory>
  ```
  使用 `-r` 选项可以递归地删除目录及其内容，但不会在本地文件系统中删除它们。

- 使用 `git rm --cached` 后，虽然文件在本地工作目录中仍然存在，但在下次执行 `git add .` 或 `git commit` 时，这些文件不会被包含在内。如果你想再次将这些文件添加到版本控制中，你需要先移除 `.gitignore` 中的相关规则（如果有的话），然后使用 `git add <file>` 添加它们。

## 注意事项

- **提交更改**：`git rm` 只是将删除操作添加到暂存区，你需要使用 `git commit` 来提交这些更改。
- **恢复文件**：如果你想恢复被删除的文件，可以使用 `git restore` 或 `git checkout` 命令。
- **与 `.gitignore` 配合使用**：如果你删除的文件是由于 `.gitignore` 配置错误导致的，确保更新 `.gitignore` 文件以避免将来的问题。

## 示例

假设有一个名为 `example.txt` 的文件，你想要从项目中删除它：

```bash
git rm example.txt
git commit -m "Remove example.txt"
```

这个过程将 `example.txt` 从工作目录和暂存区中删除，并通过提交更新仓库。

# git mv 移动文件
> [Git - git-mv Documentation](https://git-scm.com/docs/git-mv) 

`git mv` 是 Git 中用于重命名或移动文件和目录的命令。与普通的文件系统操作不同，`git mv` 不仅在文件系统中移动或重命名文件，还会记录这一更改在 Git 的历史记录中。

1. **重命名文件**：将文件的名称更改，并更新 Git 仓库中的相关记录。
2. **移动文件**：将文件从一个目录移动到另一个目录，并更新 Git 仓库中的相关记录。
3. **记录更改**：`git mv` 会将文件的移动或重命名作为一次提交的一部分记录下来。

## 使用场景

- **文件重命名**：当你需要更改文件的名称，并且希望这个更改被版本控制跟踪时。
- **文件移动**：当你需要将文件从一个目录移动到另一个目录，并且希望这个移动操作被版本控制跟踪时。

## 基本使用

- **重命名文件**：
  ```bash
  git mv <old-name> <new-name>
  ```
  这个命令将 `<old-name>` 文件重命名为 `<new-name>`。

- **移动文件**：
  ```bash
  git mv <file> <directory>
  ```
  这个命令将 `<file>` 移动到 `<directory>` 目录中。

- **移动目录**：
  ```bash
  git mv <old-directory> <new-directory>
  ```
  这个命令将 `<old-directory>` 目录重命名为 `<new-directory>`。

## 选项

- **`-f` 或 `--force`**：强制移动或重命名文件，即使目标已经存在。
- **`-n` 或 `--no-overwrite`**：如果目标文件已经存在，不覆盖它。
- **`-k` 或 `--keyword`**：使用关键字参数来指定文件重命名的规则。

## 工作流程

使用 `git mv` 的典型工作流程如下：

1. 使用 `git mv` 命令移动或重命名文件。
2. 检查更改是否正确：`git status`。
3. 提交更改：`git commit -m "Moved/renamed <file>"`。

## 注意事项

- **自动添加到暂存区**：`git mv` 命令会自动将移动或重命名的更改添加到暂存区。
- **与 `git add` 和 `git commit` 的关系**：由于 `git mv` 会自动添加更改到暂存区，通常不需要额外使用 `git add`。提交时，使用 `git commit` 将这些更改记录到历史记录中。
- **文件状态**：如果文件在移动前有未提交的更改，`git mv` 会将这些更改一并移动到新的位置。
- **文件冲突**：如果移动或重命名的文件在目标位置已经存在，并且有未提交的更改，可能会发生冲突。

# git log 查看日志
> [Git - git-log Documentation](https://git-scm.com/docs/git-log) 
> [Git - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History) 

`git log` 是 Git 中用于查看提交历史的命令。它提供了丰富的选项来查看和过滤提交记录，是理解项目历史和追踪更改的重要工具。

1. **查看提交历史**：`git log` 显示项目的提交历史记录，包括提交信息、作者、日期等。
2. **过滤和格式化**：通过各种选项，可以过滤特定的提交记录、格式化输出内容等。

## 使用场景

- **查看项目历史**：当你需要了解项目的更改历史时，可以使用 `git log`。
- **追踪更改**：如果需要追踪特定文件或目录的更改历史，`git log` 可以提供详细的信息。
- **调试问题**：在调试问题时，查看提交历史可以帮助你找到引入问题的提交。

## 基本使用

- **查看所有提交**：
  ```bash
  git log
  ```
  这个命令显示项目的完整提交历史。

- **查看特定分支的提交**：
  ```bash
  git log <branch-name>
  ```
  这个命令显示指定分支的提交历史。

- **查看特定文件的提交**：
  ```bash
  git log <file>
  ```
  这个命令显示指定文件的提交历史。

## 选项

- **`--summary`**：显示每个提交的简要总结。
- **`--stat`**：显示每个提交的统计信息，包括文件更改数量。
- **`--shortstat`**：以更简洁的格式显示统计信息。
- **`--name-only`**：仅显示提交中更改的文件名。
- **`--name-status`**：显示文件名及其更改状态（如 A 表示添加，M 表示修改）。
- **`--pretty=format:"<format>"`**：自定义输出格式。例如：
  ```bash
  git log --pretty=format:"%h - %an, %ar : %s"
  ```
  这个命令自定义输出格式，显示提交哈希、作者、日期和提交信息。
- **`--oneline`**：每个提交显示为一行，包含提交哈希和提交信息。
- **`--graph`**：以图形方式显示提交历史，帮助理解分支和合并关系。
- **`--since` 和 `--until`**：过滤自指定日期以来的提交记录。
- **`--author`**：过滤指定作者的提交记录。
- **`--grep`**：过滤包含特定文本的提交信息。

## 高级用法

- **组合过滤选项**：可以组合使用多个过滤选项来精确查找特定的提交记录。例如：
  ```bash
  git log --since="2023-01-01" --author="John Doe"
  ```
  这个命令显示自 2023 年 1 月 1 日以来 John Doe 的提交记录。

- **使用路径限制**：可以限制 `git log` 的输出到特定的文件或目录。例如：
  ```bash
  git log -- <path>
  ```
  这个命令显示与指定路径相关的提交记录。

## 注意事项

- **输出量**：默认情况下，`git log` 可能会显示大量的提交记录。使用过滤选项可以帮助你快速找到相关信息。
- **图形化工具**：虽然 `git log` 提供了丰富的文本输出选项，但有时使用图形化工具（如 `gitk` 或其他第三方工具）可能更直观。
- **性能**：对于非常大的仓库，`git log` 可能会有些慢。在这种情况下，考虑使用过滤选项来减少输出量。

# git reflog
> [Git - git-reflog Documentation](https://git-scm.com/docs/git-reflog)   

`git reflog` 是 Git 中一个非常强大的命令，它用于管理和查看引用日志（reflogs）。引用日志记录了本地仓库中更新分支和其他引用的操作。以下是 `git reflog` 的详细讲解：

### 1. 什么是 `git reflog`？
`git reflog` 记录了 HEAD 和分支引用以及标签等的所有更新操作。这意味着即使某些提交被删除或者重写，你仍然可以通过 `git reflog` 来找到它们。这个特性使得 `git reflog` 成为恢复误删除或误操作的重要工具。

### 2. `git reflog` 的基本用法
- **查看引用日志**：最基本的用法是 `git reflog`，它会显示 HEAD 的引用日志，列出 HEAD 的所有历史更新操作，包括分支切换、提交、重置等。
  ```bash
  git reflog
  ```
  输出类似于：
  ```
  eb1050b (HEAD -> feature_branch) HEAD@{0}: checkout: moving from main to feature_branch
  1525c48 (origin/main, main) HEAD@{1}: checkout: moving from 2bf1773d87a7806cda25d4d313995bb08adbabf5 to main
  ```
  这里 `HEAD@{n}` 表示 HEAD 在过去第 n 次操作时的位置。

### 3. `git reflog` 的子命令
- **show**：显示指定引用的日志，如果未指定引用，则默认显示 HEAD 的日志。`git reflog show` 是 `git log -g --abbrev-commit --pretty=oneline` 的别名。
  ```bash
  git reflog show <ref>
  ```
- **list**：列出所有有对应 reflog 的引用。
  ```bash
  git reflog list
  ```
- **expire**：修剪旧的 reflog 条目，可以指定时间来删除过时的日志条目。
  ```bash
  git reflog expire [--expire=<time>] [--expire-unreachable=<time>] [--all]
  ```
- **delete**：删除单个 reflog 条目，需要指定确切的条目。
  ```bash
  git reflog delete <ref>@{<specifier>}
  ```
- **exists**：检查某个引用是否有 reflog。
  ```bash
  git reflog exists <ref>
  ```

### 4. `git reflog` 的高级用法
- **基于时间的引用**：`git reflog` 支持基于时间的引用，例如 `HEAD@{1.day.ago}` 表示 HEAD 在一天前的位置。
  ```bash
  git diff main@{0} main@{1.day.ago}
  ```
  这个命令比较了 `main` 分支当前状态和一天前的状态。

### 5. `git reflog` 的重要性
`git reflog` 是 Git 操作的一道安全保障，它能够记录几乎所有本地仓库的改变，包括所有分支的 commit 提交，以及已经被删除的 commit。这使得 `git reflog` 成为恢复丢失提交或分支的重要工具。

# git show
> [Git - git-show Documentation](https://git-scm.com/docs/git-show) 

`git show` 是一个非常强大的 Git 命令，用于展示各种 Git 对象的详细内容，包括提交（commit）、标签（tag）和分支（branch）。

## 基本用法

1. **查看提交详情**
   - `git show <commit>`：显示指定提交的详细信息，包括作者、日期、提交信息和具体的 diff（差异）。
   - `git show HEAD`：显示当前分支的最新提交的详细信息。

2. **查看标签详情**
   - `git show <tag>`：显示指定标签的详细信息，包括标签信息和指向的提交。

3. **查看分支比较**
   - `git show <branch>`：显示指定分支的最新提交的详细信息。

## 常用选项

1. **`--name-only`**
   - 仅显示提交中涉及的文件名列表。

2. **`--name-status`**
   - 显示提交中涉及的文件名以及它们的状态（新增、修改、删除）。

3. **`--stat`**
   - 显示提交的统计信息，包括每个文件的增删行数和文件状态。

4. **`--shortstat`**
   - 显示提交的简要统计信息，只包括每个文件的增删行数。

5. **`--summary`**
   - 显示提交的统计信息摘要，类似于 `--stat`，但不包括每个文件的详细信息。

6. **`--patch`**
   - 显示提交的差异（默认选项），展示具体的代码变化。

7. **`--full-index`**
   - 显示差异时，显示完整的索引信息。

8. **`--oneline`**
   - 仅显示提交的 SHA-1 哈希值和提交信息，一行显示。

9. **`--pretty`**
   - 指定输出格式，例如 `oneline`、`short`、`full`、`fuller`、`reference`、`raw` 等。

10. **`--expand-tabs`**
    - 在显示差异时，将制表符展开为适当数量的空格。

11. **`--color`**
    - 显示颜色差异。

12. **`--no-color`**
    - 不显示颜色差异。

13. **`--textconv`**
    - 使用文本转换过滤器处理文件的差异。

14. **`--word-diff`**
    - 显示单词级别的差异。

### 示例

- 查看最新提交的详细信息：
  ```bash
  git show HEAD
  ```

- 查看特定提交的文件列表：
  ```bash
  git show --name-only <commit>
  ```

- 查看特定提交的统计信息：
  ```bash
  git show --stat <commit>
  ```

- 查看特定提交的简要统计信息：
  ```bash
  git show --shortstat <commit>
  ```

- 查看特定提交的差异，不包括文件内容：
  ```bash
  git show --pretty=raw <commit>
  ```

- 查看特定提交的 SHA-1 哈希值和提交信息：
  ```bash
  git show --oneline <commit>
  ```

# HEAD 
> [Git - Reset Demystified](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified#_git_reset)      

HEAD is the pointer to the current branch reference, which is in turn a pointer to the last commit made on that branch. That means HEAD will be the parent of the next commit that is created. It’s generally simplest to think of HEAD as the snapshot of your last commit on that branch.

## `HEAD` 的作用

1. **指向当前分支**：`HEAD` 通常指向当前分支的引用，比如 `master` 或 `feature`。当你检出（checkout）一个分支时，`HEAD` 会更新为指向该分支的最新提交。
2. **确定工作目录**：`HEAD` 指向的提交决定了你的工作目录的内容。当你检出不同的提交时，工作目录会更新以反映该提交时的文件状态。
3. **暂存区的基础**：`HEAD` 也用作暂存区（staging area）的基础。当你添加（add）更改到暂存区时，这些更改是相对于 `HEAD` 指向的提交进行的。

## `HEAD` 的工作方式

- **引用文件**：在 `.git` 目录中，`HEAD` 是一个文件，通常包含对当前分支的引用。例如，`HEAD` 文件可能包含 `ref: refs/heads/master`，表示 `HEAD` 指向 `master` 分支。
- **更新 `HEAD`**：当你执行 `git checkout <branch>` 或 `git commit` 等命令时，`HEAD` 会更新为指向新的分支或新的提交。

### 使用 `HEAD`

- **查看 `HEAD`**：
  ```bash
  cat .git/HEAD
  ```
  这个命令显示 `HEAD` 文件的内容，通常是一个指向当前分支的引用。

- **检出 `HEAD`**：
  ```bash
  git checkout HEAD
  ```
  这个命令将工作目录恢复到 `HEAD` 指向的提交状态。

- **比较 `HEAD`**：
  ```bash
  git diff HEAD
  ```
  这个命令显示自 `HEAD` 指向的提交以来工作目录中的更改。

## 查看当前分支的 `HEAD` 
### 1. 使用 `git log`

运行以下命令来查看当前分支的最新提交，这通常是 `HEAD` 指向的提交：

```bash
git log -1
```

这个命令显示最近一次提交的详细信息，包括提交哈希、作者、日期和提交信息。

### 2. 使用 `git show`

如果你想查看 `HEAD` 指向的提交的详细内容，可以使用：

```bash
git show HEAD
```

这个命令显示 `HEAD` 指向的提交的详细信息，包括更改的内容。

### 3. 使用 `git rev-parse`

要获取 `HEAD` 指向的提交的哈希值，可以使用：

```bash
git rev-parse HEAD
```

这个命令输出 `HEAD` 指向的提交的哈希值。

### 4. 查看 `.git/HEAD` 文件

如果你想直接查看 `HEAD` 文件的内容，可以使用：

```bash
cat .git/HEAD
```

这个命令显示 `HEAD` 文件的内容，通常是一个指向当前分支的引用，如 `ref: refs/heads/main`。

### 5. 使用 `git status`

运行以下命令来查看当前分支的状态，包括 `HEAD` 指向的提交：

```bash
git status
```

这个命令显示当前分支的状态，包括 `HEAD` 指向的提交和任何未提交的更改。

## HEAD^

- **定义**：`HEAD^`（读作 "HEAD caret"）引用 `HEAD` 指向的提交的父提交。如果有多个父提交（例如，在合并提交中），`HEAD^` 引用第一个父提交。
- **用途**：用于指定 `HEAD` 的直接父提交。这在查看提交历史或执行需要指定特定提交的操作时非常有用。
- **示例**：`git log HEAD^` 会显示 `HEAD` 的父提交的详细信息。

## HEAD~

- **定义**：`HEAD~`（读作 "HEAD tilde"）是 `HEAD` 的简写形式，通常用于指定 `HEAD` 指向的提交的父提交。`HEAD~` 与 `HEAD^` 在大多数情况下是等效的。
- **用途**：用于指定 `HEAD` 的父提交，特别是在需要简洁引用时。
- **示例**：`git log HEAD~` 会显示 `HEAD` 的父提交的详细信息。

### HEAD~n

- **定义**：`HEAD~n`（其中 `n` 是一个正整数）引用 `HEAD` 指向的提交的第 `n` 个父提交。例如，`HEAD~3` 引用 `HEAD` 的第三个父提交。
- **用途**：用于指定 `HEAD` 的祖先提交。这在查看提交历史或执行需要指定特定提交的操作时非常有用。
- **示例**：`git log HEAD~3` 会显示 `HEAD` 的第三个父提交的详细信息。

## 使用场景

- **查看提交历史**：使用 `git log HEAD^` 或 `git log HEAD~` 查看 `HEAD` 的父提交的历史。
- **比较提交**：使用 `git diff HEAD^` 或 `git diff HEAD~` 比较 `HEAD` 和其父提交之间的差异。
- **撤销提交**：使用 `git reset --soft HEAD^` 撤销最后一次提交，但保留工作目录和暂存区的状态。
在 Git 中，`HEAD` 是一个非常重要的概念，它指向当前分支的最新提交。`HEAD` 及其相关语法（如 `HEAD~3`）用于引用特定的提交。以下是关于 `HEAD` 及其语法的详细讲解：

### 总结

`HEAD`、`HEAD^`、`HEAD~` 和 `HEAD~n` 是 Git 中用于引用提交的强大工具。它们帮助你指定和操作特定的提交及其关系。理解这些概念对于有效使用 Git 进行版本控制和历史管理至关重要。


## `HEAD` 的重要性


- **版本控制的基础**：`HEAD` 是 Git 版本控制的核心，它决定了你正在工作的版本和状态。
- **分支和合并**：在分支和合并操作中，`HEAD` 用于确定当前的工作基础和合并的目标。

## 注意事项

- **`HEAD` 与 `ORIG_HEAD`**：在某些操作（如合并冲突解决）中，Git 会创建一个 `ORIG_HEAD` 引用，以保存原始 `HEAD` 的状态，以便在需要时可以恢复。
- **`HEAD` 与 `FETCH_HEAD`**：`FETCH_HEAD` 用于记录 `git fetch` 操作的结果，与 `HEAD` 不同，它通常用于比较和合并操作。

# Index
> [Git - Reset Demystified](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified#_git_reset)      

在 Git 中，"index"（索引）是一个非常重要的概念，它通常被称为 "staging area"（暂存区）。索引是 Git 用来准备下一次提交的文件列表。

The index is your proposed next commit. We’ve also been referring to this concept as Git’s “Staging Area” as this is what Git looks at when you run git commit.

## 索引的作用

1. **暂存更改**：索引用于暂存（stage）你想要在下一次提交中包含的更改。你可以将更改的文件添加到索引中，然后一次性提交所有暂存的更改。
2. **准备提交**：当你执行 `git add` 命令时，更改的文件会被添加到索引中。这些文件将在下一次 `git commit` 时被提交。
3. **跟踪更改**：索引跟踪你对文件所做的更改，直到这些更改被提交。

## 索引的工作方式

- **索引文件**：在 `.git` 目录中，索引是一个名为 `index` 的文件，它包含了当前暂存的文件列表。
- **更新索引**：当你使用 `git add` 添加文件时，索引文件会被更新以反映这些更改。
- **重置索引**：你可以使用 `git reset` 命令来重置索引，移除暂存的文件或将索引恢复到特定状态。

## 使用索引

- **添加文件到索引**：
  ```bash
  git add <file>
  ```
  这个命令将指定文件的更改添加到索引中。

- **查看索引内容**：
  ```bash
  git ls-files --stage
  ```
  这个命令显示索引中的文件及其状态。

- **重置索引**：
  ```bash
  git reset <file>
  ```
  这个命令将指定文件从索引中移除，但保留工作目录中的更改。

- **清空索引**：
  ```bash
  git reset
  ```
  这个命令清空索引，移除所有暂存的更改。

## 索引与工作目录

- **工作目录**：工作目录是你当前工作的文件夹，包含了项目的文件。
- **索引与工作目录的关系**：索引是从工作目录中选择的更改的集合，这些更改将在下一次提交时被记录。

## 注意事项

- **索引状态**：使用 `git status` 命令可以查看索引的状态，了解哪些文件已被暂存以及哪些文件尚未暂存。
- **索引与提交**：索引中的文件将在下一次提交时被提交。确保你已经将所有想要提交的更改添加到索引中。
- **索引与分支**：当你切换分支时，索引会被更新以反映新分支的状态。

# The Working Directory
> [Git - Reset Demystified](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified#_git_reset)      

you have your working directory (also commonly referred to as the “working tree”).

在 Git 中，"working directory"（工作目录）和 "working tree"（工作树）是两个密切相关但略有不同的概念。它们都涉及到你在本地检出的文件和目录，但它们的含义和用途有所不同。以下是关于这两个概念的详细讲解：

1. **定义**：工作目录是指你当前正在工作的目录，它是你检出的文件和目录的集合。当你克隆一个仓库或检出一个分支时，Git 会在你的本地文件系统中创建一个工作目录。
2. **内容**：工作目录包含了项目的文件和目录，这些文件和目录是你从 Git 仓库中检出的。你可以在这个目录中编辑文件、添加新文件或删除文件。
3. **更改跟踪**：当你在工作目录中进行更改时，这些更改不会立即被 Git 跟踪。你需要使用 `git add` 将更改添加到暂存区（索引），然后使用 `git commit` 提交这些更改。

- **检出分支或提交**：使用 `git checkout <branch>` 或 `git checkout <commit>` 检出不同的分支或提交，Git 会更新工作目录和工作树以反映所检出的状态。
- **查看状态**：使用 `git status` 查看工作目录和工作树的状态，了解哪些文件已被修改但尚未提交。
- **添加更改**：使用 `git add <file>` 将工作目录或工作树中的更改添加到暂存区。
- **提交更改**：使用 `git commit` 提交暂存区中的更改，更新工作目录和工作树的状态。

# workflow
> [Git - Reset Demystified](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified#_git_reset)      

# Undo things
> [Git - Undoing Things](https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things) 

## 修改提交 git commit --amend
`git commit --amend` 是 Git 中用于修改最近一次提交的命令。这个命令允许你更改最后一次提交的内容，包括提交信息和提交内容。

1. **修改提交信息**：如果你在提交后发现提交信息有误或需要补充，`git commit --amend` 可以让你编辑提交信息。
2. **添加遗漏的更改**：如果你在提交后发现遗漏了一些更改，可以使用 `git commit --amend` 将这些更改添加到最近一次提交中。
3. **更新提交内容**：如果你在提交后对文件进行了修改，可以使用 `git commit --amend` 将这些修改包含在最近一次提交中。

### 使用场景

- **修正提交信息**：当你提交后发现提交信息有错别字或不够清晰时。
- **补充遗漏的文件**：当你提交后发现有文件忘记添加时。
- **更新文件内容**：当你提交后对文件进行了修改，并希望这些修改作为最后一次提交的一部分。
- Only amend commits that are still local and have not been pushed somewhere.

### 基本使用

- **修改提交信息**：
  ```bash
  git commit --amend
  ```
  这个命令会打开一个文本编辑器，编辑最近一次提交的信息。

- **添加遗漏的更改**：
  ```bash
  git add <file>
  git commit --amend
  ```
  这个命令序列将遗漏的文件添加到暂存区，然后使用 `git commit --amend` 将这些更改包含在最近一次提交中。

### 选项

- **`-m`**：指定新的提交信息。例如：
  ```bash
  git commit --amend -m "New commit message"
  ```
  这个命令直接指定新的提交信息，而不会打开编辑器。

### 注意事项

- **本地提交**：`git commit --amend` 只能用于修改本地仓库中的提交。如果你已经将提交推送到远程仓库，修改本地提交后需要使用 `git push --force` 来覆盖远程仓库中的提交。
- **影响协作**：如果你已经将提交推送到远程仓库，修改提交后可能会对协作产生影响。确保在修改提交之前与团队成员沟通。
- **撤销更改**：如果你在 `git commit --amend` 后想要撤销更改，可以使用 `git reflog` 查找原始提交的引用，然后使用 `git reset` 恢复到原始状态。

### 示例

假设提交了一个更改，但忘记添加一个文件：

```bash
git commit -m "Initial commit"
git add forgotten_file
git commit --amend
```

这个过程将创建一个新的提交，包含所有之前的更改和新添加的文件，原始提交将被替换。

## git reset - Unstaging a Staged File
> [Git - Reset Demystified](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified#_git_reset) 
> [Git - git-reset Documentation](https://git-scm.com/docs/git-reset) 
> [Git - git-reset Documentation](https://git-scm.com/docs/git-reset#_discussion) 

`git reset` 是 Git 中用于重置当前 HEAD 和（可选地）索引（暂存区）的命令。它可以用来撤销提交、重置暂存区或恢复工作目录中的文件。

1. **撤销提交**：`git reset` 可以将当前分支的 HEAD 指针移动到指定的状态，但不影响工作目录。
2. **重置暂存区**：它可以将暂存区的内容重置为特定提交的状态。
3. **恢复工作目录**：`git reset` 还可以用来恢复工作目录中的文件到特定提交的状态。

### 使用场景

- **撤销错误的提交**：当你提交了错误的更改并希望撤销这些提交时。
- **重置暂存区**：当你想要清除暂存区中的更改时。
- **恢复文件**：当你想要将文件恢复到特定提交的状态时。

### `--soft`

- **作用**：重置 HEAD 到指定状态，但保留工作目录和暂存区的状态。
- **结果**：这允许你重新提交。`--soft` 是最安全的重置选项，因为它不会丢失任何更改。
- **使用场景**：当你想要撤销最后一次提交，但保留所有更改在暂存区时，可以使用 `--soft`。

### `--mixed`（默认）

- **作用**：重置 HEAD 和暂存区到指定状态，但保留工作目录的状态。
- **结果**：这允许你重新暂存更改。`--mixed` 是默认的重置选项，如果你没有指定任何选项，Git 将使用这个模式。
- **使用场景**：当你想要撤销最后一次提交并重置暂存区，但保留工作目录中的更改时，可以使用 `--mixed`。

### `--hard`

- **作用**：重置 HEAD、暂存区和工作目录到指定状态。
- **结果**：这将丢失所有未提交的更改。`--hard` 是最危险的重置选项，因为它会丢弃所有未提交的更改。
- **使用场景**：当你想要完全撤销最后一次提交并丢弃所有未提交的更改时，可以使用 `--hard`。

### `--merge`

- **作用**：重置 HEAD 到指定状态，并尝试合并工作目录和暂存区的更改。
- **结果**：这允许你撤销最后一次提交并尝试合并更改。如果合并失败，你将得到一个合并冲突。
- **使用场景**：当你想要撤销最后一次提交并尝试合并更改时，可以使用 `--merge`。

### `--keep`

- **作用**：重置 HEAD 到指定状态，但保留工作目录和暂存区的状态，即使这意味着 HEAD 指向不同的分支。
- **结果**：这允许你切换到不同的分支并保留所有更改。
- **使用场景**：当你想要切换到不同的分支并保留所有更改时，可以使用 `--keep`。

### undo add
git add 文件后可以 git reset 撤回 add 或者 git restore --staged 
```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (main)
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   test04.txt


lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (main)
$ git reset

lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (main)
$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test04.txt
```
### undo a commit 
新建一个提交，然后 git reset 移动 HEAD 到上一个提交，此时 git log 查看最新的提交看不到被撤销的提交。
```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (main)
$ git commit -m "1"
[main 235d5b0] 1
 1 file changed, 1 insertion(+)

lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (main)
$ git log
commit 235d5b0252a039e0edc53048fa55e5a4fff72a0b (HEAD -> main)
Author: lxwcd <15521168075@163.com>
Date:   Sun Dec 15 20:46:50 2024 +0800

    1

lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (main)
$ git reset --soft HEAD^
```

#### 显示被撤销的提交
执行 `git reset --soft HEAD^` 后，`HEAD` 指针确实指向了上一次提交。要查看被撤销的上次提交，你可以使用以下方法：

1. 使用 `ORIG_HEAD`

当你执行 `git reset` 时，Git 会自动创建一个名为 `ORIG_HEAD` 的引用，指向原始的 `HEAD` 位置。因此，你可以使用 `ORIG_HEAD` 来查看被撤销的提交：

```bash
git log ORIG_HEAD
```
```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (main)
$ git log ORIG_HEAD
commit 235d5b0252a039e0edc53048fa55e5a4fff72a0b
Author: lxwcd <15521168075@163.com>
Date:   Sun Dec 15 20:46:50 2024 +0800

    1
```
这个命令会显示被撤销的提交的详细信息。

2. 使用 `HEAD@{1}`

Git 的 reflog 功能记录了 `HEAD` 的每次更新。你可以使用 `HEAD@{1}` 来引用 `HEAD` 的上一个位置：

```bash
git log HEAD@{1}
```

这个命令会显示 `HEAD` 在上一次更新时指向的提交。

3. 使用 `git reflog`

`git reflog` 显示 `HEAD` 的更新历史，你可以通过它找到被撤销的提交：

```bash
git reflog
```

在输出中，找到对应的操作（通常是 `reset` 操作），并查看该操作之前的 `HEAD` 位置。

4. 使用 `git log` 的范围功能

如果你知道被撤销提交的哈希值，可以直接使用 `git log` 的范围功能来查看该提交：

```bash
git log <commit-hash>
```

将 `<commit-hash>` 替换为被撤销提交的实际哈希值。

### undo a commit and switch branch
```bash
$ git branch topic/wip          (1)
$ git reset --hard HEAD~3       (2)
$ git switch topic/wip          (3)
```
You have made some commits, but realize they were premature to be in the master branch. You want to continue polishing them in a topic branch, so create topic/wip branch off of the current HEAD.

Rewind the master branch to get rid of those three commits.

Switch to topic/wip branch and keep working.

### Reset a single file in the index
> [Git - git-reset Documentation](https://git-scm.com/docs/git-reset#Documentation/git-reset.txt-Resetasinglefileintheindex) 

### Keep changes in working tree while discarding some previous commits
> [Git - git-reset Documentation](https://git-scm.com/docs/git-reset#Documentation/git-reset.txt-Keepchangesinworkingtreewhilediscardingsomepreviouscommits) 

### Split a commit apart into a sequence of commits
> [Git - git-reset Documentation](https://git-scm.com/docs/git-reset#Documentation/git-reset.txt-Splitacommitapartintoasequenceofcommits) 

### 使用示例

- **撤销最后一次提交**：
  ```bash
  git reset --soft HEAD~1
  ```
  这个命令将 HEAD 指针移动到上一次提交，但保留工作目录和暂存区的状态。

- **撤销最后一次提交并重置暂存区**：
  ```bash
  git reset --mixed HEAD~1
  ```
  或者
  ```bash
  git reset HEAD~1
  ```
  这些命令将 HEAD 指针移动到上一次提交，并重置暂存区，但保留工作目录的状态。

- **撤销最后一次提交并恢复工作目录**：
  ```bash
  git reset --hard HEAD~1
  ```
  这个命令将 HEAD 指针移动到上一次提交，并重置暂存区和工作目录的状态。

### 注意事项

- **数据丢失风险**：`git reset --hard` 会丢失所有未提交的更改，使用时需谨慎。
- **撤销已推送的提交**：如果你已经将提交推送到远程仓库，使用 `git reset` 撤销提交后，需要使用 `git push --force` 来更新远程仓库。
- **与 `git checkout` 的区别**：`git reset` 用于重置当前分支的 HEAD 和暂存区，而 `git checkout` 用于切换分支或将文件恢复到最后一次提交的状态。

### 选项

- **`--soft`**：重置 HEAD 到指定状态，但保留工作目录和暂存区的状态。这允许你重新提交。
- **`--mixed`**（默认）：重置 HEAD 和暂存区到指定状态，但保留工作目录的状态。这允许你重新暂存更改。
- **`--hard`**：重置 HEAD、暂存区和工作目录到指定状态。这将丢失所有未提交的更改。

## git restore
> [Git - git-restore Documentation](https://git-scm.com/docs/git-restore) 

`git restore` 是 Git 中的一个命令，用于恢复工作目录中的文件。它允许你将文件恢复到特定的状态，通常是从 `HEAD` 或其他指定的源。

### 功能和用途

1. **恢复工作目录文件**：`git restore` 用于将工作目录中的文件恢复到某个特定的状态。这可以是从 `HEAD`、索引（暂存区）或其他指定的源。
2. **恢复索引内容**：使用 `--staged` 选项可以恢复索引（暂存区）的内容。
3. **恢复工作目录和索引**：结合 `--staged` 和 `--worktree` 选项可以同时恢复工作目录和索引的内容。

### 基本语法

```bash
git restore [<options>] [--source=<tree>] [--staged] [--worktree] [--] <pathspec>…
```

### 选项

- **`--source=<tree>`**：指定恢复内容的源。可以是提交、分支或标签。默认情况下，如果没有指定 `--staged`，则从索引恢复；如果指定了 `--staged`，则从 `HEAD` 恢复。
- **`--staged`**：恢复索引（暂存区）的内容。
- **`--worktree`**：恢复工作目录的内容。
- **`-p` 或 `--patch`**：交互式选择要恢复的更改块。
- **`--ours` 和 `--theirs`**：在恢复工作目录文件时，使用索引中的第 2 阶段（`ours`）或第 3 阶段（`theirs`）来处理未合并的路径。
- **`--merge`**：在恢复工作目录文件时，重新创建未合并路径的冲突合并。
- **`--conflict=<style>`**：指定冲突块的显示方式，覆盖 `merge.conflictStyle` 配置变量。
- **`--ignore-unmerged`**：在从索引恢复工作目录文件时，如果有未合并的条目且没有指定 `--ours`、`--theirs`、`--merge` 或 `--conflict`，则不中止操作。
- **`--recurse-submodules`**：如果路径规范指定的是活动子模块，并且恢复位置包括工作目录，则只有在指定了此选项时才会更新子模块。

### 示例

1. **从其他提交中恢复文件**：
   ```bash
   git restore --source master~2 Makefile
   ```
   这个命令将 `Makefile` 文件恢复到 `master` 分支的前两次提交的状态。

2. **恢复索引中的文件**：
   ```bash
   git restore --staged hello.c
   ```
   这个命令将 `hello.c` 文件恢复到索引中的状态。

3. **同时恢复索引和工作目录中的文件**：
   ```bash
   git restore --source=HEAD --staged --worktree hello.c
   ```
   或者使用简写形式：
   ```bash
   git restore -s@ -SW hello.c
   ```
   这些命令将 `hello.c` 文件恢复到 `HEAD` 指向的状态，并同时更新索引和工作目录。

### 注意事项

- **实验性命令**：`git restore` 是一个实验性命令，其行为可能会改变。
- **与 `git reset` 和 `git revert` 的区别**：`git restore` 用于恢复工作目录中的文件，而 `git reset` 用于重置当前分支的 HEAD 和索引，`git revert` 用于创建一个新的提交来“反做”之前的提交。

# git revert
> [Git - git-revert Documentation](https://git-scm.com/docs/git-revert) 

`git revert` 是一个 Git 命令，用于撤销之前的提交。它创建一个新的提交，这个提交的内容是前一个提交的逆操作，即“反做”之前的提交。这个操作是安全的，因为它不会改变项目的历史记录，而是在历史记录的基础上新增一个提交来表示撤销操作。

## 基本用法

1. **撤销最新的提交**
   - `git revert HEAD`：撤销当前分支最新的提交。

2. **撤销特定的提交**
   - `git revert <commit>`：撤销指定的提交。这里的 `<commit>` 可以是提交的哈希值、分支名或者标签。

3. **撤销一系列提交**
   - `git revert <commit>^..<commit>`：撤销从第一个提交到第二个提交之间的所有提交。

## 选项

1. **`--no-commit`**
   - 执行撤销操作但不创建一个新的提交对象。这允许你修改撤销的内容后再手动提交。

2. **`--no-edit`**
   - 通常 `git revert` 会打开一个编辑器让你编辑提交信息。使用这个选项可以跳过编辑步骤，使用默认的提交信息。

3. **`--edit`**
   - 强制 `git revert` 打开编辑器，即使通常不需要编辑提交信息。

4. **`--merge`**
   - 在合并操作中使用，允许在合并冲突时撤销。

5. **`--mainline`**
   - 在合并操作中使用，指定主基线。

6. **`--strategy`**
   - 指定合并策略。

7. **`--strategy-option`**
   - 传递额外的选项给合并策略。

8. **`--allow-empty`**
   - 允许在空树（即没有任何提交的仓库）上执行撤销操作。

9. **`--onto`**
   - 指定一个基底提交，用于确定撤销操作的目标分支。

## 工作流程

当你执行 `git revert` 时，Git 会做以下事情：

1. **检查提交是否存在**：确认你指定的提交在当前分支的历史中。

2. **计算差异**：计算需要撤销的提交与你指定的基底提交之间的差异。

3. **应用差异**：将这些差异应用到工作目录和暂存区，相当于做了一个“反做”操作。

4. **创建新的提交**：将这些变化作为一个新提交添加到历史记录中。

## 示例

- 撤销最新的提交：
  ```bash
  git revert HEAD
  ```

- 撤销特定的提交（提交哈希值以 `abc123` 为例）：
  ```bash
  git revert abc123
  ```

- 撤销一系列提交（从 `commit1` 到 `commit2`）：
  ```bash
  git revert commit1^..commit2
  ```

- 撤销操作但不创建提交：
  ```bash
  git revert --no-commit abc123
  ```

- 撤销操作并编辑提交信息：
  ```bash
  git revert --edit abc123
  ```

# git remote
> [Git - git-remote Documentation](https://git-scm.com/docs/git-remote) 

`git remote` 是 Git 中用于管理远程仓库的命令。它允许你查看、添加、修改和删除远程仓库的引用。以下是 `git remote` 命令的详细讲解：

### 功能和用途

1. **查看远程仓库**：`git remote` 命令可以列出所有配置的远程仓库。
2. **添加远程仓库**：你可以使用 `git remote add` 命令添加新的远程仓库。
3. **修改远程仓库**：可以更改远程仓库的 URL 或其他设置。
4. **删除远程仓库**：可以删除不再需要的远程仓库引用。

### 基本使用

- **查看远程仓库列表**：
  ```bash
  git remote
  ```
  这个命令列出所有配置的远程仓库的短名称。

- **查看远程仓库详细信息**：
  ```bash
  git remote -v
  ```
  这个命令列出所有配置的远程仓库及其对应的 URL。

- **添加远程仓库**：
  ```bash
  git remote add <name> <url>
  ```
  这个命令添加一个新的远程仓库引用，`<name>` 是远程仓库的短名称，`<url>` 是远程仓库的 URL。

- **删除远程仓库**：
  ```bash
  git remote remove <name>
  ```
  这个命令删除指定的远程仓库引用。

- **重命名远程仓库**：
  ```bash
  git remote rename <old-name> <new-name>
  ```
  这个命令将远程仓库的名称从 `<old-name>` 更改为 `<new-name>`。

- **设置远程仓库 URL**：
  ```bash
  git remote set-url <name> <new-url>
  ```
  这个命令更改指定远程仓库的 URL。

### 选项

- **`-v` 或 `--verbose`**：显示远程仓库的详细信息，包括 URL。
- **`add`**：添加新的远程仓库引用。
- **`remove`**：删除远程仓库引用。
- **`rename`**：重命名远程仓库。
- **`set-url`**：更改远程仓库的 URL。

### 使用场景

- **协作开发**：在团队协作中，你可能需要添加远程仓库来共享代码。
- **代码托管**：你可能需要将代码推送到远程仓库以进行托管或备份。
- **分支管理**：通过远程仓库，你可以管理不同分支的代码。

### 示例

假设你想要添加一个新的远程仓库：

```bash
git remote add origin https://github.com/lxwcd/git_test.git
git branch -M main
git push -u origin main
```

这个命令添加了一个名为 `origin` 的远程仓库引用，指向 `https://github.com/lxwcd/git_test.git`。

### 注意事项

- **远程仓库名称**：`origin` 是默认的远程仓库名称，但你可以使用任何名称。
- **URL 格式**：确保远程仓库的 URL 格式正确，可以是 HTTPS 或 SSH 格式。
- **权限**：在添加或修改远程仓库时，确保你有足够的权限。

通过 `git remote`，你可以有效地管理远程仓库的引用，这对于协作开发和代码托管非常重要。

# git branch
> [Git - git-branch Documentation](https://git-scm.com/docs/git-branch/2.13.7) 



# 本地分支的上游分支 
在 Git 中，每个本地分支可以设置一个对应的上游分支（也称为远程跟踪分支），这样当你执行 `git push` 或 `git pull` 时，Git 会自动知道要与哪个远程分支交互。

## 设置本地分支的上游分支

1. **设置新分支的上游分支**：
   当你创建一个新的本地分支并想要将其设置为跟踪远程仓库中的某个分支时，可以使用以下命令：
   ```bash
   git checkout -b my-branch origin/existing-remote-branch
   ```
   这个命令会创建一个新的本地分支 `my-branch` 并将其设置为跟踪远程分支 `origin/existing-remote-branch`。

2. **修改现有分支的上游分支**：
   如果你想要更改一个已经存在的本地分支的上游分支，可以使用以下命令：
   ```bash
   git branch --set-upstream-to my-branch origin/new-remote-branch
   ```
   或者，如果你的 Git 版本较旧，可能需要使用：
   ```bash
   git branch --set-upstream my-branch origin/new-remote-branch
   ```
   这些命令会将本地分支 `my-branch` 的上游分支设置为 `origin/new-remote-branch`。

### 查看本地分支的上游分支

1. **使用 `git branch` 命令**：
   你可以使用以下命令查看所有本地分支及其对应的上游分支：
   ```bash
   git branch -vv
   ```
   这个命令会列出所有本地分支，并显示它们是否与上游分支同步，以及上游分支的最后一次提交信息。

2. **单独查看特定分支的上游分支**：
   如果你想要查看特定分支的上游分支，可以使用：
   ```bash
   git branch -vv my-branch
   ```
   这会显示 `my-branch` 分支的上游分支信息。

### 删除本地分支的上游分支设置

如果你想要删除本地分支的上游分支设置，可以使用以下命令：
```bash
git branch --unset-upstream my-branch
```

这个命令会移除 `my-branch` 分支的上游分支设置，之后你将需要手动指定远程分支进行推送和拉取操作。

通过这些命令，你可以灵活地设置和管理你的本地分支与远程分支之间的关系，这对于多人协作的项目来说非常重要。


# git fetch
> [Git - git-fetch Documentation](https://git-scm.com/docs/git-fetch) 

`git fetch` 是 Git 中用于从远程仓库获取更新的命令。它允许你下载远程分支和标签的最新更改，但不会自动合并这些更改到你的当前分支。

## 功能和用途

1. **获取远程更新**：`git fetch` 用于从远程仓库下载最新的提交、分支和标签信息。
2. **不自动合并**：与 `git pull` 不同，`git fetch` 只是下载更新，不会自动合并到你的当前分支。这允许你在合并之前检查远程更改。
3. **更新远程跟踪分支**：`git fetch` 会更新本地的远程跟踪分支（如 `origin/master`），使其反映远程仓库的当前状态。

## 基本使用

- **获取所有远程更新**：
  ```bash
  git fetch
  ```
  这个命令从所有配置的远程仓库获取更新。

- **获取特定远程仓库的更新**：
  ```bash
  git fetch <remote-name>
  ```
  这个命令从指定的远程仓库（如 `origin`）获取更新。

- **获取特定分支的更新**：
  ```bash
  git fetch <remote-name> <branch-name>
  ```
  这个命令从指定的远程仓库获取特定分支的更新。

## 选项

- **`--all`**：从所有远程仓库获取更新。
- **`--prune`**：清除远程跟踪分支中不再存在于远程仓库的分支。
- **`--dry-run`**：模拟获取更新的过程，但不实际下载数据。
- **`--verbose`**：显示详细的输出，包括下载过程中的信息。

## 使用场景

- **检查远程更改**：在合并远程更改之前，使用 `git fetch` 检查远程仓库的最新状态。
- **更新远程跟踪分支**：定期使用 `git fetch` 更新本地的远程跟踪分支，以保持与远程仓库的同步。
- **避免合并冲突**：在合并远程更改之前，使用 `git fetch` 下载更新，然后手动检查和解决潜在的合并冲突。

## 示例

假设你想要从名为 `origin` 的远程仓库获取 `master` 分支的最新更新：

```bash
git fetch origin master
```

这个命令会下载 `origin` 仓库中 `master` 分支的最新更改，但不会自动合并到你的当前分支。

## 注意事项

- **不影响当前工作**：`git fetch` 不会改变你的当前工作目录或暂存区，它只是更新远程跟踪分支。
- **与 `git pull` 的区别**：`git pull` 是 `git fetch` 加上 `git merge` 的组合，它会下载远程更新并自动合并到你的当前分支。

通过 `git fetch`，你可以有效地获取远程仓库的最新更新，而不必立即合并这些更改。这使得 `git fetch` 成为检查远程更改和更新远程跟踪分支的有用工具。

# 切换到远程仓库的新分支

## 1. 获取远程分支列表

首先，你需要获取远程仓库的最新分支列表。这可以通过运行以下命令来完成：

```bash
git fetch --all
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (main)
$ git fetch --all
From https://github.com/lxwcd/git_test
 * [new branch]      remote_branch01 -> origin/remote_branch01
```

这个命令会从所有配置的远程仓库获取更新，但不会自动合并到你的当前分支。它会更新本地的远程跟踪分支，使其反映远程仓库的当前状态。

## 2. 列出远程分支

接下来，你可以列出所有远程分支，以确认新添加的分支名称：

```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (main)
$ git branch -r
  origin/main
  origin/remote_branch01
```

这个命令会显示所有远程跟踪分支的列表。

## 3. 切换到新分支

切换到一个已经存在的远程分支，如果本地没有对应的跟踪分支，Git 会自动创建一个。
执行这个命令后，你的本地工作目录会切换到指定的远程分支。如果本地没有这个分支的跟踪信息，Git 会自动为你设置一个本地分支来跟踪远程分支。

```bash
git checkout <new-branch-name>
```

将 `<new-branch-name>` 替换为远程仓库中新添加的分支名称。

## 4. 创建本地分支（如果需要）

如果你希望在本地创建一个新分支来跟踪远程分支，可以使用以下命令：

```bash
git checkout -b <local-branch-name> <remote-name>/<new-branch-name>
```

将 `<local-branch-name>` 替换为你想要的本地分支名称，`<remote-name>` 替换为远程仓库的名称（如 `origin`），`<new-branch-name>` 替换为远程分支的名称。
执行这个命令后，Git 会在本地创建一个新的分支 <local-branch-name>，并将其设置为跟踪远程分支 <remote-name>/<new-branch-name>。然后，你的工作目录会切换到这个新创建的本地分支。

```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (main)
$ git checkout -b remote_branch01 origin/remote_branch01
Switched to a new branch 'remote_branch01'
branch 'remote_branch01' set up to track 'origin/remote_branch01'.
```

## 5. 确认分支切换

最后，你可以使用 `git branch` 命令确认你已经切换到了正确的分支：

```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (remote_branch01)
$ git branch -a
  feature01
  main
* remote_branch01
  remotes/origin/main
  remotes/origin/remote_branch01
```

# git pull
> [Git - git-pull Documentation](https://git-scm.com/docs/git-pull) 

`git pull` 是 Git 中的一个命令，用于将远程仓库的更改拉取到本地仓库。它实际上是一个组合命令，等同于 `git fetch` 后跟 `git merge`。

## 基本用法

1. **`git pull`：** 这个命令会从默认的远程仓库（通常是 `origin`）和默认分支（通常是你的当前分支）拉取最新的更改，并尝试与你的本地分支合并。

2. **`git pull <remote-name>`：** 指定从哪个远程仓库拉取更改。`<remote-name>` 是远程仓库的名称，例如 `origin`。

3. **`git pull <remote-name> <branch-name>`：** 指定从哪个远程仓库的哪个分支拉取更改。`<branch-name>` 是远程分支的名称。

## 工作原理

- **`git fetch`：** `git pull` 首先执行 `git fetch`，从远程仓库获取最新的分支和数据，但不会自动合并到你的当前分支中。这一步确保你的本地仓库知道远程仓库的最新状态。

- **`git merge`：** 在获取了远程分支的最新数据后，`git pull` 会执行 `git merge`，将远程分支的更改合并到你的本地分支中。如果合并过程中出现冲突，你需要手动解决这些冲突。

## 选项

- **`--ff-only`：** 只进行快进合并。如果远程分支的提交历史不是你的本地分支的直接祖先，合并将被拒绝。

- **`--no-ff`：** 创建一个新的合并提交，即使合并可以快进。这有助于保留分支的历史。

- **`--rebase`：** 使用 `git pull --rebase` 代替默认的合并行为。这会将你的本地更改重新应用到远程分支的顶部，使得历史更加线性。

## 常见问题

1. **合并冲突：** 如果远程分支的更改与你的本地更改冲突，`git pull` 会停止并要求你解决冲突。解决冲突后，你需要提交这些更改以完成合并。 如远程和本地对同一个文件的同一行进行修改，本地 git pull:
```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (remote_branch01)
$ git pull
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 962 bytes | 80.00 KiB/s, done.
From https://github.com/lxwcd/git_test
   e67a0f3..c8d5a84  remote_branch01 -> origin/remote_branch01
Auto-merging test01.txt
CONFLICT (content): Merge conflict in test01.txt
Automatic merge failed; fix conflicts and then commit the result.

$ git status
On branch remote_branch01
Your branch and 'origin/remote_branch01' have diverged,
and have 1 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   test01.txt

no changes added to commit (use "git add" and/or "git commit -a")

lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (remote_branch01|MERGING)
$ cat test01.txt
test01
<<<<<<< HEAD
local modify test01.txt
=======
git pull
>>>>>>> c8d5a8479666ce11a479c2ed9568bde02dc17257
```
在你提供的代码片段中，`test01` 文件发生了冲突。冲突发生在 `HEAD`（你的本地分支）和远程分支 `c8d5a8479666ce11a479c2ed9568bde02dc17257` 之间。以下是冲突的标记：

- `<<<<<<< HEAD`：标记冲突的开始，以下是本地分支的代码。
- `=======`：分隔符，标记远程分支的代码开始。
- `>>>>>>> c8d5a8479666ce11a479c2ed9568bde02dc17257`：标记冲突的结束，以上是远程分支的代码。

要解决这个冲突，你需要决定保留哪些更改。以下是如何手动解决这个冲突的步骤：

### 步骤 1: 打开冲突文件
在 VSCode 中打开 `test01` 文件。

### 步骤 2: 查看冲突内容
文件内容显示了冲突的部分：

```plaintext
test01
<<<<<<< HEAD
local modify test01.txt
=======
git pull
>>>>>>> c8d5a8479666ce11a479c2ed9568bde02dc17257
```
如果你想保留本地更改并忽略远程更改，文件内容将变为：
```plaintext
test01
local modify test01.txt
```

如果你想保留远程更改并忽略本地更改，文件内容将变为：
```plaintext
test01
git pull
```

如果你想合并两者，文件内容可能变为：
```plaintext
test01
local modify test01.txt
git pull
```

# github 文档换行处理  
上传到 github 上的文档，行末尾需要添加两个空格才会换行  
      
## 行末尾添加空格  
每行末尾添加两个空格  
      
利用宏，普通模式，按 q，然后选择一个寄存器，如 a，开始录制：按 `A` 切换到行末尾且切换到插入模式，输入两个空格，按 `Esc` 回到普通模式，按 `q` 录制结束  
      
选择需要处理的行，如全文处理，则切换到第一行，按 `V` 选择当前行，按 `G` 选择到最后一行，即选中全文，然后按 `:` 切换到命令行模式，此时自动选中选择的行 `:'<,'>`，后面输入 `normal @a`，即 `:'<,'>normal @a`  
      
      
## 删除行末尾空格  
在文档上传前，批量处理每行，在其末尾加两个空格，但文档可能重复修改，不能每次上传都加空格，因此在加空格前，先删除末尾的空格  
      
规则为：不处理空白行，包含多个空格的行，仅处理有内容，末尾有两个或以上空格的行，删除末尾空格  
      
### vim 中处理  
不用 very magic 模式：  
```bash  
%s/\(\S\)\s\{2,\}$/\1/g  
```  
      
用 very magic 模式：  
```bash  
%s/\v(\S)\s{2,}$/\1/g  
```  
      
可用 `:set list` 查看文本  
      
### sed 处理  
```bash  
sed -rn '/^ *$/!s/\s{2,}$//p'  
```  
      
# 不能提交到远程仓库管理的文件  
windows 中为一个文件建立硬链接，然后将链接文件用 git 管理，git push 上传到远程仓库时失败  
    
# 克隆 github 仓库中部分目录到本地  
如 github 远程仓库地址为 https://github.com/lxwcd/linux.git，只想拷贝 linux 目录下的 notes/shell_scripts 目录到本地，可以使用以下命令：  
```bash  
git clone --depth 1 --filter=blob:none --no-checkout https://github.com/lxwcd/linux.git  
cd linux  
git checkout main -- notes/shell_scripts  
```  
  
克隆后不要直接提交到远程仓库  
  
# git 密码认证失败解决  
> [Support for password authentication was removed. Please use a personal access token instead.](https://dev.to/shafia/support-for-password-authentication-was-removed-please-use-a-personal-access-token-instead-4nbk)  
  
在虚拟机中用 git push 时输入用户名和密码，直接输入 github 账号密码会提示失败，要用 token，见上面文章描述方法。  
  
  
# git 退回之前的版本并提交到远程仓库  
从 github 克隆部分文件然后提交后，远程仓库最新的版本只剩下克隆的部分文件，本地退回到上一个版本后，再提交到远程仓库。  
  
查看最近的三个版本提交记录  
```bash  
git log -3   
git log -3 --oneline # 简化输出  
```  
```bash  
[root@lx-virtual-machine linux]$ git log -3 --oneline   
11ca27e (HEAD -> main, origin/main, origin/HEAD) add shell scripts  
8e041c9 update shell scripts  
4951326 update shell scripts  
```  
  
*******************  
如上面，要退回到 80=e041c9 的版本，执行以下命令：  
```bash  
git reset 8e041c9 # 这里模式 --soft --mixed --hard 根据实际需求选择  
```  
**`git reset --soft HEAD^`：**  
- `--soft` 选项表示软重置，只是移动 `HEAD` 指针到上一个提交，不会修改暂存区和工作目录。  
- 保留了在上一个提交中的所有更改，这些更改会保留在暂存区和工作目录中。  
- 这使得可以重新提交这些更改或者进行其他修改。  
  
**`git reset HEAD^`（或 `git reset HEAD^` 的简写）：**  
- 没有指定 `--soft` 或 `--hard`，默认是 `--mixed`，即混合重置。  
- 这会移动 `HEAD` 指针到上一个提交，并重置暂存区，但不会修改工作目录。  
- 保留了在上一个提交中的所有更改，但这些更改被放入暂存区中，你需要重新提交它们。  
  
**`git reset --hard HEAD^`：**  
- `--hard` 选项表示硬重置，会将 `HEAD` 指针、暂存区和工作目录都重置到上一个提交的状态。  
- 所有在上一个提交之后的更改都会被丢弃，工作目录会变为上一个提交的状态，慎用这个选项，因为它会永久删除未提交的更改。  
  
总的来说，`--soft` 保留了工作目录和暂存区的更改，`--mixed` 重置了暂存区但保留了工作目录的更改，而 `--hard` 会删除工作目录和暂存区的所有更改。  
  
*********************  
提交到远程仓库：  
```bash  
git push origin main --force  # brance name 通过 git branch --show-current 查看  
```  
