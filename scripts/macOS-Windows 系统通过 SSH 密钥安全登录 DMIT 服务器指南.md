# macOS-Windows 系统通过 SSH 密钥安全登录 DMIT 服务器指南

对于刚接触云服务器的用户来说，DMIT 仅支持 SSH 密钥登录的方式可能会带来一些困扰。本文将详细介绍如何在 macOS 和 Windows 系统上配置 SSH 私钥连接 DMIT 服务器。

## 一、获取 DMIT SSH 密钥文件

在开始连接前，您需要先获取 SSH 密钥对：

1. 登录 DMIT 后台管理面板
2. 进入「SSH 密钥管理」页面
3. 下载包含公钥和私钥的密钥文件包

**重要提示**：
- 密钥文件仅能下载一次
- 若丢失密钥，需重新生成并重启服务器
- 私钥文件包含 `.ppk` 和 `.pem` 两种格式

👉 [【点击查看】2025年最新 DMIT 优惠码及特价云服务器方案汇总](https://bit.ly/dmit_coupon)

## 二、macOS 系统连接教程

### 1. 设置私钥文件权限
bash
chmod 600 id_rsa.pem

### 2. 建立 SSH 连接
bash
ssh -i id_rsa.pem root@服务器IP地址

## 三、Windows 系统连接教程

推荐使用 PuTTY 或 XShell 进行连接，以下是 PuTTY 的设置步骤：

1. **基本设置**：
   - 输入服务器 IP 地址
   - 选择 SSH 连接类型
   - 在 Connection > Data 中填写用户名 "root"

2. **密钥配置**：
   - 展开 SSH > Auth
   - 点击 "Browse" 选择 `.ppk` 格式的私钥文件
   - 点击 "Open" 开始连接

## 四、常见问题解答

Q：连接时提示权限被拒绝怎么办？
A：请检查私钥文件权限设置是否正确，并确认使用的是 root 账户

Q：密钥丢失后如何处理？
A：需要在管理后台重新生成密钥对，并重启服务器生效

通过以上步骤，您应该能够顺利连接到 DMIT 服务器。如需了解更多 DMIT 服务器使用技巧，可以参考我们的其他教程。

**小贴士**：定期更换 SSH 密钥可以有效提升服务器安全性，建议每3-6个月更新一次密钥对。