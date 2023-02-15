# micropython-customsymbols

# English: 

<details>
<summary> <b></b> (<i>click to expand</i>)</summary>

## Small library for drawing your own characters

### Principle of operation

The work is carried out by embedding into display library wrappers based on framebuf and intercepting the symbol with its subsequent reaching. Replacement is carried out by the algorithm of the basic commands for framebuf such as pixel, line ...

### Example of work:

```Python
from customsymbols import CustomSymbols
from machine import Pin, SPI
from st7565 import ST7565

''' Create a new class with CustomSymbols '''
class ST7565 (ST7565, CustomSymbols): pass

import sys
import os

if 'symbols' in os.listdir('/'):
     sys.path.ppend("symbols")# add a folder with characters
else:
     print("Download Symbols!")

'''Initialization of the display'''
DRST = Pin(1, Pin.OUT)
DRS  = Pin(4, Pin.OUT)
DCS  = Pin(5, Pin.OUT)
DSPIbus = SPI(0, baudrate=2000000, polarity=1, phase=1, sck=Pin(2), mosi=Pin(3), miso=Pin(0))

Display = ST7565(DSPIbus, DRS, DCS, DRST)
Display.set_contrast(0x25)

''' Load the symbols '''
Display.loadsymbols('<symbols>') #loads certain user characters in memory
#Display.loadallsymbols() loads all user characters in memory
#Display.loadsymbol('<symbol>') loads one specific symbol in memory

''' Display information '''
Display.fill(0)
#ctext is a complete analogue of text, but with a replacement of characters
Display.ctext ('<symbols>', 0, 1, 1)
Display.show()
```

For example, our Fork Library "Micropython-st7565" was chosen (https://github.com/immersive-programs/micropython-st7565)

<details>
<summary> <b> Adding your symbols </b> (<i> click to expand </i>) </Summary>

####
- 1.In the folder <b><i>symbols</i></b> create a new file <b><i>< symbol >.py</i></b> 
- 2.Spread the code to the file:
```Python
class char:
    def draw(buf,x,y,index,col):
        zero = x+8*index+1 #initial position
```
- 3.Create your symbol
- 4.Save and check whether the symbol will be loaded in memory

</details>

### Notes:
  - development was carried out in the Thonny IDE V4.0.2;
  - performance was checked for: "Micropython v1.19.1 on 2022-06-18";
  - used controller: "Raspberry Pi Pico";
  - To load code, it is recommended to use rshell: https://github.com/dhylands/rshell

#### Author: Denis
</details>

# Русский: 

<details>
<summary> <b></b> (<i>нажмите, чтобы развернуть</i>)</summary>

## Небольшая библиотека для отрисовки собственных символов

### Принцип работы:

Работа осуществляется при помощи встраивания в дисплейные библеотеки-драйверы основанные на framebuf и перехвата символа с последующей его отрисовкой. Замена осуществляется алгоритмом состоящих из базовых команд для framebuf таких, как pixel, line...

### Пример работы:

```Python
from customsymbols import CustomSymbols
from machine import Pin, SPI
from st7565 import ST7565

'''Создаём новый класс с влюченным в него CustomSymbols'''
class ST7565(ST7565, CustomSymbols): pass

import sys
import os

if 'symbols' in os.listdir('/'):
    sys.path.append("symbols")# добавляем папку с символами
else:
    print("Загрузите symbols!")

'''Инициализация дисплея'''
DRST = Pin(1, Pin.OUT)
DRS  = Pin(4, Pin.OUT)
DCS  = Pin(5, Pin.OUT)
DSPIbus = SPI(0, baudrate=2000000, polarity=1, phase=1, sck=Pin(2), mosi=Pin(3), miso=Pin(0))

Display = ST7565(DSPIbus, DRS, DCS, DRST)
Display.set_contrast(0x25)

'''Загружаем символы'''
Display.loadsymbols('ЕНОПСУШ') #загружает в память определённые пользовательские символы
#Display.loadallsymbols() загружает в память все пользовательские символы
#Display.loadsymbol('<символ>') загружает в память один определённый символ

'''Отображаем информацию'''
Display.fill(0)
#ctext является полным аналогом text, но с заменой символов
Display.ctext('!!!УСПЕШНО!!!',   0, 1, 1)
Display.show()
```

Для примера работы был выбран наш форк библиотеки "micropython-st7565" (https://github.com/Immersive-programs/micropython-st7565)

<details>
<summary> <b>Добавление своих символов</b> (<i>нажмите, чтобы развернуть</i>)</summary>

####
- 1.В папке <b><i>symbols</i></b> создайте новый файл <b><i><Символ>.py</i></b> 
- 2.Скопируйте код в файл: 
```Python
class char:
    def draw(buf,x,y,index,col):
        zero = x+8*index+1 #начальная позиция
```
- 3.Создайте свой символ
<details>
<summary> <b>Пример 'Ё'</b> (<i>нажмите, чтобы развернуть</i>)</summary>

```Python
class char:
    def draw(buf,x,y,index,col):
        zero = x+8*index+1
        buf.line(zero,y+2,zero,y+6,col)
        buf.line(zero+1,y+2,zero+1,y+6,col)
        buf.line(zero,y+2,zero+4,y+2,col)
        buf.line(zero,y+4,zero+3,y+4,col)
        buf.line(zero,y+6,zero+4,y+6,col)
        buf.pixel(zero+1,y,col)
        buf.pixel(zero+3,y,col)
```
</details>

- 4.Сохраните и проверти будет ли загружен символ в память

</details>

### Примечания:
 - Разработка велась в Thonny IDE V4.0.2;
 - Работоспособность проверена на: "MicroPython v1.19.1 on 2022-06-18";
 - Использованный контроллер: "Raspberry Pi Pico";
 - Для загрузки кода рекомендуется использовать Rshell: https://github.com/dhylands/rshell

#### Автор кода: Денис

</details>
