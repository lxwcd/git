git 学习

# 学习资源
> 初步了解 git：[廖雪峰 Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)
> github 官方文档：[GitHub Docs](https://docs.github.com/en/get-started/quickstart/set-up-git)
> git 命令官方文档：[git](https://git-scm.com/docs/)
> git book：[Pro Git book](https://git-scm.com/book/en/v2)



# git 配置代理
> [git设置、查看、取消代理](https://blog.csdn.net/qq_43331089/article/details/129637569)

- 如 windows 中安装 clash for windows，可查看其端口，例如 7890

在 git 设置代理：
```git
git config --global http.https://github.com.proxy socks5://127.0.0.1:7890
```

配置完查看：
```git
$ git config --global --list
http.https://github.com.proxy=socks5://127.0.0.1:7890
```


# 安装 git
## linux 安装
> [安装 Git](https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496)

## Windows 安装
官网下载地址：[Download for Windows](https://git-scm.com/download/win)

这个地址下载慢，可能不成功，可以点击下载后可以查看下载的版本，然后在[镜像网站](https://registry.npmmirror.com/binary.html?path=git-for-windows/)下载，从官网页面查看最新的日期和版本：
![1](https://img-blog.csdnimg.cn/fb9fc2812f6b4c7f80f2065b155fb357.png)
Git-2.39.2-64-bit 下载：[Index of /git-for-windows/v2.39.2.windows.1/](https://registry.npmmirror.com/binary.html?path=git-for-windows/v2.39.2.windows.1/)



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


# Git config
> [Git Config](https://www.gitkraken.com/learn/git/git-config)
> [配置 git config](https://tsejx.github.io/devops-guidebook/code/git/config/)

## 查看全局配置信息
```bash
git config --global --list
```





# 删除远程仓库文件
> [How to Delete a File or a Directory from a Git Repository](https://www.w3docs.com/snippets/git/how-to-delete-a-file-from-a-git-repository.html)


- `git rm file`
- `git commit -m "delete file"`
- `git push origin <remote repo>`