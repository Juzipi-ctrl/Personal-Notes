## ping 命令

`ping` 是一个常用的网络诊断工具，可用于测试网络连接和测量与目标主机之间的往返延迟（Round-Trip Time，RTT）。它在大多数操作系统中都可用，包括 Windows、macOS 和 Linux。

使用 `ping` 命令时，会向指定的目标主机发送 ICMP（Internet Control Message Protocol）回显请求，并等待目标主机返回 ICMP 回显应答。通过分析应答的时间和状态，可以评估网络的响应速度和可用性。

以下是 `ping` 命令的一般语法和常见选项：

复制

```bash
ping [选项] 目标主机

# 例如
ping -t www.baidu.com
```

常见选项包括：

- `-c count` 或 `--count=count`：指定发送的回显请求次数。
- `-i interval` 或 `--interval=interval`：指定发送回显请求之间的时间间隔（单位为秒）。
- `-s packetsize` 或 `--packetsize=packetsize`：指定发送的回显请求的数据包大小（单位为字节）。
- `-t ttl` 或 `--ttl=ttl`：指定发送回显请求时的生存时间（Time to Live）值。
- `-w deadline` 或 `--deadline=deadline`：指定超时时间，即等待回显应答的最长时间（单位为秒）。

`ping` 命令执行后，会显示每个回显请求的结果，包括目标主机的 IP 地址、数据包大小、往返时间、丢包率等信息。通过分析这些信息，可以判断网络连接的稳定性和性能。