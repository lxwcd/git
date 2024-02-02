git 学习  
      
# 学习资源  
> 初步了解 git：[廖雪峰 Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)  
> github 官方文档：[GitHub Docs](https://docs.github.com/en/get-started/quickstart/set-up-git)  
> git 命令官方文档：[git](https://git-scm.com/docs/)  
> git book：[Pro Git book](https://git-scm.com/book/en/v2)  
      
      
# 安装 git  
## linux 安装  
> [安装 Git](https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496)  
      
## Windows 安装  
官网下载地址：[Download for Windows](https://git-scm.com/download/win)  
      
这个地址下载慢，可能不成功，可以点击下载后可以查看下载的版本，然后在[镜像网站](https://registry.npmmirror.com/binary.html?path=git-for-windows/)下载，从官网页面查看最新的日期和版本： ![1](https://img-blog.csdnimg.cn/fb9fc2812f6b4c7f80f2065b155fb357.png)  
      
Git-2.39.2-64-bit 下载：[Index of /git-for-windows/v2.39.2.windows.1/](https://registry.npmmirror.com/binary.html?path=git-for-windows/v2.39.2.windows.1/)  
      
      
# Git config 配置Git  
> [Git Config](https://www.gitkraken.com/learn/git/git-config)  
> [配置 git config](https://tsejx.github.io/devops-guidebook/code/git/config/)  
      
## 查看全局配置信息  
```bash  
git config --global --list  
```  
      
## 设置用户名和电子邮件  
```bash  
root@ubuntu2204c12:~# git config --global user.name "name"  
root@ubuntu2204c12:~# git config --global user.email "email@163.com"  
```  
      
      
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
      
      
# git clone 克隆仓库到新目录  
如果远程仓库地址为：https://github.com/lxwcd/learnVim.git，直接用 git clone url 会将远程仓库克隆到当前目录  
      
将远程仓库克隆到指定目录并且修改仓库名字为 `new_folder`：  
```bash  
git clone https://github.com/lxwcd/learnVim.git /usr/local/src/new_folder  
```  
      
也可以指定多级目录，如果不存在，则自动创建  
```bash  
git clone https://github.com/lxwcd/learnVim.git /usr/local/src/1/2/3/new_folder  
```  
      
      
# 删除远程仓库文件  
> [How to Delete a File or a Directory from a Git Repository](https://www.w3docs.com/snippets/git/how-to-delete-a-file-from-a-git-repository.html)  
      
      
- `git rm file`  
- `git commit -m "delete file"`  
- `git push origin <remote repo>`  
      
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
