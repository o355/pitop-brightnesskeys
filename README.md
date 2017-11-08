# Using the brightness keys & other keys on the Pi-Top
As the title says, we'll be using key shortcuts to enable the brightness keys on the pi-top to work with Raspbian Stretch.

I have a Pi-Top v1 running Stretch, and that's what I'm testing on. Please submit a pull request if you have your hands on a Pi-Top v2 and have the keycodes for the shortcuts, if they're different.

# Technical stuff
Running `xev` shows that the brightness decrease key is set to `198`, and the increase key is set to `199`. In hex with `0x` this translates to `0xC6` and `0xC7` being the keys to decrease and increase brightness respectively.

In addition, the folder key is `200`, terminal `201`, and calc `202`. This translates to `0xC8`, `0xC9`, and `0xCA` being the hex for these keys.

# Getting shortcuts to work
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
        <command>pcmanfm</command>
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
 
 Once you're done adding the key shortcuts, make sure to restart your Pi-Top.
 
 # Extra messages
 I absolutely despise of the scaling that gets thrown in when you install the hub software. This should be configurable, and a user can't easily hack some code to disable the scaling. Not cool!
 
 Right now, I can't pinpoint how and why this is happening, all of their code for the manager isn't open source (ARGHHHH!!!!!), so bear with blurry icons until I can see the source code and track down why this is happening.
 
 For the UI, a semi-decent fix is to go into apperance settings, change the font size to 14, and change the menu size from medium back to large. I can't pinpoint a fix for the terminal, and I suspect pt-desktop is causing these permanent changes.
 
 I also had an issue where after a reboot after installing the pt-hub software I was entirely unable to control the brightness, it was stuck at 0 brightness.
 
 # Conclusion
 Thanks to @rricharz for the original code to do shortcuts for the Pi-Top brightness.
 
 Thanks to the pi-top team for finally making some improvements for open-sourcing their code and allowing the Pi-Top to work on normal Raspbian. I do suggest to the team that they should open-source everything pi-top related, and allow their code to work on platforms like Ubuntu MATE for the Pi.
