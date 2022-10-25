## 功能

- 利用STM32G031J6M6单片机实现UART和SPI的互相转换。
- 用LED显示数据收发。
- 兼容0.7V~5V输入，可选3.3V/5V输出。

## 基本特性

- 20mm*20mm双层板。
- 为兼容输入和输出电压，采用了Boost电路+Buck电路，Boost电路的主要芯片为QX2303L50T，Buck电路的主要芯片为LM1117F-3.3（采用体积小的SOT-89封装）。
- 采用的主控芯片为STM32G031J6M6，封装为SOP8，是STM32中体积最小且引脚数最少的系列。
- 主控芯片8个引脚中2个用于供电，2个用于UART，4个用于SPI；程序下载口SWD是与UART和SPI共用的，通过在UART和SPI初始化之前先执行一定的延时的操作留出下载程序的时间；该芯片没有专用的reset引脚，采用在3V3上加一个常闭按钮的方式来实现复位按键功能。
- 在UART的TX、RX引脚和3V3之间接上LED来实现收发状态的显示，通过一个贴片开关选择3.3V/5V电压输出。

## 原理图

![spi-uart-sch](https://timp2100.cn/images/hardware/spi-uart/spi-uart-sch.png)

## 外观

![spi-uart-top](https://timp2100.cn/images/hardware/spi-uart/spi-uart-top.png)

![spi-uart-bottom](https://timp2100.cn/images/hardware/spi-uart/spi-uart-bottom.png)

## 源文件

[原理图及PCB文件地址](https://github.com/timp2100/hardware)