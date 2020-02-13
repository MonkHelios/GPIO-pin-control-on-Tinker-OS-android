# GPIO pin control on Tinker OS android

`There are two basic ways of controlling the GPIO pins`

## 1. Via ADB on a seperate machine 

* Enable developer options on the tinker board's android OS by selecting the about phone/tinker board in settings and clicking on the build number at the bottom repeatedly untill it tells you that you are a developer

* Go into developer options inside settings and turn on USB debugging

* on the PC, download [android platform tools](https://developer.android.com/studio/releases/platform-tools) for your operating system and extract it somewhere in your computer which can be easily accessed.

* Make sure that the tinker board and the PC are connected to the same network or preferably connected to each other via ethernet.

* Open the "android platform tools" directory on the PC and right click while pressing L-shift.

* Select "open power shell window here" (the option name might vary) or open CMD/Powershell and `cd` into the "android platform tools" directory.

* Find the IP address of the tinker board by running `ip a` in termux on the android OS.

or go into "about phone" and into "status", here you will find the IP addr also.

* in the powershell run 
```
> adb connect 192.168.xxx.xxx:5555     (replace the tinke rboard IP address in place of the 'x')
```
```
> adb root
```
```
> adb connect 192.168.xxx.xxx:5555     (again)
```
```
> adb shell
```

* Now you will get a root shell of the android system, in the root shell run
```
# cd /sys/class/gpio
```

* This is where the GPIO pin directories are stored, by default no GPIO pins are **not** initialized

[![INSERT YOUR GRAPHIC HERE](https://tinkerboarding.co.uk/wiki/images/2/21/Gpio-table.png)]()

* To init the GPIO pins we need to type the following commands (The directories must have the CPU IDs for the GPIO pins, not the wPi numbers)
```
# echo 17 > /sys/class/gpio/export
```
This will create a directory called `gpio17` with the required files in it
`Similarly you can add all the GPIO pins you want to use, for example I am using gpio17(CPU) or gpio7(wPi) or pin number 7`

* Then we need to assign its direction which is `out`
```
# echo "out" > /sys/class/gpio/gpio17/direction
```

* Now we can write to the value file to switch the pin on and off
```
# echo 1 > /sys/class/gpio/gpio17/value
```
```
# echo 0 > /sys/class/gpio/gpio17/value
```

