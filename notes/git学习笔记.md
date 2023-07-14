git 学习

# 学习资源
> 初步了解 git：[廖雪峰 Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)
> github 官方文档：[GitHub Docs](https://docs.github.com/en/get-started/quickstart/set-up-git)
> git 命令官方文档：[git](https://git-scm.com/docs/)
> git book：[Pro Git book](https://git-scm.com/book/en/v2)



# github 无法访问问题
- 系统为 ubuntu 22.04

## 修改 /etc/hosts 文件
> ip 地址查询：[ipaddress](https://www.ipaddress.com/)
> [解决GitHub访问不了的方法](https://note.dolyw.com/other/02-Github-Failure.html)

1. 用 [ip 地址查询工具](https://www.ipaddress.com/) 查询 `www.github.com`，`github.global.ssl.fastly.net` 和 `assets-cdn.github.com` 的 ip 后添加到 `/etc/hosts` 中，查询到的 ip 有几个，就都添加上去，保存退出文件
2. 保存后没有立即生效，参考 [Linux修改本机/etc/hosts的hostName后经常不生效](https://blog.csdn.net/hguisu/article/details/49278355)，重启后生效

## 自动更新 hosts 内容
> Gitee：[GitHub520](https://gitee.com/snow2zhou/GitHub520)
> Github：[GitHub520](https://github.com/521xueweihan/GitHub520)


# 安装 git
## linux 安装
> [安装 Git](https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496)

## Windows 安装
官网下载地址：[Download for Windows](https://git-scm.com/download/win)

这个地址下载慢，可能不成功，可以点击下载后可以查看下载的版本，然后在[镜像网站](https://registry.npmmirror.com/binary.html?path=git-for-windows/)下载，从官网页面查看最新的日期和版本：
![1](https://img-blog.csdnimg.cn/fb9fc2812f6b4c7f80f2065b155fb357.png)
Git-2.39.2-64-bit 下载：[Index of /git-for-windows/v2.39.2.windows.1/](https://registry.npmmirror.com/binary.html?path=git-for-windows/v2.39.2.windows.1/)






# 远程仓库


************
问题：
- vim 打开 id_rsa.pub 文件复制到 github 中，提示错误，gedit 打开成功


# 删除远程仓库文件
> [How to Delete a File or a Directory from a Git Repository](https://www.w3docs.com/snippets/git/how-to-delete-a-file-from-a-git-repository.html)


- `git rm file`
- `git commit -m "delete file"`
- `git push origin <remote repo>`