1. 查看已安装的内核版本

```bash
dpkg --get-selections | grep linux
dpkg --get-selections | grep linux-image
```

2. 查看正在使用的内核版本

```bash
uname -a
```

3. 删除不用的内核版本

```bash
sudo apt-get purge linux-image-5.4.0-84-generic
sudo apt-get purge linux-headers-5.4.0-84-generic
sudo apt-get purge linux-hwe-5.4-headers-5.4.0-84
sudo apt-get purge linux-modules-5.4.0-84-generic
```

4. 禁用内核更新

```bash
sudo apt-mark hold linux-image-generic linux-headers-generic
```

5. （启用内核更新）

```bash
sudo apt-mark unhold linux-image-generic linux-headers-generic
```

