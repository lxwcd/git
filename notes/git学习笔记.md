git 学习  
      
# 学习资源  
> 初步了解 git：[廖雪峰 Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)  
> github 官方文档：[GitHub Docs](https://docs.github.com/en/get-started/quickstart/set-up-git)  
> git 命令官方文档：[git](https://git-scm.com/docs/)  
> git book：[Pro Git book](https://git-scm.com/book/en/v2)  
> [Learn Git Branching](https://learngitbranching.js.org/?locale=zh_CN) 
> [Git 教程 - Rebase](https://www.delftstack.com/zh/tutorial/git/git-rebase/) 
> [Learn Git and GitHub](https://roadmap.sh/git-github) 
      
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

## 修改时区
```bash
user.timezone=Asia/Shanghai
diff.date=+date: '%Y-%m-%d %H:%M:%S'
log.date=local
```

## 配置换行符
- **Unix/Linux/Mac** 使用 LF（Line Feed，`\n`）作为换行符。
- **Windows** 使用 CRLF（Carriage Return + Line Feed，`\r\n`）作为换行符。

由于这些差异，当开发者在不同操作系统之间协作时，可能会遇到换行符不一致的问题。Git 提供了 `core.autocrlf` 和 `core.safecrlf` 配置选项来帮助处理这些问题。

这些设置的主要目的是在不同操作系统之间协作时，确保文件的换行符保持一致，从而避免因换行符不一致导致的合并冲突和其他问题。

windows 上配置后有点问题，暂未使用。
### 对于 Unix/Mac 用户

1. **`git config --global core.autocrlf input`**：
   - 这个配置使得当文件从工作目录添加到索引（即暂存区）时，Git 会将 CRLF 转换为 LF。
   - 当文件从索引检出(checkout)到工作目录时，Git 不会进行任何转换。
   - 这样可以确保在 Unix/Mac 系统上，文件总是以 LF 结尾。

这种设置通常用于 Unix 和 Mac 系统，因为这些系统默认使用 LF 作为换行符。通过这种方式，可以确保在这些系统上工作的开发者不会因为换行符问题而遇到麻烦。

2. **`git config --global core.safecrlf true`**：
   - 这个配置选项启用了一个安全检查，以确保在转换过程中不会损坏文件。
   - 如果 Git 检测到转换可能会导致文件内容变化（例如，文件中包含混合的换行符），它会拒绝转换并报错。

### 对于 Windows 用户

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

# git bash 配置
## 配置主题字体
右键选择 option 进行配置，配置完成后保存即可

## vim 配置
输入 vim 后，输入 `:verion` 查看配置文件的路径，如：
```bash
  system vimrc file: "/etc/vimrc"
     user vimrc file: "$HOME/.vimrc"
 2nd user vimrc file: "~/.vim/vimrc"
 3rd user vimrc file: "~/.config/vim/vimrc"
      user exrc file: "$HOME/.exrc"
       defaults file: "$VIMRUNTIME/defaults.vim"
  fall-back for $VIM: "/etc"
 f-b for $VIMRUNTIME: "/usr/share/vim/vim91"
```

在 Git Bash 和其他类 Unix 环境中，`/etc/vimrc` 是 Vim 编辑器的系统级配置文件的传统路径。这个路径源自 Unix 和 Linux 系统，其中 `/etc` 是用于存储系统级配置文件的目录。然而，在 Windows 系统中，并没有 `/etc` 这样的目录，这是一个 Unix 和 Linux 特有的目录结构。

在 Git Bash 中，`/etc/vimrc` 的路径是一个模拟的路径，它映射到 Windows 系统中的一个实际位置。这样做是为了保持与 Unix 和 Linux 环境的兼容性，使得 Unix 和 Linux 用户能够在 Windows 上的 Git Bash 中使用他们熟悉的 Vim 配置。

最后两行的意思是：

1. **fall-back for $VIM: "/etc"**
   - 这行表示如果环境变量 `$VIM` 没有设置，Git Bash 会回退到 "/etc" 目录来查找 Vim 相关的配置和文件。这是一个备用方案，以防 `$VIM` 环境变量未定义。

2. **f-b for $VIMRUNTIME: "/usr/share/vim/vim91"**
   - `$VIMRUNTIME` 是另一个环境变量，它指向 Vim 的运行时文件，包括语法文件、脚本等。这行表示如果 `$VIMRUNTIME` 没有设置，Git Bash 会使用 "/usr/share/vim/vim91" 作为默认路径。这里的 "vim91" 可能指的是 Vim 的某个特定版本，例如 8.1 版本。

下载 [vimrc 文件](https://github.com/lxwcd/learnVim/blob/main/vimrc.local) 重命名到 `$HOME/.vimrc`，退出后重新进入即可生效。

修改配置文件的路径：
```bash
" 设置全局自定义配置文件的路径变量
let $MYVIMRC = "$HOME/.vimrc"
```

git bash 中用 ls 查看有 /etc/vimrc 文件，可以在最后加上一个自己的 vimrc 文件配置：
```bash
" Source a global configuration file if available
if filereadable("$HOME/.vimrc")
  source $HOME/.vimrc
endif
```

## 设置别名
希望全局配置，可以在 `/etc/profile.d/aliases.sh` 中添加。
针对当前用户配置，在 `$HOME/.bashrc` 中添加。

```bash
export TZ='Asia/Shanghai'
alias stashsimulator='git diff --name-only | grep -E "\.(suo|bin)$" | xargs git stash push -m ".suo and .bin files" '
alias restoresimulator='git status --porcelain | cut -d" " -f3- |  grep -E "\.(suo|bin)$" | xargs git restore -- '
alias addCppAndHFiles='git diff --name-only | grep -E "\.(cpp|h)$" | xargs git add -- '
alias checkSkipWorktree=' git ls-files -v | grep "^S"'
```

### 修改 vim 中光标样式
```bash
" modify cursor style
if &term =~ "xterm\\|rxvt"
  " 设置插入模式下的光标样式为竖线
  let &t_SI .= "\<Esc>[5 q"  " SI = INSERT mode
  " 设置替换模式下的光标样式为竖线
  let &t_SR .= "\<Esc>[5 q"  " SR = REPLACE mode
  " 设置普通模式下的光标样式为块状
  let &t_EI .= "\<Esc>[2 q"  " EI = NORMAL mode (ELSE)
endif
```
### 复制到系统剪贴板
选中后使用 `"+ y` 复制内容，即复制到系统剪贴板。
```bash
set clipboard=unnamedplus
```
`set clipboard=unnamedplus` 是 Vim 中的一个配置选项，用于指定 Vim 如何与系统剪贴板交互。下面是这个配置选项的详细解释：

1. **`clipboard` 选项**：
   - Vim 的 `clipboard` 选项控制 Vim 如何使用系统剪贴板。通过设置这个选项，你可以让 Vim 的复制（yank）和粘贴（paste）操作直接与系统剪贴板进行交互。

2. **`unnamedplus` 的含义**：
   - `unnamedplus` 是 `clipboard` 选项的一个值，它告诉 Vim 使用系统剪贴板作为复制和粘贴操作的存储。在 Vim 中，`"+` 寄存器通常与系统剪贴板相关联，而 `unnamedplus` 使得这个寄存器的行为与系统剪贴板一致。

3. **如何工作**：
   - 当你设置了 `set clipboard=unnamedplus`，Vim 会将复制（yank）操作的内容存储到 `"+` 寄存器，这个寄存器与系统剪贴板同步。因此，当你在 Vim 中复制文本时，它也会出现在系统剪贴板上，你可以在其他程序中粘贴。
   - 同样地，从系统剪贴板粘贴（paste）文本到 Vim 中时，Vim 会从 `"+` 寄存器读取内容。

4. **在 Linux 中的配置**：
   - 这个配置同样适用于 Linux 系统。在 Linux 系统中，`"+` 寄存器可能与 X11 的 CLIPBOARD 选区相关联，这取决于你的桌面环境和配置。在大多数现代 Linux 发行版中，`"+` 寄存器用于系统剪贴板操作。

5. **检查 Vim 是否支持剪贴板**：
   - 可以使用 `vim --version | grep clipboard` 命令来检查你的 Vim 是否支持剪贴板功能。如果输出中包含 `+clipboard`，则表示支持。

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

# 快速前进（fast-forward）和非快速前进
- **快速前进（fast-forward）**：当你的本地分支落后于远程分支时，Git 可以安全地将本地分支的指针向前移动到远程分支的最新提交，这称为快速前进。这种情况下，没有新的合并提交产生，因为历史是线性的。
- **非快速前进**：如果远程分支有新的提交分叉，你的本地分支不是远程分支的直接祖先，那么 Git 无法通过快速前进来更新本地分支。这时，Git 需要创建一个新的合并提交，将两个分支的历史合并在一起。

# Refs（引用）
在 Git 中，`refs` 是指向提交对象（commit objects）的指针。它们存储在 `.git/refs` 目录下，分为几个部分：

1. **HEAD**：指向当前分支的最新提交。
2. **branches**：本地分支引用，例如 `refs/heads/master`。
3. **remotes**：远程分支引用，例如 `refs/remotes/origin/master`。
4. **tags**：标签引用，例如 `refs/tags/v1.0`。

# Refspec（引用规范）
> [Git - The Refspec](https://git-scm.com/book/en/v2/Git-Internals-The-Refspec) 

`refspec` 是一个字符串，用于定义如何将远程仓库的引用（refs）映射到本地仓库的引用。它通常用于 `git fetch` 和 `git push` 命令中，以指定要操作的远程引用和本地引用。

一个 `refspec` 的一般格式如下：
```
<src>:<dst>
```

- **<src>**：源引用，可以是分支名、标签名或使用通配符的引用模式。
- **<dst>**：目标引用，是远程引用映射到本地引用的路径。

`refspec` 的强大之处在于它允许你精确控制 Git 引用的同步和映射，这对于管理复杂的分支结构和远程仓库非常有用。

假设有一个远程仓库 `origin`，其 URL 为 `https://github.com/user/repo.git`，并且你想要管理远程分支和本地分支的映射。

## **简单的 refspec**
如果你想要将远程的 `master` 分支拉取到本地的 `master` 分支，你可以使用以下 `refspec`：
```bash
git fetch origin master:refs/heads/master
```
这里，`master` 是源引用（远程的 `master` 分支），`refs/heads/master` 是目标引用（本地的 `master` 分支）。

## **使用通配符的 refspec**
如果你想要拉取远程仓库的所有分支到本地，可以使用通配符 `*`：
```bash
git fetch origin '*:refs/heads/*'
```
这里，`*` 匹配远程仓库的所有引用，`refs/heads/*` 指定所有匹配的远程引用都应该映射到本地的 `refs/heads/` 下。

## **推送标签**
如果你想要推送本地的所有标签到远程仓库，可以使用以下 `refspec`：
```bash
git push origin 'refs/tags/*:refs/tags/*'
```
这里，`refs/tags/*` 匹配本地的所有标签，并且将它们推送到远程仓库的 `refs/tags/` 下。

## **删除远程引用**
`refspec` 也可以用于删除远程引用。例如，要删除远程的 `feature` 分支，可以使用以下命令：
```bash
git push origin ':refs/heads/feature'
```
注意，这里 `<src>` 只有一个冒号 `:`，这意味着没有源引用，只有目标引用，这将导致远程的 `feature` 分支被删除。

## `+` 的用途
> $ git fetch origin +seen:seen maint:tmp
> This updates (or creates, as necessary) branches seen and tmp in the local repository by fetching from the branches (respectively) seen and maint from the remote repository.
> The seen branch will be updated even if it does not fast-forward, because it is prefixed with a plus sign; tmp will not be.

在 refspec 中，`+` 符号用于强制更新本地分支以匹配远程分支的状态，即使这个更新不是快速前进。具体来说：
- **带有 `+` 的 refspec**：`+seen:seen` 表示强制更新本地的 `seen` 分支以匹配远程的 `seen` 分支，即使这个更新需要创建一个新的合并提交。
- **不带 `+` 的 refspec**：`maint:tmp` 表示更新本地的 `tmp` 分支以匹配远程的 `maint` 分支，但如果这个更新不是快速前进，Git 将拒绝这个操作，以避免覆盖本地的提交历史。

假设你有两个分支：本地的 `seen` 和远程的 `origin/seen`。

1. **不带 `+` 的情况**：
   - 你执行 `git fetch origin seen:seen`。
   - 如果远程的 `origin/seen` 分支有新的提交，并且这些提交可以被快速前进，那么本地的 `seen` 分支将被更新。
   - 如果远程的 `origin/seen` 分支有新的提交分叉，Git 将拒绝更新本地的 `seen` 分支，以保护你的本地提交历史。

2. **带 `+` 的情况**：
   - 你执行 `git fetch origin +seen:seen`。
   - 不管远程的 `origin/seen` 分支的更新是否可以被快速前进，本地的 `seen` 分支都将被强制更新以匹配远程分支的状态。
   - 如果远程分支有新的提交分叉，Git 将创建一个新的合并提交，将这些更改合并到本地分支。

**结论**: 
`+` 符号的用途是强制更新本地分支，即使这个更新涉及到非快速前进的合并。这可以确保本地分支始终与远程分支保持一致，但也可能会覆盖本地的提交历史，因此在没有 `+` 的情况下，Git 会拒绝这种操作以保护本地数据。

# 裸仓库
裸仓库是一个没有工作目录（working directory）的 Git 仓库。在普通的 Git 仓库中，你有一个 `.git` 目录，它包含了所有的版本控制信息，以及一个工作目录，这是你实际编写代码的地方。而在裸仓库中，没有工作目录，只有 `.git` 目录。这意味着你不能直接在裸仓库中进行提交（commit）或其他修改，它主要用于以下用途：

1. **作为远程仓库**：裸仓库通常用作远程仓库，因为它不包含工作目录，所以不会有任何未提交的更改。这样可以确保所有通过 `git push` 和 `git fetch` 操作推送和拉取的更改都是干净和一致的。

2. **备份**：裸仓库可以作为其他仓库的备份，因为它包含了完整的历史记录和所有分支。

3. **Git 服务**：裸仓库可以作为 Git 服务运行，比如 Git 服务器或 CI/CD 系统，它们需要处理多个项目的推送和拉取操作。

## `git clone --mirror` 命令

当使用 `git clone --mirror` 克隆一个仓库时，你实际上是在创建一个裸仓库。这个命令会复制所有的引用（refs），包括分支、标签和远程引用，并且设置特殊的 refspec，使得所有这些引用在目标仓库中都会被覆盖。这意味着任何推送到这个镜像仓库的更改都会反映到所有相关的引用上。

具体来说，`git clone --mirror` 命令做了以下几件事情：

1. **克隆所有引用**：克隆远程仓库的所有分支和标签。

2. **设置 refspec**：设置一个 refspec，这是一个规则，定义了如何从远程仓库同步引用。对于镜像仓库，这个 refspec 通常设置为 `+refs/*:refs/*`，意味着所有远程的引用都会被推送到本地。

3. **创建裸仓库**：创建的仓库没有工作目录，只有 `.git` 目录。

## 示例

```bash
git clone --mirror https://github.com/user/repo.git
```

这个命令会创建一个名为 `repo.git` 的裸仓库，其中包含了 `https://github.com/user/repo.git` 仓库的所有引用。你可以使用这个裸仓库来推送更新到远程服务器，或者作为其他仓库的备份。

# 子模块
> [Git - git-submodule Documentation](https://git-scm.com/docs/git-submodule) 

Git 子模块（Submodule）是一种将一个 Git 仓库嵌入到另一个 Git 仓库中的方法。这使得你可以将一个项目（子模块）作为另一个项目的依赖项，并保持两者的独立性。以下是子模块的一些基本概念和操作步骤，以及一个实际的例子。

- **依赖管理**：子模块常用于管理项目依赖。例如，一个大型项目可能依赖于几个库或工具，这些库或工具可以作为子模块被包含在项目中。

- **独立性**：子模块有自己的提交历史和分支结构，它们在父项目中是独立的，可以单独更新。

- **同步更新**：你可以在父项目中更新子模块到新的提交或分支，而不影响子模块自己的历史。

## 子模块的操作

1. **添加子模块**：
   使用 `git submodule add` 命令将远程仓库添加为子模块。
   ```bash
   git submodule add <repository-url> <path>
   ```
   例如，将一个名为 `lib` 的远程仓库添加为子模块：
   ```bash
   git submodule add https://github.com/user/lib.git lib
   ```

2. **克隆包含子模块的仓库**：
   克隆时使用 `--recurse-submodules` 参数来初始化并克隆子模块。
   ```bash
   git clone --recurse-submodules https://github.com/user/repo.git
   ```

3. **更新子模块**：
   使用 `git submodule update` 命令来更新子模块到最新提交。
   ```bash
   git submodule update --init --recursive
   ```

4. **同步子模块**：
   如果你在父项目中做了一些关于子模块的更改（比如更新了子模块的引用），你需要使用 `git submodule sync` 来同步这些更改。
   ```bash
   git submodule sync
   ```

5. **检出特定提交**：
   你可以检出子模块的特定提交。
   ```bash
   git checkout -b <branch-name>
   cd <path-to-submodule>
   git checkout <commit-hash>
   cd ..
   ```

## 示例

假设有一个名为 `MyProject` 的项目，它依赖于一个名为 `CommonLib` 的库。你可以将 `CommonLib` 作为子模块添加到 `MyProject` 中。

1. **初始化 MyProject 仓库**：
   ```bash
   git init MyProject
   cd MyProject
   ```

2. **添加 CommonLib 作为子模块**：
   ```bash
   git submodule add https://github.com/user/CommonLib.git lib
   ```
   这会在 `MyProject` 中创建一个 `lib` 目录，并将 `CommonLib` 仓库克隆到这个目录中。

3. **提交子模块引用**：
   ```bash
   git commit -m "Add CommonLib as a submodule"
   ```

4. **克隆 MyProject 并递归子模块**：
   ```bash
   git clone --recurse-submodules https://github.com/user/MyProject.git
   cd MyProject
   ```

5. **更新子模块**：
   如果 `CommonLib` 有更新，你可以更新子模块：
   ```bash
   git submodule update --init --recursive
   ```

6. **同步子模块引用**：
   如果你更改了子模块的远程 URL 或其他设置，你需要同步这些更改：
   ```bash
   git submodule sync
   ```

通过使用子模块，你可以保持项目的清晰结构，同时管理复杂的依赖关系。子模块提供了一种灵活的方式来集成外部代码，同时保持项目的独立性和可维护性。

# git clone
> [Git - git-clone Documentation](https://git-scm.com/docs/git-clone)   

## **克隆默认分支**
   ```bash
   git clone https://github.com/user/repo.git
   ```
   这将克隆 `user/repo` 仓库的默认分支（通常是 `master` 或 `main`）到本地目录 `repo`。

## **克隆特定分支**
   ```bash
   git clone -b develop https://github.com/user/repo.git
   ```
   这将克隆 `user/repo` 仓库的 `develop` 分支。

## **克隆不包含标签**
   ```bash
   git clone --no-tags https://github.com/user/repo.git
   ```
   这将克隆仓库，但不包括任何标签。

## **浅克隆**
   ```bash
   git clone --depth 1 https://github.com/user/repo.git
   ```
   这将创建一个浅克隆，只包含最新的提交（即最近一次提交的历史）。

## **克隆并指定分支名称**
   ```bash
   git clone --branch new-branch --single-branch https://github.com/user/repo.git
   ```
   这将克隆 `user/repo` 仓库，并检查出 `new-branch` 分支。
   `git clone --branch new-branch --single-branch https://github.com/user/repo.git` 这个命令包含了两个参数：`--branch` 和 `--single-branch`。

1. **--branch <name>**：
   这个参数后面跟的是你想要克隆的分支名称。在这个例子中，`<name>` 被替换成了 `new-branch`，意味着你想要克隆远程仓库中名为 `new-branch` 的分支。

2. **--single-branch**：
   这个参数告诉 Git 你只想要克隆一个分支，而不是整个仓库的所有分支。当你使用 `--branch` 参数指定了一个分支后，`--single-branch` 会确保 Git 只克隆那个特定的分支，而不是克隆整个仓库的所有分支。

这个命令特别有用在你只对远程仓库中的某个特定分支感兴趣，而不需要整个仓库的所有分支和标签时。这样可以减少克隆操作所需的时间和带宽，因为你只获取了你感兴趣的那部分代码。

## **克隆并初始化所有子模块**
   ```bash
   git clone --recurse-submodules https://github.com/user/repo.git
   ```
   这将克隆仓库以及所有子模块。
   `git clone --recurse-submodules https://github.com/user/repo.git` 这个命令用于克隆一个包含子模块的 Git 仓库，并且初始化并克隆所有的子模块。

1. **git clone**：
   这是 Git 的克隆命令，用于从一个远程仓库复制代码到本地。

2. **--recurse-submodules**：
   这个参数告诉 Git，在克隆主仓库的同时，也递归地克隆所有子模块（submodule）。子模块是指在 Git 仓库中包含的另一个 Git 仓库，它们可以有自己的提交历史和分支。

3. **https://github.com/user/repo.git**：
   这是远程仓库的 URL。在这个例子中，`user` 是仓库所有者的 GitHub 用户名，`repo` 是仓库的名称。`.git` 表示这是一个 Git 仓库。

当你执行这个命令时，Git 会做以下几件事情：

- 克隆指定的远程仓库到本地。
- 检查仓库中的 `.gitmodules` 文件，这个文件列出了所有子模块的路径和对应的远程仓库 URL。
- 递归地克隆每个子模块到对应的路径。
- 初始化子模块的 Git 仓库，并设置为相应的远程仓库。

这个命令特别有用在你想要克隆一个复杂的项目时，这个项目包含了多个依赖的子项目（子模块）。使用 `--recurse-submodules` 参数可以确保你不仅克隆了主项目，还克隆了所有需要的子模块，这样可以保证项目的完整性和可构建性。

## **创建裸仓库**
   ```bash
   git clone --mirror https://github.com/user/repo.git
   ```
   这将创建一个裸仓库，即没有工作目录的仓库，通常用于作为其他仓库的镜像。

## **使用模板克隆**
   ```bash
   git clone --template=/path/to/template https://github.com/user/repo.git
   ```
   这将使用指定的模板目录来初始化新仓库。

## **设置配置变量**
   ```bash
   git clone --config user.name="Your Name" https://github.com/user/repo.git
   ```
   这将在克隆时设置仓库的用户名称。

## **不检出 HEAD**
    ```bash
    git clone --no-checkout https://github.com/user/repo.git
    ```
这将克隆仓库，但不会检出 HEAD 对应的工作目录。
`git clone --no-checkout` 是一个 Git 命令的选项，它用于克隆远程仓库但不检出代码。

`git clone --no-checkout <repository-url>` 命令会从 `<repository-url>` 指定的远程仓库克隆一个空目录，其中包含远程仓库的所有分支和标签的引用，但不包含任何工作目录中的文件。

- `--no-checkout`：这个选项告诉 Git 在克隆过程中不要检出 HEAD 或任何其他分支的最新提交。这意味着在克隆完成后，你将得到一个空的工作目录。

### 使用场景

1. **节省带宽和时间**：如果你只对仓库的元数据（如分支、标签）感兴趣，或者你想要离线工作而不需要立即检出代码，使用 `--no-checkout` 可以节省下载代码的带宽和时间。

2. **初始化裸仓库**：创建裸仓库（bare repository）时，通常不需要工作目录，因此可以使用 `--no-checkout` 选项来克隆。

3. **脚本和自动化**：在自动化脚本中，你可能需要克隆仓库并执行一些 Git 操作，但不需要实际的代码文件。

### 注意事项

- 克隆完成后，你可以使用 `git checkout` 命令来检出特定的分支或提交。
- 如果你需要检出特定的分支，可以在克隆后执行 `git checkout <branch-name>`。
- 如果你想要检出远程分支的最新提交，可以先执行 `git fetch`，然后使用 `git checkout -b <branch-name> origin/<branch-name>`。
- 使用 `--no-checkout` 克隆的仓库将不会包含任何文件，直到你显式地检出分支或提交。

## **稀疏检出**
    ```bash
    git clone --sparse https://github.com/user/repo.git
    ```
    这将使用稀疏检出克隆仓库，只检出顶级目录中的文件。

## **部分克隆**
    ```bash
    git clone --filter=blob:none https://github.com/user/repo.git
    ```
    这将创建一个不包含任何二进制文件的克隆。

这些示例展示了如何根据不同的需求使用 `git clone` 命令的参数。在实际使用中，你可以根据需要组合这些参数来实现更复杂的克隆操作。

## 克隆仓库到新目录  
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

## 克隆本地仓库
```bash
git clone /path/to/source/repo /path/to/new/repo
```

这条命令会将 `/path/to/source/repo` 仓库的内容克隆到 `/path/to/new/repo` 目录中。

- **`git clone <source> <destination>`**：
  - `<source>`：源仓库的路径。
  - `<destination>`：目标仓库的路径。如果目标路径已经存在，Git 会报错。如果目标路径不存在，Git 会自动创建该目录。

### **浅克隆只包含最新的提交**
这条命令会创建一个只包含最新提交的浅克隆，不包含完整的提交历史。

```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents
$ git clone --depth=1 file:///d/Documents/git_test /d/Documents/git_test_03
Cloning into 'D:/Documents/git_test_03'...
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 5 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (5/5), done.
```
本地克隆默认使用文件系统路径，而不是通过网络协议（如 http 或 git）进行克隆。

## **file 协议克隆**
在 Git 中，`file` 协议用于通过本地文件系统路径克隆或访问仓库。`file` 协议的使用方式与通过网络协议（如 `http`、`https`、`git`）克隆仓库类似，但它专门用于本地文件系统。下面详细讲解 `file` 协议的使用方法和注意事项。

```bash
file:///path/to/repo
```
- **`file://`**：这是协议前缀，表示使用文件系统路径。
- **`/`**：在 Unix-like 系统中，路径从根目录开始，因此使用三个斜杠 `///`。
- **`/path/to/repo`**：这是仓库的路径。

### **克隆本地仓库**
```bash
git clone file:///d/Documents/git_test /d/Documents/git_test_03
```
- 源路径：`file:///d/Documents/git_test`，表示 `D:/Documents/git_test` 仓库。
- 目标路径：`/d/Documents/git_test_03`，表示克隆到 `D:/Documents/git_test_03` 目录。

### **添加本地远程仓库**
```bash
git remote add local-origin file:///d/Documents/git_test
```
- 将 `D:/Documents/git_test` 仓库添加为远程仓库，别名为 `local-origin`。

### 注意事项
`file://` 协议不支持相对路径。如果需要使用相对路径，可以直接使用本地文件系统路径。
```bash
git clone /d/Documents/git_test /d/Documents/git_test_03
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

## 参数详解

1. **-s, --short**
   - 显示简短的状态信息，不显示文件的具体更改内容。
   ```bash
   git status -s
   ```

2. **-b, --branch**
   - 显示当前分支的信息以及与上游分支的差异。
   ```bash
   git status -b
   ```

3. **-u, --untracked-files[=<mode>]**
   - 显示未跟踪的文件。`<mode>` 可以是 `no`, `normal`, 或 `all`。
     - `no`：不显示未跟踪的文件。
     - `normal`：显示未跟踪的文件，但排除那些在 `.gitignore` 中指定的文件。
     - `all`：显示所有未跟踪的文件，包括那些在 `.gitignore` 中指定的文件。
   ```bash
   git status -u
   git status -uno
   git status -uall
   ```

4. **--ignored**
   - 只显示被 `.gitignore` 忽略的文件。
   ```bash
   git status --ignored
   ```

5. **--porcelain**
   - 机器可读格式输出，便于脚本处理。
   ```bash
   git status --porcelain
   ```

6. **-z, --null**
   - 分隔输出字段，字段之间用 `\0` 分隔，用于脚本处理。
   ```bash
   git status -z
   ```

7. **---ahead-behind**
   - 显示当前分支与上游分支的领先或落后的提交数。
   ```bash
   git status --ahead-behind
   ```

8. **--branch --ahead-behind**
   - 显示当前分支与上游分支的详细领先或落后信息。
   ```bash
   git status --branch --ahead-behind
   ```

9. **--untracked-files=no**
   - 不显示未跟踪的文件。
   ```bash
   git status --untracked-files=no
   ```

10. **--ignore-submodules**
    - 忽略子模块的变化。
    ```bash
    git status --ignore-submodules
    ```

假设你有一个名为 `project` 的 Git 仓库，并且你进行了以下操作：

1. 修改了 `file1.txt` 并且已经暂存。
2. 修改了 `file2.txt` 但还没有暂存。
3. 添加了 `file3.txt` 但还没有暂存。

```bash
# 显示完整的仓库状态
git status

# 显示简短的状态信息
git status -s

# 显示未跟踪的文件
git status -u

# 显示被 .gitignore 忽略的文件
echo "file3.txt" >> .gitignore
git status --ignored

# 显示机器可读格式的输出
git status --porcelain

# 使用 \0 分隔输出字段
git status -z
```

## 注意事项

- **查看详细信息**：如果你想查看更详细的信息，可以使用 `git status --verbose` 或 `git status -vv`。
- **忽略文件**：`git status` 会显示未跟踪的文件，但你可以通过 `.gitignore` 文件指定要忽略的文件模式。
- **分支同步**：`git status` 显示的分支同步状态基于远程分支的最新已知状态，可能需要 `git fetch` 来更新。

# Ignoring files
> [Learn Git and GitHub](https://roadmap.sh/git-github) 
> [Git - gitignore Documentation](https://git-scm.com/docs/gitignore) 
> [GitHub - github/gitignore: A collection of useful .gitignore templates](https://github.com/github/gitignore) 
> [.gitignore file - ignoring files in Git | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/saving-changes/gitignore) 

`.gitignore` 是一个在 Git 仓库中使用的特殊文件，用于指定 Git 应该忽略的文件和目录。这个文件帮助你防止不小心提交不需要版本控制的文件，比如编译产物、日志文件、个人配置文件等。

不影响已被跟踪的文件。

可以写到多个位置，如果忽略文件只针对本地仓库，将忽略的文件放到 `$GIT_DIR/info/exclude` 中，即仓库根目录的 `.git` 目录中。

## 作用

- **指定忽略规则**：`.gitignore` 文件包含一系列的模式（pattern），用于匹配文件和目录路径。Git 会根据这些模式决定哪些文件不需要版本控制。
- **保持仓库清洁**：通过忽略不必要的文件，`.gitignore` 帮助保持仓库的清洁和组织。

## 文件位置

- **项目根目录**：通常，`.gitignore` 文件位于 Git 仓库的根目录。
- **多个 `.gitignore` 文件**：可以在子目录中创建 `.gitignore` 文件，这些文件会影响其所在目录及其子目录。

## 本地仓库忽略
放在下面文件中
```bash
.git/info/excluede
```

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

## 将已跟踪的文件加入 .gitignore

# git merge-base 查找分支的共同祖先
> [Git - git-merge-base Documentation](https://git-scm.com/docs/git-merge-base) 

## 两个分支的共同祖先
Given two commits A and B, git merge-base A B will output a commit which is reachable from both A and B through the parent relationship.

For example, with this topology:

	 o---o---o---B
	/
---o---1---o---o---o---A
the merge base between A and B is 1.

## 多个分支的共同祖先
Given three commits A, B, and C, git merge-base A B C will compute the merge base between A and a hypothetical commit M, which is a merge between B and C. For example, with this topology:

       o---o---o---o---C
      /
     /   o---o---o---B
    /   /
---2---1---o---o---o---A
the result of git merge-base A B C is 1. This is because the equivalent topology with a merge commit M between B and C is:

       o---o---o---o---o
      /                 \
     /   o---o---o---o---M
    /   /
---2---1---o---o---o---A
and the result of git merge-base A M is 1. Commit 2 is also a common ancestor between A and M, but 1 is a better common ancestor, because 2 is an ancestor of 1. Hence, 2 is not a merge base.

The result of git merge-base --octopus A B C is 2, because 2 is the best common ancestor of all commits.

# git diff 查看文件差异
> [Git - git-diff Documentation](https://git-scm.com/docs/git-diff)   
> [git diff - Comparing Changes in Git | Refine](https://refine.dev/blog/git-diff-command/#basic-example) 

`git diff` 是 Git 中用于显示文件差异的命令。它可以帮助你查看自上次提交以来文件发生了哪些更改，或者比较不同分支、标签或提交之间的差异。

1. **显示未暂存的更改**：`git diff` 默认显示自上次提交以来未暂存的更改。
2. **比较暂存区与提交**：可以查看已暂存的更改与上次提交的差异。
3. **比较不同提交**：可以比较任意两个提交之间的差异。
4. **比较分支**：可以比较不同分支或标签之间的差异。

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

## **比较工作区和暂存区的差异**
> [Git - git-diff Documentation](https://git-scm.com/docs/git-diff#Documentation/git-diff.txt-codegitdiffcode) 
> [git diff - Comparing Changes in Git | Refine](https://refine.dev/blog/git-diff-command/#basic-example) 

```bash
git diff
```
这个命令显示自上次提交以来未暂存的更改。
不包括没有被跟踪的文件。
如果文件已暂存，不会查看到。

```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ git diff
warning: in the working copy of 'test01.txt', LF will be replaced by CRLF the next time Git touches it
diff --git a/test01.txt b/test01.txt
index cd7fb11..a821b44 100644
--- a/test01.txt
+++ b/test01.txt
@@ -4,3 +4,4 @@ local modify test01.txt
 A
 b
 C
+001
```
上面 a 表示最新提交的版本，即旧的版本，b 表示当前工作目录的版本，即新的版本。
`100` 表示文件类型为普通文件，`644` 表示文件权限，可以通过 `ll` 查看：
```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ ll test01.txt
-rw-r--r-- 1 lx 197121 56 12月 21 22:10 test01.txt
```

## **比较已暂存的文件和最新提交的差异**
```bash
git diff --cached
```
或者
```bash
git diff --staged
```
这些命令显示已暂存的更改与上次提交的差异。
不会查看到没有暂存的文件差异。

将工作目录的修改 add 到暂存区后，查看：
```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ git status
On branch fix_B
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   test01.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test05.txt


lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ git diff

lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ git diff --cached
diff --git a/test01.txt b/test01.txt
index cd7fb11..a821b44 100644
--- a/test01.txt
+++ b/test01.txt
@@ -4,3 +4,4 @@ local modify test01.txt
 A
 b
 C
+001
```
a 表示最新的提交版本，旧的版本； b 表示暂存区的版本，新的版本。

## **比较工作区和最新提交的差异**
```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ git diff HEAD
warning: in the working copy of 'test02.txt', LF will be replaced by CRLF the next time Git touches it
diff --git a/test01.txt b/test01.txt
index cd7fb11..a821b44 100644
--- a/test01.txt
+++ b/test01.txt
@@ -4,3 +4,4 @@ local modify test01.txt
 A
 b
 C
+001
diff --git a/test02.txt b/test02.txt
index 8de02e1..98bbcac 100644
--- a/test02.txt
+++ b/test02.txt
@@ -1,2 +1,3 @@
 test02
-local git rebase
\ No newline at end of file
+local git rebase002
+002
```

工作区中跟踪的文件，已暂存和未暂存的文件和最新提交的差异都能看到。
a 表示最新的提交版本，旧的版本； b 表示工作目录的版本，新的版本。
`+001` 表示 a 中不存在， b 中新增的内容。

## **比较当前工作目录中特定文件和暂存区的差异**
```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ git diff HEAD -- test01.txt
diff --git a/test01.txt b/test01.txt
index cd7fb11..a821b44 100644
--- a/test01.txt
+++ b/test01.txt
@@ -4,3 +4,4 @@ local modify test01.txt
 A
 b
 C
+001
```

指定当前工作目录，即 b 版本的 test01.txt 文件和 HEAD 的差异。

## **比较当前工作目录和任意提交的差异** 
```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ git diff 332de10
warning: in the working copy of 'test02.txt', LF will be replaced by CRLF the next time Git touches it
diff --git a/test01.txt b/test01.txt
index 4c19859..a821b44 100644
--- a/test01.txt
+++ b/test01.txt
@@ -1 +1,7 @@
 test01
+git pull
+local modify test01.txt
+A
+b
+C
+001
diff --git a/test02.txt b/test02.txt
index 4c19859..98bbcac 100644
--- a/test02.txt
+++ b/test02.txt
@@ -1 +1,3 @@
-test01
+test02
+local git rebase002
+002
diff --git a/test03.txt b/test03.txt
new file mode 100644
index 0000000..23bc844
--- /dev/null
+++ b/test03.txt
@@ -0,0 +1 @@
+test03
```
a 为指定的提交版本，b 为当前工作目录，包括为暂存的修改，不包括未跟踪的文件。

## **比较当前已暂存和任意提交的差异** 
```bash
$ git diff 332de10 --cached
diff --git a/test01.txt b/test01.txt
index 4c19859..a821b44 100644
--- a/test01.txt
+++ b/test01.txt
@@ -1 +1,7 @@
 test01
+git pull
+local modify test01.txt
+A
+b
+C
+001
diff --git a/test02.txt b/test02.txt
index 4c19859..8de02e1 100644
--- a/test02.txt
+++ b/test02.txt
@@ -1 +1,2 @@
-test01
+test02
+local git rebase
\ No newline at end of file
diff --git a/test03.txt b/test03.txt
new file mode 100644
index 0000000..23bc844
--- /dev/null
+++ b/test03.txt
@@ -0,0 +1 @@
+test03
```
a 为指定的提交版本，b 为当前工作目录已暂存的文件修改，不包括为暂存的修改，不包括未跟踪的文件。

## **比较两个提交**
```bash
git diff <commit1> <commit2>
```
这个命令比较两个提交之间的差异。顺序不同则结果不同。

```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ git diff 332de10 HEAD
diff --git a/test01.txt b/test01.txt
index 4c19859..cd7fb11 100644
--- a/test01.txt
+++ b/test01.txt
@@ -1 +1,6 @@
 test01
+git pull
+local modify test01.txt
+A
+b
+C
diff --git a/test02.txt b/test02.txt
index 4c19859..8de02e1 100644
--- a/test02.txt
+++ b/test02.txt
@@ -1 +1,2 @@
-test01
+test02
+local git rebase
\ No newline at end of file
diff --git a/test03.txt b/test03.txt
new file mode 100644
index 0000000..23bc844
--- /dev/null
+++ b/test03.txt
@@ -0,0 +1 @@
+test03
```
a 为 332de10 提交版本，b 为当前分支最新提交。

如果调换顺序：
```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ git diff HEAD 332de10
diff --git a/test01.txt b/test01.txt
index cd7fb11..4c19859 100644
--- a/test01.txt
+++ b/test01.txt
@@ -1,6 +1 @@
 test01
-git pull
-local modify test01.txt
-A
-b
-C
diff --git a/test02.txt b/test02.txt
index 8de02e1..4c19859 100644
--- a/test02.txt
+++ b/test02.txt
@@ -1,2 +1 @@
-test02
-local git rebase
\ No newline at end of file
+test01
diff --git a/test03.txt b/test03.txt
deleted file mode 100644
index 23bc844..0000000
--- a/test03.txt
+++ /dev/null
@@ -1 +0,0 @@
-test03
```
b 为 332de10 提交版本，a 为当前分支最新提交。
则相当于 332de10 相对于 HEAD 的变化，因此 HEAD 中增加的内容前面为 -，表示需要减去这些内容才能和 a 的版本一致。

## **比较当前最新提交和上一次提交的差异**
```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ git diff HEAD^ HEAD
diff --git a/test01.txt b/test01.txt
index 5c232c3..cd7fb11 100644
--- a/test01.txt
+++ b/test01.txt
@@ -2,5 +2,5 @@ test01
 git pull
 local modify test01.txt
 A
-B
+b
 C
```
a 为 HEAD^ 上一次提交版本，b 为 HEAD 最新提交版本。

## **比较两个分支最新提交的差异**
> [git diff - Comparing Changes in Git | Refine](https://refine.dev/blog/git-diff-command/#git-diff-between-two-branches-two-dots-method) 

```bash
git diff <branch1> <branch2>
```
或者等价于：
```bash
git diff <branch1>..<branch2>
```
这个顺序则 a 为 branch1 版本，b 为 branch2。 
查看的是两个分支的最新提交的差异。

如果调换顺序，则 a 和 b 的版本也调换：
```bash
git diff <branch2> <branch1>
```
这个顺序则 a 为 branch2 版本，b 为 branch1。

## **比较一个分支相对于另一个分支的差异**
> [git diff - Comparing Changes in Git | Refine](https://refine.dev/blog/git-diff-command/#git-diff-between-two-branches-three-dots-method) 

```bash
git diff <branch1>...<branch2>
```
这个命令显示从 `branch1` 和 `branch2` 的共同祖先到 `branch2` 的所有差异。
即从两个分支开始分叉后，branch2 上所有的提交内容相对共同祖先的差异。
查看差异中 a 为两个分支共同的祖先，b 为 branch2 最新提交。

注意和 ```git diff <branch1>..<branch2>``` 的区别，两个点号表示两个分支最新提交的差异。

## **查看差异的文件名**
```bash
$ git diff --name-only
```

## **比较工作目录和 stash 中特定文件差别**
```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (main)
$ echo "000 modify after stash test01" >> test01.txt

lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (main)
$ git diff stash@{0} -- test01.txt
warning: in the working copy of 'test01.txt', LF will be replaced by CRLF the next time Git touches it
diff --git a/test01.txt b/test01.txt
index d494af0..86e607d 100644
--- a/test01.txt
+++ b/test01.txt
@@ -4,4 +4,4 @@ local modify test01.txt
 A
 B
 add main test01.txt
-stash test01.txt
+000 modify after stash test01
```

a 为 stash@{0} 的版本，b 为当前工作目录`。
`-` 那行表示 a 中的版本存在，b 不存在，需要 - 去改行才能将 a 版本变成 b 版本。
`+` 那行则是 a 中不存在，需要加上才能变成 b 版本。

## **比较暂存区和 stash 中特定文件差别**
```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (main)
$ git diff stash@{0} --cached -- test01.txt
diff --git a/test01.txt b/test01.txt
index d494af0..9d86808 100644
--- a/test01.txt
+++ b/test01.txt
@@ -4,4 +4,3 @@ local modify test01.txt
 A
 B
 add main test01.txt
-stash test01.txt
```
a 为 stash@{0}，b 为暂存区。

## **查看当前最新提交和 stash 的差异**
`git diff stash@{0} HEAD`

## **查看两个分支某个文件的差异**
```bash
git diff <branch1> <branch2> -- <file-path>
```

要查看两个分支中某个文件夹的差异，你可以使用以下命令：
```bash
git diff <branch1> <branch2> -- <folder-path>
```

## **比较标签**
```bash
git diff <tag1> <tag2>
```
这个命令比较两个标签之间的差异。

## **git diff --base` 比较合并冲突中的文件版本**
> [git diff - Comparing Changes in Git | Refine](https://refine.dev/blog/git-diff-command/#using---base-with-git-diff) 

`git diff --base` 命令用于比较合并冲突中的文件版本。具体来说，`--base` 选项用于显示合并冲突中基线版本（即合并前的共同祖先版本）与当前工作目录中的版本之间的差异。

通过使用 `git diff --base`，你可以查看合并冲突中基线版本与当前工作目录中的版本之间的差异。

```bash
git diff --base <file>
```
这条命令会显示文件 `<file>` 的基线版本与当前工作目录中的版本之间的差异。

假设你有一个文件 `example.py`，在合并过程中出现了冲突。你可以使用 `git diff --base` 来查看基线版本与当前工作目录中的版本之间的差异。

## **git diff 导出补丁文件**
```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ git diff HEAD^ HEAD -- test01.txt
diff --git a/test01.txt b/test01.txt
index cd7fb11..a821b44 100644
--- a/test01.txt
+++ b/test01.txt
@@ -4,3 +4,4 @@ local modify test01.txt
 A
 b
 C
+001

lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ git diff HEAD^ HEAD -- test01.txt > ../test01.patch
```
将一个仓库中的某个文件的最新修改生产补丁文件。

在另一个仓库应用该补丁文件：
```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test_02 (fix_B)
$ cat test01.txt
test01
git pull
local modify test01.txt
A
b
C

lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test_02 (fix_B)
$ git apply ../test01.patch
```

# git format-patch 生成补丁文件
> [Git - git-format-patch Documentation](https://git-scm.com/docs/git-format-patch) 

`git format-patch` 命令用于将一个或多个提交转换成补丁文件。这些补丁文件以邮件格式输出，包含提交的作者、日期和提交信息等元数据，可以方便地通过邮件发送给其他人。补丁文件中除了代码更改外，还包含提交的元数据，如作者、日期和提交信息等。

## **生成最近一次提交的补丁文件**

```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ git format-patch HEAD^
0001-update-fix_B.patch
```

## **生成最近两次提交的补丁文件**

```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ git log --oneline -2
51da54a (HEAD -> fix_B) update fix_B
9aaa1c6 (branch01) fix B
```

```bash
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)
$ git format-patch HEAD^^
0001-fix-B.patch
0002-update-fix_B.patch
```

## **生成指定提交范围的补丁文件**

```bash
git format-patch <start-commit>..<end-commit>
```

这条命令会生成从 `<start-commit>` 到 `<end-commit>` 之间的所有提交的补丁文件。例如，生成从 `abc123` 到 `def456` 之间的所有提交的补丁文件：

```bash
git format-patch abc123..def456
```

## **生成某个提交以来的所有补丁文件**

```bash
git format-patch <commit>
```

这条命令会生成从指定提交以来的所有提交的补丁文件，但不包括指定的提交。例如，生成从 `abc123` 以来的所有提交的补丁文件：

```bash
git format-patch abc123
```

## **生成从根到某个提交的所有补丁文件**

```bash
git format-patch --root <commit>
```

这条命令会生成从仓库的根到指定提交的所有补丁文件。例如，生成从根到 `abc123` 的所有补丁文件：

```bash
git format-patch --root abc123
```

## 输出格式选项

### **输出到标准输出**

```bash
git format-patch --stdout <commit> > output.patch
```

这条命令会将补丁文件输出到标准输出，并重定向到 `output.patch` 文件中。

### **以 mbox 格式输出**

```bash
git format-patch --mbox <commit>
```

这条命令会以 mbox 格式输出补丁文件，适合通过电子邮件发送。

### **以原始格式输出**

```bash
git format-patch --raw <commit>
```

这条命令会以原始格式输出补丁文件，适合向非 Git 存储库应用补丁。

### **按顺序编号补丁**

```bash
git format-patch --numbered <commit>
```

### **使用 --subject-prefix 自定义补丁文件前缀**

`--subject-prefix` 选项可以自定义补丁文件名的前缀。默认前缀是 `[PATCH]`，但你可以通过这个选项更改它。

**命令**：
```bash
git format-patch --subject-prefix="MY_PATCH" <commit>
```

这条命令会生成补丁文件，文件名前缀为 `MY_PATCH`。例如，生成的文件名可能是 `0001-MY_PATCH-commit-message.patch`。

### **使用 --output-directory 自定补丁文件目录*

`--output-directory` 选项可以指定生成的补丁文件的保存目录。

```bash
git format-patch --output-directory=/path/to/patches <commit>
```

这条命令会将生成的补丁文件保存到 `/path/to/patches` 目录中。

### **使用 --numbered-files 生成仅包含数字的文件名**

`--numbered-files` 选项可以生成仅包含数字的文件名，不包含提交信息。

```bash
git format-patch --numbered-files <commit>
```

这条命令会生成补丁文件，文件名仅为数字，例如 `0001.patch`、`0002.patch` 等。

### **使用 --suffix 指定补丁文件后缀**

`--suffix` 选项可以自定义补丁文件的后缀名。默认后缀名是 `.patch`，但你可以通过这个选项更改它。

```bash
git format-patch --suffix=.txt <commit>
```

这条命令会生成补丁文件，文件名后缀为 `.txt`，例如 `0001-commit-message.txt`。

### 示例

假设你有一个本地仓库，并且已经对其中一个文件作了一些更改并提交了。你可以使用以下命令生成自定义补丁文件：

```bash
git format-patch --subject-prefix="MY_PATCH" --output-directory=/path/to/patches --suffix=.txt HEAD^
```

这条命令会生成从 `HEAD^` 到 `HEAD` 之间的所有提交的补丁文件，文件名前缀为 `MY_PATCH`，后缀为 `.txt`，并保存到 `/path/to/patches` 目录中。生成的文件名可能是 `0001-MY_PATCH-commit-message.txt`。

# 应用补丁文件

## **git apply 应用补丁文件**

```bash
git apply /path/to/mypatch.patch
```

这条命令会将 `mypatch.patch` 文件中的更改应用到当前工作目录中。如果应用成功，你会看到提示信息。如果应用失败，Git 会提示哪些更改无法应用，并给出相应的错误信息。

##  **git am 应用补丁文件**

```bash
git am /path/to/mypatch.patch
```

这条命令会将 `mypatch.patch` 文件作为新的提交应用到当前分支中。如果补丁文件应用成功，Git 会自动创建一个新的提交，其中包含补丁中的更改。如果应用失败，Git 会提示哪些更改无法应用，并给出相应的错误信息。

# git blame 查看文件每行的最新提交信息
> [Git - git-blame Documentation](https://git-scm.com/docs/git-blame) 
> [git diff - Comparing Changes in Git | Refine](https://refine.dev/blog/git-diff-command/#using-git-diff-with-other-git-commands) 


# 分支
> [Git - Basic Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging) 
> [Git Branches Tutorial](https://www.youtube.com/watch?v=e2IbNHi4uCI&ab_channel=freeCodeCamp.org) 


# git checkout
> [Git - git-checkout Documentation](https://git-scm.com/docs/git-checkout) 

`git checkout` 是 Git 中用于切换分支或检出特定版本的文件到工作目录的命令。

## **切换到已存在的分支**
```bash
git checkout <branch-name>
```
这个命令会将 HEAD 移动到指定的分支，并更新工作目录以匹配该分支的状态。

## **创建新分支并切换**
```bash
git checkout -b <new-branch-name>
```
或者在较新版本的 Git 中：
```bash
git switch -c <new-branch-name>
```
这些命令会创建一个新的分支，并立即切换到这个分支。

## **基于远程分支创建新分支并切换**
```bash
git checkout -b <new-branch-name> origin/<branch-name>
```
这个命令会创建一个新的分支，并将其设置为跟踪远程分支 `origin/<branch-name>`。

## **检出特定文件到工作目录**
```bash
git checkout <branch-name> -- <file-path>
```
这个命令会从 `<branch-name>` 分支检出 `<file-path>` 文件到当前工作目录，替换本地的文件。

## **检出特定提交到工作目录**
```bash
git checkout <commit-hash> -- <file-path>
```
这个命令会从 `<commit-hash>` 提交检出 `<file-path>` 文件到当前工作目录。

## **检出特定提交到新分支**
```bash
git checkout <commit-hash> -b <new-branch-name>
```
这个命令会创建一个新的分支 `<new-branch-name>` 并检出 `<commit-hash>` 提交的内容到这个新分支。

## **恢复已修改但未暂存的文件**
```bash
git checkout -- <file-path>
```
这个命令会将 `<file-path>` 文件恢复到最近一次提交的状态，放弃本地的修改。

## **恢复已暂存的文件**
```bash
git restore --staged -- <file-path>
```
或者使用旧版本的 Git 命令：
```bash
git checkout -- <file-path>
```
这些命令会将 `<file-path>` 文件从暂存区取消暂存，恢复到工作目录的状态。

## **检出标签对应的版本**
```bash
git checkout <tag-name>
```
这个命令会检出包含 `<tag-name>` 标签的提交，通常用于检出某个特定的发布版本。

## **有冲突时使用对方版本**
1. **识别冲突文件**：
   合并操作后，使用 `git status` 命令来识别哪些文件存在冲突。

2. **手动选择对方版本**：
   对于每个存在冲突的文件，你可以手动编辑文件来解决冲突，或者使用以下命令来选择对方的版本：

   ```bash
   git checkout --ours -- <file-path>
   ```

   或者，如果你想要使用对方的版本（即被合并分支的版本），可以使用：

   ```bash
   git checkout --theirs -- <file-path>
   ```

   这里 `<file-path>` 是存在冲突的文件的路径。这些命令会用被合并分支（对方的分支）的版本覆盖工作目录中的文件。

3. **添加到暂存区**：
   选择对方版本后，你需要将这些文件添加到暂存区：

   ```bash
   git add <file-path>
   ```

4. **继续合并**：
   如果你已经解决了所有文件的冲突，你可以继续完成合并操作：

   ```bash
   git commit
   ```

   Git 会提示你输入合并提交的消息。

## 注意事项

- 使用 `git checkout` 切换分支时，如果你有未提交的更改，Git 会警告你，因为这些更改可能会丢失。你可以先暂存更改，或者使用 `git stash` 保存更改。
- `git checkout` 命令在检出文件时，如果文件在工作目录中被修改过，Git 会阻止检出操作以防止数据丢失。你需要先解决这些冲突，或者使用 `git checkout --force` 强制覆盖本地更改。
- 在使用 `git checkout` 检出文件时，如果你想要保留工作目录中的更改，可以先将更改暂存，然后再检出文件。

# git checkout 和 git cherry-pick
`git checkout <commit-hash> -- <file-path>` 命令和 `git cherry-pick` 命令都可以用来将更改应用到当前分支，但它们的目的和行为有所不同，因此不能互相代替。

## `git checkout <commit-hash> -- <file-path>`
这个命令用于从特定的提交（`<commit-hash>`）中检出文件（`<file-path>`）到当前工作目录。这个操作不会改变分支的历史记录，也不会创建新的提交。它仅仅是替换工作目录中的文件内容，用指定提交中的文件版本覆盖。这个命令不会记录任何新的提交，也不会影响项目的提交历史。

## `git cherry-pick`
`git cherry-pick` 命令用于将一个或多个提交的应用到当前分支，从而创建新的提交。这个操作会将指定提交的更改作为新的提交引入到当前分支的历史中。`git cherry-pick` 可以用于将特定提交从一个分支应用到另一个分支，或者在同一个分支中重新应用已经存在的提交。

## 区别

- **历史记录**：`git checkout` 不会改变分支的历史记录，而 `git cherry-pick` 会创建新的提交，改变历史记录。
- **提交**：`git cherry-pick` 会创建新的提交，而 `git checkout` 不会。
- **原子性**：`git cherry-pick` 操作是原子性的，要么全部成功，要么全部失败。如果一个提交被 cherry-picked，那么它会被完全应用到当前分支。而 `git checkout` 只是简单地替换文件，不涉及提交的过程。
- **冲突解决**：在使用 `git cherry-pick` 时，如果出现冲突，你需要解决冲突并完成 cherry-pick 操作。而在使用 `git checkout` 时，如果文件存在冲突，Git 会停止操作并让你手动解决。

虽然 `git checkout <commit-hash> -- <file-path>` 可以用来获取特定提交的文件版本，但它不能代替 `git cherry-pick` 的功能，因为后者涉及到创建新的提交和改变项目的历史记录。如果你只是想替换文件而不创建新的提交，使用 `git checkout`。如果你需要将更改作为新的提交引入到当前分支，那么 `git cherry-pick` 是正确的选择。

# git switch 
`git switch` 是 Git 2.23 版本引入的命令，用于切换分支。这个命令的作用与 `git checkout` 类似，但提供了更清晰的语义和错误检查。

## **切换到已存在的分支**
```bash
git switch <branch-name>
```
例如，将工作目录切换到主分支：
```bash
git switch master
```

## **使用 `-c` 或 `--create` 参数创建并切换新分支**
  ```bash
  git switch -c <new-branch-name>
  ```
  例如，创建一个名为 `feature-branch` 的新分支并切换到它：
  ```bash
  git switch -c feature-branch
  ```
  这相当于先执行 `git branch <new-branch-name>` 然后执行 `git switch <new-branch-name>` 的快捷方式。

## **使用 `-C` 或 `--force-create` 参数强制创建新分支**
  ```bash
  git switch -C <new-branch>
  ```
  如果 `<new-branch>` 已经存在，它将被重置为 `<start-point>`。这相当于先执行 `git branch -f <new-branch>` 然后执行 `git switch <new-branch>`。

## 根据远程分支创建本地分支
使用 `git switch --track` 命令创建一个新的本地分支，并设置它跟踪远程分支。例如，如果你想要创建一个本地分支 `feature` 并跟踪远程的 `origin/feature`，可以执行以下命令：

```bash
git switch --track origin/feature
```

或者使用 `-t` 选项：

```bash
git switch -t origin/feature
```

这个命令会创建一个新的本地 `feature` 分支，并立即设置它跟踪远程的 `origin/feature` 分支。

也可以使用下面方法：
```bash
git checkout -b feature origin/feature
```

## **使用 `-d` 或 `--detach` 参数切换到一个提交**
  ```bash
  git switch -d <commit-hash>
  ```
  这会将 HEAD 分离并指向 `<commit-hash>`，允许你在一个提交上进行临时的检查或实验。

## **使用 `<commit_hash>` 恢复工作目录**
  ```bash
  git switch <commit_hash>
  ```
  这会将工作目录切换到指定提交 `<commit_hash>` 的状态，处于分离 HEAD 的状态。

## **使用 `-` 快速切换回前一个分支**
  ```bash
  git switch -
  ```
  这允许你快速切换回前一个分支，无需记住分支名称。

## **使用 `git switch <branchName>` 从远程分支创建同名的本地分支并关联远程分支**
  ```bash
  git switch testmaster
  ```
  这会拉取远程分支到本地，并建立远程分支和本地分支的关联关系。

## **使用 `--orphan <new-branch>` 创建孤儿分支**
  ```bash
  git switch --orphan <new-branch>
  ```
  这会创建一个新的孤儿分支，并删除所有跟踪的文件。

## **使用 `--recurse-submodules` 更新所有初始化的子模块**
  ```bash
  git switch --recurse-submodules <branch>
  ```
  这会根据超级项目中记录的提交更新所有活动子模块的内容。

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

## 使用通配符
```bash
git add *.cpp *.h
```

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

1. **记录更改**：`git commit` 将暂存区中的更改保存为一个新的提交（commit），并记录更改的内容和时间。
2. **更新项目历史**：每次提交都会更新项目的提交历史，形成一个版本记录。
3. **要求提交信息**：执行提交时，Git 会要求你提供一个提交信息，以描述所做的更改。

## **指定提交信息 -m**
```bash
git commit -m "Commit message"
```
使用 `-m` 选项可以直接在命令行中指定提交信息。

## **提交所有更改 -am**
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

## **修改最后一次提交 --amend**
`git commit --amend` 是一个Git命令，用于修改最近一次提交的信息。这个命令通常用于当你想要修改最后一次提交的提交信息，或者当你想要将未暂存的更改添加到最近的提交中时。

- 如果你刚刚做了一次提交，然后意识到提交信息有误或者不完整，你可以使用 `git commit --amend` 来修改它。
- 如果你在提交后发现还有一些更改忘记加入，你可以使用 `git commit --amend` 将这些更改加入到上一个提交中。
- 如果修改提交内容后不更新提交日志，可以加 `--no-edit` 选项。

### 注意事项
- **重写历史**：
`git commit --amend` 实际上会创建一个新的提交对象，它有一个不同的提交ID。这意味着它会重写项目的历史。如果你已经将原始提交推送到了远程仓库，那么使用 `git commit --amend` 后，你需要使用 `git push --force` 来更新远程仓库。这可能会影响其他协作者的工作，因此在团队项目中使用时需要谨慎。

- **使用场景限制**：
`git commit --amend` 只能用于最近的提交。如果你想要修改更早的提交，你需要使用 `git rebase` 命令。

- **处理冲突**：
如果在修正提交的过程中出现冲突，你需要手动解决这些冲突，然后继续修正过程。

## **从文件读取提交日志 -F**
```bash
git commit -F commit_msg.txt
```

## **输入多行提交日志**
```bash
$ git commit -F - <<EOF
> modify test.md
> EOF
[feature c433384cd] modify test.md
 1 file changed, 1 insertion(+), 1 deletion(-)
```

- `-F`：这个选项用于指定提交信息的来源。通常 `-F` 后面跟一个文件名，表示从文件中读取提交信息。
- `-`：在这里，`-` 表示从标准输入（stdin）读取提交信息。这意味着提交信息将从命令行中直接输入，而不是从文件中读取。
- `<<`：这是 here 文档的开始标记。它告诉 shell，接下来的输入将被重定向到命令的标准输入，直到遇到一个特定的结束标记。
- `EOF`：这是结束标记（End Of File）。你可以选择任何字符串作为结束标记，但 `EOF` 是最常用的。这里表示输入将一直持续，直到遇到另一个 `EOF`。


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

## 处理错误的提交
> [Git Guides - git commit](https://github.com/git-guides/git-commit#what-can-go-wrong-while-changing-history) 

- `git revert`是更改历史记录的最安全方式。它不会删除现有提交，而是在新提交中应用特定提交引入变化的逆操作。
- `git reset`是一个强大的命令，可以移动HEAD指针和分支指针到另一个时间点，但可能会导致工作丢失。在使用`git reset`之前，确保与团队沟通，并了解三种类型的重置（--soft, --mixed, --hard）。

- `git reflog`是一个记录HEAD指向的每个提交的日志。如果你在使用`git reset`时无意中丢失了提交，可以使用`git reflog`找到并访问它们。

- `git commit --amend`只更改当前分支上的最近一次提交。
- 这个命令对于尚未推送到远程的提交、提交信息中有拼写错误或者提交中未包含预期更改的情况非常有用。

# 防止本地分支修改提交历史顺序
本地在 git commit 前先 git fetch，更新远程分支的引用，可以查看本地和远程的差异，是否有冲突等，
然后提交，防止本地先提交后合并，修改提交历史的顺序。

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
> [Git Log Command Explained](https://www.freecodecamp.org/news/git-log-command/) 

List commits that are reachable by following the parent links from the given commit(s), but exclude commits that are reachable from the one(s) given with a ^ in front of them. The output is given in reverse chronological order by default.

You can think of this as a set operation. Commits reachable from any of the commits given on the command line form a set, and then commits reachable from any of the ones given with ^ in front are subtracted from that set. The remaining commits are what comes out in the command’s output. Various other options and paths parameters can be used to further limit the result.

1. **查看提交历史**：`git log` 显示项目的提交历史记录，包括提交信息、作者、日期等。
2. **过滤和格式化**：通过各种选项，可以过滤特定的提交记录、格式化输出内容等。

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

## **查看所有提交**
```bash
git log
```
这个命令显示项目的完整提交历史，默认按照时间顺序，从最新的开始显示。

## **查看特定分支的提交**
```bash
git log <branch-name>
```
这个命令显示指定分支的提交历史。

## **查看不同分支差异**
```bash
$ git log foo bar ^baz
```
上面命令查看那些可达于 foo 或 bar 分支最新提交，但不可达于 baz 的提交。即列出那些在 foo 或 bar 分支上存在，但在 baz 分支上不存在的提交。

## **查看一个分支相对于另一个分支的提交差异**
### git log branch1..branch2
```bash
$ git log origin..HEAD --oneline
```
HEAD 当前分支最新提交相对于 origin 分支最新提交的提交记录，即 HEAD 有但 origin 没有的提交记录
和下面命令功能相同：
```bash
$ git log HEAD ^origin --oneline
```

## **查看特定文件的提交**
```bash
git log <file>
```
这个命令显示指定文件的提交历史。

```bash
$ git log -3 --oneline  demo/test.md
748d2f6b4 modify test.md
75844c6a5 modify test.md
d3c488765 modify test.md
```

## **指定输出日志数目**
```bash
git log -3
```
输出日志显示最新的 3 条

## **查看提交差异 --patch**
> [Git - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History) 

使用`-p`或`--patch`参数，可以查看每个提交的具体差异，下面是官方文档示例：
```bash
$ git log -p -2
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    Change version number

diff --git a/Rakefile b/Rakefile
index a874b73..8f94139 100644
--- a/Rakefile
+++ b/Rakefile
@@ -5,7 +5,7 @@ require 'rake/gempackagetask'
 spec = Gem::Specification.new do |s|
     s.platform  =   Gem::Platform::RUBY
     s.name      =   "simplegit"
-    s.version   =   "0.1.0"
+    s.version   =   "0.1.1"
     s.author    =   "Scott Chacon"
     s.email     =   "schacon@gee-mail.com"
     s.summary   =   "A simple gem for using Git in Ruby code."

commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 16:40:33 2008 -0700

    Remove unnecessary test
```

这将显示最新两个提交的详细差异，包括文件的增删改。
其中 a 表示该提交前的版本，b 表示该提交后的版本。
`@@` 标记差异的开始，对于提交前的 a 版本，从第 5 行开始的 7 行内容，对于提交后的 b 版本，从第 5 行开始的 7 行内容。
`-` 表示原始版本中存在但新版本被删除的行，`+` 表示原始版本没有 ，新版本添加的行。

## **统计信息 --stat**

```bash
$ git log -1 --stat
commit 740e65b2fd98f0b99f3bcfd8dc8e1b8ad8bb6a3f (HEAD -> feature)
Author: lxw <15521168075@163.com>
Date:   Thu Jan 9 13:09:24 2025

    modify test.md

 demo/test.md | 4 ++--
 1 file changed, 2 insertions(+), 2 deletions(-)
```
这将显示每个提交修改的文件列表、文件数量变化以及添加和删除的行数统计。

## **自定义格式 --pretty**

使用`--pretty`参数，我们可以自定义日志的显示格式。例如，`oneline`将每个提交显示在一行上：

```bash
$ git log --pretty=oneline
```

输出示例：

```
ca82a6dff817ec66f44342007202690a93763949 Change version number
085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7 Remove unnecessary test
a11bef06a3f659402fe7563abf99ad00de2209e6 Initial commit
```

## **格式化输出 --pretty=format**
> [Git - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History#pretty_format) 

`--pretty=format`允许自定义输出格式。例如，显示提交的哈希值、作者和提交信息：

```bash
$ git log --pretty=format:"%h - %an, %ar : %s"
```

输出示例：

```
ca82a6d - Scott Chacon, 6 years ago : Change version number
085bb3b - Scott Chacon, 6 years ago : Remove unnecessary test
a11bef0 - Scott Chacon, 6 years ago : Initial commit
```

## **ASCII 图形显示历史 --graph**

```bash
$ git log --pretty=format:"%h %s" --graph -5
```

## **显示提交的引用信息 --decorate**
从 Git 2.10 版本开始，`--decorate` 选项默认是开启的。
如果你希望关闭 `--decorate` 选项，可以使用 `--no-decorate`：
```bash
git log --no-decorate -1
```
这个命令会显示最近一次提交的详细信息，但不会显示指向该提交的引用名称。

假设你有以下提交历史：
```bash
A -- B -- C -- D -- E
       \         /
        F-------G
```
执行 `git log --decorate -1`：
```bash
commit 9aaa1c654b076de24c529ce46d3c4d95211a2871 (HEAD -> fix_B, branch01)
Author: lxwcd <15521168075@163.com>
Date:   Thu Dec 19 21:43:41 2024 +0800

    fix B
```
在这个例子中：
- `9aaa1c654b076de24c529ce46d3c4d95211a2871` 是当前提交的哈希值。
- `(HEAD -> fix_B, branch01)` 表示：
  - `HEAD` 指向 `fix_B` 分支。
  - `fix_B` 分支的最新提交是这个提交。
  - `branch01` 分支的最新提交也是这个提交。

## **时间限制**
> [Git - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History#pretty_format) 

`--since`和`--until`参数可以用来限制显示特定时间范围内的提交：

```bash
$ git log --since="2 weeks ago"
```

这将显示最近两周内的提交记录。

## **作者和关键词搜索**

`--author`和`--grep`参数可以用来根据作者或提交信息中的关键词来过滤提交：

```bash
$ git log --author="Scott Chacon" --grep="version"
```

这将显示所有作者为“Scott Chacon”且提交信息中包含“version”的提交。

## 文件路径过滤

最后，我们可以通过文件路径来限制显示特定文件的提交历史：

```bash
$ git log -- path/to/file
```

这将只显示影响`path/to/file`文件的提交记录。

## **查看特定内容的日志 -S**
`git log -S` 选项是一个非常有用的过滤器，用于查找那些改变了指定字符串出现次数的提交。这个选项通常被称为 Git 的“pickaxe”选项。

- **查找字符串变化**：`-S<string>` 选项用于查找那些添加或删除了指定字符串的提交。这可以帮助你快速定位某个特定代码片段或功能的引入和修改历史。

```bash
git log -S "function_name"
```
这个命令会列出所有添加或删除了 `function_name` 这个字符串的提交。

### 注意事项
- **字符串匹配**：`-S` 选项使用简单的字符串匹配，而不是正则表达式。如果你需要使用正则表达式，可以使用 `-G` 选项。
- **性能考虑**：对于大型项目，使用 `-S` 选项可能会比较慢，因为它需要检查每个提交中的每个文件。

### 结合其他选项使用
- **`--pickaxe-regex`**：如果你需要使用正则表达式来匹配字符串，可以结合 `--pickaxe-regex` 选项使用。
- **`--stat`**：显示每个提交的统计信息，帮助你更好地理解每个提交的影响。
- **`--graph`**：以图形方式显示提交历史，帮助你理解分支和合并的结构。

## **--first-parent**
> [Visualize Merge History with git log --graph, --first-parent, and --no-merges](https://redfin.engineering/visualize-merge-history-with-git-log-graph-first-parent-and-no-merges-c6a9b5ff109c)   

`git log --first-parent` 用于查看提交历史时只显示每个提交的第一个父提交。这在处理包含合并提交的历史时特别有用，因为它可以帮助你从“主分支”的角度查看历史，跳过那些来自合并分支的提交。

- **显示第一父提交**：`--first-parent` 选项告诉 `git log` 只显示每个提交的第一个父提交。这对于理解主分支（如 `main` 或 `master`）的线性历史非常有帮助，因为它会忽略那些通过合并操作引入的分支提交。
- **应用场景**：当你想要查看主分支的清晰历史，而不被合并操作引入的复杂分支历史干扰时，这个选项非常有用。例如，如果你遵循一个严格的分支策略，其中所有功能分支最终都合并回主分支，`--first-parent` 可以帮助你只看到主分支上的关键提交。

## **排除合并信息 --no-merges****
`--no-merges` 选项用于排除合并信息。当使用 `--no-merges` 选项时，`git log` 只显示那些没有合并操作的提交。
- **排除合并信息**：`--no-merges` 选项告诉 `git log` 只显示那些没有合并操作的提交。这在处理包含合并提交的历史时特别有用，因为它可以避免看到那些通过合并操作引入的分支提交。
- **应用场景**：当你想要查看主分支的线性历史，而不被合并操作引入的复杂分支历史干扰时，这个选项非常有用。例如，如果你遵循一个严格的分支策略，其中所有功能分支最终都合并回主分支，`--no-merges` 可以帮助你只看到主分支上的关键提交。

## 注意事项

- **输出量**：默认情况下，`git log` 可能会显示大量的提交记录。使用过滤选项可以帮助你快速找到相关信息。
- **图形化工具**：虽然 `git log` 提供了丰富的文本输出选项，但有时使用图形化工具（如 `gitk` 或其他第三方工具）可能更直观。
- **性能**：对于非常大的仓库，`git log` 可能会有些慢。在这种情况下，考虑使用过滤选项来减少输出量。

# git reflog
> [Git - git-reflog Documentation](https://git-scm.com/docs/git-reflog)   

`git reflog` 是 Git 中一个非常强大的命令，它用于管理和查看引用日志（reflogs）。引用日志记录了本地仓库中更新分支和其他引用的操作。

`git reflog` 记录了 HEAD 和分支引用以及标签等的所有更新操作。这意味着即使某些提交被删除或者重写，你仍然可以通过 `git reflog` 来找到它们。

`git reflog` 是 Git 操作的一道安全保障，它能够记录几乎所有本地仓库的改变，包括所有分支的 commit 提交，以及已经被删除的 commit。这使得 `git reflog` 成为恢复丢失提交或分支的重要工具。

## **查看引用日志**
最基本的用法是 `git reflog`，它会显示 HEAD 的引用日志，列出 HEAD 的所有历史更新操作，包括分支切换、提交、重置等。
```bash
git reflog
```
输出类似于：
```
eb1050b (HEAD -> feature_branch) HEAD@{0}: checkout: moving from main to feature_branch
1525c48 (origin/main, main) HEAD@{1}: checkout: moving from 2bf1773d87a7806cda25d4d313995bb08adbabf5 to main
```
这里 `HEAD@{n}` 表示 HEAD 在过去第 n 次操作时的位置。

## **show**
显示指定引用的日志，如果未指定引用，则默认显示 HEAD 的日志。`git reflog show` 是 `git log -g --abbrev-commit --pretty=oneline` 的别名。
```bash
git reflog show <ref>
```
## **list**
列出所有有对应 reflog 的引用。
```bash
git reflog list
```
## **expire**
修剪旧的 reflog 条目，可以指定时间来删除过时的日志条目。
```bash
git reflog expire [--expire=<time>] [--expire-unreachable=<time>] [--all]
```
## **delete**
删除单个 reflog 条目，需要指定确切的条目。
```bash
git reflog delete <ref>@{<specifier>}
```
## **exists**
检查某个引用是否有 reflog。
```bash
git reflog exists <ref>
```

## **基于时间的引用**
`git reflog` 支持基于时间的引用，例如 `HEAD@{1.day.ago}` 表示 HEAD 在一天前的位置。
```bash
git diff main@{0} main@{1.day.ago}
```
这个命令比较了 `main` 分支当前状态和一天前的状态。

# git show
> [Git - git-show Documentation](https://git-scm.com/docs/git-show) 

`git show` 用于展示各种 Git 对象的详细内容，包括提交（commit）、标签（tag）和分支（branch）。

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

## **查看提交详情**
- `git show <commit>`：显示指定提交的详细信息，包括作者、日期、提交信息和具体的 diff（差异）。
- `git show HEAD`：显示当前分支的最新提交的详细信息。

## **查看标签详情**
- `git show <tag>`：显示指定标签的详细信息，包括标签信息和指向的提交。

## **查看分支比较**
- `git show <branch>`：显示指定分支的最新提交的详细信息。

## **查看最新提交的详细信息**
```bash
git show HEAD
```

## **查看特定提交的文件列表**
```bash
git show --name-only <commit>
```

## **查看特定提交的统计信息**
```bash
git show --stat <commit>
```

## **查看特定提交的简要统计信息**
```bash
git show --shortstat <commit>
```

## **查看特定提交的差异，不包括文件内容**
```bash
git show --pretty=raw <commit>
```

## **查看特定提交的 SHA-1 哈希值和提交信息**
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

### 撤销远程的提交
本地提交后 Push 到远程，本地用 git reset --soft HEAD^ 撤销了最近一次提交，如果远程该分支只有自己用，可以 git push --force 覆盖远程提交记录。

### **撤销最后一次提交**
  ```bash
  git reset --soft HEAD~1
  ```
  这个命令将 HEAD 指针移动到上一次提交，但保留工作目录和暂存区的状态。

### **撤销最后一次提交并重置暂存区**
  ```bash
  git reset --mixed HEAD~1
  ```
  或者
  ```bash
  git reset HEAD~1
  ```
  这些命令将 HEAD 指针移动到上一次提交，并重置暂存区，但保留工作目录的状态。

### **撤销最后一次提交并恢复工作目录**
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
> [Managing remote repositories - GitHub Docs](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories) 

`git remote` 是 Git 中用于管理远程仓库的命令。它允许你查看、添加、修改和删除远程仓库的引用。

## 功能和用途

1. **查看远程仓库**：`git remote` 命令可以列出所有配置的远程仓库。
2. **添加远程仓库**：你可以使用 `git remote add` 命令添加新的远程仓库。
3. **修改远程仓库**：可以更改远程仓库的 URL 或其他设置。
4. **删除远程仓库**：可以删除不再需要的远程仓库引用。

## 基本使用

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

## 选项

- **`-v` 或 `--verbose`**：显示远程仓库的详细信息，包括 URL。
- **`add`**：添加新的远程仓库引用。
- **`remove`**：删除远程仓库引用。
- **`rename`**：重命名远程仓库。
- **`set-url`**：更改远程仓库的 URL。

## 使用场景

- **协作开发**：在团队协作中，你可能需要添加远程仓库来共享代码。
- **代码托管**：你可能需要将代码推送到远程仓库以进行托管或备份。
- **分支管理**：通过远程仓库，你可以管理不同分支的代码。

## 示例

```bash
git remote add origin https://github.com/lxwcd/git_test.git
git branch -M main
git push -u origin main
```

这个命令添加了一个名为 `origin` 的远程仓库引用，指向 `https://github.com/lxwcd/git_test.git`。

## 注意事项

- **远程仓库名称**：`origin` 是默认的远程仓库名称，但你可以使用任何名称。
- **URL 格式**：确保远程仓库的 URL 格式正确，可以是 HTTPS 或 SSH 格式。
- **权限**：在添加或修改远程仓库时，确保你有足够的权限。

通过 `git remote`，你可以有效地管理远程仓库的引用，这对于协作开发和代码托管非常重要。

# git branch
> [Git - git-branch Documentation](https://git-scm.com/docs/git-branch/2.13.7) 

`git branch` 是一个用于创建、列出、删除和管理 Git 分支的命令。分支在 Git 中是一个轻量级的移动指针，指向你代码历史的某个特定提交。

## **创建分支**
```bash
git branch <branch-name>
```
这个命令会创建一个新分支，但不会切换到该分支。例如，`git branch feature-x` 会创建一个名为 `feature-x` 的新分支。

## **创建并切换分支**
```bash
git checkout -b <branch-name>
```
或者在某些 Git 版本中：
```bash
git switch -c <branch-name>
```
这些命令会创建一个新分支并立即切换到该分支。

## **列出所有本地分支**
```bash
git branch
```
这个命令会列出所有的本地分支。

## **列出所有远程分支**
```bash
git branch -r
```
这个命令会列出所有的远程分支。

## **列出所有本地和远程分支**
```bash
git branch -a
```
这个命令会列出所有的本地分支和远程分支。

## **显示当前分支**
```bash
git branch --show-current
```
或者使用 `git rev-parse --abbrev-ref HEAD`。
这个命令会显示当前检出的分支名称。

## **删除分支**
```bash
git branch -d <branch-name>
```
这个命令会删除一个已经完全合并到当前分支的本地分支。如果分支未完全合并，Git 会阻止删除以防止数据丢失。

## **强制删除分支**
```bash
git branch -D <branch-name>
```
这个命令会强制删除一个分支，无论它是否已经合并。

## 重命名分支
`git branch -m` 和 `git branch -M` 是 Git 中用于重命名分支的两个命令，它们的主要区别在于处理分支重命名时的安全性。

### git branch -m
- `-m` 是 `--move` 的缩写。
- 这个命令用于重命名当前分支。
- 如果目标分支名称已经存在，并且没有进行任何提交，`git branch -m` 会失败，以防止潜在的数据丢失。
- 如果目标分支已经存在并且有提交，`git branch -m` 会报错，因为它不想覆盖任何现有的分支历史。

```bash
git branch -m <old-name> <new-name>
```
这个命令会将分支 `<old-name>` 重命名为 `<new-name>`。

### git branch -M

- `-M` 是 `--move` 的缩写，与 `-m` 类似，但它的行为更加激进。
- 这个命令也用于重命名当前分支。
- 如果目标分支名称已经存在，`git branch -M` 会强制覆盖目标分支。这意味着目标分支的历史将被当前分支的历史替换，这可能会导致数据丢失。
- `git branch -M` 通常用于修复损坏的分支或者在确定目标分支没有重要历史的情况下使用。

## 创建新远程分支
本地创建一个分支，git push -u origin remote_branch 可以将本地和远程分支关联且新建远程分支

## 设置跟踪关系

## **设置上游分支**
```bash
git branch -u <remote-branch>
```
或者使用 `git branch --set-upstream-to <remote-branch>`。
这个命令会设置当前分支跟踪指定的远程分支。

## **查看上游分支**
```bash
git branch -vv
```
这个命令会显示所有分支及其上游信息。

## 重命名远程分支
在 Git 中，重命名远程分支可以通过两步完成：首先重命名本地分支，然后将其推送到远程仓库以更新远程分支的名称。

### 步骤 1: 重命名本地分支

1. **检出你想要重命名的分支**：
   ```bash
   git checkout <old-branch-name>
   ```
   将 `<old-branch-name>` 替换为你想要重命名的分支的当前名称。

2. **重命名本地分支**：
   ```bash
   git branch -m <new-branch-name>
   ```
   将 `<new-branch-name>` 替换为你想要设置的新分支名称。

如果还没有本地分支，则用下面直接新建本地分支：
```bash
git checkout -b <new-branch-name> origin/<old-branch-name>
```
可以用 `git branch -vv` 查看本地分支与远程分支对应关系。

### 步骤 2: 推送更改到远程仓库

1. **强制推送到远程仓库**：
   ```bash
   git push -u origin :<old-branch-name>
   git push -u origin <new-branch-name>
   ```
   这里的 `<old-branch-name>` 是分支的旧名称，而 `<new-branch-name>` 是新名称。第一个命令用于删除远程分支的旧名称，第二个命令用于将重命名后的本地分支推送到远程仓库。

   - `:<old-branch-name>` 表示删除远程分支。
   - `-u` 参数是 `--set-upstream` 的简写，它设置远程跟踪分支。

### 注意事项

- 如果你的分支已经被其他人使用，强制推送 (`git push --force`) 可能会导致其他人的工作丢失。在这种情况下，你应该先与团队成员沟通，以确保不会覆盖其他人的更改。
- 如果你的远程分支已经被设置为跟踪分支，你可能需要使用 `-u` 参数来更新跟踪信息，如下所示：
  ```bash
  git push -u origin <new-branch-name>
  ```
  这将设置新的本地分支作为远程分支的上游（upstream）。

- 如果你只想更新远程分支的名称，而不改变本地分支的名称，你可以使用以下命令：
  ```bash
  git push origin :<old-branch-name>
  git push origin <new-branch-name>
  ```
  这将删除旧的远程分支并推送新的远程分支，而不会改变你当前检出的本地分支名称。

## **包含已合并/未合并信息**
```bash
git branch --merged
git branch --no-merged
```
这些命令分别列出所有已经合并到当前分支的分支和所有未合并到当前分支的分支。

## **删除远程跟踪分支**
```bash
git branch -dr <remote/branch>
```
这条命令会删除本地的远程跟踪分支。但并不会直接删除远程仓库中的分支，只是删除了本地对远程分支的跟踪信息。

# **本地分支的上游分支** 
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

# git apply

`git apply` 命令用于将补丁文件（通常是通过 `git diff` 生成的）应用到工作目录中的文件上。基本语法如下：
```bash
git apply <patch-file>
```

其中 `<patch-file>` 是补丁文件的路径。执行此命令后，Git 会根据补丁文件的内容对当前工作目录中的文件进行修改。

## 参数选项

- `--stat`：显示补丁文件应用的统计信息，包括修改了哪些文件以及进行了何种修改。
- `--numstat`：显示每个文件的详细统计信息，包括添加和删除的行数。
- `--summary`：显示补丁文件应用的概要信息。
- `--check`：检查补丁文件是否能够成功应用，但并不实际应用补丁文件。
- `--3way`：当补丁文件与目标文件存在冲突时，尝试使用三方合并算法解决冲突。
- `--index`：将补丁文件应用到索引中，而不仅仅是应用到工作目录中的文件。
- `--intent-to-add`：允许应用补丁到尚未跟踪的文件，Git 会将这些文件添加到索引中。
- `--allow-binary-replacement`：允许补丁替换二进制文件。
- `-R` 或 `--reverse`：反向应用补丁，即撤销补丁中所做的更改。
- `-p<n>`：指定补丁文件中路径的前缀层数，用于处理包含前缀的补丁文件。

## **应用补丁文件**
```bash
git apply patchfile.diff
```
这会将 `patchfile.diff` 中的差异应用到当前工作目录中的对应文件。

## **检查补丁是否可应用**
```bash
git apply --check patchfile.diff
```
这会检查 `patchfile.diff` 是否可以成功应用到当前工作目录中的文件，但不会实际应用补丁。

## **应用补丁并添加到索引**
```bash
git apply --index patchfile.diff
```
这会将补丁应用到索引中，而不仅仅是工作目录中的文件。

# git stash

`git stash` 是 Git 中一个非常有用的命令，它允许你临时保存工作目录中的修改，以便你可以在不提交这些修改的情况下切换分支或返回到一个干净的工作状态。

## 功能

- **保存当前工作状态**：当你的工作目录中有未提交的更改，而这些更改可能阻碍你切换分支或执行其他操作时，`git stash` 可以让你保存这些更改，以便稍后恢复。
- **保持工作目录干净**：使用 `git stash` 可以清理工作目录，让你可以在一个干净的状态下来执行其他 Git 操作，比如拉取最新的代码或切换分支。
- **恢复工作状态**：你可以在任何时候恢复之前保存的工作状态，无论是在同一个分支还是不同的分支上。

## 基本用法

- **保存工作状态**：
  ```bash
  git stash save "optional message"
  ```
  这个命令会保存当前的工作状态到一个 stash 中，并清理工作目录。如果省略 `"optional message"`，Git 会自动生成一个消息。

- **列出所有 stash**：
  ```bash
  git stash list
  ```
  这个命令会列出所有的 stash，每个 stash 前面都有一个标识符，如 `stash@{0}`。

- **应用 stash**：
  ```bash
  git stash apply
  ```
  这个命令会应用最近的 stash 到当前工作目录。你也可以指定一个 stash 来应用：
  ```bash
  git stash apply stash@{n}
  ```
  其中 `n` 是 stash 的索引号，最新的 stash 编号为 0，编号最大的为最先 stash 的内容。

- **删除 stash**：
  ```bash
  git stash drop stash@{n}
  ```
  这个命令会删除指定的 stash。

- **应用 stash 并删除**：
  ```bash
  git stash pop
  ```
  这个命令会应用最近的 stash 并从 stash 列表中删除它。

## 查看 stash 的内容
1. **查看 stash 列表**：
   使用 `git stash list` 命令来查看所有存储的 stash 列表。这个列表会显示每个 stash 的唯一标识符和相关的提交信息。

2. **预览 stash 内容**：
   要预览特定 stash 的内容，可以使用 `git stash show stash@{n}` 命令，其中 `n` 是 stash 的索引号。这个命令会显示指定 stash 的详细信息，包括更改的文件列表和更改的内容。

3. **比较 stash 与当前工作目录**：
   如果你需要比较某个 stash 与当前工作目录的差异，可以使用 `git stash show -p stash@{n}` 命令。这个命令会以补丁格式显示 stash 的变更详情，包括修改的文件和具体的变更内容。

4. **查看 stash 的变更文件列表**：
   如果你只想查看某个 stash 的变更文件列表，可以使用 `git stash show --name-only stash@{n}` 命令。这个命令会显示该 stash 中所有修改的文件名。

通过这些命令，你可以查看 stash 的内容，并且对于有冲突的 stash，可以使用 `git stash show -p` 来查看与当前分支的差异，从而更好地决定如何应用 stash。这些方法可以帮助你管理和恢复工作目录中的更改。

## git stash push

## git stash save

## 应用特定文件
`git checkout stash@{n} -- <file-path>`

1. **`git checkout`**：
   这是 Git 中用于切换分支或恢复工作树文件的命令。它可以用于切换到不同的分支，或者检出特定的文件或分支到当前工作目录。

2. **`stash@{n}`**：
   这是指最新的 stash（暂存）。在 Git 中，`stash` 是一个用于临时存储你的工作进度的机制，允许你保存当前工作目录的状态（包括未提交的修改和暂存的变更），以便之后可以恢复。`stash@{0}` 表示最近一次 stash 的引用，`stash@{1}` 表示之前的 stash，以此类推。

3. **`--`**：
   这是一个分隔符，用于区分 stash 引用和后续的文件路径参数。在 Git 命令中，`--` 通常用于指示命令行参数的结束，确保之后的参数不被解释为命令的选项或参数。

4. **`<file-path>`**：
   这是你想要检出的文件的路径。你需要替换 `<file-path>` 为实际的文件名或路径。例如，如果你想要检出 `README.md` 文件，你应该使用 `git checkout stash@{0} -- README.md`。

`git checkout stash@{0} -- <file-path>` 命令的作用是从最新的 stash（`stash@{0}`）中检出特定的文件（`<file-path>`）到当前工作目录。这个操作会覆盖工作目录中指定文件的内容，用 stash 中的版本替换它。

这个命令在以下场景中非常有用：

- 当你想要恢复某个文件到 stash 时的状态，但不想应用整个 stash。
- 当你之前 stash 了一些更改，现在想要将这些更改的部分文件恢复到工作目录，而不是恢复所有文件。
- 当你解决了合并冲突后，想要从 stash 中恢复特定文件的版本，而不是使用工作目录或分支中的版本。

### 强制覆盖
```bash
git checkout --force stash@{0} -- <file-path>
```
或者：
```bash
git checkout -f stash@{0} -- <file-path>
```

## 应用部分文件

1. **列出 stash 中的文件**：
首先，你需要列出 stash@{0} 中的所有文件。可以使用 `git stash show` 命令来查看 stash 中的内容。

2. **应用 stash 中的 `.cpp` 文件**：
然后，你可以使用 `git checkout` 命令从 stash 中检出 `.cpp` 文件。以下是一个示例脚本，它使用 `git stash show` 命令来获取 stash 中的 `.cpp` 文件列表，并逐个检出：

```bash
git stash show stash@{0} -- .cpp | git apply
```

这个命令会显示 stash@{0} 中所有 `.cpp` 文件的差异，并尝试应用这些差异到工作目录中。

3. **添加应用后的文件**：
应用 stash 中的更改后，你需要将这些更改添加到暂存区：

```bash
git add *.cpp
```

这个方法可能会有一些限制和风险：

- 如果 stash 中的 `.cpp` 文件在当前分支上不存在或者已经被修改，这可能会导致冲突。
- 使用 `git apply` 命令时，如果存在冲突，你需要手动解决这些冲突。
- 这个方法不会自动删除 stash，如果你想要删除应用后的 stash，需要手动运行 `git stash drop stash@{0}`。

## 冲突时强制使用 stash 的更改
1. **应用 stash 中的更改**：
   首先，尝试应用 stash 中的更改：
   ```bash
   git stash apply stash@{0}
   ```
   如果遇到冲突，Git 会提示你哪些文件存在冲突。

2. **解决冲突**：
   手动编辑冲突的文件，解决冲突后，你需要将这些文件标记为已解决。这可以通过添加冲突文件到暂存区来完成：
   ```bash
   git add <resolved-file>
   ```
   其中 `<resolved-file>` 是你解决冲突后的文件。

3. **强制应用 stash**：
   如果你想要强制使用 stash 中的版本，忽略本地的更改，可以使用以下命令：
   ```bash
   git checkout stash@{0} -- <file-path>
   ```
   这会用 stash 中的版本覆盖工作目录中的文件。请注意，这会丢弃本地对该文件的任何更改。

4. **删除 stash**：
   一旦冲突解决并且更改被应用，你可以删除 stash：
   ```bash
   git stash drop stash@{0}
   ```

## 高级用法

- **保存特定文件的更改**：
  你可以使用 `git stash push` 的 `-k` 选项来保留索引（即暂存区）的更改，而只 stash 工作目录中的更改：
  ```bash
  git stash push -k "optional message"
  ```
  或者，你可以使用 `git stash --include-untracked` 来 stash 未跟踪的文件。

- **保存和应用特定文件的更改**：
  你可以使用 `git stash push` 的 `--patch` 选项来交互式地选择要 stash 的文件：
  ```bash
  git stash push --patch
  ```
  然后你可以应用特定的 stash 中的文件：
  ```bash
  git stash apply --index stash@{n} -- "file1" "file2"
  ```

- **创建分支并应用 stash**：
  如果你想要在一个新分支上恢复 stash，你可以这样做：
  ```bash
  git stash branch new-branch
  ```
  Git 会自动应用 stash 并创建一个新分支。

## 注意事项

- **stash 与分支**：stash 是与分支无关的，你可以在任何分支上保存和应用 stash。
- **stash 与提交**：stash 不会记录在你的项目历史中，它是一个临时的保存点。
- **stash 与冲突**：如果你尝试应用一个 stash 到一个与之有冲突的工作目录，Git 会阻止应用并提醒你解决冲突。
- **stash 与清理**：当你 stash 了更改后，你的工作目录会回到干净的状态，就像你刚刚检出了最新的提交一样。

`git stash` 是一个强大的工具，可以帮助你管理临时的更改，保持工作目录的整洁，并在不同上下文之间灵活切换。

# git fetch
> [Git - git-fetch Documentation](https://git-scm.com/docs/git-fetch) 
> [Git Fetch | What is Git Fetch and How to Use it | Learn Git](https://www.youtube.com/watch?v=uEEcw1s_wWk&ab_channel=GitKraken) 

`git fetch` 是 Git 中用于从远程仓库获取更新的命令。它允许你下载远程分支和标签的最新更改，但不会自动合并这些更改到你的当前分支。

## 功能和用途

1. **获取远程更新**：`git fetch` 用于从远程仓库下载最新的提交、分支和标签信息。
2. **不自动合并**：与 `git pull` 不同，`git fetch` 只是下载更新，不会自动合并到你的当前分支。这允许你在合并之前检查远程更改。
3. **更新远程跟踪分支**：`git fetch` 会更新本地的远程跟踪分支（如 `origin/master`），使其反映远程仓库的当前状态。

`git fetch` 是一个非常重要的 Git 命令，用于从远程仓库获取数据到你的本地仓库。这个命令不会改变你的工作目录，它只是将远程仓库的最新状态下载到你的本地仓库中。

## **获取远程仓库的所有分支的最新状态**
```bash
git fetch origin
```
这里 `origin` 是远程仓库的默认名称。这个命令会获取 `origin` 上所有分支的最新状态，并将它们存储为远程分支（如 `origin/master`）。

## **获取特定远程分支的最新状态**
```bash
git fetch origin develop
```
这个命令只会获取 `origin` 远程仓库的 `develop` 分支的最新状态。

### **在当前 `develop` 分支上执行 `git fetch origin develop`**
这个命令是合法的，并且通常会执行以下操作：
- 从远程 `origin` 仓库拉取 `develop` 分支的最新内容。
- 更新本地的远程分支引用 `origin/develop`。
- 如果你在本地 `develop` 分支上，Git 会将远程的 `develop` 分支的最新内容与本地的 `develop` 分支进行比较，但不会自动合并或重写你的本地提交历史。

## **获取远程特定分支并映射到本地分支**
**`git fetch origin develop:develop`**：
这个命令是一个带有特定参数的 `git fetch` 命令，它执行了一个特定的操作，称为“分支映射”（branch mapping）。这里的 `origin develop:develop` 表示从远程的 `origin` 仓库的 `develop` 分支拉取内容，并与本地的 `develop` 分支进行关联。这样做的好处是，你可以只更新特定的远程分支到本地，而不影响其他分支。这个命令实际上执行了两个步骤：
- 首先，它会从远程仓库拉取 `develop` 分支的最新内容，即 `:` 前的分支，`:` 前表示 src，即拉取的来源。
- 然后，它会将拉取的内容与本地的 `develop` 分支进行关联，这样你就可以通过 `git merge origin/develop` 或 `git rebase origin/develop` 将这些更改合并到本地分支。

**在当前 `develop` 分支上执行 `git fetch origin develop:develop`** 命令尝试将远程的 `develop` 分支映射到本地的 `develop` 分支，但当你已经在本地的 `develop` 分支上时，Git 会拒绝这个操作，因为它不想覆盖你当前的工作。Git 的这个限制是为了防止潜在的数据丢失，特别是当你的本地分支落后于远程分支时。

如提示错误信息 `fatal: refusing to fetch into branch 'refs/heads/develop' checked out at 'E:/src_git/demo'` 就是 Git 拒绝执行这个操作的提示。

为了避免这个问题，你可以采取以下步骤：

- **切换到其他分支**：在执行 `git fetch origin develop:develop` 之前，先切换到其他分支，比如 `master` 或者一个新的临时分支。

  ```bash
  git checkout master
  ```

  或者创建并切换到一个新的分支：

  ```bash
  git checkout -b temp_branch
  ```

- **执行 `git fetch`**：在其他分支上执行 `git fetch origin develop:develop`。

  ```bash
  git fetch origin develop:develop
  ```

- **切换回 `develop` 分支**：完成 `git fetch` 后，切换回 `develop` 分支。

  ```bash
  git checkout develop
  ```

- **合并或重新基线**：如果你想将远程 `develop` 分支的更改合并到本地 `develop` 分支，可以使用 `git merge` 或 `git rebase` 命令。

  ```bash
  git merge origin/develop
  ```

  或者

  ```bash
  git rebase origin/develop
  ```

## 使用场景

1. **保持本地分支与远程同步**：
   ```bash
   git fetch origin
   git checkout feature-x
   git merge origin/feature-x
   ```
   这个流程确保你在本地 `feature-x` 分支上合并了远程分支的最新更改。

2. **准备拉取最新更改**：
   在准备开始工作之前，拉取远程仓库的最新更改，以便本地仓库包含最新的提交。
   ```bash
   git fetch origin
   ```
   这个命令让你可以看到远程分支的最新状态，但不会自动合并到你的当前分支。

3. **检查远程分支的提交**：
   如果你想要查看远程分支上有哪些新的提交，但不打算立即合并它们：
   ```bash
   git fetch origin
   git log origin/develop..
   ```
   这个命令会显示从本地 `develop` 分支落后于远程 `origin/develop` 分支的所有提交。

4. **处理冲突前的准备**：
   在合并远程分支之前，检查是否会有冲突：
   ```bash
   git fetch origin
   git diff --name-only origin/develop
   ```
   这个命令会显示本地 `develop` 分支和远程 `origin/develop` 分支之间的差异，帮助在合并之前识别潜在的冲突。

## 选项

- **`--all`**：从所有远程仓库获取更新。
- **`--prune`**：清除远程跟踪分支中不再存在于远程仓库的分支。
- **`--dry-run`**：模拟获取更新的过程，但不实际下载数据。
- **`--verbose`**：显示详细的输出，包括下载过程中的信息。

### --dry-run 选项
`git fetch --dry-run` 命令用于模拟执行 `git fetch` 操作，但实际上不会改变任何东西。这个选项在 Git 中并不常用，因为 `git fetch` 本身就是一个“安全”的操作，不会改变工作目录，所以通常不需要模拟。但是，如果你想查看即将被拉取的提交，可以使用 `git fetch --dry-run` 来查看。

### --prune
`git fetch --prune` 是一个Git命令，用于在从远程仓库获取最新信息的同时，删除本地引用的远程分支，如果这些分支已经从远程仓库中删除。

也可以进行配置：
```bash
git config --global fetch.prune true
```

1. **功能**：
   - `git fetch --prune` 命令的功能是获取远程仓库的最新状态，并同步到本地。同时，它会检查本地的远程分支引用，如果远程分支已经被删除，那么对应的本地引用也会被删除。

2. **使用场景**：
   - 当在一个团队中工作时，可能会有分支被合并后删除，或者不再需要的分支被移除。使用 `git fetch --prune` 可以确保你的本地仓库不会保留这些已经不存在的远程分支的引用。

3. **命令组合**：
   - `git fetch --prune` 实际上等同于先执行 `git fetch --all` 来获取所有远程分支的最新状态，然后执行 `git remote prune origin` 来删除那些在远程仓库中已经不存在的分支的本地引用。

4. **配置自动修剪**：
   - 你可以通过配置Git的全局变量或远程仓库的特定设置来实现每次执行 `git fetch` 或 `git pull` 命令时自动修剪已删除的分支。这可以通过设置 `fetch.prune` 或 `remote.<name>.prune` 来实现。

5. **修剪标签**：
   - 与 `git fetch --prune` 类似，`git fetch --prune-tags` 可以用于删除那些在远程仓库中不存在的本地标签引用。

6. **命令效果**：
   - 使用 `git fetch --prune` 后，Git会自动检测远程仓库中已删除的分支，并将其从本地仓库中清除，保持本地和远程仓库的一致性。

7. **注意事项**：
   - 使用 `git fetch --prune` 时，只有在远程仓库的refspec（参考规范）中包含对应的规则时，本地的引用才会被删除。例如，如果远程仓库的refspec包括 `refs/tags/*:refs/tags/*`，那么本地不存在的远程标签也会被删除。

8. **命令示例**：
   - 要清理所有远程仓库中已删除的分支，可以使用 `git fetch --prune origin`。
   - 如果只想修剪特定的远程仓库，可以指定远程仓库的名字，如 `git fetch --prune <remote_name>`。

## 使用场景

- **检查远程更改**：在合并远程更改之前，使用 `git fetch` 检查远程仓库的最新状态。
- **更新远程跟踪分支**：定期使用 `git fetch` 更新本地的远程跟踪分支，以保持与远程仓库的同步。
- **避免合并冲突**：在合并远程更改之前，使用 `git fetch` 下载更新，然后手动检查和解决潜在的合并冲突。

# git push
> [Pushing commits to a remote repository - GitHub Docs](https://docs.github.com/en/get-started/using-git/pushing-commits-to-a-remote-repository) 
> [Git - git-push Documentation](https://git-scm.com/docs/git-push) 

`git push` 是一个将本地 Git 仓库的更改（提交）推送到远程仓库的命令。在 Git 的分布式版本控制模型中，每个开发者都有自己的本地仓库，并且通常也会有至少一个共享的远程仓库，通常是在服务器上。`git push` 命令使得开发者可以将本地的更改分享给其他团队成员。

- **同步更改**：当你在本地仓库完成一系列提交后，你可能希望将这些更改同步到远程仓库，以便其他团队成员可以看到和使用这些更改。
- **备份**：推送到远程仓库也是备份你的代码的一种方式，以防本地仓库损坏或丢失。
- **协作**：在团队项目中，多个开发者可能在不同的分支上工作。`git push` 允许他们分享自己的进度，并在远程仓库中合并更改。

当运行 `git push` 命令时，Git 会尝试将指定的本地分支的更改推送到远程仓库。如果远程仓库中没有对应的分支，Git 会为你创建一个。

## **推送到远程仓库**
```bash
git push <remote> <branch>
```
- `<remote>`：远程仓库的名称，通常是 `origin`，但也可以是任何你在 `git remote` 中设置的远程仓库名称。
- `<branch>`：你想要推送的本地分支的名称。

## **推送到远程仓库的特定分支**
如果你想要推送到远程仓库的特定分支，而不是本地分支的同名分支，你可以使用：
```bash
git push <remote> <local-branch>:<remote-branch>
```

## **设置本地分支跟踪远程分支**
使用 `-u` 选项，你可以设置本地分支跟踪远程分支，这样后续的推送和拉取都会更加方便：
```bash
git push -u origin <branch>
```

## **推送所有本地分支**
如果你想要推送所有本地分支到远程仓库，可以使用：
```bash
git push --all <remote>
```

## **推送所有标签**
如果你想要推送所有本地标签到远程仓库，可以使用：
```bash
git push --tags <remote>
```

## **强制推送**
如果你需要覆盖远程仓库的历史（这通常是不推荐的做法，因为它会导致其他人丢失工作），可以使用 `--force` 选项：
```bash
git push --force <remote> <branch>
```
或者，如果你使用的是 Git 2.0 或更高版本，可以使用更安全的 `-f` 选项：
```bash
git push -f <remote> <branch>
```

## **删除远程分支**
如果你想要删除远程仓库中的分支，可以使用：
```bash
git push <remote> --delete <branch>
```
或者：
```bash
git push <remote> :<branch>
```

## **推送特定提交**
如果你想要推送某个特定的提交到远程分支，可以使用：
```bash
git push <remote> <commit>:<branch>
```

## 推送冲突
- 如果你尝试推送到的远程分支有你本地分支没有的提交，Git 会阻止推送，以防止覆盖远程仓库的历史。你需要先拉取远程分支的更改并解决任何冲突，然后再尝试推送。

# git pull
> [Git - git-pull Documentation](https://git-scm.com/docs/git-pull) 

`git pull` 是 Git 中的一个命令，用于将远程仓库的更改拉取到本地仓库。它实际上是一个组合命令，等同于 `git fetch` 后跟 `git merge`。

1. **`git pull`：** 这个命令会从默认的远程仓库（通常是 `origin`）和默认分支（通常是你的当前分支）拉取最新的更改，并尝试与你的本地分支合并。

2. **`git pull <remote-name>`：** 指定从哪个远程仓库拉取更改。`<remote-name>` 是远程仓库的名称，例如 `origin`。

3. **`git pull <remote-name> <branch-name>`：** 指定从哪个远程仓库的哪个分支拉取更改。`<branch-name>` 是远程分支的名称。

`git pull` 是一个常用的 Git 命令，用于将远程仓库的更改合并到当前分支中。它实际上是 `git fetch` 和 `git merge` 的组合。以下是 `git pull` 的详细讲解和常用参数：

## **从远程仓库拉取最新代码并合并到当前分支**
```bash
git pull origin master
```
这个命令会从远程仓库 `origin` 的 `master` 分支拉取最新的代码，并尝试与当前分支合并。

## **省略远程分支名**
如果当前分支已经设置跟踪远程分支，可以省略远程分支名：
```bash
git pull origin
```
这个命令会将远程分支的更新合并到当前分支。

## **省略远程仓库和分支名**
如果当前分支只跟踪一个远程分支，可以完全省略参数：
```bash
git pull
```
这个命令会合并唯一跟踪的远程分支的更新到当前分支。

## **--rebase**
使用 `rebase` 代替 `merge` 来合并更改：
```bash
git pull --rebase origin master
```
这个命令会将本地更改重新应用到拉取的远程更改之上，保持提交历史的线性。

## **--ff-only**
只允许快进式合并，不允许产生新合并提交：
```bash
git pull --ff-only origin master
```
如果无法进行快进式合并，命令会失败。

## **--no-rebase**
覆盖配置选项，强制使用 `merge` 而不是 `rebase`：
```bash
git pull --no-rebase origin master
```

## **--no-commit**
拉取后不自动提交合并的结果：
```bash
git pull --no-commit origin master
```
这个参数在需要进一步审查和修改合并结果时很有用。

## **--allow-unrelated-histories**
允许合并没有共同历史记录的分支：
```bash
git pull --allow-unrelated-histories origin master
```

## **--tags**
拉取远程仓库的标签：
```bash
git pull --tags origin master
```

## **--prune**
拉取后清除本地不存在于远程仓库的分支：
```bash
git pull --prune origin master
```

## **--recurse-submodules**
递归地拉取和更新子模块：
```bash
git pull --recurse-submodules origin master
```

## **--depth**
指定拉取的历史记录深度，减少拉取的数据量，加快拉取速度：
```bash
git pull --depth=1 origin master
```

## **--verbose**
详细输出拉取的过程：
```bash
git pull --verbose origin master
```

## **--progress**
显示拉取进度：
```bash
git pull --progress origin master
```

## 工作原理

- **`git fetch`：** `git pull` 首先执行 `git fetch`，从远程仓库获取最新的分支和数据，但不会自动合并到你的当前分支中。这一步确保你的本地仓库知道远程仓库的最新状态。

- **`git merge`：** 在获取了远程分支的最新数据后，`git pull` 会执行 `git merge`，将远程分支的更改合并到你的本地分支中。如果合并过程中出现冲突，你需要手动解决这些冲突。

## 合并冲突处理

**合并冲突：** 如果远程分支的更改与你的本地更改冲突，`git pull` 会停止并要求你解决冲突。解决冲突后，你需要提交这些更改以完成合并。 如远程和本地对同一个文件的同一行进行修改，本地 git pull:
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
在上面代码片段中，`test01` 文件发生了冲突。冲突发生在 `HEAD`（你的本地分支）和远程分支 `c8d5a8479666ce11a479c2ed9568bde02dc17257` 之间。以下是冲突的标记：

- `<<<<<<< HEAD`：标记冲突的开始，以下是本地分支的代码。
- `=======`：分隔符，标记远程分支的代码开始。
- `>>>>>>> c8d5a8479666ce11a479c2ed9568bde02dc17257`：标记冲突的结束，以上是远程分支的代码。

要解决这个冲突，需要决定保留哪些更改，打开冲突文件，编辑，删除上面的冲突标记行。

# git rebase
> [Git - Rebasing](https://git-scm.com/book/en/v2/Git-Branching-Rebasing) 

## git rebase --onto
`git rebase --onto` 是一个强大的 Git 命令，它允许你将一系列提交从一个分支重新应用到另一个分支上。这个命令特别有用，当你想要将一个特性分支上的特定提交应用到另一个分支上，而不希望在目标分支上保留这些提交的原始提交记录。

`git rebase --onto <newbase> <since> <onto>`

- `<newbase>`：目标分支，你想要将提交应用到这个分支上。
- `<since>`：起始提交，你想要从这个提交开始重新应用。
- `<onto>`：结束提交，你想要到这个提交结束重新应用。

当你执行 `git rebase --onto B A` 命令时，Git 会做以下事情：

1. **找到共同祖先**：Git 会找到分支 A 和分支 B 的共同祖先提交。
2. **暂存提交**：从共同祖先提交开始，Git 会暂存分支 A 上的所有提交。
3. **重置分支 A**：Git 会将分支 A 重置到共同祖先提交。
4. **重新应用提交**：Git 会将暂存的提交重新应用到分支 B 的顶部。

假设你有两个分支：`master` 和 `feature`。`feature` 分支基于 `master` 分支的某个提交 A 分叉出去，并在 A 之后做了几个提交 B、C 和 D。现在你想要将 B、C 和 D 这三个提交应用到 `master` 分支上，但不保留这些提交的原始记录。

1. **切换到 `feature` 分支**：
   ```bash
   git checkout feature
   ```

2. **执行 `git rebase --onto` 命令**：
   ```bash
   git rebase --onto master A feature
   ```
   这个命令的意思是：“从 `feature` 分支的起始提交 A 开始，将所有提交重新应用到 `master` 分支上。”

3. **结果**：
   - `feature` 分支上的提交 B、C 和 D 会被重新应用到 `master` 分支上，就像是直接在 `master` 分支上做的一样。
   - `feature` 分支本身不会改变，它的提交历史仍然包含 A、B、C 和 D。
   - `master` 分支现在包含了来自 `feature` 分支的更改，但是没有额外的合并提交记录。

### 注意事项

- 使用 `git rebase --onto` 时，如果重新应用的提交与目标分支有冲突，你需要解决这些冲突，然后继续变基过程。
- 这个命令会改变历史，所以如果你的分支已经推送到远程仓库，你应该避免使用这个命令，除非你确定不会影响其他人的工作。
- 如果你需要撤销变基操作，可以使用 `git rebase --abort` 命令。

通过这种方式，`git rebase --onto` 允许你在不合并提交记录的情况下，将一个分支上的更改应用到另一个分支上，使得项目的历史更加清晰和线性。

# git merge
> [Git - git-merge Documentation](https://git-scm.com/docs/git-merge) 

## --no-commit
> [Git - git-merge Documentation](https://git-scm.com/docs/git-merge#Documentation/git-merge.txt---no-commit) 

## --ff

## --squash

## --aboart

## --continue

## -X 合并策略
> [Git - git-merge Documentation](https://git-scm.com/docs/git-merge#_merge_strategies) 

### ort





# git prune
> [Git - git-prune Documentation](https://git-scm.com/docs/git-prune) 

# 分支共同祖先
> [Git - git-merge-base Documentation](https://git-scm.com/docs/git-merge-base#_discussion) 

Git 中的共同祖先（common ancestor）是指两个分支之间最后一个共有的提交。
```
A <- B <- C (master)
 \
  D <- E <- F (feature)
```

- `A` 是共同祖先，因为它是 `master` 和 `feature` 分支在分叉之前共享的最后一个提交。
- `B` 是 `master` 和 `feature` 分支分叉后的第一个提交，它是两个分支共有的。
- `C` 是 `master` 分支独有的提交。
- `D`、`E`、`F` 是 `feature` 分支独有的提交。


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

# 切换到远程仓库的新分支

## 1. 获取远程分支列表

获取远程仓库的最新分支列表：

```bash
git fetch --all
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (main)
$ git fetch --all
From https://github.com/lxwcd/git_test
 * [new branch]      remote_branch01 -> origin/remote_branch01
```

这个命令会从所有配置的远程仓库获取更新，但不会自动合并到你的当前分支。它会更新本地的远程跟踪分支，使其反映远程仓库的当前状态。

## 2. 列出远程分支

接下来，可以列出所有远程分支，以确认新添加的分支名称：

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

# 合并到错误的分支解决
案例：本地从 develop 分支新建一个 bug01 分支解决 bug，但合并时错误的合并到 main 分支并推送到远程仓库。

## 步骤 1: 确定错误的提交

首先，你需要确定合并到 `main` 分支的提交的哈希值。你可以使用 `git log` 查看提交历史：

```bash
git log origin/main
```
## 步骤 2: 从 `main` 分支中移除提交

你可以选择强制推送一个没有该提交的新的历史到 `main` 分支。这可以通过 `git reset` 和 `git push --force` 来完成：

```bash
git checkout main
git reset --hard <正确的提交哈希值>
git push origin main --force
```

**警告**：`git push --force` 是一个危险的操作，因为它会重写远程分支的历史。只有在你完全确定需要这么做，并且没有其他人正在基于这个分支工作时才使用。

如果不介意保留历史，可以用 git revert：
```bash
git checkout main
git log
git rever <错误的提交哈希值>
git add
git commit
```
这样不会修改历史，而是重新添加一个提交

## 步骤 3: 将更改合并到 `develop` 分支

```bash
git checkout develop
git merge main
git push origin develop
```
也可以直接将本地 bug01 分支推送到远程的 develop 分支。
或者用 git cherry-pick。

## 步骤 4: 检查远程仓库

最后，检查远程仓库以确保 `main` 和 `develop` 分支现在的状态是正确的：

```bash
git log origin/main
git log origin/develop
```

## 替代方案：使用 `git revert`

如果你不想重写历史，另一个选择是使用 `git revert` 来撤销对 `main` 分支的合并：

```bash
git checkout main
git revert --no-commit <错误的提交哈希值>
git commit -m "Revert incorrect merge"
git push origin main
```

这将创建一个新的提交，撤销了错误的合并更改，然后你可以将这个撤销操作推送到远程的 `main` 分支。

## 如果 main 分支错误合并后有新的提交记录
如果 `main` 分支在错误合并之后又有新的提交，而你希望撤销中间的某个特定合并，同时又不影响后面的提交，你可以使用 `git revert` 来逐个撤销不需要的提交。`git revert` 会创建一个新的提交，它包含被撤销更改的内容，因此不会影响分支上的其他提交。

### 步骤 1: 确定要撤销的提交

首先，使用 `git log` 查看 `main` 分支的提交历史，并找到你希望撤销的合并提交的哈希值：

```bash
git log origin/main
```

### 步骤 2: 使用 `git revert` 撤销提交

对于每个需要撤销的提交，执行 `git revert` 命令。假设你找到了需要撤销的提交的哈希值是 `<commit-hash>`：

```bash
git checkout main
git revert <commit-hash>
```

这会创建一个新的提交，它撤销了 `<commit-hash>` 提交所做的更改。如果撤销过程中出现冲突，你需要解决这些冲突，并完成撤销提交：

```bash
# 解决可能出现的冲突
git add <resolved-files>
# 完成 revert 提交
git commit --no-edit
```

### 步骤 3: 推送更改到远程仓库

将这些撤销操作推送到远程 `main` 分支：

```bash
git push origin main
```

### 步骤 4: 重复撤销操作

如果需要撤销多个提交，重复步骤 2 和步骤 3，直到所有需要撤销的提交都被撤销。

### 注意事项

- 使用 `git revert` 撤销提交时，每次只能撤销一个提交。如果需要撤销多个提交，你需要对每个提交重复执行 `git revert` 命令。
- `git revert` 会创建新的提交，因此不会影响分支上的其他提交。这是它与 `git reset` 的主要区别，后者会重写历史。
- 在执行 `git revert` 之前，最好与团队成员沟通，确保撤销操作不会干扰到其他人的工作。
- 如果你不确定哪些提交需要被撤销，可以使用 `git log` 查看每个提交的详细信息，包括合并提交和它们的描述。

通过这种方式，你可以安全地撤销 `main` 分支上的特定合并，而不影响分支上的其他提交。

# 保存不能提交但修改的特定文件
有些文件被修改，但不能提交到远程仓库，每次切换分支或者合并总提示，可以 git stash 保存，
因为操作频繁，可以创建别名，如在 git bash 中 `$HOME/.bashrc` 中创建别名：
```bash
alias stashTempFiles='git diff --name-only | grep -E "\.(suo|bin)$" | xargs git stash save "save .suo and .bin files which can't commit"'
```

# 本地开发需要用测试代码
- 本地拉取最新的代码到主分支，然后以此新建
- 编写测试代码，git stash 保存

# 合并本地分支但不产生新的提交
将本地一个分支 A  合并到本地 分支 B，分支 A 多了一些提交，希望合并到 B 后不要这些提交记录。

## git rebase --onto
如果希望将本地分支 A 合并到本地分支 B，并且不希望在分支 B 的合并历史中保留分支 A 的提交记录，你可以使用 `git rebase` 命令将分支 A 上的更改“重新播放”到分支 B 上，然后再将分支 B 合并回它原来的位置。这样，分支 A 的更改就像是直接在分支 B 上做的一样，不会有额外的合并提交记录。

1. **切换到分支 B**：
   ```bash
   git checkout B
   ```

2. **将分支 A 变基到分支 B 上**：
   首先，你需要确保分支 A 上的更改是最新的。然后，使用 `git rebase` 将分支 A 上的更改变基到分支 B 上：
   ```bash
   git rebase --onto B A
   ```
   这个命令会将分支 A 上的更改重新应用到分支 B 的顶部。这里的 `--onto` 选项指定了目标基底分支（这里是分支 B），而 A 是当前分支。

3. **解决可能出现的冲突**：
   如果变基过程中出现冲突，你需要手动解决这些冲突。解决冲突后，使用以下命令添加更改并继续变基：
   ```bash
   git add .
   git rebase --continue
   ```
   如果一切顺利，没有冲突，那么分支 A 上的更改就会被应用到分支 B 上，而不会有额外的合并提交。

4. **快进合并分支 B**：
   由于分支 A 的更改已经被“重新播放”到分支 B 上，你现在可以简单地使用 `git merge` 命令将分支 B 合并回它原来的位置，这将是一个快进合并，不会产生新的合并提交：
   ```bash
   git checkout A
   git merge B
   ```

5. **推送更改**：
   如果你需要将这些更改推送到远程仓库，可以使用以下命令：
   ```bash
   git push origin A
   git push origin B
   ```

请注意，如果你的分支已经推送到远程仓库，并且其他人可能基于这些分支进行了工作，那么你应该避免使用 `git rebase`，因为这会改变历史。如果确实需要这样做，你需要使用 `--force` 选项来推送更改，但这可能会影响其他人的工作。在这种情况下，最好与团队成员沟通，以确保所有人都了解这些更改。

## git merge --squash
如果你希望通过合并的方式将分支 A 的内容合并到分支 B，同时又不想在分支 B 上产生新的提交记录，你可以使用 `git merge` 命令的 `--squash` 选项。这样可以将分支 A 的所有提交压缩成单个提交，或者直接将更改应用到分支 B 上而不创建新的提交。

1. **切换到分支 B**：
   ```bash
   git checkout B
   ```

2. **合并分支 A 并压缩提交**：
   ```bash
   git merge --squash A
   ```
   这个命令会将分支 A 自上次合并以来的所有提交压缩成单个更改集，但不创建新的提交。你的工作目录将包含所有分支 A 的更改，但这些更改尚未被提交。

3. **（可选）提交更改**：
   如果你对合并的更改满意，可以手动提交这些更改到分支 B：
   ```bash
   git commit -m "Merge changes from A without commit history"
   ```
   这将创建一个新的提交，它包含了分支 A 的所有更改。

### 注意事项

- 使用 `git merge --squash` 时，你可以选择不提交合并的更改，这样就不会在分支 B 上产生新的提交记录。
- 快进合并不会在分支历史中添加新的提交，但它要求分支 B 能够直接快进到分支 A，这意味着分支 A 必须是分支 B 的直接上游。
- 如果你不想保留任何合并记录，确保在合并前没有未提交的更改，因为未提交的更改总是需要被提交。

## git rebase --onto 和 git merge --squash 区别
`git merge --squash` 和 `git rebase --onto` 都可以用来将一个分支的更改合并到另一个分支，同时避免产生额外的提交记录。但是，它们在实现方式和使用场景上有一些区别：

### git merge --squash

1. **合并但不创建新提交**：
   `git merge --squash` 将另一个分支上的更改合并到当前分支，但不创建一个新的合并提交。所有合并的更改都处于暂存状态，你可以检查这些更改，然后手动创建一个提交。

2. **非线性历史**：
   使用 `git merge --squash` 不会改变项目的历史记录，它只是在当前分支上复制了另一个分支的更改。

3. **简单易用**：
   这个命令比较简单直接，不需要考虑分支的基底（base）问题，适合快速合并更改。

4. **适用于**：
   当你想要将某个分支上的更改合并到当前分支，并且不希望在当前分支上保留合并分支的提交历史时。

### git rebase --onto

1. **变基和重新应用**：
   `git rebase --onto` 将一个分支上的提交重新应用到另一个分支上，实际上是在进行变基操作。这个命令会将一个分支上的提交“移植”到另一个分支的顶部。

2. **线性历史**：
   使用 `git rebase --onto` 会创建一个线性的提交历史，它改变了项目的历史记录，使得所有提交都看起来像是在另一个分支上直接进行的。

3. **复杂的操作**：
   这个命令相对复杂，需要考虑多个分支之间的关系，并且可能会涉及到解决冲突。

4. **适用于**：
   当你想要将一个特性分支的更改移植到另一个分支上，并且希望保持一个清晰的线性历史时。

### 主要区别

- **历史改变**：
  `git rebase --onto` 会改变历史，因为它实际上是在重写提交。而 `git merge --squash` 不会改变历史，它只是在当前分支上复制了另一个分支的更改。

- **冲突处理**：
  在使用 `git rebase --onto` 时，如果出现冲突，你需要解决冲突并继续变基。而在 `git merge --squash` 中，如果出现冲突，你只需要解决冲突然后提交更改。

- **安全性**：
  `git rebase --onto` 因为会改变历史，所以如果你的分支已经被推送到远程仓库，使用这个命令可能会影响其他人的工作。`git merge --squash` 更安全，因为它不会改变历史。

- **使用场景**：
  `git rebase --onto` 适合在特性分支开发过程中，将特性分支的更改移植到主分支上。`git merge --squash` 适合在准备将特性分支合并到主分支时，快速合并更改而不产生新的提交记录。

# git status 过滤 - 只显示文件名 
`git status --porcelain | cut -d" " -f3-`
1. `git status --porcelain` 命令以一种格式化的方式输出当前 Git 仓库的状态信息。
2. 这个输出被传递给 `cut` 命令，该命令使用空格作为分隔符。
3. `cut` 命令提取每一行的第三个字段及其后的所有字段，这些字段通常包含文件名和可能的状态信息。

## git status --porcelain

`git status` 命令用于显示当前 Git 仓库的状态，包括未跟踪的文件、已修改但未暂存的文件，以及已暂存的文件。

- `--porcelain` 选项是 `git status` 命令的一个输出选项，它生成一种易于脚本解析的输出格式。在这种模式下，输出被设计成机器可读的格式，而不是为人类阅读设计的。这个选项对于自动化脚本和工具特别有用。

## | (管道)

管道符号（`|`）用于将一个命令的输出作为另一个命令的输入。在这个命令组合中，`git status --porcelain` 的输出被传递给 `cut` 命令。

## cut -d" " -f3-

`cut` 是一个文本处理工具，用于从输入文本中提取特定的字段。

- `-d" "` 选项指定字段的分隔符。在这里，`" "`（空格）被指定为字段分隔符，意味着 `cut` 命令将使用空格来分割每一行的输入。

- `-f3-` 选项指定要提取的字段范围。`-f` 表示字段（field），而 `3-` 表示从第三个字段到最后一个字段的所有字段。在这个上下文中，这意味着 `cut` 命令将提取每一行的第三个字段及其后的所有字段。

## 示例
假设你有以下 Git 仓库状态：
```bash
$ git status --porcelain
 M README.md
?? NEWFILE.txt
```

当你运行 `git status --porcelain | cut -d" " -f3-` 时，输出将是：

```bash
README.md
NEWFILE.txt
```
这里，`cut` 命令提取了每个状态行的第三个字段及其后的所有字段，即文件名。

# git status 过滤 - 筛选特定文件 

## 筛选路径包含特定文件夹的文件
```bash
git status --porcelain | cut -d" " -f3- | grep -E "*/demo/*"
```

## 筛选特定后缀的文件
```bash
git status --porcelain | cut -d" " -f3- |  grep -E "\.(cpp|h)$"
```

# git stash 过滤文件保存
```bash
git status --porcelain | cut -d" " -f3- | grep -E "*/demo/*" | xargs git stash push -m "stash demo files" --
```

# git add 过滤 - 筛选路径包含特定文件夹的文件
```bash
git diff --name-only | grep -E "*/demo/*" | xargs git add --
```

# 忽略本地已经被跟踪文件的修改
> [How to ignore files already managed by Git: how to use assume-unchanged and skip-worktree](https://tips.madoromi.org/en/git-ignore-assume-unchanged-skip-worktree/) 

## skip-worktree
`git skip-worktree` 是一个 Git 属性，用于控制 Git 如何处理特定文件或目录的更改。这个属性可以用来优化仓库性能，或者在多个分支间共享文件时避免不必要的冲突。

`skip-worktree` 是一个文件级别的属性，当你设置一个文件为 `skip-worktree` 时，Git 会停止跟踪该文件在本地工作目录中的更改。这意味着即使文件被修改，Git 也不会认为它是“已修改”的状态，也不会包括在下次提交中，除非你明确地告诉 Git 这样做。

- **用途**：`skip-worktree` 命令用于将文件标记为忽略工作树中的更改，但仍会进行某些操作。这适用于那些需要在本地修改但不希望这些更改被提交到远程仓库的场景，比如配置文件。
- **行为**：与 `assume-unchanged` 不同，`skip-worktree` 会保留本地的更改，即使这些更改与远程仓库中的版本不同。这意味着，当你执行 `git pull` 或 `git push` 时，Git 会尽量维护你的本地更改，而不是覆盖它们。
- **取消**：可以通过 `git update-index --no-skip-worktree <file>` 命令来取消 `skip-worktree` 标记，恢复对文件的跟踪。

### 设置 `skip-worktree`

```bash
git update-index --skip-worktree <file>
```

这个命令会更新索引，告诉 Git 忽略 `<file>` 文件的本地更改。

### 取消 `skip-worktree`

如果想要重新开始跟踪文件的更改，可以使用以下命令取消 `skip-worktree` 属性：

```bash
git update-index --no-skip-worktree <file>
```

### 使用远程最新的版本
```bash
git update-index --no-skip-worktree <file>
git pull
```

### 查看所有被 `skip-worktree` 的文件

要查看哪些文件被设置了 `skip-worktree` 属性，可以使用 `git ls-files` 命令：

```bash
git ls-files -v | grep '^S'
```

这将列出所有被 Git 跟踪的文件，以及它们各自的属性。带有 `S` 前缀的文件表示被设置了 `skip-worktree` 属性。

### 查看某个文件是否被 `skip-worktree`
```bash
git ls-files -v | grep '^S' | grep 'file.cpp'
```

### 使用场景

1. **性能优化**：对于大型文件或二进制文件，频繁的提交可能会降低性能。通过设置 `skip-worktree`，可以避免这些文件的更改被跟踪，从而提高性能。

2. **跨分支共享文件**：如果你有多个分支需要共享某些文件，但又不希望这些文件的更改在分支间传播，可以使用 `skip-worktree` 来避免冲突。

3. **忽略特定文件更改**：在某些情况下，你可能不希望跟踪某些文件的更改，例如自动生成的配置文件或日志文件。

4. **配置文件**：当你的主仓库中包含了一些生产就绪的配置文件，而你不想不小心提交对这些文件的更改时，使用 `skip-worktree` 是一个很好的选择。

5. **本地环境依赖**：开发时，可能需要的开发环境部分配置与测试及生产环境不一样，如数据库配置，需要手动修改，又不想把修改过的配置文件提交，这时候可以使用 `skip-worktree`。

### 注意事项

- **冲突处理**：如果你在本地对一个设置了 `skip-worktree` 的文件进行了更改，并且这些更改与远程仓库中的更改冲突，Git 在下次拉取时可能会报告冲突。你需要手动解决这些冲突。
当执行 `git pull` 并且远程的更改与本地的更改发生冲突时，Git 会识别这些冲突并通知用户。即使文件被标记为 `skip-worktree`，Git 仍然会识别出冲突，因为 `skip-worktree` 只影响文件状态的跟踪，并不会影响合并过程。Git 会提示哪些文件有冲突，并需要用户手动解决这些冲突。

总结来说，即使文件被标记为 `skip-worktree`，远程的修改仍然可以被拉取到本地，并且在发生冲突时，Git 能够识别并提示用户解决这些冲突。

- **分支切换**：当你切换到另一个分支时，Git 会尝试应用 `skip-worktree` 文件的远程版本，这可能会覆盖你的本地更改。如果你有未提交的更改，最好在切换分支之前提交它们。

- **远程仓库影响**：`skip-worktree` 属性只影响本地仓库。当你推送更改到远程仓库时，这个属性不会推送，所以其他协作者不会自动应用这个设置。

- **与其他 Git 属性的关系**：`skip-worktree` 与 `assume-unchanged` 类似，但 `assume-unchanged` 用于告诉 Git 一个文件没有被修改，即使它实际上已经被修改了。`skip-worktree` 则用于告诉 Git 忽略文件的修改。

通过使用 `git skip-worktree`，你可以更精细地控制 Git 如何处理工作目录中的文件，这对于管理大型项目或处理特定类型的文件非常有用。

## git assume-unchanged
- **用途**：这个命令告诉 Git 忽略对某个文件的更改，即使文件实际上已经被修改了。这可以用于提高性能，特别是在处理大文件或者不需要跟踪的文件时。
- **行为**：当一个文件被标记为 `assume-unchanged` 后，Git 会认为这个文件没有被修改，即使实际上文件内容已经发生了变化。这会导致 Git 在执行 `git status` 时不再显示这个文件为已修改状态。
- **取消**：可以通过 `git update-index --no-assume-unchanged <file>` 命令来取消 `assume-unchanged` 标记，恢复对文件的跟踪。
- **性能与用途**：`assume-unchanged` 通常用于优化性能，比如忽略那些不需要跟踪的大文件或者二进制文件；而 `skip-worktree` 更多用于处理需要在本地修改但不希望影响远程仓库的文件。
- **冲突处理**：在使用 `pull` 时，`assume-unchanged` 可能会导致本地更改被远程版本覆盖，而 `skip-worktree` 会尽量保留本地的更改。
- **文件状态**：`assume-unchanged` 会使得 Git 认为文件未被修改，而 `skip-worktree` 允许文件在本地被修改，但这些修改不会被 Git 跟踪。

`git update-index --assume-unchanged` 命令用于更新 Git 索引或暂存区，允许用户更改或更新索引中的文件状态信息。使用 `--assume-unchanged` 选项可以告知 Git 忽略某些已修改但未提交的文件。

### **标记文件为 assume-unchanged**
```bash
git update-index --assume-unchanged <file>
```
这会告诉 Git 忽略 `<file>` 文件的后续更改。

### **取消标记**
```bash
git update-index --no-assume-unchanged <file>
```
这会取消对 `<file>` 文件的 “假定未更改” 标记，并让 Git 开始跟踪和提交对该文件的更改。

### 查看被标记的文件
如果你想要查看哪些文件被标记为 `assume-unchanged`，可以使用以下命令：
```bash
git ls-files -v | grep "^h"
```
这会列出所有标记为 `assume-unchanged` 的文件，其中 `h` 表示文件被标记为 `assumed-unchanged`。

### 注意事项
- **标记只在本地有效**：`assume-unchanged` 标记只在本地有效，其他协作用户不会受到该标记的影响。
- **克隆或拉取时的标记丢失**：默认情况下，`git update-index –assume-unchanged` 命令不会将标记的文件保存到 Git 仓库中。因此，在克隆或拉取代码时，这些标记可能会丢失。如果你希望这些标记在克隆或拉取代码后依然有效，可以使用 `git update-index –skip-worktree` 命令来实现。

通过合理使用 `git assume-unchanged`，你可以更高效地处理代码版本控制，特别是在处理大型项目或需要优化性能的场景中。

### assume-unchanged 配置场景
`assume-unchanged` 用于优化性能，假定文件未更改，适用于那些不需要或不应该被更改的文件。例如：

- **大型二进制文件或 SDK**：对于大型二进制文件或者 SDK 这类不常更改的文件，使用 `assume-unchanged` 可以提高 Git 的性能。
- **不想跟踪的文件**：如果你有一些文件不想被 Git 跟踪更改，但又不想完全忽略它们（比如因为需要这些文件来构建项目），你可以使用 `assume-unchanged` 来告诉 Git 忽略这些文件的更改。

`skip-worktree` 更适合那些需要在本地更改但不希望这些更改影响到远程仓库的情况，而 `assume-unchanged` 更适合那些不需要更改的文件，用于提高性能和避免不必要的跟踪。

# 检出特定版本
## 使用 `git checkout` 检出对方的版本

如果你想要检出（即覆盖）当前分支上特定文件的版本，可以使用 `git checkout` 命令。以下是如何操作的：

```bash
git checkout <their-branch> -- <file-path>
```

这里 `<their-branch>` 是对方分支的名称，而 `<file-path>` 是你想要检出的文件的路径。这个命令会将指定文件从对方分支检出到你当前的工作目录，覆盖本地的版本。

## 使用 `git checkout` 检出提交的版本

如果你知道对方的具体提交哈希值，你也可以直接检出那个提交中的文件版本：

```bash
git checkout <commit-hash>^ -- <file-path>
```

这里 `<commit-hash>` 是对方提交的哈希值，`^` 符号表示父提交（即对方提交的前一个提交），而 `<file-path>` 是文件的路径。这个命令会检出指定提交中的文件版本。

## 使用 `git reset` 检出版本
你还可以使用 `git reset` 命令将文件重置为特定版本：

```bash
git reset <commit-hash> -- <file-path>
```

然后，你可以使用 `git checkout` 来检出这些文件：

```bash
git checkout -- <file-path>
```

## 查看两个分支之间提交日志的差异
### 查看分支 branch02 相对 branch01 有哪些新的提交
```bash
$ git log branch01..branch02 --oneline
34cf81fb9 (HEAD -> branch03) test03
8c5435155 test02
eecf45b89 test01
```

### 查看最下面一个提交所涉及的文件
```bash
$ git log develop..HEAD --oneline | tail -n 1 | awk '{print $1}' | xargs git show --name-only
commit eecf45b892ec8a5250636a30ad7af4ac7cc0e31b
Author: lx <15521168075@163.com>
Date:   Fri Jan 3 15:29:04 2025

    modify test code

demo/test.md
```

### 查看差异倒数第二个提交的文件修改状态
```bash
$ git log develop..HEAD --oneline | awk 'NR==2 {print$1}' | xargs git show --name-status
commit 8c54351552e0267726c82aa7b9f40357a883ee58
Author: lx <15521168075@163.com>
Date:   Mon Jan 6 15:10:04 2025

    add test text

M       demo/test.md
```
