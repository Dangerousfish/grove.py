grove.py
========

[![Build Status](https://travis-ci.org/Seeed-Studio/grove.py.svg?branch=master)](https://travis-ci.org/Seeed-Studio/grove.py)
[![](https://img.shields.io/pypi/v/grove.py.svg)](https://pypi.python.org/pypi/grove.py)

Python library for Seeedstudio Grove Devices on Raspberry Pi.



### Install grove.py from pypi 
- For Python2
```shell
sudo pip install grove.py
```

- For Python3
```shell
sudo pip3 install grove.py
```
### Install grove.py from source code
```shell
git clone https://github.com/Seeed-Studio/grove.py
cd grove.py
# Python2
sudo pip install .
# Python3
sudo pip3 install .
```

### Install MRAA and UPM for Raspberry Pi

- Add repository
```
echo "deb https://seeed-studio.github.io/pi_repo/ stretch main" | sudo tee /etc/apt/sources.list.d/seeed.list
```

- Add public GPG key
```
curl https://seeed-studio.github.io/pi_repo/public.key | sudo apt-key add -
```
or
```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys BB8F40F3
```

- Install MRAA & UPM
```
sudo apt update
sudo apt install python-mraa python-upm
```

### Install library raspberry-gpio-python
```
sudo apt-get install python-rpi.gpio python3-rpi.gpio
```

### Install library rpi_ws281x
```
sudo pip install rpi_ws281x
sudo pip3 install rpi_ws281x
```


### Usage
After installing `grove.py`, A few CLI commands with prefix `grove_` is available, such as `grove_led`, `grove_button`, `grove_ultrasonic_ranger` and etc. For I2C Grove devices, the default bus is used (I2C 1 on Pi). For digital input & output Grove devices, pin numbers should be provided as the arguments of these commands.

```shell
sudo grove_pwm_buzzer
grove_i2c_color_sensor_v2
grove_led 12
grove_button 22
grove_ultrasonic_sensor 12 13
......
```

#### Digital output device like Grove - LED
```python
import time
from grove.grove_led import GroveLed

led = GroveLed(12)

while True:
    led.on()
    time.sleep(1)
    led.off()
    time.sleep(1)
```

#### Digital input device like Grove - Button
```python
pin = 12
button = Factory.getButton("GPIO-HIGH", pin)

while True:
    if button.is_pressed():
        print('Button is pressed')
    else:
        print('Button is released')
    time.sleep(1)
```

#### Red/Yellow/Blue LED Button
```shell
# single click to light on
# double click to blink
# long press   to light off
grove_ryb_led_button
```

#### Basic GPIO Input & Output
```python
import time
from grove.gpio import GPIO

led = GPIO(12, GPIO.OUT)
button = GPIO(22, GPIO.IN)

while True:
    if button.read():
        led.write(1)
    else:
        led.write(0)
    time.sleep(0.1)
```

#### PIR Motion Sensor
#### mini PIR motion sensor
```python
import time
from grove.factory import Factory

### connect to pin 5(slot D5)
pir = Factory.getGpioWrapper("PIRMotion", 5)
while True:
    if pir.has_motion():
        print("Hi, people is moving")
    else:
        print("Watching")
    time.sleep(1)
```

#### Buzzer
```python
import time
from grove.factory import Factory

buzzer = Factory.getGpioWrapper("Buzzer", 12)
while True:
    buzzer.on()
    time.sleep(1)
    buzzer.off()
    time.sleep(3)
```

#### Electromagnet
```python
import time
from grove.factory import Factory

magnet = Factory.getGpioWrapper("Electromagnet", 12)
while True:
    magnet.on()
    time.sleep(1)
    magnet.off()
    time.sleep(3)
```

#### 4 Digit Display
```python
import time
from grove.grove_4_digit_display import Grove4DigitDisplay

display = Grove4DigitDisplay(12, 13))

count = 0
while True:
    t = time.strftime("%H%M", time.localtime(time.time()))
    display.show(t)
    display.set_colon(count & 1)
    count += 1
    time.sleep(1)
```

#### I2C Color Sensor V2
```python
import time
from grove.grove_i2c_color_sensor_v2 import GroveI2CColorSensorV2
sensor = GroveI2cColorSensorV2()

print('Raw data of red-filtered, green-filtered, blue-filtered and unfiltered photodiodes')
while True:
    # r, g, b = sensor.rgb
    r, g, b, clear = sensor.raw
    print((r, g, b, clear))
    time.sleep(1.0)
```

#### I2C Motor Driver
use along with DC-Motor
```python
import time
from grove.grove_i2c_motor_driver import MotorDriver

motor = MotorDriver()
while True:
    # speed range: 0(lowest) - 100(fastest)
    motor.set_speed(100)
    # channel 1 only
    # to set channel 1&2: motor.set_speed(100, 100)

    # direction: True(clockwise), False(anti-clockwise)
    motor.set_dir(True)
    # channel 1 only,
    # to set channel 1&2: motor.set_dir(True, True)

    time.sleep(2)

    motor.set_speed(70)
    motor.set_dir(False)
    time.sleep(2)
```

#### Buzzer PWM mode
```python
from upm import pyupm_buzzer as GroveBuzzer

buzzer = GroveBuzzer.Buzzer(32)
# 1000 Hz sound last 2 seconds
print(buzzer.playSound(1000, 2000000))
```

#### Temperature & Humidity Sensor(DHT11)
```python
import time
from grove.grove_temperature_humidity_sensor import DHT

# DHT11 type
# insert to GPIO pin 5, slot D5
dht11 = DHT("11", 5)

while True:
    humi, temp = dht11.read()
    print('humidity {0}%, temperature {1}*'.format(humi, temp))
    time.sleep(1)
```

#### LCD 16x2 Characters
#### OLED Display 1.12"
```python
import time
from grove.factory import Factory

# LCD 16x2 Characters
lcd = Factory.getLcd("JHD1802")
# If it's OLED Display 1.12"
# lcd = Factory.getLcd("SH1107G")
rows, cols = lcd.size()
print("LCD model: {}".format(lcd.name()))
print("LCD type : {} x {}".format(cols, rows))

lcd.setCursor(0, 0)
lcd.write("hello world!")
lcd.setCursor(0, cols - 1)
lcd.write('X')
lcd.setCursor(rows - 1, 0)
for i in range(cols):
    lcd.write(chr(ord('A') + i))
time.sleep(3)

lcd.clear()
```

#### Temperature Sensor
```shell
grove_temperature_sensor
```

#### Thumb Joystick
```shell
grove_thumb_joystick
```

#### I2C High Accuracy Temperature Sensor(MCP9808)
```shell
grove_high_accuracy_temperature
```

#### Mech Keycap
```shell
grove_mech_keycap
```

