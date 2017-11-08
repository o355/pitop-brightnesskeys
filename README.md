# Using the brightness keys & other keys on the Pi-Top
As the title says, we'll be using key shortcuts to enable the brightness keys on the pi-top to work with Raspbian Stretch.

I have a Pi-Top v1 running Stretch, and that's what I'm testing on. Please submit a pull request if you have your hands on a Pi-Top v2 and have the keycodes for the shortcuts, if they're different.

# Technical stuff
Running `xev` shows that the brightness decrease key is set to `198`, and the increase key is set to `199`. In hex with `0x` this translates to `0xC6` and `0xC7` being the keys to decrease and increase brightness respectively.

In addition, the folder key is `200`, terminal `201`, and calc `202`. This translates to `0xC8`, `0xC9`, and `0xCA` being the hex for these keys.

# Getting this stuff to work
Thanks to @rricharz for the original code. To restore functionality to your brightness keys with the new device manager, you'll want to add the following code to the keyboard section of the file `/home/pi/.config/openbox/lxde-pi-rc.xml`.

```
    <keybind key="0xC7">
      <action name="Execute">
        <command>pt-brightness -i</command>
      </action>
    </keybind>
    <keybind key="0xC6">
      <action name="Execute">
        <command>pt-brightness -d</command>
      </action>
    </keybind>
 ```
 
 If you want functionality for the additional 3 keys, you'll want to add this code into the same file, same section.
 
 **File manager:**
 
 ```
    <keybind key="0xC8">
      <action name="Execute">
        <command>pcmanfm %U</command>
      </action>
    </keybind>
 ```
 
 **Terminal:**
 
 ```
    <keybind key="0xC9">
      <action name="Execute">
        <command>lxterminal</command>
      </action>
    </keybind>
 ```
 
 **Calculator:**
 
 ```
    <keybind key="0xCA">
      <action name="Execute">
        <command>galculator</command>
      </action>
    </keybind>
 ```
 
 # Conclusion
 Thanks to @rricharz for the original code to do shortcuts for the Pi-Top brightness.
