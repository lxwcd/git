Gitee 配置

# Github 同步仓库到 Gitte

1.  在 Gitee 上创建镜像仓库：在 Gitee 上创建一个与 GitHub 仓库同名的空仓库，用于接收同步的代码。
2.  生成并配置 SSH 密钥对：这是实现自动化认证的关键。
    ◦ 生成密钥：在本地终端执行 ssh-keygen -t rsa -C "your_email@example.com"，在提示设置密码时直接按三次回车，生成无密码的密钥对（例如 id_rsa 和 id_rsa.pub）。

    ◦ 配置公钥：将生成的公钥（如 id_rsa.pub 的内容）添加到你的 Gitee 账户的 SSH 公钥设置中。

    ◦ 配置私钥：将生成的私钥（如 id_rsa 的内容）添加到你的 GitHub 仓库的 Secrets 中，通常命名为 GITEE_PRIVATE_KEY 或 GITEE_RSA_PRIVATE_KEY。

3.  创建 Gitee 私人令牌（部分方案需要）：
    ◦ 在 Gitee 的「安全设置」->「私人令牌」中生成一个新令牌，并授予所有权限（或至少仓库相关权限）。

    ◦ 将此令牌值也添加到 GitHub 仓库的 Secrets 中，通常命名为 GITEE_TOKEN。

⚙️ 两种主流的同步方案

完成准备工作后，可以根据需求选择一种方案，在 GitHub 仓库的 .github/workflows/ 目录下创建 .yml 文件（例如 sync-to-gitee.yml）。

## 方案一：使用 hub-mirror-action

这个 Action 功能强大，特别适合同步多个仓库或需要复杂配置的场景。
```yaml
name: Batch Sync to Gitee

on:
  schedule:
    - cron: '0 2 * * *'  # 每天UTC时间2点（北京时间10点）自动同步
  workflow_dispatch:       # 支持手动触发
  push:
    branches: [ main ]     # 主分支有推送时也触发同步

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - name: Mirror to Gitee
        uses: Yikun/hub-mirror-action@master
        with:
          # 源和目标设置
          src: github/lxwcd
          dst: gitee/cd-00
          account_type: user  # 如果是组织则改为'org'
          
          # 认证信息
          dst_key: ${{ secrets.GITEE_PRIVATE_KEY }}
          dst_token: ${{ secrets.GITEE_TOKEN }}
          
          # 同步范围控制
          # static_list: "repo1,repo2,repo3"  # 要同步的仓库列表，用逗号分隔，不写则同步全部

          # 黑白名单控制（可选）
          # white_list: "repo1,repo2"  # 白名单模式
          # black_list: "repo3,repo4"  # 黑名单模式
          force_update: true  # 强制更新，覆盖目标仓库的改动
          
          # 高级选项
          clone_style: "https"  # 克隆方式，可选https或ssh
          debug: true  # 启用调试模式，显示详细日志
          timeout: '600s'  # 设置超时时间
```


## 方案二：使用 git-mirror-action

这个 Action 更轻量，专注于单个仓库的简单镜像。
```yaml
name: Sync to Gitee Using Git Mirror

on:
  push: # 当向 main 分支推送代码时触发同步
    branches: [ main ]

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - name: Mirror to Gitee
        uses: wearerequired/git-mirror-action@master
        env:
          SSH_PRIVATE_KEY: ${{ secrets.GITEE_RSA_PRIVATE_KEY }} # 对应私钥的 Secret
        with:
          source-repo: 'git@github.com:your_github_username/your_repo_name.git' # 替换为你的 GitHub 仓库 SSH 地址
          destination-repo: 'git@gitee.com:your_gitee_username/your_repo_name.git' # 替换为你的 Gitee 仓库 SSH 地址
```

## ✅ 测试与验证

将配置文件推送到 GitHub 仓库后，同步工作流会自动触发。

1.  检查 Action 运行状态：进入你的 GitHub 仓库，点击 Actions 选项卡，查看相应工作流（如 "Sync to Gitee Using Hub Mirror"）的运行状态。绿色对勾表示成功。
2.  查看日志：如果运行失败，点击对应的运行记录查看详细日志，根据错误信息排查问题。开启 debug: true 会获得更详细的日志。
3.  确认同步结果：前往的 Gitee 仓库页面，刷新并确认代码已成功同步。