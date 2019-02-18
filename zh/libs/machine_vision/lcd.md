lcd 屏幕显示驱动
====



## 函数

### lcd.init(type=1)

初始化 `LCD` 屏幕显示黑色

#### 参数

* `type`： `LCD` 的类型（保留给未来使用）:
  * `0`: None
  * `1`: lcd shield（默认值）
> type 是键值参数，必须在函数调用中通过写入 type= 来显式地调用

### lcd.deinit()

注销 `LCD` 驱动，释放I/O引脚

### lcd.width()

返回 `LCD` 的宽度（水平分辨率）


### lcd.height()

返回 `LCD` 的高度（垂直分辨率）。


### lcd.type()

返回 `LCD` 的类型（保留给未来使用）：

0: None
1: lcd Shield


### lcd.set_backlight(state)

设置 `LCD` 的背光状态， 关闭背光会大大降低lcd扩展板的能耗

> //TODO: 未实现

#### 参数

* `state`： 背光亮度， 取值 [0,100]

### lcd.get_backlight()

返回背光状态

#### 返回值

背光亮度， 取值 [0,100]

### lcd.display(image, roi=Auto)

在液晶屏上显示一张 `image`（GRAYSCALE或RGB565）。

roi 是一个感兴趣区域的矩形元组(x, y, w, h)。若未指定，即为图像矩形

若 roi 宽度小于lcd宽度，则用垂直的黑色边框使 roi 居于屏幕中心（即用黑色填充未占用区域）。

若 roi 宽度大于lcd宽度，则 roi 居于屏幕中心，且不匹配像素不会显示（即液晶屏以窗口形态显示 roi 的中心）。

若 roi 高度小于lcd高度，则用垂直的黑色边框使 roi 居于屏幕中心（即用黑色填充未占用区域）。

若 roi 高度大于lcd高度，则 roi 居于屏幕中心，且不匹配像素不会显示（即液晶屏以窗口形态显示 roi 的中心）。

> roi 是键值参数，必须在函数调用中通过写入 roi= 来显式地调用。

### lcd.clear()

将液晶屏清空为黑色。




## 例程

### 例程 1： 显示英文

```python
import lcd

lcd.init()
lcd.lcd.draw_string(100, 100, "hello maixpy", lcd.RED, lcd.BLACK)

```

### 例程 2： 显示图片

```python
import lcd
import image

img = image.Image("/sd/pic.bmp")
lcd.display(img)
```

### 例程 3： 利用显示图片的方式显示英文

```python
import lcd
import image

img = image.Image()
img.draw_string(60, 100, "hello maixpy", scale=2) 
lcd.display(img)
```

### 例程 4： 实时显示摄像头捕捉到的图像

```python
import sensor, lcd

sensor.reset()
sensor.set_pixformat(sensor.RGB565)
sensor.set_framesize(sensor.QVGA)
sensor.skip_frames()
sensor.run(1)
lcd.init()

while(True):
    lcd.display(sensor.snapshot())
```




