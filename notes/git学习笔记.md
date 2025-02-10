git 学习  
        
# 学习资源  
> 初步了解 git：[廖雪峰 Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)  
> github 官方文档：[GitHub Docs](https://docs.github.com/en/get-started/quickstart/set-up-git)  
> git 命令官方文档：[git](https://git-scm.com/docs/)  
> git book：[Pro Git book](https://git-scm.com/book/en/v2)  
> [Learn Git Branching](https://learngitbranching.js.org/?locale=zh_CN)   
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
        
# git 密码认证失败解决  
> [Support for password authentication was removed. Please use a personal access token instead.](https://dev.to/shafia/support-for-password-authentication-was-removed-please-use-a-personal-access-token-instead-4nbk)  
    
在虚拟机中用 git push 时输入用户名和密码，直接输入 github 账号密码会提示失败，要用 token，见上面文章描述方法。  
    
# git bash 配置  
## 配置主题字体  
右键选择 option 进行配置，配置完成后保存即可  
  
## 修改时区  
  
先查看当前时间是否正确：  
```bash  
lxw@lx MINGW64 /e/src_git/demo (develop)  
$ date  
Fri Jan 17 06:41:27 GMT 2025  
```  
  
修改 `TZ` 变量，注意这里时区设置和 linux 中格式有区别 (linux 中国时区为 `Asia/Shanghai`)  
  
在 Windows 的 Git Bash 中，TZ 环境变量的格式通常为：  
```bash  
TZ=<标准时间>-<UTC偏移量><夏令时时间>-<夏令时UTC偏移量>  
```  
要设置中国时区（东八区），可以使用以下命令：  
```bash  
export TZ="CST-8"  
```  
  
永久修改则在配置文件中修改，如当前用户修改可在 `~/.bashrc` 中设置  
修改完后 `. ~/.bashrc` 时期生效，再用 date 命令查看，时区已修改成功：  
```bash  
lxw@lx MINGW64 /e/src_git/demo (develop)  
$ date  
Fri Jan 17 14:46:31 CST 2025  
```  
  
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
alias stashsuobin='git diff --name-only | grep -E "\.(suo|bin)$" | xargs git stash push -m ".suo and .bin files" '  
alias restoresuobin='git status --porcelain | cut -d" " -f3- |  grep -E "\.(suo|bin)$" | xargs git restore -- '  
alias checkSkipWorktree=' git ls-files -v | grep "^S"'  
  
alias addUnchanged='git update-index --assume-unchanged '  
alias cancelAllSkipWorktree='git ls-files -v | grep "^S" | cut -d" " -f2 | xargs git update-index --no-skip-worktree '  
alias cancelAllUnchangedSkipWorktree='git ls-files -v | grep "^[S|s]" | cut -d" " -f2 | xargs git update-index --no-skip-worktree '  
alias cancelSkipWorktree='git update-index --no-skip-worktree '  
alias cancelUnchanged='git update-index --no-assume-unchanged '  
alias checkDeletedLog='git fsck --unreachable | grep commit | cut -d" " -f3 | xargs git log --merges --no-walk --oneline '  
alias checkSkipWorktree='git ls-files -v | grep "^S" '  
alias checkUnchangedSkipWorktree=' git ls-files -v | grep "^[S|s]" '  
alias restoreStashCommit='git update-ref --create-reflog refs/stash '  
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
  
- Vim 的 `clipboard` 选项控制 Vim 如何使用系统剪贴板。通过设置这个选项，你可以让 Vim 的复制（yank）和粘贴（paste）操作直接与系统剪贴板进行交互。  
- `unnamedplus` 是 `clipboard` 选项的一个值，它告诉 Vim 使用系统剪贴板作为复制和粘贴操作的存储。在 Vim 中，`"+` 寄存器通常与系统剪贴板相关联，而 `unnamedplus` 使得这个寄存器的行为与系统剪贴板一致。  
- 当设置了 `set clipboard=unnamedplus`，Vim 会将复制（yank）操作的内容存储到 `"+` 寄存器，这个寄存器与系统剪贴板同步。因此，当你在 Vim 中复制文本时，它也会出现在系统剪贴板上，你可以在其他程序中粘贴。  
- 从系统剪贴板粘贴（paste）文本到 Vim 中时，Vim 会从 `"+` 寄存器读取内容。  
- 可以使用 `vim --version | grep clipboard` 命令来检查你的 Vim 是否支持剪贴板功能。如果输出中包含 `+clipboard`，则表示支持。  
  
# Git config 配置Git  
> [Git Config](https://www.gitkraken.com/learn/git/git-config)  
> [配置 git config](https://tsejx.github.io/devops-guidebook/code/git/config/)  
> [Git - git-config Documentation](https://git-scm.com/docs/git-config)   
  
```bash  
lxw@lx MINGW64 /e/doc/git_test (main)  
$ git config  
edit             get              list             remove-section   rename-section   set              unset  
```  
  
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
  
### 示例  
  
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
$ git config list --global  
```  
  
## 获取某个配置的信息  
```bash  
lxw@lx MINGW64 /e/doc/git_test (main)  
$ git config get --global diff.tool  
vimdiff  
```  
  
## 取消某个配置  
```bash  
lxw@lx MINGW64 /e/doc/git_test (main)  
$ git config unset --global diff.date  
```  
  
## 修改配置文件的路径  
修改 Git 配置文件的路径通常涉及到更改 Git 查找配置文件的位置。Git 配置文件有三个主要层级：系统级（system）、全局级（global）和项目级（local）。每个层级的配置文件路径可以通过环境变量或 Git 命令进行修改。  
  
确保新的配置文件路径是可访问的，并且 Git 有权限读取和写入这些文件。  
  
### 修改全局配置文件路径  
  
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
  
### 修改系统配置文件路径  
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
  
### 修改项目配置文件路径  
  
项目配置文件位于每个 Git 仓库的 `.git/config` 文件中。如果你想为特定项目指定不同的配置文件路径，可以使用 `git config` 命令的 `--file` 选项。  
  
- **指定配置文件**：  
  ```bash  
  git config --file /path/to/your/project/config --get core.editor  
  ```  
        
## 设置用户名和电子邮件  
```bash  
root@ubuntu2204c12:~# git config --global user.name "name"  
root@ubuntu2204c12:~# git config --global user.email "email@163.com"  
```  
  
## 设置初始默认分支名  
```bash  
sudo git config --system init.defaultBranch main  
```  
  
git config --global diff.date format:'%Y-%m-%d %H:%M:%S'  
  
## 修改 log 时区  
修改时区以便用 git log 查看日志时的时间和系统时间处于一个时区：  
```bash  
git config --global log.date=local  
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
```bash  
git config --global http.https://github.com.proxy socks5://127.0.0.1:7890  
```  
        
配置完查看：  
```bash  
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
lxw@lx MINGW64 /e/doc/git_test (main)  
$ git config list --global --show-origin  
file:C:/Users/lxw/.gitconfig    user.name=li-736  
file:C:/Users/lxw/.gitconfig    user.email=xiaowan.li@mt.com  
file:C:/Users/lxw/.gitconfig    diff.tool=vimdiff  
file:C:/Users/lxw/.gitconfig    log.date=local  
file:C:/Users/lxw/.gitconfig    core.pager=less  
file:C:/Users/lxw/.gitconfig    core.quotepath=false  
file:C:/Users/lxw/.gitconfig    gui.encoding=utf-8  
file:C:/Users/lxw/.gitconfig    i18n.commitencoding=utf-8  
file:C:/Users/lxw/.gitconfig    i18n.logoutputencoding=utf-8  
```  
  
`git config --show-origin` 是一个非常有用的命令，它允许你查看 Git 配置项及其来源文件。这个命令可以帮助你理解每个配置项是从哪个配置文件中读取的。  
  
- **显示配置来源**：`--show-origin` 选项用于显示每个配置项的来源，即配置项是从哪个文件中读取的。这包括文件路径、标准输入、blob 或命令行等来源。  
- **调试配置问题**：当你不确定某个配置项是从哪个文件中读取时，使用 `--show-origin` 可以帮助你找到答案。  
- **查看配置文件路径**：通过显示配置项的来源，你可以快速找到相关的配置文件路径。  
  
# Git 存储数据方式  
> [Git Internals Part 2: How does Git store your data?](https://www.developernation.net/blog/git-internals-how-does-git-store-your-data)  
> [Commits are snapshots, not diffs](https://github.blog/2020-12-17-commits-are-snapshots-not-diffs/)  
> [BASIC SNAPSHOTTING](http://git.github.io/git-reference/basic/)  
> [What is a git "Snapshot"?](https://stackoverflow.com/questions/4964099/what-is-a-git-snapshot)  
> [Is the git storage model wasteful?](https://stackoverflow.com/questions/7321360/is-the-git-storage-model-wasteful)  
> [Are Git's pack files deltas rather than snapshots?](https://stackoverflow.com/questions/5176225/are-gits-pack-files-deltas-rather-than-snapshots)  
> [Git Internals - Packfiles](https://git-scm.com/book/en/v2/Git-Internals-Packfiles)  
        
- In git, commits are snapshots, not diffs  
  
## Git仓库（Repositories）  
Git仓库是存储项目所有信息的数据库，用于保留和管理项目的修订和历史记录。Git仓库包含以下内容：  
**项目完整副本**：Git仓库保存了项目整个生命周期的完整副本。  
**配置信息**：Git在每个仓库中维护一套配置值，例如用户的姓名和电子邮件地址。这些配置信息不会在克隆、分叉或其他复制操作中传播，而是以站点、用户和仓库为基础进行管理。  
**存储位置**：所有仓库数据都存储在工作目录根目录下的隐藏文件夹.git中。  
  
Git仓库中有两个核心数据结构：对象存储（Object Store）和索引（Index）。  
  
## 对象存储（Object Store）  
对象存储是Git数据存储机制的核心，包含以下内容：  
**原始数据文件**：存储项目的文件内容。  
**日志消息、作者信息等**：记录每次提交的详细信息。  
  
**对象类型**：Git对象存储中有四种类型的对象，它们构成了Git高级数据结构的基础，blob、tree、commits和tags。  
  
### Blob（二进制大对象）  
binary large object。  
表示文件的每个版本。  
不包含文件名或元数据，仅包含文件内容。  
  
### Tree（树）  
表示目录结构的一个层级。  
包含文件的Blob ID、路径名和元数据。  
可以递归引用其他子树对象，构建完整的文件和子目录层级。  
  
### Commit（提交）  
表示对仓库的一次更改。  
包含作者、提交日期和日志消息等元数据。  
每个提交都链接到一个Tree对象，记录提交时仓库的状态。  
提交对象通过有向无环图（DAG）组织，表示项目的版本历史。  
  
### Tag（标签）  
给某个对象（通常是提交）一个可读的名称，例如“Ver-1.0-Alpha”。  
Git通过将对象压缩并存储在包文件（Pack Files）中，优化磁盘空间和网络流量的使用。  
  
## 索引（Index）  
索引是一个临时的、动态的二进制文件，描述了整个仓库的目录结构。它有以下特点：  
**捕获项目结构**：索引捕获了项目在某个时间点的结构版本。  
**阶段性更改**：Git允许在逻辑上分阶段更改索引内容，区分逐步开发和提交改进。  
  
## Git跟踪对象历史  
Git对象存储是一个基于内容寻址的存储系统，每个对象都有一个唯一的名称，通过SHA-1哈希算法生成。  
  
**SHA-1哈希**：对对象内容应用SHA-1算法，生成一个40字符的哈希值。  
**内容唯一性**：任何文件内容的微小变化都会导致SHA-1哈希值的变化，从而将新版本的文件单独索引。  
**存储方式**：Git只存储文件内容，而不是文件之间的差异。每个文件内容通过SHA-1哈希值引用，确保其唯一性。  
**全局唯一性**：相同的文件内容在不同位置或不同机器上会产生相同的SHA-1哈希值，因此SHA-1哈希值是一个全局唯一的标识符。  
  
# 文件的两种状态 - tracked and untracked  
> [Git - Recording Changes to the Repository](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)   
  
## tracked file  
Tracked files are files that were in the last snapshot, as well as any newly staged files; they can be unmodified, modified, or staged. In short, tracked files are files that Git knows about.  
  
## untracked file  
Tracked files are files that were in the last snapshot, as well as any newly staged files; they can be unmodified, modified, or staged. In short, tracked files are files that Git knows about.  
  
# Refs（引用）  
在 Git 中，`refs` 是指向提交对象（commit objects）的指针。它们存储在 `.git/refs` 目录下，分为几个部分：  
  
1. **HEAD**：指向当前分支的最新提交。  
2. **branches**：本地分支引用，例如 `refs/heads/master`。  
3. **remotes**：远程分支引用，例如 `refs/remotes/origin/master`。  
4. **tags**：标签引用，例如 `refs/tags/v1.0`。  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test04/.git/refs (GIT_DIR!)  
$ git show-ref  
a3df94d293f63c5fa18ce4733153f563f487f8c7 refs/heads/fix_B  
69cf6cc13264c001fb2857eb647bf7d116c2cb50 refs/heads/fix_C  
03d14aef6659233305d25c2c16ec7f73fd872243 refs/heads/main  
a47ac74dcd61d613ac569ff3167eb79ad9386cdc refs/heads/main2  
ee19c9a15ba4a472b63bcbd1ed7b3a4fd9a9c720 refs/heads/main3  
e190c9a249b47160664e52940e00e806509de7c2 refs/remotes/origin/HEAD  
b3852e1989fdf14d219a362ab1eac7a74fef83de refs/remotes/origin/branch01  
a3df94d293f63c5fa18ce4733153f563f487f8c7 refs/remotes/origin/fix_B  
e190c9a249b47160664e52940e00e806509de7c2 refs/remotes/origin/main  
f9e71d645c5ec284d6bd0c185e1bf47838462eeb refs/remotes/origin/tb01  
15f80f22ef8906b949207a200829008727a953c9 refs/remotes/origin/test  
  
lx@lx MINGW64 /d/Documents/git_test04 (fix_C)  
$ git log --oneline -1  
69cf6cc (HEAD -> fix_C) modify 2.txt  
```  
  
# Refspec（引用规范）  
> [Git - The Refspec](https://git-scm.com/book/en/v2/Git-Internals-The-Refspec)   
  
`refspec` 是一个字符串，用于定义如何将远程仓库的引用（refs）映射到本地仓库的引用。它通常用于 `git fetch` 和 `git push` 命令中，以指定要操作的远程引用和本地引用。  
  
一个 `refspec` 的一般格式如下：  
```  
<src>:<dst>  
```  
  
- **<src>**：源引用，可以是分支名、标签名或使用通配符的引用模式。  
- **<dst>**：目标引用，是远程引用映射到本地引用的路径。  
  
`refspec` 的强大之处在于它允许精确控制 Git 引用的同步和映射，这对于管理复杂的分支结构和远程仓库非常有用。  
  
## `+` 的用途  
> $ git fetch origin +seen:seen maint:tmp  
> This updates (or creates, as necessary) branches seen and tmp in the local repository by fetching from the branches (respectively) seen and maint from the remote repository.  
> The seen branch will be updated even if it does not fast-forward, because it is prefixed with a plus sign; tmp will not be.  
  
`+` 符号的用途是强制更新本地分支，即使这个更新涉及到非快速前进的合并。这可以确保本地分支始终与远程分支保持一致，但也可能会覆盖本地的提交历史，因此在没有 `+` 的情况下，Git 会拒绝这种操作以保护本地数据。  
  
在 refspec 中，`+` 符号用于强制更新本地分支以匹配远程分支的状态，即使这个更新不是快速前进。具体来说：  
- **带有 `+` 的 refspec**：`+seen:seen` 表示强制更新本地的 `seen` 分支以匹配远程的 `seen` 分支，即使这个更新需要创建一个新的合并提交。  
- **不带 `+` 的 refspec**：`maint:tmp` 表示更新本地的 `tmp` 分支以匹配远程的 `maint` 分支，但如果这个更新不是快速前进，Git 将拒绝这个操作，以避免覆盖本地的提交历史。  
  
假设你有两个分支：本地的 `seen` 和远程的 `origin/seen`。  
  
1. **不带 `+` 的情况**：  
   - 执行 `git fetch origin seen:seen`。  
   - 如果远程的 `origin/seen` 分支有新的提交，并且这些提交可以被快速前进，那么本地的 `seen` 分支将被更新。  
   - 如果远程的 `origin/seen` 分支有新的提交分叉，Git 将拒绝更新本地的 `seen` 分支，以保护你的本地提交历史。  
  
2. **带 `+` 的情况**：  
   - 执行 `git fetch origin +seen:seen`。  
   - 不管远程的 `origin/seen` 分支的更新是否可以被快速前进，本地的 `seen` 分支都将被强制更新以匹配远程分支的状态。  
   - 如果远程分支有新的提交分叉，Git 将创建一个新的合并提交，将这些更改合并到本地分支。  
  
# 裸仓库  
裸仓库是一个没有工作目录（working directory）的 Git 仓库。在普通的 Git 仓库中，你有一个 `.git` 目录，它包含了所有的版本控制信息，以及一个工作目录，这是你实际编写代码的地方。而在裸仓库中，没有工作目录，只有 `.git` 目录。这意味着你不能直接在裸仓库中进行提交（commit）或其他修改，它主要用于以下用途：  
  
1. **作为远程仓库**：裸仓库通常用作远程仓库，因为它不包含工作目录，所以不会有任何未提交的更改。这样可以确保所有通过 `git push` 和 `git fetch` 操作推送和拉取的更改都是干净和一致的。  
  
2. **备份**：裸仓库可以作为其他仓库的备份，因为它包含了完整的历史记录和所有分支。  
  
3. **Git 服务**：裸仓库可以作为 Git 服务运行，比如 Git 服务器或 CI/CD 系统，它们需要处理多个项目的推送和拉取操作。  
  
## 创建裸仓库  
  
```bash  
git init --bare myproject.git  
```  
  
这将创建一个名为 `myproject.git` 的目录，其中包含一个裸仓库。  
  
## 使用裸仓库  
  
- **推送和拉取**：开发者可以将本地更改推送到裸仓库，或者从裸仓库拉取更改到本地。  
- **克隆裸仓库**：如果你想从裸仓库开始本地开发，需要克隆裸仓库以创建一个包含工作目录的常规仓库。  
  
## `git clone --mirror` 命令  
  
当使用 `git clone --mirror` 克隆一个仓库时，你实际上是在创建一个裸仓库。这个命令会复制所有的引用（refs），包括分支、标签和远程引用，并且设置特殊的 refspec，使得所有这些引用在目标仓库中都会被覆盖。这意味着任何推送到这个镜像仓库的更改都会反映到所有相关的引用上。  
  
具体来说，`git clone --mirror` 命令做了以下几件事情：  
  
1. **克隆所有引用**：克隆远程仓库的所有分支和标签。  
  
2. **设置 refspec**：设置一个 refspec，这是一个规则，定义了如何从远程仓库同步引用。对于镜像仓库，这个 refspec 通常设置为 `+refs/*:refs/*`，意味着所有远程的引用都会被推送到本地。  
  
3. **创建裸仓库**：创建的仓库没有工作目录，只有 `.git` 目录。  
  
```bash  
git clone --mirror https://github.com/user/repo.git  
```  
这个命令会创建一个名为 `repo.git` 的裸仓库，其中包含了 `https://github.com/user/repo.git` 仓库的所有引用。可以使用这个裸仓库来推送更新到远程服务器，或者作为其他仓库的备份。  
  
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
  
# Ignoring files  
> [Learn Git and GitHub](https://roadmap.sh/git-github)   
> [Git - gitignore Documentation](https://git-scm.com/docs/gitignore)   
> [GitHub - github/gitignore: A collection of useful .gitignore templates](https://github.com/github/gitignore)   
> [.gitignore file - ignoring files in Git | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/saving-changes/gitignore)   
  
`.gitignore` 是一个在 Git 仓库中使用的特殊文件，用于指定 Git 应该忽略的文件和目录。这个文件帮助你防止不小心提交不需要版本控制的文件，比如编译产物、日志文件、个人配置文件等。  
  
不影响已被跟踪的文件。  
  
可以写到多个位置，如果忽略文件只针对本地仓库，将忽略的文件放到 `$GIT_DIR/info/exclude` 中，即仓库根目录的 `.git` 目录中。  
  
- **指定忽略规则**：`.gitignore` 文件包含一系列的模式（pattern），用于匹配文件和目录路径。Git 会根据这些模式决定哪些文件不需要版本控制。  
- **保持仓库清洁**：通过忽略不必要的文件，`.gitignore` 帮助保持仓库的清洁和组织。  
  
## 本地仓库忽略  
  
放在下面文件中  
```bash  
.git/info/excluede  
```  
  
## 注释和空行  
以 `#` 开头的行被视为注释，空行会被忽略。  
  
  
## `/` 作用  
> If there is a separator at the beginning or middle (or both) of the pattern, then the pattern is relative to the directory level of the particular .gitignore file itself. Otherwise the pattern may also match at any level below the .gitignore level.  
  
### `/` 在开头  
  
```bash  
/1.txt  
```  
排除 `.gitignore` 文件所在目录下的 1.txt 文件。  
  
### `/` 在中间  
  
```bash  
dir1/file2.txt  
```  
  
匹配 `.gitignore` 文件所在目录中的 `dir1` 目录下的 `file2.txt` 文件。  
  
### `/` 在结尾  
  
```bash  
dir1/  
```  
  
将排除 `.gitignore` 目录及其子目录中所有名为 `dir1` 的目录及其所有内容。  
一旦该目录被排除，则后续无法再排除目录中文件的忽略。  
```bash  
dir1/  
!dir1/file2.txt  
```  
将无法撤销 `dir1/file2.txt` 文件的忽略。  
  
### 无 `/` 结尾  
  
```bash  
dir1  
```  
  
将排除 `.gitignore` 目录及其子目录中所有名为 `dir1` 的目录及其所有内容，或者名为 `dir1` 的文件。  
一旦该目录被排除，则后续无法再排除目录中文件的忽略。  
  
## 忽略目录及其子目录  
```bash  
dir/  
```  
  
## 忽略目录中的文件  
```bash  
dir/*  
```  
  
不会忽略目录，因此后续可以为目录中的特定文件加规则：  
```bash  
dir1/*  
!dir1/file2.txt  
```  
  
忽略 `dir` 目录中全部文件，但排除 `dir1/file2.txt` 文件。  
  
## 多级目录的忽略  
  
如下目录结构：  
```bash  
project/  
├── .gitignore  
├── doc/  
│   └── frotz/  
│       └── file1.txt  
├── a/  
│   └── doc/  
│       └── frotz/  
│           └── file2.txt  
└── frotz/  
    └── file3.txt  
```  
  
- `doc/frotz/` 匹配结果  
匹配 `project/doc/frotz/` 目录及其内容。  
不匹配 `project/a/doc/frotz/` 目录及其内容，因为路径 `doc/frotz/` 是相对于 `.gitignore` 文件所在的目录的，而 `a/doc/frotz/` 不在该路径范围内。  
  
  
- `frotz/` 匹配结果  
匹配 `project/frotz/` 目录及其内容。  
也匹配 `project/a/frotz/` 目录及其内容，因为路径 `frotz/` 会匹配 `.gitignore` 文件所在目录及其所有子目录中的 `frotz` 目录。  
  
## `*` 匹配任意除了 / 外的字符  
> The pattern foo/*, matches foo/test.json (a regular file), foo/bar (a directory), but it does not match foo/bar/hello.c (a regular file), as the asterisk in the pattern does not match bar/hello.c which has a slash in it.  
  
`*` 是一个通配符，用于匹配任意数量的字符（包括零个字符）。  
  
```bash  
*.txt  
```  
匹配结果：  
```text  
file1.txt：会被匹配并忽略。  
file2.txt：会被匹配并忽略。  
dir1/file3.txt：会被匹配并忽略。  
dir1/subdir/file4.txt：会被匹配并忽略。  
```  
  
```bash  
dir1/*  
```  
根据官方讲解，匹配结果应该如下：  
```text  
dir1/file1.txt：会被匹配并忽略。  
dir1/file2.log：会被匹配并忽略。  
dir1/subdir/file3.txt：不会被匹配并忽略（因为 * 只匹配 dir1 目录中的直接子文件，不匹配 subdir/file3.txt）。  
```  
但实际测试发现子目录的文件也被匹配了，因为 Git 在处理 `.gitignore` 文件时，会递归对子目录应用相同的规则。  
  
## `?` 匹配任意一个除了 / 外的一个字符  
  
## `[]` 匹配范围内地任意字符  
  
如 `[a-zA-Z]` 可以匹配范围内的任意一个字符。  
  
## `!` 取消忽略  
> An optional prefix "!" which negates the pattern; any matching file excluded by a previous pattern will become included again. It is not possible to re-include a file if a parent directory of that file is excluded. Git doesn’t list excluded directories for performance reasons, so any patterns on contained files have no effect, no matter where they are defined. Put a backslash ("\") in front of the first "!" for patterns that begin with a literal "!", for example, "\!important!.txt".  
  
- `!` 符号用于取消之前忽略的规则。  
- 如果文件的父目录被排除，则无法重新包含该文件。  
如果忽略目录 `folder1/`，则即使后面用 `!folder1/foo.txt` 取消特定文件的忽略也不能生效，因为 git 不会检查 folder1 目录中的文件是否还有其他规则。  
- 如果用 `folder1/*` 仅忽略目录中的文件而不忽略目录本身，则后续可以用 `!folder1/foo.txt` 取消特定文件的忽略。  
- 用 `\!` 来匹配 `!` 本身。  
  
## 双星号 `**`  
  
### leading `**`  
> A leading "**" followed by a slash means match in all directories. For example, "**/foo" matches file or directory "foo" anywhere, the same as pattern "foo". "**/foo/bar" matches file or directory "bar" anywhere that is directly under directory "foo".  
  
### trailing `/**`  
> A trailing "/**" matches everything inside. For example, "abc/**" matches all files inside directory "abc", relative to the location of the `.gitignore` file, with infinite depth.  
  
### middle `/**`  
> A slash followed by two consecutive asterisks then a slash matches zero or more directories. For example, "a/**/b" matches "a/b", "a/x/b", "a/x/y/b" and so on.  
  
## 示例  
```bash  
# exclude everything except directory foo/bar  
/*  
!/foo  
/foo/*  
!/foo/bar  
```  
  
## 应用 `.gitignore` 规则  
- **现有文件**：如果文件已经被跟踪（即已经提交过），那么即使后来在 `.gitignore` 中添加了匹配的规则，这些文件仍然会被跟踪。要停止跟踪这些文件，需要先从仓库中删除它们。但已跟踪的文件加入 `.gitignore` 规则后，这些文件如果被修改然后 `git add`，会出现提示信息。  
- **新文件**：对于尚未被跟踪的文件，`.gitignore` 规则会立即生效。  
  
# 分支  
> [Git - Basic Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)   
> [Git Branches Tutorial](https://www.youtube.com/watch?v=e2IbNHi4uCI&ab_channel=freeCodeCamp.org)   
  
# HEAD   
> [Git - Reset Demystified](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified#_git_reset)  
> [Git - Git References](https://git-scm.com/book/en/v2/Git-Internals-Git-References#:~:text=want%20to%20create.-,The%20HEAD,-The%20question%20now)   
  
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
  
## Detached HEAD  
> In Git, a detached head occurs when you check out a commit directly using its hash instead of a branch name. This leaves your repository’s HEAD pointer pointing directly at that commit, rather than being linked to a specific branch. To view the history and changes made in a detached head, use git log or git show. If you want to see the differences between the current detached head and another branch, use git diff <branch>. A detached head can be a useful temporary state for exploring specific commits or features, but it’s essential to merge those changes back into a branch before sharing them with others.   
  
在 Git 中，detached HEAD 状态是指 HEAD 指针直接指向一个具体的提交，而不是指向一个分支。这种状态通常在以下几种情况下发生：  
使用 git checkout <commit-hash> 命令切换到某个特定的提交。  
使用 git checkout origin/<branch> 命令切换到远程分支，但本地没有对应的分支。  
使用 git checkout <tag> 命令切换到某个标签。  
  
在 detached HEAD 状态下，你可以进行正常的 Git 操作，如提交、合并、重置等。但需要注意以下几点：  
提交的引用：在 detached HEAD 状态下进行的提交不会关联到任何分支，因此这些提交可能会变得不可访问。你可以通过查看 Git 的引用日志（git reflog）来找回这些提交。  
  
当在 detached HEAD 状态下进行提交时，这些提交不会关联到任何分支。HEAD 直接指向这些提交，而不是通过分支引用指向它们。因此，如果切换到其他分支，这些提交将不会被自动保留。  
  
在 detached HEAD 状态下，可以创建一个新的分支来保留当前状态：  
bash  
```bash  
git checkout -b new-branch  
```  
  
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
  
# git remote  
> [Git - git-remote Documentation](https://git-scm.com/docs/git-remote)   
> [Managing remote repositories - GitHub Docs](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories)   
  
1. **查看远程仓库**：`git remote` 命令可以列出所有配置的远程仓库。  
2. **添加远程仓库**：可以使用 `git remote add` 命令添加新的远程仓库。  
3. **修改远程仓库**：可以更改远程仓库的 URL 或其他设置。  
4. **删除远程仓库**：可以删除不再需要的远程仓库引用。  
  
## 选项  
  
- **`-v` 或 `--verbose`**：显示远程仓库的详细信息，包括 URL。  
- **`add`**：添加新的远程仓库引用。  
- **`remove`**：删除远程仓库引用。  
- **`rename`**：重命名远程仓库。  
- **`set-url`**：更改远程仓库的 URL。  
  
## 查看远程仓库名称列表  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main2)  
$ git remote  
origin  
```  
  
## 查看远程仓库URL  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main2)  
$ git remote -vv  
origin  https://github.com/lxwcd/git_test.git (fetch)  
origin  https://github.com/lxwcd/git_test.git (push)  
```  
  
## 添加远程仓库  
```bash  
git remote add <name> <url>  
```  
添加一个新的远程仓库引用，`<name>` 是远程仓库的短名称，`<url>` 是远程仓库的 URL。  
  
## 删除远程仓库  
```bash  
git remote remove <name>  
```  
  
## 重命名远程仓库  
```bash  
git remote rename <old-name> <new-name>  
```  
  
## 设置远程仓库 URL  
```bash  
git remote set-url <name> <new-url>  
```  
  
## 添加本地远程仓库  
```bash  
git remote add local-origin file:///d/Documents/git_test  
```  
- 将 `D:/Documents/git_test` 仓库添加为远程仓库，别名为 `local-origin`。  
  
# git clone  
> [Git - git-clone Documentation](https://git-scm.com/docs/git-clone)  
  
## 克隆默认分支  
```bash  
git clone https://github.com/user/repo.git  
```  
这将克隆 `user/repo` 仓库的默认分支（通常是 `master` 或 `main`）到本地。  
  
## 克隆远程仓库的特定分支  
```bash  
git clone -b develop https://github.com/user/repo.git  
```  
这将克隆 `user/repo` 仓库的 `develop` 分支，这个分支必须是远程仓库已经存在的分支。  
克隆完后本地会创建一个和远程 `develop` 对应的分支，同时也会克隆远程仓库的其他分支。  
  
```bash  
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test03  
$ git clone -b tb01 https://github.com/lxwcd/git_test.git .  
Cloning into '.'...  
remote: Enumerating objects: 33, done.  
remote: Counting objects: 100% (33/33), done.  
remote: Compressing objects: 100% (22/22), done.  
remote: Total 33 (delta 2), reused 29 (delta 1), pack-reused 0 (from 0)  
Receiving objects: 100% (33/33), 4.15 KiB | 1.38 MiB/s, done.  
Resolving deltas: 100% (2/2), done.  
  
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test03 (tb01)  
$ git branch -vv  
* tb01 f9e71d6 [origin/tb01] Update test01.txt  
  
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test03 (tb01)  
$ git branch -a  
* tb01  
  remotes/origin/HEAD -> origin/main  
  remotes/origin/branch01  
  remotes/origin/main  
  remotes/origin/tb01  
```  
  
## 克隆不包含标签  
```bash  
git clone --no-tags https://github.com/user/repo.git  
```  
这将克隆仓库，但不包括任何标签。  
  
## 浅克隆  
```bash  
git clone --depth 1 https://github.com/user/repo.git  
```  
这将创建一个浅克隆，只包含最新的提交（即最近一次提交的历史）。  
  
## 仅克隆远程仓库指定分支  
```bash  
git clone --branch new-branch --single-branch https://github.com/user/repo.git  
```  
这将克隆 `user/repo` 仓库，并检查出 `new-branch` 分支，本地看不到远程仓库的其他分支。  
  
```bash  
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test02  
$ git clone -b tb01 --single-branch https://github.com/lxwcd/git_test.git  
Cloning into '.'...  
remote: Enumerating objects: 18, done.  
remote: Counting objects: 100% (18/18), done.  
remote: Compressing objects: 100% (11/11), done.  
remote: Total 18 (delta 1), reused 15 (delta 1), pack-reused 0 (from 0)  
Receiving objects: 100% (18/18), done.  
Resolving deltas: 100% (1/1), done.  
  
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test02 (tb01)  
$ ls -a  
./  ../  .git/  test01.txt  test02.txt  test03.txt  test04.txt  
  
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test02 (tb01)  
$ git branch -a  
* tb01  
  remotes/origin/tb01  
  
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test02 (tb01)  
$ git branch -vv  
* tb01 f9e71d6 [origin/tb01] Update test01.txt  
```  
  
## 克隆并初始化所有子模块  
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
  
## 创建裸仓库  
```bash  
git clone --bare https://github.com/user/repo.git  
```  
这将创建一个裸仓库，即没有工作目录的仓库，通常用于作为其他仓库的镜像。  
  
> Make a bare Git repository. That is, instead of creating <directory> and placing the administrative files in <directory>/.git, make the <directory> itself the $GIT_DIR. This obviously implies the --no-checkout because there is nowhere to check out the working tree. Also the branch heads at the remote are copied directly to corresponding local branch heads, without mapping them to refs/remotes/origin/. When this option is used, neither remote-tracking branches nor the related configuration variables are created.  
  
## 创建镜像仓库  
```bash  
git clone --mirror https://github.com/user/repo.git  
```  
和创建裸仓库类似，但还包含远程分支的引用。  
  
> Set up a mirror of the source repository. This implies --bare. Compared to --bare, --mirror not only maps local branches of the source to local branches of the target, it maps all refs (including remote-tracking branches, notes etc.) and sets up a refspec configuration such that all these refs are overwritten by a git remote update in the target repository.  
  
## 不检出 HEAD  
```bash  
git clone --no-checkout https://github.com/user/repo.git  
```  
这将克隆仓库，但不会检出 HEAD 对应的工作目录。  
  
`git clone --no-checkout <repository-url>` 命令会从 `<repository-url>` 指定的远程仓库克隆一个空目录，其中包含远程仓库的所有分支和标签的引用，但不包含任何工作目录中的文件。  
  
## 使用模板克隆  
```bash  
git clone --template=/path/to/template https://github.com/user/repo.git  
```  
这将使用指定的模板目录来初始化新仓库。  
  
## 设置配置变量  
```bash  
git clone --config user.name="Your Name" https://github.com/user/repo.git  
```  
这将在克隆时设置仓库的用户名称。  
  
### 使用场景  
  
1. **节省带宽和时间**：如果你只对仓库的元数据（如分支、标签）感兴趣，或者你想要离线工作而不需要立即检出代码，使用 `--no-checkout` 可以节省下载代码的带宽和时间。  
  
2. **初始化裸仓库**：创建裸仓库（bare repository）时，通常不需要工作目录，因此可以使用 `--no-checkout` 选项来克隆。  
  
3. **脚本和自动化**：在自动化脚本中，你可能需要克隆仓库并执行一些 Git 操作，但不需要实际的代码文件。  
  
### 注意事项  
  
- 克隆完成后，你可以使用 `git checkout` 命令来检出特定的分支或提交。  
- 如果你需要检出特定的分支，可以在克隆后执行 `git checkout <branch-name>`。  
- 如果你想要检出远程分支的最新提交，可以先执行 `git fetch`，然后使用 `git checkout -b <branch-name> origin/<branch-name>`。  
- 使用 `--no-checkout` 克隆的仓库将不会包含任何文件，直到你显式地检出分支或提交。  
  
## 稀疏检出  
```bash  
git clone --sparse https://github.com/user/repo.git  
```  
这将使用稀疏检出克隆仓库，只检出顶级目录中的文件。  
  
## 克隆部分目录到本地  
> [Git - git-clone Documentation](https://git-scm.com/docs/git-clone#Documentation/git-clone.txt-code--filterltfilter-specgtcode)   
  
```bash  
git clone --depth 1 --filter=blob:none --no-checkout https://github.com/lxwcd/linux.git  
cd linux  
git checkout main -- notes/shell_scripts  
```  
  
## 仅克隆仓库中的文件  
如果不想远程仓库的目录，只将目录内的文件克隆到本地当前目录下，则如下：  
```bash  
git clone https://github.com/lxwcd/cpp.git .  
```  
        
## 克隆仓库到新目录  
将远程仓库克隆到指定目录并且修改仓库名字为 `new_folder`：  
```bash  
git clone https://github.com/lxwcd/learnVim.git /usr/local/src/new_folder  
```  
        
也可以指定多级目录，如果不存在，则自动创建  
```bash  
git clone https://github.com/lxwcd/learnVim.git /usr/local/src/1/2/3/new_folder  
```  
  
## file 协议克隆  
在 Git 中，`file` 协议用于通过本地文件系统路径克隆或访问仓库。`file` 协议的使用方式与通过网络协议（如 `http`、`https`、`git`）克隆仓库类似，但它专门用于本地文件系统。  
  
```bash  
file:///path/to/repo  
```  
- **`file://`**：这是协议前缀，表示使用文件系统路径。  
- **`/`**：在 Unix-like 系统中，路径从根目录开始，因此使用三个斜杠 `///`。  
- **`/path/to/repo`**：这是仓库的路径。  
  
## 克隆本地仓库  
```bash  
git clone file:///d/Documents/git_test /d/Documents/git_test_03  
```  
- 源路径：`file:///d/Documents/git_test`，表示 `D:/Documents/git_test` 仓库。  
- 目标路径：`/d/Documents/git_test_03`，表示克隆到 `D:/Documents/git_test_03` 目录。  
  
本地克隆默认使用文件系统路径，而不是通过网络协议（如 http 或 git）进行克隆。  
  
# git init 初始化仓库  
> [Git - git-init Documentation](https://git-scm.com/docs/git-init)   
  
`git init` 是 Git 中用于初始化新仓库的命令。它将一个现有的目录转换为 Git 仓库，使其可以进行版本控制。  
  
1. **创建新的 Git 仓库**：`git init` 在当前目录中创建一个新的 `.git` 目录，该目录包含所有必要的 Git 仓库文件。  
2. **初始化仓库结构**：命令会初始化仓库的基本结构，包括配置文件、对象数据库、引用等。  
  
## 使用场景  
  
- **开始新项目**：当开始一个新项目并希望使用 Git 进行版本控制时，`git init` 是第一步。  
- **将现有项目转换为 Git 仓库**：如果有一个未使用 Git 版本控制的现有项目，`git init` 可以将其转换为 Git 仓库。  
  
## 初始化当前目录  
```bash  
git init  
```  
  
执行 `git init` 后，当前目录（或指定目录）将包含一个新的 `.git` 目录，其中包含以下内容：  
  
- **`HEAD`**：指向当前分支的引用。  
- **`config`**：仓库的配置文件。  
- **`objects`**：存储 Git 对象的目录。  
- **`refs`**：存储分支和标签引用的目录。  
  
## 初始化指定目录  
```bash  
git init <directory>  
```  
这个命令将指定目录初始化为一个 Git 仓库。如果目录不存在，Git 会尝试创建它。  
  
## 创建裸仓库  
```bash  
git init --bare  
```  
创建一个裸仓库（bare repository），这种仓库没有工作目录，通常用于服务器上的中央仓库。  
  
# git status 检查文件状态  
> [Git - git-status Documentation](https://git-scm.com/docs/git-status)   
  
`git status` 是 Git 中一个非常常用的命令，用于显示当前仓库的状态。这个命令提供了关于工作目录和暂存区的详细信息，帮助用户了解哪些文件被修改、哪些文件已暂存、哪些文件尚未跟踪等。  
  
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
  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git --version  
git version 2.47.1.windows.1  
  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git status  
On branch fix_B  
Changes to be committed:  
  (use "git restore --staged <file>..." to unstage)  
        new file:   git.md  
  
Changes not staged for commit:  
  (use "git add <file>..." to update what will be committed)  
  (use "git restore <file>..." to discard changes in working directory)  
        modified:   git.md  
        modified:   test01.txt  
  
Untracked files:  
  (use "git add <file>..." to include in what will be committed)  
        0001-commit-B.patch  
        0001-fix-B.patch  
        0001-update-fix_B.patch  
        0002-commit-C.patch  
        0002-update-fix_B.patch  
        1.patch  
```  
  
## -s, --short 显示简短的状态信息  
不显示文件的具体更改内容。  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git status -s  
A  git.md  
 M test01.txt  
?? 0001-commit-B.patch  
?? 0001-fix-B.patch  
?? 0001-update-fix_B.patch  
?? 0002-commit-C.patch  
?? 0002-update-fix_B.patch  
?? 1.patch  
```  
  
## -u, --untracked-files[=<mode>] 显示未跟踪的文件  
`<mode>` 可以是 `no`, `normal`, 或 `all`  
     - `no`：不显示未跟踪的文件。  
     - `normal`：显示未跟踪的文件，但排除那些在 `.gitignore` 中指定的文件。  
     - `all`：显示所有未跟踪的文件，包括那些在 `.gitignore` 中指定的文件。  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git status --short --untracked-files=no  
A  git.md  
 M test01.txt  
  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git status --short  
A  git.md  
 M test01.txt  
?? 0001-commit-B.patch  
?? 0001-fix-B.patch  
?? 0001-update-fix_B.patch  
?? 0002-commit-C.patch  
?? 0002-update-fix_B.patch  
?? 1.patch  
```  
  
## --ignored 显示被忽略的文件  
> [Git - git-status Documentation](https://git-scm.com/docs/git-status#Documentation/git-status.txt---ignoredltmodegt)   
  
  
## --porcelain 便于脚本处理的输出  
  
和 --short 输出类似：  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git status --porcelain  
A  git.md  
 M test01.txt  
?? 0001-commit-B.patch  
?? 0001-fix-B.patch  
?? 0001-update-fix_B.patch  
?? 0002-commit-C.patch  
?? 0002-update-fix_B.patch  
?? 1.patch  
```  
  
## 输出未被跟踪的文件名  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git status -s  
AM git.md  
 M test01.txt  
?? .gitignore  
?? 0001-commit-B.patch  
?? 0001-fix-B.patch  
?? 0001-update-fix_B.patch  
?? 0002-commit-C.patch  
?? 0002-update-fix_B.patch  
?? 1.patch  
?? 2.txt  
  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git status -s |  grep "??" | cut -d" " -f2  
.gitignore  
0001-commit-B.patch  
0001-fix-B.patch  
0001-update-fix_B.patch  
0002-commit-C.patch  
0002-update-fix_B.patch  
1.patch  
2.txt  
```  

# Author and Committer
> [Why is git AuthorDate different from CommitDate?](https://stackoverflow.com/questions/11856983/why-is-git-authordate-different-from-commitdate) 
> [Git - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History) 

> You may be wondering what the difference is between author and committer. The author is the person who originally wrote the work, whereas the committer is the person who last applied the work. So, if you send in a patch to a project and one of the core members applies the patch, both of you get credit — you as the author, and the core member as the committer. 
  
# git date
> [Dates in Git - Azure Repos](https://learn.microsoft.com/en-us/azure/devops/repos/git/git-dates?view=azure-devops) 


## Author Date
作者时间是指提交的作者（Author）创建提交时的时间戳。它记录了最初编写代码并创建提交的时间。

在正常的 git commit 操作中，作者时间和提交者时间是相同的。

### 查看 Author Date
> [Git - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History#pretty_format) 

```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_B)
$ git log --pretty=fuller  -1
commit baddcc29cc6f0cd12a793ad33f8caa198c97bcaa (HEAD -> fix_B)
Author:     John <John@163.com>
AuthorDate: Sun Feb 9 20:46:40 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 21:00:08 2025 +0800

    add files and modify author
```

```bash
lx@lx MINGW64 /d/Documents/git_test04 (main3)
$ git log --pretty=format:"%h %an %ad" fix_C -1
b3e36b5 John Sun Feb 9 20:46:40 2025 +0800
```
%h：提交的哈希值（短格式）
%an：作者名称（Author Name）
%ad：作者时间（Author Date）

### git commit --date 修改 Author date
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D)
$ date
2025年02月 9日 21:17:02
```

```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D)
$ git commit --date="2025-01-02 14:00:00" -m "Fix bug" --author="Alice <ALice@163.com>"
[fix_D 91b0e3c] Fix bug
 Author: Alice <ALice@163.com>
 Date: Thu Jan 2 14:00:00 2025 +0800
 1 file changed, 1 insertion(+)
```

查看日志，Author Date 被修改为指定时间，但 commit date 为当前时间。
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D)
$ git log --pretty=fuller -1
commit 91b0e3c6432ccf89a9809c087fe933bf05c6966e (HEAD -> fix_D)
Author:     Alice <ALice@163.com>
AuthorDate: Thu Jan 2 14:00:00 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 21:17:51 2025 +0800

    Fix bug
```

### git cherry-pick 不会修改 Author date
`git cherry-pick` 没有使用 `--no-commit` 选项，且没有冲突，不会修改作者时间戳，但会更新提交时间。

fix_C 分支有一个提交记录：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_C)
$ git log --pretty=fuller -1
commit b3e36b570b1067a9a3bf6e57fe33589afbfdb31c (HEAD -> fix_C)
Author:     John <John@163.com>
AuthorDate: Sun Feb 9 20:46:40 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 20:46:40 2025 +0800

    add files and modify author
```

`git cherry-pick` 应用该提交到 fix_B 分支：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_B)
$ git cherry-pick fix_C
[fix_B baddcc2] add files and modify author
 Author: John <John@163.com>
 Date: Sun Feb 9 20:46:40 2025 +0800
 24 files changed, 390 insertions(+)
```

查看 fix_B 分支的提交记录，发现提交时间更新了，但 Author Date 没有更新：
```cpp
lx@lx MINGW64 /d/Documents/git_test04 (fix_B)
$ git log --pretty=fuller  -1
commit baddcc29cc6f0cd12a793ad33f8caa198c97bcaa (HEAD -> fix_B)
Author:     John <John@163.com>
AuthorDate: Sun Feb 9 20:46:40 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 21:00:08 2025 +0800

    add files and modify author
```

### git cherry-pick 解决冲突后不修改 Author Date
`git cherry-pick` 如果有冲突，根据提示和 git status 查看的状态打开冲突文件解决冲突。
```bash

lx@lx MINGW64 /d/Documents/git_test04 (main2_01)
$ git cherry-pick main2
Auto-merging test01.txt
CONFLICT (content): Merge conflict in test01.txt
error: could not apply 3b671ba... modify test01.txt , add C
hint: After resolving the conflicts, mark them with
hint: "git add/rm <pathspec>", then run
hint: "git cherry-pick --continue".
hint: You can instead skip this commit with "git cherry-pick --skip".
hint: To abort and get back to the state before "git cherry-pick",
hint: run "git cherry-pick --abort".
hint: Disable this message with "git config advice.mergeConflict false"
```

```bash
lx@lx MINGW64 /d/Documents/git_test04 (main2_01|CHERRY-PICKING)
$ git status
On branch main2_01
You are currently cherry-picking commit 3b671ba.
  (fix conflicts and run "git cherry-pick --continue")
  (use "git cherry-pick --skip" to skip this patch)
  (use "git cherry-pick --abort" to cancel the cherry-pick operation)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   test01.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

解决冲突后 `git add` 将文件添加到暂存区，然后 `git cherry-pick --continue` 继续执行 cherry-pick 操作，这时会打开窗口写提交日志信息，默认显示原始的日志，可以直接使用或者修改日志 message：
```bash
modify test01.txt , add C

# Conflicts:
#	test01.txt
#
# It looks like you may be committing a cherry-pick.
# If this is not correct, please run
#	git update-ref -d CHERRY_PICK_HEAD
# and try again.


# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Author:    Bob <Bob@163.com>
# Date:      Sun Feb 9 18:58:12 2025 +0800
#
# On branch main2_01
# You are currently cherry-picking commit 3b671ba.
#
# Changes to be committed:
#	modified:   test01.txt
#
```

完成后查看日志发现 Author Date 没有被修改，但 Commit Date 更新为当前时间：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (main2_01)
$ git log --pretty=fuller -1
commit f537c63676cc209de5bdcd1b79ba79234c7d1552 (HEAD -> main2_01)
Author:     Bob <Bob@163.com>
AuthorDate: Sun Feb 9 18:58:12 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 22:32:24 2025 +0800

    modify test01.txt , add C
```

### git cherry-pick --no-commit 修改 Author date
如果 git cherry-pick --no-commit 则会自己提交，因此改变作者信息和时间：

fix_C 分支有一个提交记录：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_C)
$ git log --pretty=fuller -1
commit b3e36b570b1067a9a3bf6e57fe33589afbfdb31c (HEAD -> fix_C)
Author:     John <John@163.com>
AuthorDate: Sun Feb 9 20:46:40 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 20:46:40 2025 +0800

    add files and modify author
```

`git cherry-pick` 应用该提交到 main3 分支：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (main3)
$ git cherry-pick fix_C --no-commit

```

手动提交：
```cpp
lx@lx MINGW64 /d/Documents/git_test04 (main3)
$ git commit -m "cherry-pick fix_C and commit manually"
[main3 d228105] cherry-pick fix_C and commit manually
 24 files changed, 390 insertions(+)
```

查看日志发现作者时间戳和提交时间戳都更新了：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (main3)
$ git log --pretty=fuller  -1
commit d228105d37848565b1ab948a8ae5d12c32bdb10f (HEAD -> main3)
Author:     lxwcd <15521168075@163.com>
AuthorDate: Sun Feb 9 21:05:30 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 21:05:30 2025 +0800

    cherry-pick fix_C and commit manually
```

### git rebase 和 git cherry-pick 影响相同

## Commit Date
提交者时间是指提交被最终记录到仓库中的时间戳。它记录了提交被实际写入 Git 历史的时间。

在正常的 git commit 操作中，提交者时间和作者时间是相同的。

### 查看 Commit Date 
> [Git - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History#pretty_format) 

```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D)
$ git log --pretty=fuller  -1 fix_C
commit b3e36b570b1067a9a3bf6e57fe33589afbfdb31c (fix_C)
Author:     John <John@163.com>
AuthorDate: Sun Feb 9 20:46:40 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 20:46:40 2025 +0800

    add files and modify author
```

或者：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D)
$ git log --pretty=format:"%h %cn %cd" fix_C -1
b3e36b5 lxwcd Sun Feb 9 20:46:40 2025 +0800
```

%cn：提交者名称（Committer Name）
%cd：提交者时间（Committer Date）

### git cherry-pick 和 git rebase 更新 commit 时间戳
在 git rebase 或 git cherry-pick 等操作中，提交者时间会更新为当前时间，因为这些操作会重新生成提交对象。

## Push Date
> [Dates in Git - Azure Repos](https://learn.microsoft.com/en-us/azure/devops/repos/git/git-dates?view=azure-devops) 

推送时间是指提交被推送到远程仓库的时间。Git 本身并没有直接记录推送时间，但可以通过一些工具或远程仓库的记录来查看。

推送时间通常由远程仓库（如 GitHub、GitLab 等）记录，而不是直接存储在 Git 提交对象中。

每次执行 git push 时，远程仓库会记录推送的时间戳。

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
  
## 默认根据 Commit Date 排序
即使 Author Date 比较旧，但排序根据 Commit Date，因此其他分支合并到主分支时，尽管某些提交的 Author Date 时间比较旧，但最后排序显示时根据合并到主分支的顺序显示。

```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_C)
$ git log --pretty=fuller -3
commit 3b634a779435438654cdbcd2479d14e4855ce5ee (HEAD -> fix_C)
Author:     lxwcd <15521168075@163.com>
AuthorDate: Wed Jan 1 23:03:34 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 23:03:34 2025 +0800

    modify 1.patch , change author date

commit 95e40db1e205b1de7ac81fb58d40c7114df160b8
Author:     lxwcd <15521168075@163.com>
AuthorDate: Mon Jan 20 22:53:50 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 22:53:50 2025 +0800

    modify 2.txt, change author date

commit 9d7b614d7f37f3e6fbe29967f8d499e8d736d4d1
Author:     lxwcd <15521168075@163.com>
AuthorDate: Tue Feb 4 22:44:33 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 22:44:33 2025 +0800

    modify 2.txt, change author date
```

## 查看当前分支所有提交  
```bash  
git log  
```  
默认按照时间顺序，从最新的开始显示。  
  
## 查看特定分支的提交  
```bash  
git log <branch-name>  
```  
这个命令显示指定分支的提交历史。  
  
## 查看特定分支的过去某个提交  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main3)  
$ git log --oneline -7 main2  
a47ac74 (main2) Revert "update main test01.txt"  
ca44b51 Revert "update test01.txt: add main"  
006fed4 Reapply "update test01.txt: add main"  
b93b033 Revert "add test02.txt and test03.txt"  
dc76ad7 Revert "update test01.txt: add main"  
16ac277 update test01.txt: add main  
03d14ae (HEAD -> main3, origin/main, origin/HEAD, main) update main test01.txt  
```  
  
查看 main2 分支的第 6 个父提交：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main3)  
$ git log --oneline main2~6 -1  
03d14ae (HEAD -> main3, origin/main, origin/HEAD, main) update main test01.txt  
```  
  
## 查看特定分支的过去部分提交  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main3)  
$ git log --oneline -7 main2  
a47ac74 (main2) Revert "update main test01.txt"  
ca44b51 Revert "update test01.txt: add main"  
006fed4 Reapply "update test01.txt: add main"  
b93b033 Revert "add test02.txt and test03.txt"  
dc76ad7 Revert "update test01.txt: add main"  
16ac277 update test01.txt: add main  
03d14ae (HEAD -> main3, origin/main, origin/HEAD, main) update main test01.txt  
```  
  
查看 main2 分支的第 2 个父提交和之后的 3 个提交：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main3)  
$ git log --oneline main2~2 -3  
006fed4 Reapply "update test01.txt: add main"  
b93b033 Revert "add test02.txt and test03.txt"  
dc76ad7 Revert "update test01.txt: add main"  
```  
  
## 指定输出日志数目  
```bash  
git log -3  
```  
输出日志显示最新的 3 条  
  
## 查看提交差异 --patch  
> [Git - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)   
  
使用`-p`或`--patch`参数，可以查看每个提交的具体差异：  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git log -p -1  
commit 51da54a57cdc95263072173726d187a544725289 (HEAD -> fix_B)  
Author: lxwcd <15521168075@163.com>  
Date:   Sun Jan 12 21:22:45 2025 +0800  
  
    update fix_B  
  
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
  
这将显示最新两个提交的详细差异，包括文件的增删改。  
其中 a 表示该提交前的版本，b 表示该提交后的版本。  
`@@` 标记差异的开始，如 `@@ -4,3 +4,4 @@ local modify test01.txt` 表示对于 a 版本从第 4 行开始的 3 行内容，对于 b 版本从第 4 行开始的 4 行内容，有差异。  
`-` 表示原始版本中存在但新版本被删除的行，`+` 表示原始版本没有 ，新版本添加的行，即状态表示从 a 版本到 b 版本需要进行的添加、删除等操作。  
  
## 统计信息 --stat  
  
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
  
## 简短 stat 信息  
> Display only the changed/insertions/deletions line from the --stat command.  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git log --shortstat -1  
commit 51da54a57cdc95263072173726d187a544725289 (HEAD -> fix_B)  
Author: lxwcd <15521168075@163.com>  
Date:   Sun Jan 12 21:22:45 2025 +0800  
  
    update fix_B  
  
 3 files changed, 4 insertions(+), 1 deletion(-)  
```  
  
## 自定义格式 --pretty  
> [Git - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History#pretty_format)   
  
使用`--pretty`参数，可以自定义日志的显示格式。  
  
### --pretty=fuller 查看 Author 和 Committer
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_E)
$ git log --pretty=fuller fix_C -1
commit b3e36b570b1067a9a3bf6e57fe33589afbfdb31c (fix_C)
Author:     John <John@163.com>
AuthorDate: Sun Feb 9 20:46:40 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 20:46:40 2025 +0800

    add files and modify author
```

### 查看 Author Date
> [Git - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History#pretty_format) 

```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_B)
$ git log --pretty=fuller  -1
commit baddcc29cc6f0cd12a793ad33f8caa198c97bcaa (HEAD -> fix_B)
Author:     John <John@163.com>
AuthorDate: Sun Feb 9 20:46:40 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 21:00:08 2025 +0800

    add files and modify author
```

```bash
lx@lx MINGW64 /d/Documents/git_test04 (main3)
$ git log --pretty=format:"%h %an %ad" fix_C -1
b3e36b5 John Sun Feb 9 20:46:40 2025 +0800
```
%h：提交的哈希值（短格式）
%an：作者名称（Author Name）
%ad：作者时间（Author Date）

### 查看 Commit Date 
> [Git - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History#pretty_format) 

```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D)
$ git log --pretty=fuller  -1 fix_C
commit b3e36b570b1067a9a3bf6e57fe33589afbfdb31c (fix_C)
Author:     John <John@163.com>
AuthorDate: Sun Feb 9 20:46:40 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 20:46:40 2025 +0800

    add files and modify author
```

或者：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D)
$ git log --pretty=format:"%h %cn %cd" fix_C -1
b3e36b5 lxwcd Sun Feb 9 20:46:40 2025 +0800
```

%cn：提交者名称（Committer Name）
%cd：提交者时间（Committer Date）

### 哈希值 - 作者，相对日期 : message  
```bash  
$ git log --pretty=format:"%h - %an, %ar : %s"  
```  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git log --pretty=format:"%h - %an, %ar : %s" -1  
51da54a - lxwcd, 7 days ago : update fix_B  
```  
  
### 哈希值 - 作者，绝对日期 : message  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git log --pretty=format:"%h - %an, %ad : %s" -1  
51da54a - lxwcd, Sun Jan 12 21:22:45 2025 +0800 : update fix_B  
```  
  
## ASCII 图形显示历史 --graph  
  
官方示例：  
```bash  
$ git log --pretty=format:"%h %s" --graph  
* 2d3acf9 Ignore errors from SIGCHLD on trap  
*  5e3ee11 Merge branch 'master' of https://github.com/dustin/grit.git  
|\  
| * 420eac9 Add method for getting the current branch  
* | 30e367c Timeout code and tests  
* | 5a09431 Add timeout protection to grit  
* | e1193f8 Support for heads with slashes in them  
|/  
* d6016bc Require time for xmlschema  
*  11d191e Merge branch 'defunkt' into local  
```  
  
## 显示提交的引用信息 --decorate  
从 Git 2.10 版本开始，`--decorate` 选项默认是开启的。  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git log --oneline -1  
51da54a (HEAD -> fix_B) update fix_B  
```  
  
如果希望关闭 `--decorate` 选项，可以使用 `--no-decorate`：  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git log --oneline --no-decorate -1  
51da54a update fix_B  
```  
这个命令会显示最近一次提交的详细信息，但不会显示指向该提交的引用名称。  
  
假设有以下提交历史：  
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
  
## 根据 Commit Date 筛选日志 
> [Git - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History#pretty_format)   
  
`--since`和`--until`参数可以用来限制显示特定时间范围内的提交：  
  
```bash  
$ git log --since="2 weeks ago"  
```  

  
### 绝对时间  
```bash  
git log --since="2024-12-01" --until="2024-12-31"  
git log --since="2024-12-01 00:00:00" --until="2024-12-31 23:59:59"  
```  
  
### 相对时间  
  
```bash  
git log --since="1 week ago"  
git log --until="yesterday"  
git log --since="2 days ago"  
git log --since="1 hour ago"  
git log --since="1 minute ago"  
git log --since="2 weeks ago" --until="1 week ago"  
git log --since="yesterday" --until="today"  
```  

### 示例
新建一个提交记录，修改 Author Date 使其和 Commit Date 不同
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_C)
$ git commit --date="5 days ago" -m "modify 2.txt, change author date"
[fix_C 9d7b614] modify 2.txt, change author date
 Date: Tue Feb 4 22:44:33 2025 +0800
 1 file changed, 1 insertion(+)
```

查看日志：
```bash

lx@lx MINGW64 /d/Documents/git_test04 (fix_C)
$ git log --pretty=fuller -3
commit 9d7b614d7f37f3e6fbe29967f8d499e8d736d4d1 (HEAD -> fix_C)
Author:     lxwcd <15521168075@163.com>
AuthorDate: Tue Feb 4 22:44:33 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 22:44:33 2025 +0800

    modify 2.txt, change author date

commit b3e36b570b1067a9a3bf6e57fe33589afbfdb31c
Author:     John <John@163.com>
AuthorDate: Sun Feb 9 20:46:40 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 20:46:40 2025 +0800

    add files and modify author

commit 69cf6cc13264c001fb2857eb647bf7d116c2cb50
Author:     lxwcd <15521168075@163.com>
AuthorDate: Sat Feb 1 21:31:08 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sat Feb 1 21:31:08 2025 +0800

    modify 2.txt
```

筛选 Commit Date 在 2025 年 2 月 1 日之后的日志，即最新的两个日志，最新的提交 Author Date 不符合，但仍会筛选：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_C)
$ git log --since="2025-2-2" --pretty=fuller
commit 9d7b614d7f37f3e6fbe29967f8d499e8d736d4d1 (HEAD -> fix_C)
Author:     lxwcd <15521168075@163.com>
AuthorDate: Tue Feb 4 22:44:33 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 22:44:33 2025 +0800

    modify 2.txt, change author date

commit b3e36b570b1067a9a3bf6e57fe33589afbfdb31c
Author:     John <John@163.com>
AuthorDate: Sun Feb 9 20:46:40 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 20:46:40 2025 +0800

    add files and modify author
```

## --author-date-order 根据 Author Date 筛选日志 (?)
> [Git - git-log Documentation](https://git-scm.com/docs/git-log#Documentation/git-log.txt---author-date-order) 

> Show no parents before all of its children are shown, but otherwise show commits in the author timestamp order.

```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_C)
$ git log --author-date-order --pretty=fuller -2
commit 95e40db1e205b1de7ac81fb58d40c7114df160b8 (HEAD -> fix_C)
Author:     lxwcd <15521168075@163.com>
AuthorDate: Mon Jan 20 22:53:50 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 22:53:50 2025 +0800

    modify 2.txt, change author date

commit 9d7b614d7f37f3e6fbe29967f8d499e8d736d4d1
Author:     lxwcd <15521168075@163.com>
AuthorDate: Tue Feb 4 22:44:33 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 22:44:33 2025 +0800

    modify 2.txt, change author date
```

这里没有按照 Author Date 的顺序排序？

## --top0-order  
> [Git - git-log Documentation](https://git-scm.com/docs/git-log#Documentation/git-log.txt---topo-order) 

> Show no parents before all of its children are shown, and avoid showing commits on multiple lines of history intermixed.

For example, in a commit history like this:

```bash
---1----2----4----7
    \	             \
     3----5----6----8---
```

where the numbers denote the order of commit timestamps, git rev-list and friends with --date-order show the commits in the timestamp order: 8 7 6 5 4 3 2 1.

With --topo-order, they would show 8 6 5 3 7 4 2 1 (or 8 7 4 2 6 5 3 1); some older commits are shown before newer ones in order to avoid showing the commits from two parallel development track mixed together.

## 作者和关键词搜索  
  
`--author`和`--grep`参数可以用来根据作者或提交信息中的关键词来过滤提交：  
  
```bash  
$ git log --author="Scott Chacon" --grep="version"  
```  
  
这将显示所有作者为“Scott Chacon”且提交信息中包含“version”的提交。  
  
## 查看特定文件的日志  
  
可以通过文件路径来限制显示特定文件的提交历史：  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git log --oneline  -- test02.txt  
51da54a (HEAD -> fix_B) update fix_B  
b3852e1 (origin/branch01) local git rebase  test test02.txt  
e67a0f3 add test02.txt and test03.txt  
332de10 update file  
```  
  
## 查看特定内容的日志 -S  
`git log -S` 选项是一个非常有用的过滤器，用于查找那些改变了指定字符串出现次数的提交。  
这个选项通常被称为 Git 的“pickaxe”选项。  
  
`-S<string>` 选项用于查找那些添加或删除了指定字符串的提交。这可以帮助你快速定位某个特定代码片段或功能的引入和修改历史。  
`-S` 选项使用简单的字符串匹配，而不是正则表达式。  
对于大型项目，使用 `-S` 选项可能会比较慢，因为它需要检查每个提交中的每个文件。  
  
```bash  
$ git log --oneline -S "function_name"  
8ef1913 local modify test01.txt  
e67a0f3 add test02.txt and test03.txt  
332de10 update file  
470dcf0 add files  
```  
  
这个命令会列出所有添加或删除了 `function_name` 这个字符串的提交。  
  
## 正则表达式筛选特定内容的日志  
> [Git - git-log Documentation](https://git-scm.com/docs/git-log#Documentation/git-log.txt-code-Gltregexgtcode)   
  
```bash  
git log -G"frotz\(nitfol"  
```  
  
> While git log -G"frotz\(nitfol" will show this commit, git log -S"frotz\(nitfol" --pickaxe-regex will not (because the number of occurrences of that string did not change).  
  
## 显示第一个父提交 --first-parent  
> [Visualize Merge History with git log --graph, --first-parent, and --no-merges](https://redfin.engineering/visualize-merge-history-with-git-log-graph-first-parent-and-no-merges-c6a9b5ff109c)  
  
`git log --first-parent` 用于查看提交历史时只显示每个提交的第一个父提交。这在处理包含合并提交的历史时特别有用，因为它可以从“主分支”的角度查看历史，跳过那些来自合并分支的提交。  
  
- **显示第一父提交**：`--first-parent` 选项告诉 `git log` 只显示每个提交的第一个父提交。这对于理解主分支（如 `main` 或 `master`）的线性历史非常有帮助，因为它会忽略那些通过合并操作引入的分支提交。  
- **应用场景**：当你想要查看主分支的清晰历史，而不被合并操作引入的复杂分支历史干扰时，这个选项非常有用。例如，如果你遵循一个严格的分支策略，其中所有功能分支最终都合并回主分支，`--first-parent` 可以帮助你只看到主分支上的关键提交。  
  
对于有多个分支的项目，如果其他分支用 `git merge` 合并到主分支，后，合并到主分支上最终会产生一个合并的提交记录，该合并的提交有两个父提交，当前分支所在的合并前的最新提交为 first parent，而另一个分支的最新提交为 second parent。  
```bash  
lx@lx MINGW64 /d/Documents/git_test (main)  
$ git log --oneline --graph -15  
*   a00fc7a (HEAD -> main) Merge branch 'fix_B'  
|\  
| * 099b5e1 (fix_B) update test files' '  
| * 51da54a update fix_B  
| * 9aaa1c6 (branch01) fix B  
| * 09035ad commit C  
| * e8867c1 commit B  
| * 0b4aed3 commit A  
| * b3852e1 (origin/branch01) local git rebase  test test02.txt  
| * 8ef1913 local modify test01.txt  
| * c8d5a84 Update test01.txt  git pull  
* | 03d14ae (origin/main) update main test01.txt  
* | 737c5b7 commit B  
|/  
* e67a0f3 add test02.txt and test03.txt  
* 332de10 update file  
* 470dcf0 add files  
```  
  
如上面 `a00fc7a` 合并提交，其 first parent 为 `03d14ae`，其 second parent 为 `099b5e`。  
  
如果只显示 first parent，则只会显示 main 分支上的提提交和最终合并到 main 上的提交：  
```bash  
lx@lx MINGW64 /d/Documents/git_test (main)  
$ git log --oneline --graph --first-parent -15  
* a00fc7a (HEAD -> main) Merge branch 'fix_B'  
* 03d14ae (origin/main) update main test01.txt  
* 737c5b7 commit B  
* e67a0f3 add test02.txt and test03.txt  
* 332de10 update file  
* 470dcf0 add files  
```  
  
### 查看合并提交的多个父提交  
```bash  
lx@lx MINGW64 /d/Documents/git_test (main)  
$ git show a00fc7a --shortstat  
commit a00fc7a17f1e55dee84a79f4d16b4e88edb0ba00 (HEAD -> main)  
Merge: 03d14ae 099b5e1  
Author: lxwcd <15521168075@163.com>  
Date:   Sun Jan 19 18:34:59 2025 +0800  
  
    Merge branch 'fix_B'  
  
 12 files changed, 322 insertions(+)  
```  
  
从 `Merge: 03d14ae 099b5e1` 可以看出，03d14ae 为 first parent, 099b5e1 为 second parent。  
  
## 排除合并信息 --no-merges  
`--no-merges` 选项用于排除合并信息。当使用 `--no-merges` 选项时，`git log` 只显示那些没有合并操作的提交。  
  
所有提交：  
```bash  
lx@lx MINGW64 /d/Documents/git_test (main)  
$ git log --oneline --graph --no-merges -15  
* 099b5e1 (fix_B) update test files' '  
* 51da54a update fix_B  
* 9aaa1c6 (branch01) fix B  
* 09035ad commit C  
* e8867c1 commit B  
* 0b4aed3 commit A  
* b3852e1 (origin/branch01) local git rebase  test test02.txt  
* 8ef1913 local modify test01.txt  
* c8d5a84 Update test01.txt  git pull  
| * 03d14ae (origin/main) update main test01.txt  
| * 737c5b7 commit B  
|/  
* e67a0f3 add test02.txt and test03.txt  
* 332de10 update file  
* 470dcf0 add files  
```  
  
排除合并后的提交：  
```bash  
lx@lx MINGW64 /d/Documents/git_test (main)  
$ git log --oneline --graph -15  
*   a00fc7a (HEAD -> main) Merge branch 'fix_B'  
|\  
| * 099b5e1 (fix_B) update test files' '  
| * 51da54a update fix_B  
| * 9aaa1c6 (branch01) fix B  
| * 09035ad commit C  
| * e8867c1 commit B  
| * 0b4aed3 commit A  
| * b3852e1 (origin/branch01) local git rebase  test test02.txt  
| * 8ef1913 local modify test01.txt  
| * c8d5a84 Update test01.txt  git pull  
* | 03d14ae (origin/main) update main test01.txt  
* | 737c5b7 commit B  
|/  
* e67a0f3 add test02.txt and test03.txt  
* 332de10 update file  
* 470dcf0 add files  
```  
  
## 查看不同分支差异  
  
```bash  
$ git log foo bar ^baz  
```  
  
上面命令查看那些可达于 foo 或 bar 分支，但不可达于 baz 的提交。即列出那些在 foo 或 bar 分支上存在，但在 baz 分支上不存在的提交。  
  
## 查看一个分支相对于另一个分支的提交差异  
  
### git log branch1..branch2  
  
```bash  
$ git log origin..HEAD --oneline  
```  
  
HEAD 当前分支最新提交相对于 origin 分支最新提交的提交记录，即 HEAD 有但 origin 没有的提交记录  
  
和下面命令功能相同：  
```bash  
$ git log HEAD ^origin --oneline  
```  
  
# git show  
> [Git - git-show Documentation](https://git-scm.com/docs/git-show)   
  
`git show` 用于展示各种 Git 对象的详细内容，包括提交（commit）、标签（tag）和分支（branch）。  
  
> Shows one or more objects (blobs, trees, tags and commits).  
> For commits it shows the log message and textual diff. It also presents the merge commit in a special format as produced by git diff-tree --cc.  
> For tags, it shows the tag message and the referenced objects.  
> For trees, it shows the names (equivalent to git ls-tree with --name-only).  
> For plain blobs, it shows the plain contents.  
> Some options that git log command understands can be used to control how the changes the commit introduces are shown.  
> This manual page describes only the most frequently used options.  
  
## 查看当前分支最新提交的详细信息  
```bash  
git show  
```  
输出最新提交修改的文件内容  
  
## 查看当前分支最新提交的详细信息  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git show main --stat  
commit a00fc7a17f1e55dee84a79f4d16b4e88edb0ba00 (main)  
Merge: 03d14ae 099b5e1  
Author: lxwcd <15521168075@163.com>  
Date:   Sun Jan 19 18:34:59 2025 +0800  
  
    Merge branch 'fix_B'  
  
 .gitignore              |   1 +  
 0001-commit-B.patch     |  33 ++++++++++++  
 0001-fix-B.patch        |  23 +++++++++  
 0001-update-fix_B.patch |  41 +++++++++++++++  
 0002-commit-C.patch     |  20 ++++++++  
 0002-update-fix_B.patch |  41 +++++++++++++++  
 1.patch                 |   1 +  
 2.txt                   |   1 +  
 git.md                  | 130 ++++++++++++++++++++++++++++++++++++++++++++++++  
 test01.txt              |  28 +++++++++++  
 test02.txt              |   2 +  
 test05.txt              |   1 +  
 12 files changed, 322 insertions(+)  
```  
  
## 查看特定提交的信息  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git log --oneline -2  
099b5e1 (HEAD -> fix_B) update test files' '  
51da54a update fix_B  
```  
  
查看上面第二个提交的文件名的修改情况：  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git log --oneline -2 | cut -d" " -f1 | tail -n1 | xargs git show --name-status  
commit 51da54a57cdc95263072173726d187a544725289  
Author: lxwcd <15521168075@163.com>  
Date:   Sun Jan 12 21:22:45 2025 +0800  
  
    update fix_B  
  
M       test01.txt  
M       test02.txt  
A       test05.txt  
  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git log --oneline -2  
099b5e1 (HEAD -> fix_B) update test files' '  
51da54a update fix_B  
```  
  
## --name-only  
仅显示提交中涉及的文件名列表。  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git show --name-only  
commit 099b5e1194fcb305b239e1a04d1a8ddac66bdb3d (HEAD -> fix_B)  
Author: lxwcd <15521168075@163.com>  
Date:   Sun Jan 19 18:33:57 2025 +0800  
  
    update test files'  
    '  
  
.gitignore  
0001-commit-B.patch  
0001-fix-B.patch  
0001-update-fix_B.patch  
0002-commit-C.patch  
0002-update-fix_B.patch  
1.patch  
2.txt  
git.md  
test01.txt  
```  
上面显示最新提价涉及的文件名。  
  
## --name-status  
显示提交中涉及的文件名以及它们的状态（新增、修改、删除）。  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git show --name-status  
commit 099b5e1194fcb305b239e1a04d1a8ddac66bdb3d (HEAD -> fix_B)  
Author: lxwcd <15521168075@163.com>  
Date:   Sun Jan 19 18:33:57 2025 +0800  
  
    update test files'  
    '  
  
A       .gitignore  
A       0001-commit-B.patch  
A       0001-fix-B.patch  
A       0001-update-fix_B.patch  
A       0002-commit-C.patch  
A       0002-update-fix_B.patch  
A       1.patch  
A       2.txt  
A       git.md  
M       test01.txt  
```  
  
## --stat  
显示提交的统计信息，包括每个文件的增删行数和文件状态。  
  
## --shortstat  
显示提交的简要统计信息，只包括每个文件的增删行数。  
  
## --summary  
显示提交的统计信息摘要，类似于 `--stat`，但不包括每个文件的详细信息。  
  
## --patch  
显示提交的差异（默认选项），展示具体的代码变化。  
  
## --full-index  
显示差异时，显示完整的索引信息。  
  
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
> [git diff - Comparing Changes in Git | Refine](https://refine.dev/blog/git-diff-command/#highlighting-diff-changes-in-one-line)   
  
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
  
差异内容显示从 a 版本到 b 版本需要做的修改。  
  
## 比较工作区和暂存区的差异  
> [Git - git-diff Documentation](https://git-scm.com/docs/git-diff#Documentation/git-diff.txt-codegitdiffcode)   
> [git diff - Comparing Changes in Git | Refine](https://refine.dev/blog/git-diff-command/#basic-example)   
  
```bash  
git diff  
```  
这个命令显示自上次提交以来**未暂存**的更改。  
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
  
- a 暂存区，旧版本  
- b 工作区，最新版本，比 a 多了已修改但未暂存的内容  
- `100644` 中 `100` 表示文件类型为普通文件，`644` 表示文件权限，可以通过 `ll` 查看：  
```bash  
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)  
$ ll test01.txt  
-rw-r--r-- 1 lx 197121 56 12月 21 22:10 test01.txt  
```  
- `@@ -4,3 +4,4 @@ local modify test01.txt`   
a 版本的修改从第 4 行开始，共 3 行  
b 版本的修改为第 4 行开始，共 4 行  
- `001` 表示 a 版本需要增加改行才能和 b 版本一致  
  
## 比较已暂存的文件和最新提交的差异  
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
a 表示最新的提交版本，旧版本  
b 表示暂存区的版本，新版本，已修改且已暂存的版本  
  
## 比较工作区和最新提交的差异  
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
a 表示最新的提交版本，旧版本  
b 表示工作目录的版本，新版本  
  
## 比较当前工作目录中特定文件和最新提交的差异  
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
  
a 表示最新的提交版本  
b 表示工作目录的版本  
指定查看 test01.txt 文件和 HEAD 的差异。  
  
## 比较当前工作目录和任意提交的差异  
```bash  
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)  
$ git diff 332de10  
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
```  
  
a 为指定的提交版本  
b 为当前工作目录，包括未暂存的修改，不包括未跟踪的文件  
  
## 比较当前已暂存和任意提交的差异   
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
```  
  
a 为指定的提交版本  
b 为当前工作目录已暂存的文件修改  
  
## 比较两个提交  
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
```  
  
a 为 332de10 提交版本  
b 为当前分支最新提交。  
  
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
```  
  
a 为当前分支最新提交。  
b 为 332de10 提交版本  
相当于 332de10 相对于 HEAD 的变化，因此 HEAD 中增加的内容前面为 -，表示需要减去这些内容才能和 a 的版本一致。  
  
## 比较当前最新提交和上一次提交的差异  
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
  
a 为 HEAD^ 上一次提交版本  
b 为 HEAD 最新提交版本  
  
## 比较两个分支最新提交的差异  
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
  
## 比较一个分支相对于另一个分支的差异  
> [git diff - Comparing Changes in Git | Refine](https://refine.dev/blog/git-diff-command/#git-diff-between-two-branches-three-dots-method)   
  
```bash  
git diff <branch1>...<branch2>  
```  
  
这个命令显示从 `branch1` 和 `branch2` 的共同祖先到 `branch2` 的所有差异。  
即从两个分支开始分叉后，branch2 上所有的提交内容相对共同祖先的差异。  
查看差异中 a 为两个分支共同的祖先，b 为 branch2 最新提交。  
  
注意和 ```git diff <branch1>..<branch2>``` 的区别，两个点号表示两个分支最新提交的差异。  
  
## 查看差异的文件名  
```bash  
$ git diff --name-only  
```  
  
## 比较工作目录和 stash 中特定文件差别  
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
  
a 为 stash@{0} 的版本  
b 为当前工作目录  
  
## 比较暂存区和 stash 中特定文件差别  
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
  
a 为 stash@{0}  
b 为暂存区  
  
## 查看当前最新提交和 stash 的差异  
```bash  
git diff stash@{0} HEAD  
```  
  
a 为 stash@{0}  
b 为HEAD  
  
## 查看两个分支某个文件的差异  
```bash  
git diff <branch1> <branch2> -- <file-path>  
```  
  
要查看两个分支中某个文件夹的差异：  
```bash  
git diff <branch1> <branch2> -- <folder-path>  
```  
  
## 比较标签  
```bash  
git diff <tag1> <tag2>  
```  
这个命令比较两个标签之间的差异。  
  
## git diff --base` 比较合并冲突中的文件版本  
> [git diff - Comparing Changes in Git | Refine](https://refine.dev/blog/git-diff-command/#using---base-with-git-diff)   
  
`git diff --base` 命令用于比较合并冲突中的文件版本。具体来说，`--base` 选项用于显示合并冲突中基线版本（即合并前的共同祖先版本）与当前工作目录中的版本之间的差异。  
  
通过使用 `git diff --base`，可以查看合并冲突中基线版本与当前工作目录中的版本之间的差异。  
  
```bash  
git diff --base <file>  
```  
这条命令会显示文件 `<file>` 的基线版本与当前工作目录中的版本之间的差异。  
  
## git diff 导出补丁文件  
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
  
## 生成最近一次提交的补丁文件  
  
```bash  
lx@LAPTOP-VB238NKA MINGW64 /d/Documents/git_test (fix_B)  
$ git format-patch HEAD^  
0001-update-fix_B.patch  
```  
  
## 生成最近两次提交的补丁文件  
  
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
  
## 生成指定提交范围的补丁文件  
  
```bash  
git format-patch <start-commit>..<end-commit>  
```  
  
这条命令会生成从 `<start-commit>` 到 `<end-commit>` 之间的所有提交的补丁文件。  
例如，生成从 `abc123` 到 `def456` 之间的所有提交的补丁文件：  
但不包括 start-commit 那个提交。  
  
如果希望包括起点和终点两个提交，则如下：  
```bash  
lx@LAPTOP-VB238NKA MINGW64 /e/src_git/demo (develop)  
$ git format-patch --output-directory=../patch c433384cd^..910b59afe  
../patch/0001-modify-test01.md.patch  
../patch/0002-modify-test02.patch  
../patch/0003-modify-test03.patch  
```  
  
## 生成某个提交以来的所有补丁文件  
  
```bash  
git format-patch <commit>  
```  
  
这条命令会生成从指定提交以来的所有提交的补丁文件，但不包括指定的提交。  
  
## 生成从根到某个提交的所有补丁文件  
  
```bash  
git format-patch --root <commit>  
```  
  
这条命令会生成从仓库的根到指定提交的所有补丁文件。  
  
## 输出格式选项  
  
### 输出到标准输出  
  
```bash  
git format-patch --stdout <commit> > output.patch  
```  
  
这条命令会将补丁文件输出到标准输出，并重定向到 `output.patch` 文件中。  
  
### 以 mbox 格式输出  
  
```bash  
git format-patch --mbox <commit>  
```  
  
这条命令会以 mbox 格式输出补丁文件，适合通过电子邮件发送。  
  
### 以原始格式输出  
  
```bash  
git format-patch --raw <commit>  
```  
  
这条命令会以原始格式输出补丁文件，适合向非 Git 存储库应用补丁。  
  
### 按顺序编号补丁  
  
```bash  
git format-patch --numbered <commit>  
```  
  
### 使用 --subject-prefix 自定义补丁文件前缀  
  
`--subject-prefix` 选项可以自定义补丁文件名的前缀。默认前缀是 `[PATCH]`，但你可以通过这个选项更改它。  
  
**命令**：  
```bash  
git format-patch --subject-prefix="MY_PATCH" <commit>  
```  
  
这条命令会生成补丁文件，文件名前缀为 `MY_PATCH`。例如，生成的文件名可能是 `0001-MY_PATCH-commit-message.patch`。  
  
### 使用 --output-directory 自定补丁文件目录  
  
`--output-directory` 选项可以指定生成的补丁文件的保存目录。  
  
```bash  
git format-patch --subject-prefix="MY_PATCH" --output-directory=/path/to/patches --suffix=.txt HEAD^  
```  
  
这条命令会生成从 `HEAD^` 到 `HEAD` 之间的所有提交的补丁文件，文件名前缀为 `MY_PATCH`，后缀为 `.txt`，并保存到 `/path/to/patches` 目录中。生成的文件名可能是 `0001-MY_PATCH-commit-message.txt`。  
  
### 使用 --numbered-files 生成仅包含数字的文件名  
  
`--numbered-files` 选项可以生成仅包含数字的文件名，不包含提交信息。  
  
```bash  
git format-patch --numbered-files <commit>  
```  
  
这条命令会生成补丁文件，文件名仅为数字，例如 `0001.patch`、`0002.patch` 等。  
  
### 使用 --suffix 指定补丁文件后缀  
  
`--suffix` 选项可以自定义补丁文件的后缀名。默认后缀名是 `.patch`，但你可以通过这个选项更改它。  
  
```bash  
git format-patch --suffix=.txt <commit>  
```  
  
这条命令会生成补丁文件，文件名后缀为 `.txt`，例如 `0001-commit-message.txt`。  
  
# 应用补丁文件  
  
## git apply 应用补丁文件  
  
```bash  
git apply /path/to/mypatch.patch  
```  
  
这条命令会将 `mypatch.patch` 文件中的更改应用到当前工作目录中。  
如果应用成功，会看到提示信息。  
如果应用失败，Git 会提示哪些更改无法应用，并给出相应的错误信息。  
  
如果补丁文件有多个，在一个目录中，应用时不能指定目录，需要遍历里面的文件来应用：  
```bash  
for patch in ../patch/*.patch; do  
    git apply "$patch"  
done  
```  
  
## git am 应用补丁文件  
  
```bash  
git am /path/to/mypatch.patch  
```  
  
这条命令会将 `mypatch.patch` 文件作为新的提交应用到当前分支中。  
如果补丁文件应用成功，Git 会自动创建一个新的提交，其中包含补丁中的更改。  
如果应用失败，Git 会提示哪些更改无法应用，并给出相应的错误信息。  
  
# git blame 查看文件每行的最新提交信息  
> [Git - git-blame Documentation](https://git-scm.com/docs/git-blame)   
> [git diff - Comparing Changes in Git | Refine](https://refine.dev/blog/git-diff-command/#using-git-diff-with-other-git-commands)   
  

显示的是 Author Name 和 Author Date，而不是 Committer Name 和 Committer Date。  
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D_copy)
$ git show --pretty=fuller 91b0e3c6
commit 91b0e3c6432ccf89a9809c087fe933bf05c6966e
Author:     Alice <ALice@163.com>
AuthorDate: Thu Jan 2 14:00:00 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 21:17:51 2025 +0800

    Fix bug

diff --git a/2.txt b/2.txt
index e36953d..6ea0285 100644
--- a/2.txt
+++ b/2.txt
@@ -1,2 +1,3 @@
 222
 fix_c
+111
```

下面 2.txt 的 111 内容是上面提交修改的，显示的是 Author Date，而不是 Committer Date：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D_copy)
$ git blame 2.txt
f54dd265 (lxwcd 2025-01-19 21:13:50 +0800 1) 222
69cf6cc1 (lxwcd 2025-02-01 21:31:08 +0800 2) fix_c
91b0e3c6 (Alice 2025-01-02 14:00:00 +0800 3) 111
0cda0f60 (lxwcd 2025-02-09 21:25:57 +0800 4) 222
```

# git checkout  
> [Git - git-checkout Documentation](https://git-scm.com/docs/git-checkout)   
  
`git checkout` 是 Git 中用于切换分支或检出特定版本的文件到工作目录的命令。  
  
## 切换分支  
```bash  
git checkout <branch-name>  
```  
  
如果分支已存在，则切换到该分支。  
如果分支不存在，但分支名在远程仓库存在，则创建并切换到该分支，且设置本地该分支跟踪远程对应名字的分支，相当于执行 `git checkout -b <branch-name> origin/<branch-name>`。  
  
## 创建新分支并切换  
```bash  
git checkout -b <new-branch-name>  
```  
或者在较新版本的 Git 中：  
```bash  
git switch -c <new-branch-name>  
```  
这些命令会创建一个新的分支，并立即切换到这个分支。  
  
## 基于远程分支创建新分支并切换  
```bash  
git checkout -b <new-branch-name> origin/<branch-name>  
```  
这个命令会创建一个新的分支，并将其设置为跟踪远程分支 `origin/<branch-name>`。  
  
## 检出特定文件到工作目录  
```bash  
git checkout <branch-name> -- <file-path>  
```  
这个命令会从 `<branch-name>` 分支检出 `<file-path>` 文件到当前工作目录，替换本地的文件。  
  
## 检出特定提交到工作目录  
```bash  
git checkout <commit-hash> -- <file-path>  
```  
这个命令会从 `<commit-hash>` 提交检出 `<file-path>` 文件到当前工作目录。  
  
## 检出特定提交到新分支  
```bash  
git checkout <commit-hash> -b <new-branch-name>  
```  
这个命令会创建一个新的分支 `<new-branch-name>` 并检出 `<commit-hash>` 提交的内容到这个新分支。  
  
## 恢复已修改但未暂存的文件  
```bash  
git checkout -- <file-path>  
```  
这个命令会将 `<file-path>` 文件恢复到最近一次提交的状态，放弃本地的修改。  
检出最新提交的相应文件替换当前工作目录的文件。  
  
## 恢复已暂存的文件  
```bash  
git restore --staged -- <file-path>  
```  
或者：  
```bash  
git checkout -- <file-path>  
```  
这些命令会将 `<file-path>` 文件从暂存区取消暂存，恢复到工作目录的状态。  
  
## 检出标签对应的版本  
```bash  
git checkout <tag-name>  
```  
这个命令会检出包含 `<tag-name>` 标签的提交，通常用于检出某个特定的发布版本。  
  
## 有冲突时指定使用版本  
  
两个仓库中的一个分支都修改了文件 2.txt 的相同一行，但修改内容内容不同，一个仓库已经将修改推送到远程仓库，另一个仓库修改后提交到本地，然后 git pull 时提示有冲突：  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (fix_B)  
$ git pull  
remote: Enumerating objects: 5, done.  
remote: Counting objects: 100% (5/5), done.  
remote: Compressing objects: 100% (1/1), done.  
remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0 (from 0)  
Unpacking objects: 100% (3/3), 239 bytes | 9.00 KiB/s, done.  
From https://github.com/lxwcd/git_test  
   15f80f2..f54dd26  fix_B      -> origin/fix_B  
Auto-merging 2.txt  
CONFLICT (content): Merge conflict in 2.txt  
Automatic merge failed; fix conflicts and then commit the result.  
```  
  
查看当前工作目录的状态，可以看见有个文件处于冲突中，待解决：  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (fix_B|MERGING)  
$ git status  
On branch fix_B  
Your branch and 'origin/fix_B' have diverged,  
and have 1 and 1 different commits each, respectively.  
  (use "git pull" if you want to integrate the remote branch with yours)  
  
You have unmerged paths.  
  (fix conflicts and run "git commit")  
  (use "git merge --abort" to abort the merge)  
  
Unmerged paths:  
  (use "git add <file>..." to mark resolution)  
        both modified:   2.txt  
  
no changes added to commit (use "git add" and/or "git commit -a")  
  
```  
  
查看冲突文件的内容：  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (fix_B|MERGING)  
$ cat 2.txt  
<<<<<<< HEAD  
22  
=======  
222  
>>>>>>> f54dd265ddebde6a06e2ea619a0588d2b1555945  
```  
  
`<<<<<<< HEAD` 表示下方表示当前版本  
`=======` 表示分隔符，下方内容为冲突版本的内容  
`>>>>>>> f54dd265ddebde6a06e2ea619a0588d2b1555945` 表示冲突结束位置  
  
### 使用对方版本  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (fix_B|MERGING)  
$ git checkout --theirs 2.txt  
Updated 1 path from the index  
  
lx@lx MINGW64 /d/Documents/git_test03 (fix_B|MERGING)  
$ cat 2.txt  
222  
```  
  
### 使用本地版本  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (fix_B|MERGING)  
$ git checkout --ours 2.txt  
Updated 1 path from the index  
  
lx@lx MINGW64 /d/Documents/git_test03 (fix_B|MERGING)  
$ cat 2.txt  
22  
```  
  
### 添加到暂存区  
选择版本后，将这些文件添加到暂存区：  
  
```bash  
git add <file-path>  
```  
  
### 继续合并  
如果你已经解决了所有文件的冲突，你可以继续完成合并操作：  
  
```bash  
git commit -m "message"  
```  
  
或者   
```bash  
git merge --continue  
```  
  
# git checkout 和 git cherry-pick  
`git checkout <commit-hash> -- <file-path>` 命令和 `git cherry-pick` 命令都可以用来将更改应用到当前分支，但它们的目的和行为有所不同。  
  
## `git checkout <commit-hash> -- <file-path>`  
这个命令用于从特定的提交（`<commit-hash>`）中检出文件（`<file-path>`）到当前工作目录。这个操作不会改变分支的历史记录，也不会创建新的提交。它仅仅是替换工作目录中的文件内容，用指定提交中的文件版本覆盖。这个命令不会记录任何新的提交，也不会影响项目的提交历史。  
  
## `git cherry-pick`  
`git cherry-pick` 命令用于将一个或多个提交的应用到当前分支，从而创建新的提交。这个操作会将指定提交的更改作为新的提交引入到当前分支的历史中。`git cherry-pick` 可以用于将特定提交从一个分支应用到另一个分支，或者在同一个分支中重新应用已经存在的提交。  
  
# git branch  
> [Git - git-branch Documentation](https://git-scm.com/docs/git-branch/2.13.7)   
  
`git branch` 是一个用于创建、列出、删除和管理 Git 分支的命令。  
分支在 Git 中是一个轻量级的移动指针，指向代码历史的某个特定提交。  
  
## 创建分支  
```bash  
git branch <branch-name>  
```  
这个命令会创建一个新分支，但不会切换到该分支。  
  
## 创建并切换分支  
```bash  
git checkout -b <branch-name>  
```  
或者在某些 Git 版本中：  
```bash  
git switch -c <branch-name>  
```  
这些命令会创建一个新分支并立即切换到该分支。  
  
## 列出所有本地分支  
```bash  
git branch  
```  
这个命令会列出所有的本地分支。  
  
## 列出所有远程分支  
```bash  
git branch -r  
```  
这个命令会列出所有的远程分支。  
  
## 列出所有本地和远程分支  
```bash  
git branch -a  
```  
这个命令会列出所有的本地分支和远程分支。  
  
## 显示当前分支  
```bash  
git branch --show-current  
```  
或者使用 `git rev-parse --abbrev-ref HEAD`。  
这个命令会显示当前检出的分支名称。  
  
## 删除分支  
```bash  
git branch -d <branch-name>  
```  
这个命令会删除一个已经完全合并到当前分支的本地分支。如果分支未完全合并，Git 会阻止删除以防止数据丢失。  
  
## 强制删除分支  
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
  
## 设置上游分支  
```bash  
git branch -u <remote-branch>  
```  
或者使用 `git branch --set-upstream-to <remote-branch>`。  
这个命令会设置当前分支跟踪指定的远程分支。  
  
## 查看当前分支与上游分支的对应关系  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git branch -vv  
  branch01  9aaa1c6 [origin/branch01: ahead 4] fix B  
  feature01 b387cb1 [origin/tb01: ahead 2] Merge branch 'tb01' of https://github.com/lxwcd/git_test into feature01  
  feature02 f3f08ca add test04.txt  
* fix_B     f54dd26 [origin/fix_B] update 2.txt 222  
  main      a00fc7a [origin/main: ahead 10] Merge branch 'fix_B'  
  tb01      f9e71d6 [origin/tb01] Update test01.txt  
```  
  
- 显示所有分支及其上游信息  
- `*` 表示当前分支的对应关系  
- 显示与远程分支的 ahead  和 behind 的信息  
  
## 查看当前分支与上游分支的对应关系  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git branch -vv | grep "*"  
* fix_B     f54dd26 [origin/fix_B] update 2.txt 222  
```  
  
## 包含已合并/未合并信息  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git branch  
  branch01  
  fix_B  
* main  
  tb01  
  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git branch --merged  
* main  
  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git branch --no-merged  
  branch01  
  fix_B  
  tb01  
```  
  
将 `branch01` 分支合并到 `main` 分支后查看：  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git branch --merged  
  branch01  
* main  
```  
  
## 删除远程跟踪分支  
```bash  
git branch -dr <remote/branch>  
```  
这条命令会删除本地的远程跟踪分支。但并不会直接删除远程仓库中的分支，只是删除了本地对远程分支的跟踪信息。  
  
## 删除本地分支的上游分支设置  
  
```bash  
git branch --unset-upstream my-branch  
```  
  
# git switch   
`git switch` 是 Git 2.23 版本引入的命令，用于切换分支。这个命令的作用与 `git checkout` 类似，但提供了更清晰的语义和错误检查。  
  
如果工作目录中有未被跟踪的文件，可以切换，未被跟踪的文件也会出现在切换后的分支上。  
  
## 切换到已存在的分支  
```bash  
git switch <branch-name>  
```  
  
## 创建并切换新分支  

### 依据当前分支创建新分支
```bash  
git switch -c <new-branch-name>  
```  

新分支和当前分支一摸一样

### 依据其他分支创建新分支
```bash
git switch -c <新分支名> <来源分支名>
```

```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_C)
$ git switch -c dev origin/main
branch 'dev' set up to track 'origin/main'.
Switched to a new branch 'dev'

lx@lx MINGW64 /d/Documents/git_test04 (dev)
$ git branch -vv
* dev      e190c9a [origin/main] update note
  fix_B    baddcc2 [origin/fix_B: ahead 1] add files and modify author
  fix_C    3b634a7 [origin/fix_B: ahead 5, behind 2] modify 1.patch , change author date
  fix_D    2c28453 modify test01.txt
  fix_E    1609512 [fix_D: ahead 2] Merge branch 'fix_D' into fix_E
  main     03d14ae [origin/main: ahead 2, behind 19] update main test01.txt
  main2    3b671ba [origin/main: ahead 9, behind 19] modify test01.txt , add C
  main2_01 f537c63 modify test01.txt , add C
  main3    d228105 [origin/main: ahead 6, behind 19] cherry-pick fix_C and commit manually
```
  
和 `git checkout -b <new-branch> <existing-branch>` 相同功能。

## 强制创建新分支  
```bash  
git switch -C <new-branch>  
```  
  
如果 `<new-branch>` 已经存在，它将被重置为 `<start-point>`。  
这相当于先执行 `git branch -f <new-branch>` 然后执行 `git switch <new-branch>`。  
  
## 根据远程分支创建本地分支  
使用 `git switch --track` 命令创建一个新的本地分支，并设置它跟踪远程分支。  
  
```bash  
git switch --track origin/feature  
```  
或者使用 `-t` 选项：  
```bash  
git switch -t origin/feature  
```  
创建一个新的本地 `feature` 分支，并立即设置它跟踪远程的 `origin/feature` 分支。  
  
也可以使用下面方法：  
```bash  
git checkout -b feature origin/feature  
```  
  
## 使用 `-d` 或 `--detach` 参数切换到一个提交  
  
```bash  
git switch -d <commit-hash>  
```  
  
分离的HEAD 允许你直接切换到任何提交，而不需要创建一个分支。切换后所做的修改，提交，甚至 push 到远程都不会影响其他分支。  
切换到其他分支后拉取远程仓库的最新代码，之前分离 HEAD 后 Push 的内容看不到提交记录。  
  
## 快速切换回前一个分支  
```bash  
git switch -  
```  
  
## 从远程分支创建同名的本地分支并关联远程分支  
```bash  
git switch testmaster  
```  
这会拉取远程分支到本地，并建立远程分支和本地分支的关联关系。  
  
## 创建孤儿分支  
```bash  
git switch --orphan <new-branch>  
```  
这会创建一个新的孤儿分支，并删除所有跟踪的文件。  
  
## 使用 `--recurse-submodules` 更新所有初始化的子模块  
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
  
## 选项  
  
- **`-A` 或 `--all`**：暂存所有更改，包括新文件和删除的文件。  
- **`-u`**：仅暂存已跟踪文件的更改，不包括新文件。  
- **`-p`**：交互式地选择要暂存的更改。  
- **`-i`**：启动交互式暂存模式，允许你选择要暂存的更改。  
- **`-N` 或 `--intent-to-add`**：标记新文件为暂存状态，但不实际添加内容。  
  
## 暂存文件  
```bash  
git add <file1> <file2> ...  
```  
这个命令将多个文件的更改添加到暂存区。  
  
## 暂存所有更改  
```bash  
git add .  
```  
或者  
```bash  
git add --all  
```  
这些命令将所有更改（包括新文件和修改的文件）添加到暂存区。  
  
## 使用通配符  
```bash  
git add *.cpp *.h  
```  
  
## 交互式暂存  
  
使用 `git add -i` 或 `git add --interactive` 可以进入交互式暂存模式，这允许你逐个选择要暂存的更改。这个模式特别有用，当你有多个更改但只想提交其中一部分时。  
  
## 查看可 add 的文件  
`git add -n` 或 `--dry-run` 是一个 Git 命令选项，用于模拟 `git add` 操作而不实际将文件添加到暂存区。  
  
- **模拟添加操作**：`-n` 选项用于模拟 `git add` 命令的行为。它不会实际将文件添加到暂存区，而是显示哪些文件将被添加。  
- **查看影响**：使用这个选项可以帮助你了解执行 `git add` 命令时哪些文件会被影响，从而避免意外添加不需要的文件。  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git add . --dry-run  
add 'test03.txt'  
```  
  
# git commit  
> [Git - git-commit Documentation](https://git-scm.com/docs/git-commit)   
  
`git commit` 是 Git 中用于记录更改的命令。它将暂存区中的更改保存到本地仓库的历史记录中。  
  
1. **记录更改**：`git commit` 将暂存区中的更改保存为一个新的提交（commit），并记录更改的内容和时间。  
2. **更新项目历史**：每次提交都会更新项目的提交历史，形成一个版本记录。  
3. **要求提交信息**：执行提交时，Git 会要求你提供一个提交信息，以描述所做的更改。  
  
## 选项  
  
- **`-m`**：指定提交信息。  
- **`-a` 或 `--all`**：自动暂存所有已跟踪文件的更改并提交。  
- **`--amend`**：修改最后一次提交。这允许你更改最近一次提交的信息或内容。  
- **`-C <commit>`**：使用指定提交的信息作为当前提交的信息。  
- **`--dry-run`**：模拟提交操作，显示将要提交的内容，但不实际创建提交。  
  
## 指定提交信息 -m  
```bash  
git commit -m "Commit message"  
```  
使用 `-m` 选项可以直接在命令行中指定提交信息。  
  
## 提交所有更改 -am  
```bash  
git commit -a -m  
```  
使用 `-a` 选项会自动将所有已跟踪文件的更改添加到暂存区并提交，但不包括新文件。  
  
## 修改最后一次提交 --amend  

  
`git commit --amend` 是一个Git命令，用于修改最近一次提交的信息。  
  
- 如果刚刚做了一次提交，然后意识到提交信息有误或者不完整，可以使用 `git commit --amend` 来修改它。  
- 如果在提交后发现还有一些更改忘记加入，你可以使用 `git commit --amend` 将这些更改加入到上一个提交中。  
- 如果修改提交内容后不更新提交日志，可以加 `--no-edit` 选项。  
```bash  
git commit --amend --no-edit  
```  

### 不修改 Author Date 但更新 Commit Date

初始提交记录：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (main2)
$ git commit --author="Bob <Bob@163.com>" --date="3 hours ago" -m "modify test01.txt, add 22"
[main2 13bdace] modify test01.txt, add 22
 Author: Bob <Bob@163.com>
 Date: Sun Feb 9 18:58:12 2025 +0800
 1 file changed, 1 insertion(+)
```

```bash
lx@lx MINGW64 /d/Documents/git_test04 (main2)
$ git log --pretty=fuller -1
commit 13bdace88eb6634b44a7d19dace0622daf7fcf59 (HEAD -> main2)
Author:     Bob <Bob@163.com>
AuthorDate: Sun Feb 9 18:58:12 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 21:58:12 2025 +0800

    modify test01.txt, add 22
```

修改提交记录：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (main2)
$ git commit --amend --no-edit
[main2 0d3ace1] modify test01.txt, add 22
 Author: Bob <Bob@163.com>
 Date: Sun Feb 9 18:58:12 2025 +0800
 1 file changed, 2 insertions(+)
```

查看日志发现作者日期没变，但提交日期变了。
```bash
lx@lx MINGW64 /d/Documents/git_test04 (main2)
$ git log --pretty=fuller -1
commit 0d3ace1ef1def9863b9523ab1bd682c5ccfd4e1c (HEAD -> main2)
Author:     Bob <Bob@163.com>
AuthorDate: Sun Feb 9 18:58:12 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 22:01:53 2025 +0800

    modify test01.txt, add 22
```

### --reset-author 重置作者信息

初始提交记录：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (main2_01)
$ git log --pretty=fuller -1
commit 13bdace88eb6634b44a7d19dace0622daf7fcf59 (HEAD -> main2_01)
Author:     Bob <Bob@163.com>
AuthorDate: Sun Feb 9 18:58:12 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 21:58:12 2025 +0800

    modify test01.txt, add 22
```

修改提交记录，且重置作者信息：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (main2_01)
$ echo "2" >> test01.txt

lx@lx MINGW64 /d/Documents/git_test04 (main2_01)
$ git add .
warning: in the working copy of 'test01.txt', LF will be replaced by CRLF the next time Git touches it

lx@lx MINGW64 /d/Documents/git_test04 (main2_01)
$ git commit --amend --reset-author --no-edit
[main2_01 d4d8db7] modify test01.txt, add 22
 1 file changed, 2 insertions(+)
```

查看日志发现作者重置为当前用户，作者日期更新为当前日期，提交日期也更新了。
```bash
lx@lx MINGW64 /d/Documents/git_test04 (main2_01)
$ git log --pretty=fuller -1
commit d4d8db752aed39f7256a8ff4f6db5026ad0f7047 (HEAD -> main2_01)
Author:     lxwcd <15521168075@163.com>
AuthorDate: Sun Feb 9 22:07:46 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 22:07:46 2025 +0800

    modify test01.txt, add 22
```
  
### 注意事项  
- **重写历史**：  
`git commit --amend` 实际上会创建一个新的提交对象，它有一个不同的提交ID。这意味着它会重写项目的历史。  
如果已经将原始提交推送到了远程仓库，那么使用 `git commit --amend` 后，需要使用 `git push --force` 来更新远程仓库。 使用强制推送最好先查看本地和远程的提交记录，如果本地和远程在 --amend 修改记录前一样，则可以强制推送；如果远程有新的提交记录，则不要强制推送。  
  
- **使用场景限制**：  
`git commit --amend` 只能用于最近的提交。如果你想要修改更早的提交，你需要使用 `git rebase` 命令。  
  
## 从文件读取提交日志 -F  
```bash  
git commit -F commit_msg.txt  
```  

## 输入多行提交日志  
可以直接 git commit，这样会进入一个输入界面，输入多行提交日志。

或者用下面方法：

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

## --author 修改作者信息
在提交时指定一个不同于当前 Git 配置的作者信息时，可以使用 `--author` 参数。 例如代表别人提交代码时。
```bash
--author="<name> <email>"
```

```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_C)
$ git commit --author="John <John@163.com>" -m "add files and modify author"
[fix_C b3e36b5] add files and modify author
 Author: John <John@163.com>
 24 files changed, 390 insertions(+)
```

查看日志，提交者信息不变：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_C)
$ git log --pretty=fuller -1
commit b3e36b570b1067a9a3bf6e57fe33589afbfdb31c (HEAD -> fix_C)
Author:     John <John@163.com>
AuthorDate: Sun Feb 9 20:46:40 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 20:46:40 2025 +0800

    add files and modify author
```

作者时间（Author Date） 和 提交者时间（Committer Date） 都是当前时间。
作者信息（Author Name 和 Author Email） 是你指定的 John Doe <john.doe@example.com>。
提交者信息（Committer Name 和 Committer Email） 是当前的 Git 配置。


## --date 修改 Author Date
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D)
$ date
2025年02月 9日 21:17:02
```

```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D)
$ git commit --date="2025-01-02 14:00:00" -m "Fix bug" --author="Alice <ALice@163.com>"
[fix_D 91b0e3c] Fix bug
 Author: Alice <ALice@163.com>
 Date: Thu Jan 2 14:00:00 2025 +0800
 1 file changed, 1 insertion(+)
```

查看日志，Author Date 被修改为指定时间，但 commit date 为当前时间。
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D)
$ git log --pretty=fuller -1
commit 91b0e3c6432ccf89a9809c087fe933bf05c6966e (HEAD -> fix_D)
Author:     Alice <ALice@163.com>
AuthorDate: Thu Jan 2 14:00:00 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 21:17:51 2025 +0800

    Fix bug
```

## --reset-author 重置提交作者信息
> When used with -C/-c/--amend options, or when committing after a conflicting cherry-pick, declare that the authorship of the resulting commit now belongs to the committer. This also renews the author timestamp.
  
### git commit --amend --reset-author 重置提交作者信息

`git commit --amend` 不会修改作者信息

但加上 `--reset-author` 作者重置为当前用户，作者日期更新为当前日期，提交日期也更新为当前时间。

### git cherry-pick 解决冲突后不修改 Author Date

## 钩子脚本  
  
- **`prepare-commit-msg`**：在编辑提交信息之前运行。  
- **`commit-msg`**：在提交信息被接受但提交尚未完成时运行。  
- **`post-commit`**：在提交完成后运行。  
  
## 处理错误的提交  
> [Git Guides - git commit](https://github.com/git-guides/git-commit#what-can-go-wrong-while-changing-history)   
  
- `git revert`是更改历史记录的最安全方式。它不会删除现有提交，而是在新提交中应用特定提交引入变化的逆操作。  
- `git reset`是一个强大的命令，可以移动HEAD指针和分支指针到另一个时间点，但可能会导致工作丢失。在使用`git reset`之前，确保与团队沟通，并了解三种类型的重置（--soft, --mixed, --hard）。  
- `git reflog`是一个记录HEAD指向的每个提交的日志。如果你在使用`git reset`时无意中丢失了提交，可以使用`git reflog`找到并访问它们。  
- `git commit --amend`只更改当前分支上的最近一次提交。  
这个命令对于尚未推送到远程的提交、提交信息中有拼写错误或者提交中未包含预期更改的情况非常有用。  
  
# git rm 删除文件  
> [Git - git-rm Documentation](https://git-scm.com/docs/git-rm)   
> [How to Delete a File or a Directory from a Git Repository](https://www.w3docs.com/snippets/git/how-to-delete-a-file-from-a-git-repository.html)  
  
`git rm` 是 Git 中用于删除已被 git 跟踪的文件的命令。它不仅从工作目录中删除文件，还从暂存区和 Git 仓库中删除文件。  
  
1. **删除文件**：`git rm` 用于删除工作目录中的文件，并将此删除操作添加到暂存区。  
2. **更新暂存区**：删除操作会被记录在暂存区中，以便在下次提交时更新仓库。  
3. **可选的提交**：虽然 `git rm` 将删除操作添加到暂存区，但它不会自动提交更改。需要使用 `git commit` 来提交这些更改。  
  
## 使用场景  
  
- **移除不再需要的文件**：当你需要从项目中删除文件，并确保这些更改被版本控制时，可以使用 `git rm`。  
- **清理仓库**：在重构或清理项目时，`git rm` 可以帮助你移除旧文件或不再使用的文件。  
  
## 选项  
  
- **`-r` 或 `--recursive`**：递归地删除目录及其内容。  
- **`-f` 或 `--force`**：强制删除文件，即使它们已经被修改但尚未暂存。  
- **`-n` 或 `--dry-run`**：模拟删除操作，显示将要删除的文件，但不实际删除。  
- **`-v` 或 `--verbose`**：在删除文件时显示详细信息。  
  
## 删除单个文件  
```bash  
git rm <file>  
```  
  
## 删除多个文件  
```bash  
git rm <file1> <file2> ...  
```  
  
## 删除目录  
```bash  
git rm -r <directory>  
```  
使用 `-r` 选项可以递归地删除目录及其内容。  
  
## git rm --cached 保留文件到工作目录  
- `git rm --cached` 将文件从 Git 的索引（也称为暂存区）中移除，这意味着该文件将不再被 Git 跟踪和管理。  
- 与普通的 `git rm` 命令不同，`--cached` 选项使得 Git 只是从版本控制中移除文件，而不会从你的本地工作目录中删除实际的文件。  
  
### 用途  
- 不想跟踪特定的文件或文件夹，例如大型数据文件、自动生成的文件或者敏感信息。  
- 已经误将不应该被版本控制的文件添加到了 Git 中，需要将其从版本控制中移除。  
- 调整 `.gitignore` 文件，使得新的忽略规则生效。有时候，即使你在 `.gitignore` 中添加了规则，已经追踪的文件依然会被提交。在这种情况下，你需要先使用 `git rm --cached` 移除这些文件，然后再提交更改。  
  
# git mv 移动文件  
> [Git - git-mv Documentation](https://git-scm.com/docs/git-mv)   
  
`git mv` 是 Git 中用于重命名或移动文件和目录的命令。与普通的文件系统操作不同，`git mv` 不仅在文件系统中移动或重命名文件，还会记录这一更改在 Git 的历史记录中。  
  
1. **重命名文件**：将文件的名称更改，并更新 Git 仓库中的相关记录。  
2. **移动文件**：将文件从一个目录移动到另一个目录，并更新 Git 仓库中的相关记录。  
3. **记录更改**：`git mv` 会将文件的移动或重命名作为一次提交的一部分记录下来。  
  
## 使用场景  
  
- **文件重命名**：当你需要更改文件的名称，并且希望这个更改被版本控制跟踪时。  
- **文件移动**：当你需要将文件从一个目录移动到另一个目录，并且希望这个移动操作被版本控制跟踪时。  
  
## 选项  
  
- **`-f` 或 `--force`**：强制移动或重命名文件，即使目标已经存在。  
- **`-n` 或 `--no-overwrite`**：如果目标文件已经存在，不覆盖它。  
- **`-k` 或 `--keyword`**：使用关键字参数来指定文件重命名的规则。  
  
## 重命名文件  
```bash  
git mv <old-name> <new-name>  
```  
这个命令将 `<old-name>` 文件重命名为 `<new-name>`。  
  
## 移动文件  
```bash  
git mv <file> <directory>  
```  
这个命令将 `<file>` 移动到 `<directory>` 目录中。  
  
## 移动目录  
```bash  
git mv <old-directory> <new-directory>  
```  
这个命令将 `<old-directory>` 目录重命名为 `<new-directory>`。  
  
# git reflog  
> [Git - git-reflog Documentation](https://git-scm.com/docs/git-reflog)  
  
`git reflog` 是 Git 中一个非常强大的命令，它用于管理和查看引用日志（reflogs）。引用日志记录了本地仓库中更新分支和其他引用的操作。  
  
`git reflog` 记录了 HEAD 和分支引用以及标签等的所有更新操作。这意味着即使某些提交被删除或者重写，你仍然可以通过 `git reflog` 来找到它们。  
  
`git reflog` 是 Git 操作的一道安全保障，它能够记录几乎所有本地仓库的改变，包括所有分支的 commit 提交，以及已经被删除的 commit。这使得 `git reflog` 成为恢复丢失提交或分支的重要工具。  
  
## 查看引用日志  
最基本的用法是 `git reflog`，它会显示 HEAD 的引用日志，列出 HEAD 的所有历史更新操作，包括分支切换、提交、重置等。  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git reflog  
fc003e8 (HEAD -> main) HEAD@{0}: commit: rename 1.txt to 11.txt:wq  
e43f274 HEAD@{1}: checkout: moving from orb to main  
f9e71d6 (origin/tb01, tb01) HEAD@{2}: checkout: moving from main to tb01  
e43f274 HEAD@{3}: checkout: moving from 0676fcbfe8e0b54b47d8bf168d440febb5abe0b8 to main  
```  
  
这里 `HEAD@{n}` 表示 HEAD 在过去第 n 次操作时的位置。  
  
## show  
显示指定引用的日志，如果未指定引用，则默认显示 HEAD 的日志。`git reflog show` 是 `git log -g --abbrev-commit --pretty=oneline` 的别名。  
  
```bash  
git reflog show <ref>  
```  
  
## list  
列出所有有对应 reflog 的引用。  
```bash  
git reflog list  
```  
  
## expire  
修剪旧的 reflog 条目，可以指定时间来删除过时的日志条目。  
```bash  
git reflog expire [--expire=<time>] [--expire-unreachable=<time>] [--all]  
```  
  
## delete  
删除单个 reflog 条目，需要指定确切的条目。  
  
```bash  
git reflog delete <ref>@{<specifier>}  
```  
  
## exists  
检查某个引用是否有 reflog。  
```bash  
git reflog exists <ref>  
```  
  
## 基于时间的引用  
`git reflog` 支持基于时间的引用，例如 `HEAD@{1.day.ago}` 表示 HEAD 在一天前的位置。  
```bash  
git diff main@{0} main@{1.day.ago}  
```  
这个命令比较了 `main` 分支当前状态和一天前的状态。  
  
  
# Undo things  
> [Git - Undoing Things](https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things)   
  
## 修改本地的最新提交 git commit --amend  
- 仅针对本地最新的提交  
- 最新提交还未推送到远程  
  
## git reset 撤销本地多个提交   
> [Git - Reset Demystified](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified#_git_reset)   
> [Git - git-reset Documentation](https://git-scm.com/docs/git-reset)   
> [Git - git-reset Documentation](https://git-scm.com/docs/git-reset#_discussion)   
  
`git reset` 是 Git 中用于重置当前 HEAD 和（可选地）索引（暂存区）的命令。它可以用来撤销提交、重置暂存区或恢复工作目录中的文件。  
  
1. **撤销提交**：`git reset` 可以将当前分支的 HEAD 指针移动到指定的状态，但不影响工作目录。  
2. **重置暂存区**：它可以将暂存区的内容重置为特定提交的状态。  
3. **恢复工作目录**：`git reset` 还可以用来恢复工作目录中的文件到特定提交的状态。  
  
撤销最新的提交：  
```bash  
git reset --soft HEAD^  
```  
  
撤销最近的三次提交：  
```bash  
git reset --soft HEAD~3  
```  
  
### 使用场景  
  
- **撤销错误的提交**：当你提交了错误的更改并希望撤销这些提交时。  
- **重置暂存区**：当你想要清除暂存区中的更改时。  
- **恢复文件**：当你想要将文件恢复到特定提交的状态时。  
  
### `--soft`  
  
- 重置 HEAD 到指定状态，但保留工作目录和暂存区的状态。  
  
### `--mixed`（默认）  
  
- 重置 HEAD 和暂存区到指定状态，但保留工作目录的状态。  
  
### `--hard`  
  
- 重置 HEAD、暂存区和工作目录到指定状态。  
  
### `--merge`  
  
- 重置 HEAD 到指定状态，并尝试合并工作目录和暂存区的更改。  
  
### `--keep`  
  
- 重置 HEAD 到指定状态，但保留工作目录和暂存区的状态，即使这意味着 HEAD 指向不同的分支。  
  
### 显示被撤销的提交  
执行 `git reset --soft HEAD^` 后查看被撤销的上次提交，直接用 `git log` 无法查看之前被撤销的提交。  
  
#### 使用 `ORIG_HEAD`  
  
当执行 `git reset` 时，Git 会自动创建一个名为 `ORIG_HEAD` 的引用，指向原始的 `HEAD` 位置。  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git log ORIG_HEAD --oneline -2  
fc003e8 rename 1.txt to 11.txt:wq  
e43f274 (HEAD -> main) Merge branch 'branch01'  
  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git log --oneline -2  
e43f274 (HEAD -> main) Merge branch 'branch01'  
03d14ae (origin/main, origin/HEAD) update main test01.txt  
```  
  
#### 使用 `git reflog`  
  
`git reflog` 显示 `HEAD` 的更新历史，你可以通过它找到被撤销的提交：  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git log --oneline -3  
36c7d37 (HEAD -> main) update new  
e43f274 Merge branch 'branch01'  
03d14ae (origin/main, origin/HEAD) update main test01.txt  
```  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git reflog -4  
36c7d37 (HEAD -> main) HEAD@{0}: commit: update new  
e43f274 HEAD@{1}: reset: moving to HEAD^  
5e51d74 HEAD@{2}: commit: update  
e43f274 HEAD@{3}: reset: moving to HEAD^  
```  
  
可以看见在 `5e51d74` 提交后，进行 reset，因此 HEAD 又变成 `e43f274`，然后又继续有新的提交。  
  
## 撤销暂存区的添加 git restore --staged  
撤销后修改仍会存在工作目录，但处于未暂存的状态。  
  
如撤销暂存区的全部修改：  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git restore --staged .  
```  
  
## 撤销未暂存的修改 git restore  
  
撤销未暂存的全部修改，不影响已暂存的文件：  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git restore .  
```  
  
## 撤销未暂存的修改 git restore  
  
仅撤销未暂存的修改，不影响已暂存的修改。  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git status  
On branch main  
Your branch is ahead of 'origin/main' by 5 commits.  
  (use "git push" to publish your local commits)  
  
Changes to be committed:  
  (use "git restore --staged <file>..." to unstage)  
        modified:   test02.txt  
  
Changes not staged for commit:  
  (use "git add <file>..." to update what will be committed)  
  (use "git restore <file>..." to discard changes in working directory)  
        modified:   test03.txt  
```  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git restore .  
```  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git status  
On branch main  
Your branch is ahead of 'origin/main' by 5 commits.  
  (use "git push" to publish your local commits)  
  
Changes to be committed:  
  (use "git restore --staged <file>..." to unstage)  
        modified:   test02.txt  
```  
  
## 撤销工作目录全部修改 git reset  
  
让工作目录和 HEAD 一致  
```bash  
git reset --hard HEAD  
```  
  
## Reset a single file in the index  
> [Git - git-reset Documentation](https://git-scm.com/docs/git-reset#Documentation/git-reset.txt-Resetasinglefileintheindex)   
  
## Keep changes in working tree while discarding some previous commits  
> [Git - git-reset Documentation](https://git-scm.com/docs/git-reset#Documentation/git-reset.txt-Keepchangesinworkingtreewhilediscardingsomepreviouscommits)   
  
## Split a commit apart into a sequence of commits  
> [Git - git-reset Documentation](https://git-scm.com/docs/git-reset#Documentation/git-reset.txt-Splitacommitapartintoasequenceofcommits)   
  
## 撤销远程的提交 git revert  
本地提交后 Push 到远程，本地用 git reset --soft HEAD^ 撤销了最近一次提交，如果远程该分支只有自己用，且远程没有比本地更新的提交，则可以 git push --force 覆盖远程提交记录。  
  
如果远程有更新的提交记录，则可以用 `git revert HEAD`，会新建一个撤销上次提交的提交记录，因此不会和远程冲突。  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git log --oneline -3  
36c7d37 (HEAD -> main) update new  
e43f274 Merge branch 'branch01'  
03d14ae (origin/main, origin/HEAD) update main test01.txt  
```  
  
撤销最新一次提交  
```bash  
git revert HEAD  
```  
  
查看历史记录，发现过去的历史没有改变，只是新增了撤销的记录：  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (main)  
$ git log --oneline -3  
fabbb86 (HEAD -> main) Revert "update new"  
36c7d37 update new  
e43f274 Merge branch 'branch01'  
```  
  
撤销后可以用 `git push` 推送到远程仓库。  
  
# git restore  
> [Git - git-restore Documentation](https://git-scm.com/docs/git-restore)   
  
```bash  
git restore [<options>] [--source=<tree>] [--staged] [--worktree] [--] <pathspec>…  
```  
  
1. **恢复工作目录文件**：`git restore` 用于将工作目录中的文件恢复到某个特定的状态。这可以是从 `HEAD`、索引（暂存区）或其他指定的源。  
2. **恢复索引内容**：使用 `--staged` 选项可以恢复索引（暂存区）的内容。  
3. **恢复工作目录和索引**：结合 `--staged` 和 `--worktree` 选项可以同时恢复工作目录和索引的内容。  
  
## 选项  
  
- **`--source=<tree>`**：指定恢复内容的源。可以是提交、分支或标签。默认情况下，如果没有指定 `--staged`，则从索引恢复；如果指定了 `--staged`，则从 `HEAD` 恢复。  
- **`--staged`**：恢复索引（暂存区）的内容。  
- **`--worktree`**：恢复工作目录的内容。  
- **`-p` 或 `--patch`**：交互式选择要恢复的更改块。  
- **`--ours` 和 `--theirs`**：在恢复工作目录文件时，使用索引中的第 2 阶段（`ours`）或第 3 阶段（`theirs`）来处理未合并的路径。  
- **`--merge`**：在恢复工作目录文件时，重新创建未合并路径的冲突合并。  
- **`--conflict=<style>`**：指定冲突块的显示方式，覆盖 `merge.conflictStyle` 配置变量。  
- **`--ignore-unmerged`**：在从索引恢复工作目录文件时，如果有未合并的条目且没有指定 `--ours`、`--theirs`、`--merge` 或 `--conflict`，则不中止操作。  
- **`--recurse-submodules`**：如果路径规范指定的是活动子模块，并且恢复位置包括工作目录，则只有在指定了此选项时才会更新子模块。  
  
## 指定恢复位置  
默认不指定则恢复工作目录。  
指定 `--staged` 则仅恢复暂存区。  
同时指定 `--staged --worktree` 则恢复工作目录和暂存区。  
  
## 恢复暂存区的特定文件  
  
已暂存的文件，希望取消暂存，但保持文件在工作目录中不变：  
```bash  
git restore --staged hello.c  
```  
  
## 恢复暂存区的全部文件  
  
```bash  
git restore --staged .  
```  
  
## 恢复暂存区的部分文件  
  
```bash  
git restore --staged *.cpp  
```  
  
## 恢复暂存区和工作目录的全部已跟踪的文件   
  
```bash  
$ git restore --source=HEAD --staged --worktree .  
```  
  
不会修改未跟踪的文件  
  
## 从其他提交中恢复文件  
  
```bash  
$ git restore --source=origin/main~2 test01.txt  
```  
将指定文件恢复到 `origin/main` 分支的当前提交的前 2 个提交的版本，且恢复的是工作目录，不影响暂存区。  
  
# git revert  
> [Git - git-revert Documentation](https://git-scm.com/docs/git-revert)   
  
`git revert` 用于撤销之前的提交。  
它创建一个新的提交，这个提交的内容是前一个提交的逆操作，即“反做”之前的提交。  
这个操作是安全的，因为它不会改变项目的历史记录，而是在历史记录的基础上新增一个提交来表示撤销操作。  
  
## --no-commit  
- 执行撤销操作但不创建一个新的提交对象。这允许修改撤销的内容后再手动提交。  
  
## --no-edit  
- 通常 `git revert` 会打开一个编辑器编辑提交信息。使用这个选项可以跳过编辑步骤，使用默认的提交信息。  
  
## --edit  
- 强制 `git revert` 打开编辑器，即使通常不需要编辑提交信息。  
  
## --merge  
- 在合并操作中使用，允许在合并冲突时撤销。  
  
## --mainline  
- 在合并操作中使用，指定主基线。  
  
## --strategy  
- 指定合并策略。  
  
## --strategy-option  
- 传递额外的选项给合并策略。  
  
## --allow-empty  
- 允许在空树（即没有任何提交的仓库）上执行撤销操作。  
  
## --onto  
- 指定一个基底提交，用于确定撤销操作的目标分支。  
  
## 撤销最新的提交  
```bash  
git revert HEAD  
```  
  
## 撤销特定的提交  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main2)  
$ git log --oneline -5  
dc76ad7 (HEAD -> main2) Revert "update test01.txt: add main"  
16ac277 update test01.txt: add main  
03d14ae (origin/main, origin/HEAD, main) update main test01.txt  
737c5b7 commit B  
e67a0f3 add test02.txt and test03.txt  
```  
  
如撤销上面最后一个提交，执行以下命令：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main2)  
$ git log --oneline -5 | tail -n1 | cut -d" " -f1  
e67a0f3  
  
lx@lx MINGW64 /d/Documents/git_test04 (main2)  
$ git log --oneline -5 | tail -n1 | cut -d" " -f1 | xargs git revert  
[main2 b93b033] Revert "add test02.txt and test03.txt"  
 Date: Mon Jan 20 20:50:14 2025 +0800  
 2 files changed, 1 insertion(+), 2 deletions(-)  
 delete mode 100644 test03.txt  
```  
  
撤销后查看日志，多了一个撤销的记录：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main2)  
$ git log --oneline -7  
b93b033 (HEAD -> main2) Revert "add test02.txt and test03.txt"  
dc76ad7 Revert "update test01.txt: add main"  
16ac277 update test01.txt: add main  
03d14ae (origin/main, origin/HEAD, main) update main test01.txt  
737c5b7 commit B  
e67a0f3 add test02.txt and test03.txt  
332de10 update file  
```  
  
## 撤销一系列提交  
- `git revert <commit>^..<commit>`：撤销从第一个提交到第二个提交之间的所有提交。  
- 不包括起始的提交  
  
## 撤销操作但不创建提交  
```bash  
git revert --no-commit abc123  
```  
  
## 撤销操作并编辑提交信息：  
```bash  
git revert --edit abc123  
```  
  
# git apply  
  
`git apply` 命令用于将补丁文件（通常是通过 `git diff` 生成的）应用到工作目录中的文件上。  
  
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
  
## 应用补丁文件  
  
```bash  
git apply patchfile.diff  
```  
这会将 `patchfile.diff` 中的差异应用到当前工作目录中的对应文件。  
  
## 检查补丁是否可应用  
```bash  
git apply --check patchfile.diff  
```  
这会检查 `patchfile.diff` 是否可以成功应用到当前工作目录中的文件，但不会实际应用补丁。  
  
## 应用补丁并添加到索引  
  
```bash  
git apply --index patchfile.diff  
```  
这会将补丁应用到索引中，而不仅仅是工作目录中的文件。  
  
# git stash  
> [Git - git-stash Documentation](https://git-scm.com/docs/git-stash)   
> [git stash - Saving Changes | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/saving-changes/git-stash)  
> [A practical guide to using the git stash command](https://opensource.com/article/21/4/git-stash)   
  
`git stash` 是 Git 中一个非常有用的命令，它允许临时保存工作目录中的修改，以便你可以在不提交这些修改的情况下切换分支或返回到一个干净的工作状态。  
  
> By default, running git stash will stash:  
> changes that have been added to your index (staged changes)  
> changes made to files that are currently tracked by Git (unstaged changes)  
>   
> But it will not stash:  
> new files in your working copy that have not yet been staged  
> files that have been ignored  
  
- **保存当前工作状态**：当你的工作目录中有未提交的更改，而这些更改可能阻碍你切换分支或执行其他操作时，`git stash` 可以让你保存这些更改，以便稍后恢复。  
- **保持工作目录干净**：使用 `git stash` 可以清理工作目录，让你可以在一个干净的状态下来执行其他 Git 操作，比如拉取最新的代码或切换分支。  
- **恢复工作状态**：你可以在任何时候恢复之前保存的工作状态，无论是在同一个分支还是不同的分支上。  
  
## git stash 存放位置  
  
> The latest stash you created is stored in refs/stash; older stashes are found in the reflog of this reference and can be named using the usual reflog syntax (e.g. stash@{0} is the most recently created stash, stash@{1} is the one before it, stash@{2.hours.ago} is also possible). Stashes may also be referenced by specifying just the stash index (e.g. the integer n is equivalent to stash@{n}).  
  
```bash  
$ cat .git/refs/stash  
07929627e841f63c9c306a647df4e84c32ae6de2  
  
$ git stash list  
stash@{0}: modify test.md  
stash@{1}: modify 1.md  
stash@{2}: modify 2.md  
stash@{3}: modify 3.md  
```  
  
## git stash push 保存工作状态  
git stash 和 git stash push 效果相同。  
  
> Save your local modifications to a new stash entry and roll them back to HEAD (in the working tree and in the index). The <message> part is optional and gives the description along with the stashed state.  
  
不会保存没有被跟踪的文件。  
  
### `-m` 或 `--message` 添加描述  
  
```bash  
git stash push -m "WIP: Implement login feature"  
```  
  
### `-p` 或 `--patch` 交互存储  
  
```bash  
git stash push -p  
```  
  
### `-k` 或 `--keep-index` 保留暂存区的更改  
  
只会将工作区的更改保存到 stash 中，而暂存区的更改将被保留。  
  
```bash  
git stash push -k  
```  
  
### `-u` 或 `--include-untracked` 包含未跟踪的文件  
默认情况下，`git stash push` 只会保存已被追踪的文件的更改。  
  
### `-a` 或 `--all` 保存全部文件  
这个选项会保存所有文件的更改，包括未跟踪的文件和被 `.gitignore` 忽略的文件。  
  
```bash  
git stash push -a  
```  
  
### `-q` 或 `--quiet` 静默执行  
  
```bash  
git stash push -q  
```  
使用这个选项后，命令执行时不会输出任何信息。  
  
### `--pathspec-from-file=<file>` 从文件读取  
这个选项允许从文件中读取路径规范，而不是从命令行参数中读取。如果文件内容是 `-`，则从标准输入读取。  
  
```bash  
git stash push --pathspec-from-file=pathspecs.txt  
```  
  
### `--`  
这个选项用于消除歧义，将路径规范与选项分开。  
  
```bash  
git stash push -- path/to/file  
```  
使用这个选项后，`path/to/file` 会被视为路径规范，而不是选项。  
  
## git stash save  
```bash  
git stash save "optional message"  
```  
这个命令会保存当前的工作状态到一个 stash 中，并清理工作目录。如果省略 `"optional message"`，Git 会自动生成一个消息。  
不会保存未被跟踪的文件。  
  
## 筛选部分文件保存  
  
```bash  
git diff HEAD --name-only | grep -E "*/demo/*" | xargs git stash push -m "stash demo files" --  
```  
或：  
```bash  
git status --porcelain | cut -d" " -f3- | grep -E "*/demo/*" | xargs git stash push -m "stash demo files" --  
```  
  
## git stash list 列出所有 stash  
```bash  
git stash list  
```  
这个命令会列出所有的 stash，每个 stash 前面都有一个标识符，如 `stash@{0}`。  
  
## git stash apply 应用 stash  
```bash  
git stash apply  
```  
这个命令会应用最近的 stash 到当前工作目录。  
  
也可以指定一个 stash 来应用：  
```bash  
git stash apply stash@{n}  
```  
其中 `n` 是 stash 的索引号，最新的 stash 编号为 0，编号最大的为最先 stash 的内容。  
  
## git stash drop 删除 stash  
```bash  
git stash drop stash@{n}  
```  
这个命令会删除指定的 stash。  
  
## git stash pop 应用 stash 并删除  
```bash  
git stash pop  
```  
这个命令会应用最近的 stash 并从 stash 列表中删除它。  
  
## git stash show 预览 stash 内容  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ git stash show stash@{0}  
 2.txt      |  1 -  
 test01.txt | 31 +++----------------------------  
 test03.txt |  1 +  
 3 files changed, 4 insertions(+), 29 deletions(-)  
```  
  
## 仅查看 stash 中文件名  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ git stash show stash@{0} --name-only  
2.txt  
test01.txt  
test03.txt  
```  
  
## 比较 stash 与当前工作目录差异  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ git stash show stash@{1} -p  
diff --git a/1.patch b/1.patch  
index e61c591..90d1dfa 100644  
--- a/1.patch  
+++ b/1.patch  
@@ -1 +1,2 @@  
 0001-update-fix_B.patch  
+1  
diff --git a/2.txt b/2.txt  
index c200906..91bc947 100644  
--- a/2.txt  
+++ b/2.txt  
@@ -1 +1,3 @@  
 222  
+22  
+2  
```  
  
- a 版本为工作目录版本  
- b 版本为 stash 中的版本   
  
## 应用 stash 中的特定文件  
  
当前工作目录的 2.txt 文件内容：  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ cat 2.txt  
222  
```  
  
应用 `stash@{1}` 中的 2.txt 版本：  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ git checkout stash@{1} -- 2.txt  
  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ cat 2.txt  
222  
22  
2  
```  
  
### 强制覆盖  
```bash  
git checkout --force stash@{0} -- <file-path>  
```  
或者：  
```bash  
git checkout -f stash@{0} -- <file-path>  
```  
  
## git stash clear 删除全部 stash 记录  
```bash  
git stash clear  
```  
  
## 找回被删除的 stash 记录  
> [How to undo git stash clear](https://stackoverflow.com/a/57095939/24889953)   
  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ git fsck --unreachable | grep commit | cut -d ' ' -f3 | xargs git log --merges --no-walk --oneline  
Checking object directories: 100% (256/256), done.  
Checking objects: 100% (33/33), done.  
99641b1 On test: stash test  
6fc3b2a WIP on test: 3030efb Merge branch 'fix_B' of https://github.com/lxwcd/git_test into fix_B  
99c8421 WIP on test: 3030efb Merge branch 'fix_B' of https://github.com/lxwcd/git_test into fix_B  
c66245f On fix_B: test  
c78d607 WIP on fix_B: c188c3c Merge branch 'fix_B' of https://github.com/lxwcd/git_test into fix_B  
d0bd729 WIP on fix_B: c188c3c Merge branch 'fix_B' of https://github.com/lxwcd/git_test into fix_B  
```  
  
根据日志的输出的 message 找到被删除的 stash，即 `9964b1`。  
  
将要恢复的 stash 记录重新 stash 并添加 message：  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ git update-ref --create-reflog refs/stash 99641b1 -m "restore stash : stash test"  
  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ git stash list  
stash@{0}: restore stash : stash test  
```  
  
# git fetch  
> [Git - git-fetch Documentation](https://git-scm.com/docs/git-fetch)   
> [Git Fetch | What is Git Fetch and How to Use it | Learn Git](https://www.youtube.com/watch?v=uEEcw1s_wWk&ab_channel=GitKraken)   
  
  
1. **获取远程更新**：`git fetch` 用于从远程仓库下载最新的提交、分支和标签信息。  
2. **不自动合并**：与 `git pull` 不同，`git fetch` 只是下载更新，不会自动合并到你的当前分支。这允许在合并之前检查远程更改。  
3. **更新远程跟踪分支**：`git fetch` 会更新本地的远程跟踪分支（如 `origin/master`），使其反映远程仓库的当前状态。  
  
## 选项  
  
- **`--all`**：从所有远程仓库获取更新。  
- **`--prune`**：清除远程跟踪分支中不再存在于远程仓库的分支。  
- **`--dry-run`**：模拟获取更新的过程，但不实际下载数据。  
- **`--verbose`**：显示详细的输出，包括下载过程中的信息。  
  
## 获取远程仓库的所有分支的最新状态  
```bash  
git fetch origin  
```  
  
## 获取特定远程分支的最新状态  
```bash  
git fetch origin develop  
```  
这个命令只会获取 `origin` 远程仓库的 `develop` 分支的最新状态。  
  
## 获取远程特定分支并映射到本地分支  
  
```bash  
git fetch origin src:dst  
```  
  
- src 为源端，即远程分支  
- dst 为目的端，即本地分支  
- 如果当前在 dst 分支，则无法 执行此命令  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ git fetch origin fix_B:test  
fatal: refusing to fetch into branch 'refs/heads/test' checked out at 'D:/Documents/git_test03'  
```  
  
## 删除远程不存在的分支引用 --prune  
```bash  
git fetch --prune  
```  
  
从远程仓库获取最新信息的同时， 清除远程跟踪分支中不再存在于远程仓库的分支。  
  
# git push  
> [Pushing commits to a remote repository - GitHub Docs](https://docs.github.com/en/get-started/using-git/pushing-commits-to-a-remote-repository)   
> [Git - git-push Documentation](https://git-scm.com/docs/git-push)   
  
`git push` 是一个将本地 Git 仓库的更改（提交）推送到远程仓库的命令。  
在 Git 的分布式版本控制模型中，每个开发者都有自己的本地仓库，并且通常也会有至少一个共享的远程仓库，通常是在服务器上。`git push` 命令使得开发者可以将本地的更改分享给其他团队成员。  
  
当运行 `git push` 命令时，Git 会尝试将指定的本地分支的更改推送到远程仓库。  
如果远程仓库中没有对应的分支，Git 会创建一个。  
  
  
## 设置本地分支跟踪远程分支  
  
推送到远程仓库的特定分支，而不是本地分支的同名分支：  
```bash  
git push <remote> <local-branch>:<remote-branch>  
```  
- `<remote>`：远程仓库的名称  
  
将本地 test 分支推送到远程的 test 分支，且设置跟踪状态，远程分支不存在则会在远程仓库中创建该分支：  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ git push -u origin HEAD:test  
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)  
remote:  
remote: Create a pull request for 'test' on GitHub by visiting:  
remote:      https://github.com/lxwcd/git_test/pull/new/test  
remote:  
To https://github.com/lxwcd/git_test.git  
 * [new branch]      HEAD -> test  
branch 'test' set up to track 'origin/test'.  
```  
  
- `:` 前为源分支，即本地分支  
- `:` 后为目的分支，即远程分支  
- `-u` 设置本地分支跟踪远程对应分支，以后可以直接 `git push`  
  
## 推送所有本地分支  
  
推送所有本地分支到远程仓库：  
```bash  
git push --all <remote>  
```  
  
## 推送所有标签  
  
如果想要推送所有本地标签到远程仓库，可以使用：  
```bash  
git push --tags <remote>  
```  
  
## 强制推送  
  
```bash  
git push --force <remote> <branch>  
```  
或者：  
```bash  
git push -f <remote> <branch>  
```  
  
## 删除远程分支  
  
```bash  
git push <remote> --delete <branch>  
```  
或者：  
```bash  
git push <remote> :<branch>  
```  
  
## 推送特定提交  
  
```bash  
git push <remote> <commit>:<branch>  
```  
  
# git pull  
> [Git - git-pull Documentation](https://git-scm.com/docs/git-pull)   
  
`git pull` 用于将远程仓库的更改拉取到本地仓库。  
它实际上是一个组合命令，等同于 `git fetch` 后跟 `git merge`。  
  
## 从远程仓库拉取最新代码并合并到当前分支  
```bash  
git pull origin master  
```  
这个命令会从远程仓库 `origin` 的 `master` 分支拉取最新的代码，并尝试与当前分支合并。  
  
如果当前分支已经设置跟踪远程分支，可以省略远程分支名：  
```bash  
git pull origin  
```  
  
如果当前分支只跟踪一个远程分支，可以完全省略参数：  
```bash  
git pull  
```  
  
## --rebase  
  
使用 `rebase` 代替 `merge` 来合并更改：  
```bash  
git pull --rebase origin master  
```  
  
## --ff-only  
  
只允许快进式合并，不允许产生新合并提交：  
```bash  
git pull --ff-only origin master  
```  
如果无法进行快进式合并，命令会失败。  
  
## --no-rebase  
  
覆盖配置选项，强制使用 `merge` 而不是 `rebase`：  
```bash  
git pull --no-rebase origin master  
```  
  
## --no-commit  
  
拉取后不自动提交合并的结果：  
```bash  
git pull --no-commit origin master  
```  
  
## --allow-unrelated-histories  
  
允许合并没有共同历史记录的分支：  
```bash  
git pull --allow-unrelated-histories origin master  
```  
  
## --tags  
  
拉取远程仓库的标签：  
```bash  
git pull --tags origin master  
```  
  
## --prune  
  
拉取后清除本地不存在于远程仓库的分支：  
```bash  
git pull --prune origin master  
```  
  
## --recurse-submodules  
  
递归地拉取和更新子模块：  
```bash  
git pull --recurse-submodules origin master  
```  
  
## --depth  
  
指定拉取的历史记录深度，减少拉取的数据量，加快拉取速度：  
```bash  
git pull --depth=1 origin master  
```  
  
## --verbose  
  
详细输出拉取的过程：  
```bash  
git pull --verbose origin master  
```  
  
## --progress  
  
显示拉取进度：  
```bash  
git pull --progress origin master  
```  
  
# git rebase  
> [git rebase | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase)   
> [Git - Rebasing](https://git-scm.com/book/en/v2/Git-Branching-Rebasing)   
> [git rebase - Why, When & How to fix conflicts](https://www.youtube.com/watch?v=DkWDHzmMvyg&ab_channel=Philomatics)   
> [Git Rebase --interactive: EXPLAINED](https://www.youtube.com/watch?v=H7RFt0Pxxp8&ab_channel=DevOpsToolbox)   

git rebase 会修改提交历史记录。
如果当前为 bug 分支，修改完后将 bug 分支合并到 main 分支，且 bug 分支只自己适用，合并完后不需要，可以尝试用 git rebase 进行合并，如果当前 bug 分支已经落后 main 分支很多，可以避免直接用 git merge 导致提交历史产生很长的分叉。

git rebase 的行为和 git cherry-pick 的效果相同，如果合并过程中有冲突，需要停下来修改冲突，因此会修改过去某个提交内容，如果不希望这样，则应该换其他合并方式，用 git rebase --abort 取消合并。
如果修改的提交是自己的提交记录，则可以继续用 rebase 合并。

进行合并前最好先复制当前分支来创建一个新分支操作。

## 合并有冲突解决示例

要将 fix_D 分支和 fix_C 分支合并，利用 rebase。

### 查看两个分支差异
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D)
$ git branch -vv | grep "*"
* fix_D      2c28453 [fix_C: ahead 3, behind 4] modify test01.txt
```

可见当前分支落后待合并分支 4 提交记录，超前待合并分支 3 提交记录。

进行 rebase 操作，则类似切换到 fix_C 分支，然后根据提交顺序将超前的三个提交从旧的提交开始依次 git cherry-pick 应用到 fix_C 分支。

查看超前的 3 个提交：
```cpp
lx@lx MINGW64 /d/Documents/git_test04 (fix_D)
$ git log fix_C..HEAD --oneline
2c28453 (HEAD -> fix_D) modify test01.txt
0cda0f6 modify 2.txt
91b0e3c Fix bug
```

### git rebase 合并
进行 rebase 操作，可以看到第一个在 fix_C 分支基础上应用 `91b0e3c Fix bug` 这个提交，且发生冲突：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D)
$ git rebase fix_C --verbose
Changes from b3e36b570b1067a9a3bf6e57fe33589afbfdb31c to 09cfa3587677d6bed88232919dcd356ad513c7fe:
 1.patch | 1 +
 2.txt   | 2 ++
 2 files changed, 3 insertions(+)
Rebasing (1/3)
Auto-merging 2.txt
CONFLICT (content): Merge conflict in 2.txt
error: could not apply 91b0e3c... Fix bug
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
hint: Disable this message with "git config advice.mergeConflict false"
Could not apply 91b0e3c... Fix bug

lx@lx MINGW64 /d/Documents/git_test04 (fix_D|REBASE 1/3)
$
```

可见 2.txt 文件冲突，可以用 git status 看到：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D|REBASE 1/3)
$ git status
interactive rebase in progress; onto 09cfa35
Last command done (1 command done):
   pick 91b0e3c Fix bug
Next commands to do (2 remaining commands):
   pick 0cda0f6 modify 2.txt
   pick 2c28453 modify test01.txt
  (use "git rebase --edit-todo" to view and edit)
You are currently rebasing branch 'fix_D' on '09cfa35'.
  (fix conflicts and then run "git rebase --continue")
  (use "git rebase --skip" to skip this patch)
  (use "git rebase --abort" to check out the original branch)

Unmerged paths:
  (use "git restore --staged <file>..." to unstage)
  (use "git add <file>..." to mark resolution)
        both modified:   2.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

### 解决冲突
根据实际需求，和提示的冲突文件名：

- 如果是普通文本文件，可以进入文件，在每个冲突的地方解决。
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D|REBASE 1/3)
$ cat 2.txt
222
fix_c
<<<<<<< HEAD
3
1
=======
111
>>>>>>> 91b0e3c (Fix bug)
```
- 可以 `git checkout --ours 2.txt` 或者 `git checkout --theirs 2.txt` 直接指定使用自己或者对方版本
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D|REBASE 1/3)
$ git checkout --theirs 2.txt
Updated 1 path from the index

lx@lx MINGW64 /d/Documents/git_test04 (fix_D|REBASE 1/3)
$ cat 2.txt
222
fix_c
111
```

### git add 添加解决完冲突的文件
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D|REBASE 1/3)
$ git add .

lx@lx MINGW64 /d/Documents/git_test04 (fix_D|REBASE 1/3)
$ git status
interactive rebase in progress; onto 09cfa35
Last command done (1 command done):
   pick 91b0e3c Fix bug
Next commands to do (2 remaining commands):
   pick 0cda0f6 modify 2.txt
   pick 2c28453 modify test01.txt
  (use "git rebase --edit-todo" to view and edit)
You are currently rebasing branch 'fix_D' on '09cfa35'.
  (all conflicts fixed: run "git rebase --continue")

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   2.txt
```

根据提示，第一个提交应用完成，接着会继续应用剩下两个提交。

### 继续合并
因为解决冲突从而修改了原始提交的内容，如果希望该提交信息仍保持和原始提交一致，则用 git rebase --continue，这样相当于对原始的提交 'fix_D' on '09cfa35' 进行了修改，类似用 git commit --amend，如果该提交是自己的提交，不介意修改了提交的内容，则可以用该方法。这样 Author Date 和 Author Name 不变，Commit Date 和 Commit Name 会变成当前时间和自己。
因此，如果修改的提交记录原始 Author 不是自己，则最好不用这种方法，以免修改其他人的提交记录。

如果希望修改这个提交记录的 Author Date，则自己手动提交。

#### git rebase --continue 继续合并
Author Name 和 Author Date 还是显示原始的作者和日期，但 Commit Name 和 Commit Date 是自己和当前时间。

#### git commit 重新创建提交

如果应用的提交 Author 不是自己，这样会修改 Author 的信息，最后显示 Author 变成自己，Author Date 更新为当前时间。
提交后还是需要 git rebase --continue 继续合并。

旧提交记录：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D|REBASE 1/3)
$ git show --pretty=fuller 91b0e3c
commit 91b0e3c6432ccf89a9809c087fe933bf05c6966e
Author:     Alice <ALice@163.com>
AuthorDate: Thu Jan 2 14:00:00 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 21:17:51 2025 +0800

    Fix bug

diff --git a/2.txt b/2.txt
index e36953d..6ea0285 100644
--- a/2.txt
+++ b/2.txt
@@ -1,2 +1,3 @@
 222
 fix_c
+111
```

重新提交该记录后 Author 变成自己：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D|REBASE 1/3)
$ git commit -m "rebase 91b0e3c Fix bug and fix confict"
[detached HEAD 01c7623] rebase 91b0e3c Fix bug and fix confict
 1 file changed, 1 insertion(+), 2 deletions(-)

lx@lx MINGW64 /d/Documents/git_test04 (fix_D|REBASE 1/3)
$ git log --pretty=fuller -1
commit 01c762391a07d2a8bb82e27d0b83de5fd567aa27 (HEAD)
Author:     lxwcd <15521168075@163.com>
AuthorDate: Mon Feb 10 00:13:44 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Mon Feb 10 00:13:44 2025 +0800

    rebase 91b0e3c Fix bug and fix confict
```

## git rebase -i 交互变基
```bash
pick 91b0e3c Fix bug
pick 0cda0f6 modify 2.txt
pick 2c28453 modify test01.txt

# Rebase 09cfa35..2c28453 onto 09cfa35 (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
```

可以修改 rebase 的顺序等。

### p, pick <commit>
使用指定的提交，不做任何修改。
默认行为。

### r, reword <commit>
作用：使用指定的提交，但能编辑提交日志的 message。
```bash
pick 1fc6c95 Patch A
reword 6b2481b Patch B
```

保存并退出后，Git 会暂停在 6b2481b 提交，编辑提交日志的 message。

### e, edit <commit>
使用指定的提交，但在应用后暂停，允许进行修改提交内容和日志 message。
```bash
reword 67bcef2 modify 2.txt
edit 6f95c1c modify test01.txt
```
保存并退出后，Git 会暂停在 6f95c1c 提交，可以使用 git commit --amend 修改提交内容。
```bash
lx@lx MINGW64 /d/Documents/git_test04 (fix_D_03|REBASE 3/3)
$ git status
interactive rebase in progress; onto 09cfa35
Last commands done (3 commands done):
   reword 67bcef2 modify 2.txt
   edit 6f95c1c modify test01.txt
  (see more in file .git/rebase-merge/done)
No commands remaining.
You are currently editing a commit while rebasing branch 'fix_D_03' on '09cfa35'.
  (use "git commit --amend" to amend the current commit)
  (use "git rebase --continue" once you are satisfied with your changes)

nothing to commit, working tree clean

lx@lx MINGW64 /d/Documents/git_test04 (fix_D_03|REBASE 3/3)
$
```

### s, squash <commit>
将指定的提交合并到前一个提交中。

```bash
pick 01c7623 rebase 91b0e3c Fix bug and fix confict
pick 67bcef2 modify 2.txt
squash 6f95c1c modify test01.txt
```

当合并 `67bcef2` 时会进入一个编辑界面，将 `6f95c1c` 提交一起合并到 `67bcef2` 中：
```Bash
# This is a combination of 2 commits.
# This is the 1st commit message:

modify 2.txt

# This is the commit message #2:

modify test01.txt

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:   Sun Feb 9 21:25:57 2025 +0800
#
# interactive rebase in progress; onto 09cfa35
# Last commands done (3 commands done):
#    pick 67bcef2 modify 2.txt
#    squash 6f95c1c modify test01.txt
# No commands remaining.
# You are currently rebasing branch 'fix_D_03' on '09cfa35'.
#
# Changes to be committed:
#	modified:   2.txt
#	modified:   test01.txt
#
```

### f, fixup [-C | -c] <commit>
将指定的提交合并到前一个提交中，但不保留当前提交的消息。

```bash
pick 01c7623 rebase 91b0e3c Fix bug and fix confict
pick 67bcef2 modify 2.txt
fixup 6f95c1c modify test01.txt
```

保存并退出后，Git 会将 `6f95c1c` 的内容合并到 `67bcef2` 中，但不会提示编辑提交消息。
最后查看日志看到最后两个提交记录的 message 为倒数第二个日志的提交 message。且 Author 信息更新。

### x, exec <command>
在指定的提交之后运行一个 shell 命令。

```bash
pick 1fc6c95 Patch A
exec echo "Running a command"
```

保存并退出后，Git 会在应用 1fc6c95 提交后运行 echo "Running a command"。

### b, break
在指定的提交之后暂停，允许手动处理。

```bash
pick 1fc6c95 Patch A
break
```

保存并退出后，Git 会在应用 1fc6c95 提交后暂停，可以手动处理（如 git commit --amend）。

### d, drop commit
删除指定的提交。

```bash
pick 1fc6c95 Patch A
drop 6b2481b Patch B
```

保存并退出后，Git 会删除 6b2481b 提交。

### l, label <label>
为当前的 HEAD 添加一个标签。

```bash
pick 1fc6c95 Patch A
label mylabel
```

保存并退出后，Git 会在应用 1fc6c95 提交后为当前的 HEAD 添加一个标签 mylabel。

### t, reset <label>
将 HEAD 重置到指定的标签。

```bash
pick 1fc6c95 Patch A
label mylabel
reset mylabel
```
保存并退出后，Git 会在应用 1fc6c95 提交后将 HEAD 重置到 mylabel。

### m, merge [-C <commit> | -c <commit>] <label>
创建一个合并提交。

```bash
pick 1fc6c95 Patch A
merge -c 6b2481b mylabel
```

保存并退出后，Git 会创建一个合并提交，使用 6b2481b 的提交消息。

### u, update-ref <ref>
跟踪一个占位符，用于更新指定的引用。

```bash
pick 1fc6c95 Patch A
update-ref refs/heads/mybranch
```

保存并退出后，Git 会在应用 1fc6c95 提交后更新 refs/heads/mybranch。

### git rebase --edit-todo 修改合并的顺序等
和 git rebase -i 相似，修改合并信息。

### git rebase --onto  
`git rebase --onto` 允许你将一系列提交从一个分支重新应用到另一个分支上。  
  
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
  
## --ff 快速前进（fast-forward）  
> [Git Merge | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/using-branches/git-merge)   
> [Git Fast-Forward VS Non-Fast-Forward](https://leimao.github.io/blog/Git-Fast-Forward-VS-Non-Fast-Forward/)   
  
> A Fast-Forward merge occurs when the branch you are merging into (often main or master) has not diverged from the branch you are merging (often a feature branch). In other words, the commit history of the target branch is a strict subset of the branch being merged. In a Fast-Forward merge, Git simply moves the pointer of the target branch forward to the latest commit on the branch being merged. No new merge commit is created; the history is linear.  
  
> A Non-Fast-Forward (No-FF) merge happens when the target branch has diverged from the branch being merged or when you explicitly choose to create a merge commit. In this case, Git creates a new commit that represents the merging of the two branches. Git creates a new merge commit that has two parent commits: one from the target branch and one from the branch being merged. The merge commit is a snapshot of the merged work, preserving the history of both branches.  
  
- **快速前进（fast-forward）**：当本地分支落后于远程分支且本地分支没有超前远程分支时，Git 可以安全地将本地分支的指针向前移动到远程分支的最新提交，即为快速前进。这种情况下，没有新的合并提交产生，因为历史是线性的。  
- **非快速前进**：如果远程分支有新的提交分叉，你的本地分支不是远程分支的直接祖先，那么 Git 无法通过快速前进来更新本地分支。这时，Git 需要创建一个新的合并提交，将两个分支的历史合并在一起。  
  
git fast-forward（快进合并）主要适用于本地分支落后于待合并分支，并且没有超前的部分。  
它要求合并的分支历史是线性的，即待合并的分支的提交历史是当前分支的直接延续。  
  
**条件**：  
**线性历史**：待合并的分支的提交历史是当前分支的直接延续。  
**没有新的本地提交**：当前分支没有新的提交，或者当前分支的提交历史完全包含在待合并的分支中。  
  
```bash  
A -- B -- C [main]  
          \  
           D -- E [feature]  
```  
在这个场景中，feature 分支是从 main 分支的 B 提交处创建的，并且 main 分支没有新的提交。此时，feature 分支的提交历史是 main 分支的直接延续。可以执行fast-forward 合并。  
bash复制  
```bash  
git checkout main  
git merge feature --ff-only  
```  
  
Git 会采用 fast-forward 策略，结果如下：  
```bash  
A -- B -- C -- D -- E [main, feature]  
```  
  
main 分支的指针直接移动到 feature 分支的最新提交 E 上。  
没有创建新的合并提交，历史保持线性。  
  
如果本地比待合并分支有新的提交：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (fix_C)  
$ git branch -vv  
  fix_B a3df94d [origin/fix_B] Merge branch 'fix_B' of https://github.com/lxwcd/git_test into fix_B  
* fix_C 69cf6cc [origin/fix_B: ahead 1, behind 2] modify 2.txt  
  main  03d14ae [origin/main: ahead 2, behind 19] update main test01.txt  
  main2 a47ac74 [origin/main: ahead 8, behind 19] Revert "update main test01.txt"  
  main3 ee19c9a [origin/main: ahead 5, behind 19] Revert "add test02.txt and test03.txt"  
```  
  
执行 fast-forward 合并将失败。  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (fix_C)  
$ git merge origin/fix_B --ff-only  
hint: Diverging branches can't be fast-forwarded, you need to either:  
hint:  
hint:   git merge --no-ff  
hint:  
hint: or:  
hint:  
hint:   git rebase  
hint:  
hint: Disable this message with "git config advice.diverging false"  
fatal: Not possible to fast-forward, aborting.  
```  
  
## --squash 合并多个提交记录为一个提交记录  
git merge --squash 的主要作用是将一个分支上的所有提交合并为一个单独的提交，并将这些更改应用到当前分支上。它不会创建合并提交，而是将所有更改暂存为一次新的提交。这常用于清理历史记录，将多个提交合并为一个。  
  
```bash  
git merge --squash feature  
```  
这会将 feature 分支上的所有更改合并到当前分支，但不会自动创建一个新的提交。  
  
```bash  
git commit -m "Squash commit: Merge feature branch changes"  
```  
  
## --abort  
  
## --continue  
  
## -X 合并策略  
> [Git - git-merge Documentation](https://git-scm.com/docs/git-merge#_merge_strategies)   
  
### ort  
  
# git prune  
> [Git - git-prune Documentation](https://git-scm.com/docs/git-prune)   
  
# git cherry-pick  
> [Git - git-cherry-pick Documentation](https://git-scm.com/docs/git-cherry-pick)   
  
> Apply the changes introduced by some existing commits.  
  
默认会 pick 提交到当前分支且新增一个同样的提交记录，除了 hash 值不一样，其他都一样。  
  
如果 Pick 多个提交，且顺序相关，最好按照原来的顺序从旧往前 pick：  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ git log --oneline -5 fix_B  
3030efb (fix_B) Merge branch 'fix_B' of https://github.com/lxwcd/git_test into fix_B  
3c20c79 update git.md  
171d25c update 2.txt 22  
f54dd26 update 2.txt 222  
15f80f2 (HEAD -> test, origin/test) update test02.txt  
```  
  
想 pick 上面 5 个提交，且按照原始的顺序：  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ git log --oneline -5 fix_B  | tac | cut -d" " -f1  
15f80f2  
f54dd26  
171d25c  
3c20c79  
3030efb  
  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ git log --oneline -5 fix_B  | tac | cut -d" " -f1 | xargs git cherry-pick --no-commit  
```  
  
## pick 其他分支的特定提交  
  
pick main2 分支的最新提交：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main3)  
$ git cherry-pick main2  
```  
  
pick main2 分支的第 5 个父提交：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main3)  
$ git cherry-pick main2~5  
```  
  
## 不产生提交记录 --no-commit  
  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ git log --oneline -1 main  
cbf4932 (main) update test03.txt  
  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ git log --oneline -1 main | cut -d" " -f1  
cbf4932  
  
lx@lx MINGW64 /d/Documents/git_test03 (test)  
$ git log --oneline -1 main | cut -d" " -f1  | xargs git cherry-pick --no-commit  
```  
  
修改会在暂存区，不产生提交记录。  
  
## pick 本分支落后其他分支的提交  
  
本分支当前的记录：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main2)  
$ git log --oneline -6 origin/main  
03d14ae (origin/main, origin/HEAD, main) update main test01.txt  
737c5b7 commit B  
e67a0f3 add test02.txt and test03.txt  
332de10 update file  
470dcf0 add files  
```  
  
查看本分支落后 main2 分支的记录：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main3)  
$ git log ^HEAD main2 --oneline  
a47ac74 (main2) Revert "update main test01.txt"  
ca44b51 Revert "update test01.txt: add main"  
006fed4 Reapply "update test01.txt: add main"  
b93b033 Revert "add test02.txt and test03.txt"  
dc76ad7 Revert "update test01.txt: add main"  
16ac277 update test01.txt: add main  
```  
  
应用落后的这些提交，按照原始顺序：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main3)  
$ git cherry-pick ..main2  
```  
或者：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main3)  
$ git cherry-pick ^HEAD main2  
```  
  
查看新的提交，看到最新的 6 次提交即为 pick 的提交，仅 hash 值不同，message 相同：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main3)  
$ git log --oneline -8  
784d0df (HEAD -> main3) Revert "update main test01.txt"  
c36999f Revert "update test01.txt: add main"  
2b1c993 Reapply "update test01.txt: add main"  
afd6228 Revert "add test02.txt and test03.txt"  
ed7571e Revert "update test01.txt: add main"  
3a37c60 update test01.txt: add main  
03d14ae (origin/main, origin/HEAD, main) update main test01.txt  
737c5b7 commit B  
```  
  
## pick 其他分支连续的提交  
  
pick main2 分支从第 5 个父提交到第 3 个父提交：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main3)  
$ git cherry-pick main2~6..main2~3  
```  
  
这里不包括起始提交 main2~6。   
  
main2 分支提交记录：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main3)  
$ git log --oneline -7 main2  
a47ac74 (main2) Revert "update main test01.txt"  
ca44b51 Revert "update test01.txt: add main"  
006fed4 Reapply "update test01.txt: add main"  
b93b033 Revert "add test02.txt and test03.txt"  
dc76ad7 Revert "update test01.txt: add main"  
16ac277 update test01.txt: add main  
03d14ae (HEAD -> main3, origin/main, origin/HEAD, main) update main test01.txt  
```  
  
本分支初始提交记录：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main3)  
$ git log --oneline -3  
03d14ae (HEAD -> main3, origin/main, origin/HEAD, main) update main test01.txt  
737c5b7 commit B  
e67a0f3 add test02.txt and test03.txt  
```  
  
本分支合并后的提交记录：  
```bash  
lx@lx MINGW64 /d/Documents/git_test04 (main3)  
$ git log --oneline -5  
ee19c9a (HEAD -> main3) Revert "add test02.txt and test03.txt"  
11df87e Revert "update test01.txt: add main"  
396ebec update test01.txt: add main  
03d14ae (origin/main, origin/HEAD, main) update main test01.txt  
737c5b7 commit B  
```  
  
## 解决冲突
git cherry-pick 解决冲突后不修改 Author Date。

`git cherry-pick` 如果有冲突，根据提示和 git status 查看的状态打开冲突文件解决冲突。
```bash
lx@lx MINGW64 /d/Documents/git_test04 (main2_01)
$ git cherry-pick main2
Auto-merging test01.txt
CONFLICT (content): Merge conflict in test01.txt
error: could not apply 3b671ba... modify test01.txt , add C
hint: After resolving the conflicts, mark them with
hint: "git add/rm <pathspec>", then run
hint: "git cherry-pick --continue".
hint: You can instead skip this commit with "git cherry-pick --skip".
hint: To abort and get back to the state before "git cherry-pick",
hint: run "git cherry-pick --abort".
hint: Disable this message with "git config advice.mergeConflict false"
```

```bash
lx@lx MINGW64 /d/Documents/git_test04 (main2_01|CHERRY-PICKING)
$ git status
On branch main2_01
You are currently cherry-picking commit 3b671ba.
  (fix conflicts and run "git cherry-pick --continue")
  (use "git cherry-pick --skip" to skip this patch)
  (use "git cherry-pick --abort" to cancel the cherry-pick operation)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   test01.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

解决冲突后 `git add` 将文件添加到暂存区，然后 `git cherry-pick --continue` 继续执行 cherry-pick 操作，这时会打开窗口写提交日志信息，默认显示原始的日志，可以直接使用或者修改日志 message：
```bash
modify test01.txt , add C

# Conflicts:
#	test01.txt
#
# It looks like you may be committing a cherry-pick.
# If this is not correct, please run
#	git update-ref -d CHERRY_PICK_HEAD
# and try again.


# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Author:    Bob <Bob@163.com>
# Date:      Sun Feb 9 18:58:12 2025 +0800
#
# On branch main2_01
# You are currently cherry-picking commit 3b671ba.
#
# Changes to be committed:
#	modified:   test01.txt
#
```

完成后查看日志发现 Author Date 没有被修改，但 Commit Date 更新为当前时间：
```bash
lx@lx MINGW64 /d/Documents/git_test04 (main2_01)
$ git log --pretty=fuller -1
commit f537c63676cc209de5bdcd1b79ba79234c7d1552 (HEAD -> main2_01)
Author:     Bob <Bob@163.com>
AuthorDate: Sun Feb 9 18:58:12 2025 +0800
Commit:     lxwcd <15521168075@163.com>
CommitDate: Sun Feb 9 22:32:24 2025 +0800

    modify test01.txt , add C
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
  
# git filter-branch  
> [Git - git-filter-branch Documentation](https://git-scm.com/docs/git-filter-branch)   
> [GitHub - newren/git-filter-repo: Quickly rewrite git repository history (filter-branch replacement)](https://github.com/newren/git-filter-repo)   
> [Removing sensitive data from a repository - GitHub Docs](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)   
  
# 常用案例  
  
## git fetch -p 更新远程信息
从远程仓库获取最新的分支和标签信息，并且会自动清理本地仓库中那些在远程仓库中已经被删除的远程跟踪分支。

## git add 筛选特定文件  
  
```bash  
git add *.cpp *.h  
```  
  
## 复制当前分支

如果当前分支需要执行一些合并等操作，不确定操作后行为是否有问题，可以依据当前分支创建一个临时分支，在临时分支进行操作，这样不会影响当前分支：

```bash
git switch -c <新分支名> 
```

注意先保证当前分支工作区干净，如果有未暂存的修改，不希望提交，可以 git stash 先暂存；或者 git commit 提交后，在新分支 `git reset --hard HEAD^` 丢弃该提交记录。

## 依据其他分支创建新分支

```bash
git switch -c <新分支名> <来源分支名>
```
或者
```bash
git checkout -b <new-branch> <existing-branch>
```

如创建一个 bug 分支依据远程最新 develop 分支：
```bash
git fetch -p
git checkout b fix_bug origin/develop
```

## 显示已跟踪被修改的文件名  
```bash  
git diff HEAD --name-only  
```  
  
## 筛选已跟踪被修改的文件  
  
```bash  
git diff HEAD --name-only | grep -E "*/demo/*"  
```  
或：  
```bash  
git status --porcelain | cut -d" " -f3- | grep -E "*/demo/*"  
```  
  
## 筛选已跟踪被修改的特定后缀文件  
  
```bash  
git diff HEAD --name-only |  grep -E "\.(cpp|h)$"  
```  
或：  
```bash  
git status --porcelain | cut -d" " -f3- |  grep -E "\.(cpp|h)$"  
```  
  
## git stash 过滤文件保存  
  
```bash  
git diff HEAD --name-only | grep -E "*/demo/*" | xargs git stash push -m "stash demo files" --  
```  
或：  
```bash  
git status --porcelain | cut -d" " -f3- | grep -E "*/demo/*" | xargs git stash push -m "stash demo files" --  
```  
  
## 输出未被跟踪的文件名  
```bash  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git status -s  
AM git.md  
 M test01.txt  
?? .gitignore  
?? 0001-commit-B.patch  
?? 0001-fix-B.patch  
?? 0001-update-fix_B.patch  
?? 0002-commit-C.patch  
?? 0002-update-fix_B.patch  
?? 1.patch  
?? 2.txt  
  
lx@lx MINGW64 /d/Documents/git_test (fix_B)  
$ git status -s |  grep "??" | cut -d" " -f2  
.gitignore  
0001-commit-B.patch  
0001-fix-B.patch  
0001-update-fix_B.patch  
0002-commit-C.patch  
0002-update-fix_B.patch  
1.patch  
2.txt  
```  
  
## 恢复工作目录到最新提交  
  
### git stash  
```bash  
git stash push -m "message"  
```  
  
如果有没有被跟踪的文件，希望一起存起来：  
```bash  
git stash push --all -m "message"  
```  
  
### git checkout  
恢复已跟踪的文件：  
```bash  
git checkout HEAD -- .  
```  
  
再删除没有被跟踪的文件：  
```bash  
git clean -fd  
```  
  
### git reset  
  
恢复已跟踪的文件：  
```bash  
git reset --hard HEAD  
```  
  
再删除没有被跟踪的文件：  
```bash  
git clean -fd  
```  
或者：  
```bash  
$ git status --short | grep "??" | cut -d" " -f2 | xargs rm -rf  
```  
  
### git restore  
  
恢复已跟踪的文件：  
```bash  
$ git restore --source=HEAD --staged --worktree .  
```  
  
再删除没有被跟踪的文件：  
```bash  
git clean -fd  
```  
  
## 有冲突时指定使用版本  
  
两个仓库中的一个分支都修改了文件 2.txt 的相同一行，但修改内容内容不同，一个仓库已经将修改推送到远程仓库，另一个仓库修改后提交到本地，然后 git pull 时提示有冲突：  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (fix_B)  
$ git pull  
remote: Enumerating objects: 5, done.  
remote: Counting objects: 100% (5/5), done.  
remote: Compressing objects: 100% (1/1), done.  
remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0 (from 0)  
Unpacking objects: 100% (3/3), 239 bytes | 9.00 KiB/s, done.  
From https://github.com/lxwcd/git_test  
   15f80f2..f54dd26  fix_B      -> origin/fix_B  
Auto-merging 2.txt  
CONFLICT (content): Merge conflict in 2.txt  
Automatic merge failed; fix conflicts and then commit the result.  
```  
  
查看当前工作目录的状态，可以看见有个文件处于冲突中，待解决：  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (fix_B|MERGING)  
$ git status  
On branch fix_B  
Your branch and 'origin/fix_B' have diverged,  
and have 1 and 1 different commits each, respectively.  
  (use "git pull" if you want to integrate the remote branch with yours)  
  
You have unmerged paths.  
  (fix conflicts and run "git commit")  
  (use "git merge --abort" to abort the merge)  
  
Unmerged paths:  
  (use "git add <file>..." to mark resolution)  
        both modified:   2.txt  
  
no changes added to commit (use "git add" and/or "git commit -a")  
  
```  
  
查看冲突文件的内容：  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (fix_B|MERGING)  
$ cat 2.txt  
<<<<<<< HEAD  
22  
=======  
222  
>>>>>>> f54dd265ddebde6a06e2ea619a0588d2b1555945  
```  
  
`<<<<<<< HEAD` 表示下方表示当前版本  
`=======` 表示分隔符，下方内容为冲突版本的内容  
`>>>>>>> f54dd265ddebde6a06e2ea619a0588d2b1555945` 表示冲突结束位置  
  
### 使用对方版本  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (fix_B|MERGING)  
$ git checkout --theirs 2.txt  
Updated 1 path from the index  
  
lx@lx MINGW64 /d/Documents/git_test03 (fix_B|MERGING)  
$ cat 2.txt  
222  
```  
  
### 使用本地版本  
```bash  
lx@lx MINGW64 /d/Documents/git_test03 (fix_B|MERGING)  
$ git checkout --ours 2.txt  
Updated 1 path from the index  
  
lx@lx MINGW64 /d/Documents/git_test03 (fix_B|MERGING)  
$ cat 2.txt  
22  
```  
  
### 添加到暂存区  
选择版本后，将这些文件添加到暂存区：  
  
```bash  
git add <file-path>  
```  
  
### 继续合并  
如果你已经解决了所有文件的冲突，你可以继续完成合并操作：  
  
```bash  
git commit -m "message"  
```  
  
或者   
```bash  
git merge --continue  
```  
  
## 合并 feature 分支合并到主干分支  

- git fetch -p 更新远程仓库
- 拉取远程仓库主分支到本地
```bash
git checkout -b dev origin/dev
```
- git switch -c 复制当前分支到新分支进行合并操作
如果当前分支工作目录不干净，可以 git stash 保持未提交的信息；
或者 git commmit 提交，然后到新分支后 git reset --hard HEAD^ 撤销提交。
- 查看 feature 分支和待合并的主分支的提交差异
```bash
git branch -u origin/dev
git branch -vv
```
- 如果 feature 分支仅自己使用，且只有超前主分支的记录，无落后记录，则可以用 git rebase 或者 git merge -ff 合并。
- 如果 feature 分支仅自己使用，有超前主分支的记录，也有落后记录，则可以用 git rebase 尝试合并，如果有冲突则中途解决冲突。
- 如果 feature 分支是自己和其他人合作开发的分支，比主分支有超前和落后的记录，则可以先用 git rebase 尝试合并，看是否有冲突。
- 如果 feature 分支是别人合作开发的分支，比主分支有超前和落后的记录，则需要用 git merge 合并。
  - 如果无冲突，可直接用 git rebase 合并。  
  - 如果有冲突，冲突是自己的提交记录，也可以修改冲突记录，然后继续用 git rebase 合并。  
  - 如果有冲突，但冲突是别人的提交记录，则然对方进行合并解决冲突，或者自己解决冲突。
    根据实际需要，用 git rebase，解决冲突会修改其他人的提交记录，但最终显示 Author 仍为对方或者可以改为自己。
    或者用 git merge 等其他方式合并。

## 提 Pull Request 策略

### 更新最新代码
提 PR 前更新远程仓库代码，依据远程仓库主分支的最新代码在本地新建 feature 分支。

### 冲突文件先提 PR 尽快合并
对于很容易发生的修改，如多语言，工程文件等，可以在提 PR 前更新代码，查看其他人 PR，如果当前 Active PR 没有多语言的修改，则先将这些易冲突的文件先提 PR 尽快合并到主分支。

### 提 PR 前本地合并 feature 分支到主分支
本地代码修改完后，在提 PR 前，先更新远程仓库主分支的代码并拉取到本地，然后将当前分支合并到主分支，如果有冲突解决冲突。
合并步骤见前面介绍。

合并后分支只有超前远程主分支的记录，无落后记录。

### 新建远程 feature 分支提 PR
本地合并以后，将本地 feature 分支推送到远程仓库且在远程仓库新建 featrue 分支：
```bash
git push -u origin HEAD:feature
```

### PR 通过后合并到远程仓库主分支策略
PR 经过验证后真正合并到远程仓库时，可能远程仓库主分支又有了新的提交记录，这时可以在本地拉取远程仓库主分支，再将 feature 分支尝试合并到主分支，如 git rebase，如果没有冲突，则可以在远程仓库选择 git rebase 合并方案。
如果有冲突。则本地进行合并，并解决冲突后，重新推送到远程仓库进行 PR。

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
      
