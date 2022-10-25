！！！不要尝试在rc.local里启动显卡，容易让ubuntu崩溃，可以建一个nvidia.sh，在开机后手动开启

```bash
sudo prime-select nvidia
sudo modprobe nvidia
```

新版linux无rc.local，设置方法：

1. 设置rc-local.service

```bash
sudo gedit /etc/systemd/system/rc-local.service
sudo chmod 777 /etc/systemd/system/rc-local.service
```

​	内容如下：

```bash
[Unit]
Description=/etc/rc.local Compatibility
Documentation=man:systemd-rc-local-generator(8)
ConditionFileIsExecutable=/etc/rc.local
After=network.target
[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
RemainAfterExit=yes
GuessMainPID=no
[Install]
WantedBy=multi-user.target
```

2. 重新加载systemd配置并激活rc-local.service

```bash
sudo systemctl daemon-reload
```

​	

3. 添加启动服务

   ```bash
   gedit /etc/rc.local
   内容如下：（第一行不能省略，否则会报错）
   #!/bin/sh -e
   sudo bash /etc/rc-local.sh
   exit 0
   ```

4. 给脚本赋予执行权限

   ```bash
   sudo chmod 777 /etc/rc.local
   sudo chmod 777 /etc/rc-local.sh
   rc-local.sh内容如下：
   python3 /home/timp2100/rc-local.py > /home/timp2100/rc-local.log
   ```

关机自动执行的任务同理：

1. 设置shutdown.service

   ```bash
   sudo gedit etc/systemd/system/shutdown.service
   sudo chmod 777 /etc/systemd/system/shutdown.service
   内容如下：
   [Unit]
   Description=Run command at shutdown
   Requires=network.target
   DefaultDependencies=no
   Conflicts=reboot.target
   Before=shutdown.target
   [Service]
   Type=oneshot
   RemainAfterExit=true
   ExecStart=/bin/true
   #path
   ExecStop=/bin/sh /etc/shutdown.sh
   [Install]
   WantedBy=multi-user.target
   ```

   

2. 创建要执行的脚本

   ```bash
   sudo touch /etc/shutdown.sh
   sudo chmod 777 /etc/shutdown.sh
   内容如下：
   sudo prime-select intel
   exit 0
   ```

3. 重新加载systemd配置并激活shutdown.service

   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable shutdown.service
   ```

4. 附systemctl服务管理器指令

```bash
sudo systemctl enable xxx.service
sudo systemctl start xxx.service
sudo systemctl restart xxx.service
sudo systemctl status xxx.service
```

