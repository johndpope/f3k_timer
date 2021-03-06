# f3k_timer
The timer is designed for timing the flights on DLG gliders. Allows you to save up to 30 results in a list.

## Timer ciruit
| Arduino NANO | TFT 1.8' |
| --- | --- |
| PIN 08 | A0 |
| PIN 09 | RES |
| PIN 10 | CS |
| PIN 11 | SOA |
| PIN 13 | SCK |
| PIN 3v3 | LED |

| Item | +5V | GND |
| --- | --- | --- |
| Arduino | VCC | GND |
| TFT 1.8' | VCC | GND |

| Arduino NANO | Item | Note |
| --- | --- | --- |
| PIN A0 | + 1S battery | Voltage detect |
| PIN A1 | Button Start/Stop | |
| PIN A2 | Button List/Reset | |
| PIN 07 | Buzzer + | |

## Used libraries
* \<SPI\>
* \<Adafruit_GFX\>
* \"TFT_ST7735\" Setting for display  [TFTLCD-SPI1.44](http://www.kosmodrom.com.ua/el.php?name=TFTLCD-SPI1.44) in the _setting directory
* \<VoltageReference.h\>
* \<OneButton.h\>
* \<EEPROM.h\>

## Buttons function
### Start/Stop      
* Click - Start/Stop timer
* Long Press - Only on timer stop. Simultaneously with the List/Reset button, go to the **Setup** mode

### List/Reset - enable only if timer stop
* Click - list results
* Long Press - Clear results

## Setup menu
Enter to the Setup menu - on timer stop Long Press both buttons.

In the menu list current line marked ">".

* Start/Stop - next menu line     
* List/Reset - previous menu line     

Long press Start/Stop - enter edit line mode. In the edit mode line marked as "*".

Exit from edit mode - long press any button.

### Menu *Setup*
* **Exit**    - End setup without saving params to the EEPROM
* **Save**    - End setup and save params to the EEPROM
* **Restore** - End setup and restore previous params values
* **Default** - End setup and set params to the default values

### Menu *Color*
* **Backgr**  - Select background color. Black default. Note about this: red, green & blue used for symbols in viltage indicator
* **Timer**   - Select timer digits color. White default.
* **Result**  - Select results list color. Yellow default.

### Menu *Tone*
* **Start**   - Select start beep tone. Default note C5 (523 Hz)
* **Stop**    - Select stop beep tone. Default note C6 (1047 Hz)
* **15 sec**  - Select every 15 sec beep tone. Default note C7 (2093 Hz)
* **Minute**  - Select every minutes beep tone. Default note C8 (4186 Hz)

### Menu *Batt*
* **Off**     - Off signal voltage in sV. Default 300 (3.00 V)
* **Crit**    - Critical voltage in sV. Default 350 (3.50 V)
* **Warn**    - Warning voltage in sV. Default 380 (3.80 V)

### Menu *Time*
* **Corr**    - Timer correction. Default 0
* **Start**   - Start/Stop beep duration in ms. Default 200 (0.2 sec)
* **Beep**    - 15 sec/minutes beep duration in ms. Default 70 (0.07 sec). If 0 - 15 sec beep disabled.

## Timer correction
Since the clock speed of the microcontroller may vary depending on the instance, the stopwatch may hurry or lag. To adjust this, use the **Corr** parameter of the *Time* menu.

In this parameter, you must specify how long it takes for 1 minute in ms. The calculation procedure for this parameter is as follows:

* Start the timer at the same time as the stopwatch. For example, sports
* take a time of at least 10 minutes, preferably 30 minutes for more accurate calculation.
* compare the time. For example, the timer went ahead 0.6 seconds in 30 minutes
* 0.6 = 600 ms. 600/30 = 20. Enter the parameter **Corr** = 20.
* If the timer is behind, set the **Corr** parameter to negative value
