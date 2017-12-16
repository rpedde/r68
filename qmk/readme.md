r68 keyboard firmware
======================

This is QMK firmware for the [r68 keyboard](http://github.com/rpedde/r68).

It has been successfully built against
[QMK](https://github.com/qmk/qmk_firmware) on 8a0997.

# General Instructions #

Install necessary prereqs:

```
$ sudo apt-get install -y build-essential avr-libc gcc-avr dfu-programmer
```

Checkout qmk, and copy this directory (qmk) into the keyboard
directory of qmk as "r68"

```
$ git clone git@github.com:rpedde/r68
$ git clone git@github.com:qmk/qmk_firwmare
$ cp -a r68/qmk qmk_firwmare/keyboards/r68
```

Once you have check it out, build and burn the firmware.

```
$ cd qmk_firmware
$ git checkout 8a0997    # (this may not be necessary, but 8a0997 was head when I tested this)
$ make r68:default
```

You should at this point have a `r68_default.hex` file.  Now, burn it to to the
keyboard.  You will need two keyboards to do this, or else make a shell script
or something.

First, put the keyboard in DFU mode by hitting the reset button on the back.

```
$ sudo dfu-programmer atmega32u4 erase
$ sudo dfu-programmer atmega32u4 flash r68_default.hex
$ sudo dfu-programmer atmega32u4 reset
```

And the keyboard should come up with the default firmware.  To build
your own, copy keymaps/default into a new keymap (named "custom",
maybe?), change it as necessary, and build your custom firmware with
"make r68:custom".  Then flash r68_custom.hex.


 
