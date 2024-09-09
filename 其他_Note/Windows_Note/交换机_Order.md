# 常见的交换机命令

以下是一些常见的交换机命令，用于管理和配置网络交换机。这些命令可能会因交换机型号和厂商而有所不同，因此请根据你所使用的具体交换机型号和文档进行参考。

## 显示命令：

- 显示设备信息：`show version`、`show system`、`show hardware`
- 显示接口信息：`show interfaces`、`show interface status`
- 显示 VLAN 信息：`show vlan`、`show vlan id <VLAN_ID>`
- 显示 MAC 地址表：`show mac-address-table`
- 显示路由表：`show ip route`、`show ip route static`
- 显示邻居设备：`show cdp neighbors`、`show lldp neighbors`
- 显示设备日志：`show logging`、`show log`
- 显示端口统计信息：`show interface counters`、`show interface statistics`
- 显示设备配置：`show running-config`、`show startup-config`

## 配置命令：

- 配置主机名：`hostname <HOSTNAME>`
- 配置管理接口 IP 地址：`interface <INTERFACE> ip address <IP_ADDRESS> <SUBNET_MASK>`
- 配置 VLAN：`vlan <VLAN_ID>`
- 配置端口 VLAN：`interface <INTERFACE> switchport access vlan <VLAN_ID>`
- 配置端口模式：`interface <INTERFACE> switchport mode <MODE>`
- 配置端口双工模式：`interface <INTERFACE> duplex <MODE>`
- 配置端口速率：`interface <INTERFACE> speed <SPEED>`
- 配置静态路由：`ip route <DESTINATION_NETWORK> <SUBNET_MASK> <NEXT_HOP_IP_ADDRESS>`
- 配置默认网关：`ip default-gateway <GATEWAY_IP_ADDRESS>`
- 保存配置：`write memory`、`copy running-config startup-config`

## 其他命令：

- 清除 MAC 地址表：`clear mac-address-table`
- 清除接口计数器：`clear counters <INTERFACE>`
- 重启设备：`reload`、`reboot`
- 进入特权模式：`enable`
- 退出特权模式：`disable`
- 退出配置模式：`exit`、`end`