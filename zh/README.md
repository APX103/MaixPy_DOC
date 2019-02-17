MaixPy 文档
======

<div class="title_pic">
    <img src="../assets/micropython.png"><img src="../assets/icon_sipeed2.png"  height="60">
</div>




## 什么是 MaixPy

MaixPy 是将 [Micropython](http://micropython.org/) 移植到 [K210](https://kendryte.com/)（ 一款64位双核 RISC-V CPU,  ） 的一个项目。

> MicroPython 是基于 Python3 的语法做的一款解析器，包含了 Python3 的大多数基础语法， 主要运行在性能和内存有限的嵌入式芯片上。（注意 Micropython 不包含 Python3 的所有语法）

> K210 在硬件上集成了机器视觉和机器听觉能力， 是一款定位 AI 和 AIOT 市场的SoC，同时也是一颗方便的MCU。 


Micropython 让我们在 K210 上编程更加简单快捷， 我们也将源代码开源在 [github](https://github.com/sipeed/MaixPy) 上

比如我们需要寻找**I2C**总线上的设备，只需要使用如下代码即可实现：

```python
from machine import I2C

i2c = I2C(I2C.I2C0, freq=100000, scl=28, sda=29)
devices = i2c.scan()
print(devices)
```

同样，我们需要实现一个**呼吸灯**，只需要如下代码：

```python
from machine import Timer,PWM
import time

tim = Timer(Timer.TIMER0, Timer.CHANNEL0, mode=Timer.MODE_PWM)
ch = PWM(tim, freq=500000, duty=50, pin=board_info.LED_G)
duty=0
dir = True
while True:
    if dir:
        duty += 10
    else:
        duty -= 10
    if duty>100:
        duty = 100
        dir = False
    elif duty<0:
        duty = 0
        dir = True
    time.sleep(0.05)
    ch.duty(duty)
```

**实时拍照**：
```python
import sensor
import image
import lcd
****
lcd.init()
sensor.reset()
sensor.set_pixformat(sensor.RGB565)
sensor.set_framesize(sensor.QVGA)
sensor.run(1)
while True:
    img=sensor.snapshot()
    lcd.display(img)
```

## 这篇文档的内容

所有关于 MaixPy 的内容， 包括：
* 如何选择并得到一款合适自己的模块或者开发板
* 如何开始上手使用
* 学习关于 Micropython 的基础知识
* 库和接口（API）文档查询

## 让我们开始打开 MaixPy 的神奇大门吧

首先我们选择一款适合自己的开发板， 目前有如下几款高性价比的开发板（核心板）：

* 使用了 Sipeed M1(荔枝丹) 模块的 Dan dock

![Dan dock](../assets/Dan_Dock.png)

* Sipeed Maix BiT

![BiT](../assets/BiT.png)

* Sipeed Go

![Go](../assets/Go.jpg)


要获得这些板子，可以访问Sipeed（矽速）官网[Sipeed official website](https://sipeed.com/)，或者[官方淘宝店](https://shop152705481.taobao.com/)

更多硬件的资料点击[这里](en/hardware/hardware.md)查看

然后[开始探索如何使用MaixPy吧](en/get_started.md)

## MaixPy 源码

MaixPy 源码是指 运行在 K210 上的 Micropython 的解析器， 使用 `C语言` 编写，如果只是想使用MaixPy，不需要了解源码；
如果想参与开发MaixPy的内置功能，可以下载进行开发，欢迎大家提交`PR`

MaixPy 源码托管在 [github](https://github.com/sipeed/MaixPy)

本项目主要由 &copy;<a href="https://www.sipeed.com" style="color: #f14c42">Sipeed</a> Co.,Ltd. 维护， 并接受来自开源社区的贡献， 具体贡献这见[贡献者列表](https://github.com/sipeed/MaixPy/graphs/contributors)

## MaixPy 文档源码

修改代码后，文档也会随之更新，

文档源码托管在 [github](https://github.com/sipeed/MaixPy_DOC)

注意： 在编辑文档前**必须**看[文档编写规范](contribute/doc_convention.md) 

|   分支     |   文档自动构建状态  |
| --------- | --------------- |
| master |[![Build Status](https://travis-ci.org/sipeed/MaixPy_DOC.svg?branch=master)](https://travis-ci.org/sipeed/MaixPy_DOC) |
| dev    |[![Build Status](https://travis-ci.org/sipeed/MaixPy_DOC.svg?branch=dev)](https://travis-ci.org/sipeed/MaixPy_DOC)    |




## 反馈

关于本文档或者功能或者源码方面的问题，也欢迎提交issue:

* [文档 反馈](https://github.com/sipeed/MaixPy_DOC/issues)
* [源码/功能 反馈](https://github.com/sipeed/MaixPy/issues)

------------



