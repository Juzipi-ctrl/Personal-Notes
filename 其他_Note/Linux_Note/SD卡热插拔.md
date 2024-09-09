1. 检查内核版本和架构:

   ```shell
   uname -a
   ```

   确保您的系统是基于 ARM 架构的 Ubuntu Linux。

2. 安装所需的软件包:

   ```shell
   sudo apt-get update
   sudo apt-get install udev
   ```

3. 创建 udev 规则文件:

   ```shell
   sudo vim /etc/udev/rules.d/99-sdcard.rules
   ```

   在文件中添加以下内容:

   ```shell
   KERNEL=="mmcblk[0-9]p[0-9]", SUBSYSTEM=="block", ACTION=="add|remove", RUN+="/path/to/your/script.sh"
   ```

   注意,在 ARM 架构上,SD 卡设备通常被命名为 `mmcblk[0-9]p[0-9]`。

4. 创建自定义脚本文件:

   ```shell
   sudo vim /path/to/your/script.sh
   ```

   在脚本中添加您需要执行的操作,例如:

   ```shell
   #!/bin/bash
   
   case "$ACTION" in
       add)
           echo "SD card inserted" >> /tmp/sdcard.log
           # 在此添加您需要执行的操作,如挂载 SD 卡等
           ;;
       remove)
           echo "SD card removed" >> /tmp/sdcard.log
           # 在此添加您需要执行的操作,如卸载 SD 卡等
           ;;
   esac
   ```

5. 设置脚本文件权限:

   ```shell
   sudo chmod +x /path/to/your/script.sh
   ```

6. 重新加载 udev 规则:

   ```shell
   sudo udevadm control --reload-rules
   sudo udevadm trigger
   ```

7. 测试热插拔功能:

   插入和拔出 SD 卡,查看 `/tmp/sdcard.log` 文件中是否有相应的日志输出。