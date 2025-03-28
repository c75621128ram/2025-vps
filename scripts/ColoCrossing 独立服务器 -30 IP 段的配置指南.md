# ColoCrossing 独立服务器 -30 IP 段的配置指南

## 一、IP 分配原理解析

ColoCrossing 独立服务器在开通时会分配两个网卡，每个网卡对应一个 /30 IP 段（共 8 个 IP）。这两个 IP 段的用途分别是：

1. **主服务器网络**：用于服务器常规网络连接
2. **IPMI 管理网络**：用于远程服务器管理

👉 [【点击查看】2025年最新 ColoCrossing 优惠码及特价云服务器方案汇总](https://bit.ly/ColoCrossing)

## 二、可用 IP 计算

每个 /30 网段包含 4 个 IP 地址：

- 2 个保留 IP（网关和广播地址）
- 1 个 IPMI 专用 IP（仅在第二个网段）
- 剩余 3 个为可用 IP

## 三、具体 IP 配置示例

### 1. 主网络配置（ens1）

网段：172.23.40.40/30
网卡名：ens1
可用IP：
- 172.23.40.40
- 172.23.40.42
保留IP：
- 172.23.40.41（网关）
- 172.23.40.43（广播地址）

### 2. IPMI 网络配置（ens3）

网段：23.24.55.50/30
网卡名：ens3
可用IP：
- 23.24.55.50
保留IP：
- 23.24.55.51（网关）
- 23.24.55.52（IPMI专用）
- 23.24.55.53（广播地址）

## 四、Debian 系统配置步骤

1. 编辑网络配置文件：
bash
vi /etc/network/interfaces

2. 添加以下配置内容：
bash
auto lo
iface lo inet loopback

# 主网卡配置
auto ens1
iface ens1 inet static
        address 172.23.40.42/30
        gateway 172.23.40.41
        dns-nameservers 8.8.8.8 8.8.4.4

# 附加IP配置
auto ens1:1
iface ens1:1 inet static
        address 172.23.40.40/30

# IPMI网卡配置
auto ens3
iface ens3 inet static
        address 23.24.55.50/30
        gateway 23.24.55.51
        dns-nameservers 8.8.8.8 8.8.4.4

3. 重启网络服务使配置生效

## 五、配置验证

完成上述步骤后，您的 ColoCrossing 独立服务器将可以同时使用三个可用IP地址。建议通过 `ifconfig` 命令检查IP配置是否生效。

如需更多服务器配置技巧或优惠信息，请访问我们的[特价服务器专区](https://bit.ly/ColoCrossing)。