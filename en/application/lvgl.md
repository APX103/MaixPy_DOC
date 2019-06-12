lvgl [LittlevGL](https://littlevgl.com/)
===========

Refer to the official documentation: [lvgl blog page](https://blog.littlevgl.com/2019-02-20/micropython-bindings)

## Demo

### Demo 1: Buttion

Display a button and tap it using the touchscreen

```python
import lvgl as lv
import lvgl_helper as lv_h
import lcd
import time
from machine import Timer
from machine import I2C
import touchscreen as ts
   
i2c = I2C(I2C.I2C0, freq=400000, scl=30, sda=31)
ts.init(i2c)
lcd.init()
lv.init()

disp_drv = lv.disp_drv_t()
lv.disp_drv_init(disp_drv)
disp_drv.disp_flush = lv_h.flush
disp_drv.disp_fill = lv_h.fill
lv.disp_drv_register(disp_drv)

indev_drv = lv.indev_drv_t()
lv.indev_drv_init(indev_drv) 
indev_drv.type = lv.INDEV_TYPE.POINTER
indev_drv.read = lv_h.read
lv.indev_drv_register(indev_drv)

scr = lv.obj()
btn = lv.btn(scr)
btn.align(lv.scr_act(), lv.ALIGN.CENTER, 0, 0)
label = lv.label(btn)
label.set_text("Button")
lv.scr_load(scr)


while True:
	tim = time.ticks_ms()
	lv.tick_inc(5)
	lv.task_handler()
	while time.ticks_ms()-tim < 0.005:
		pass

```
