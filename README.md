# Using the brightness keys & other keys on the Pi-Top
As the title says, we'll be using key shortcuts to enable the brightness keys on the pi-top to work with Raspbian Stretch.

I have a Pi-Top v1 running Stretch, and that's what I'm testing on. Please submit a pull request or issue if you have your hands on a Pi-Top v2 and have the keycodes for the shortcuts, if they're different.

# Technical stuff
Running `xev` shows that the brightness decrease key is set to `198`, and the increase key is set to `199`. In hex with `0x` this translates to `0xC6` and `0xC7` being the keys to decrease and increase brightness respectively.

In addition, the folder key is `200`, terminal `201`, and dashboard `202`. This translates to `0xC8`, `0xC9`, and `0xCA` being the hex for these keys.

# The dashboard key - What to do about it on Raspbian
Here's the deal, it completely blew past me that the dashboard key was the dashboard key when I wrote this, and I actually assumed it was a calculator key! It looked like a calculator. Please sue.

Anyways, you can use it as a calculator key, but you can alternatively freely use it as a macro to launch any program you wish.

# Getting shortcuts to work
Thanks to @rricharz for the original code. To restore functionality to your brightness keys with the new device manager, you'll want to add the following code to the keyboard section of the file `/home/pi/.config/openbox/lxde-pi-rc.xml`.

The code below is properly formatted to fit the file with tabbing and all.

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
 
 **Calculator for the dashboard key:**
 
 ```
     <keybind key="0xCA">
      <action name="Execute">
        <command>galculator</command>
      </action>
     </keybind>
 ```
 
 Once you're done adding the key shortcuts, make sure to restart your Pi-Top.
 
 ## Alternative: Using pt-input instead of LXDE shortcut keys
 Thanks @m-roberts (Mike) from Pi-Top for suggesting this. But before I start, quoting Mike, "This is not clear, I realise, and the visibility is something that we are working on...". In my view, take this as technical information and something to use down the line until things get clearer. 
 
 To summarize his issue post, Pi-Top already provides a package called `pt-input` to do the same thing as LXDE shortcut keys.
 
 To install the package, use `sudo apt install pt-input`. Then, in `/etc/pi-top/pt-input/keyboard-commands`, you can edit the file with a shortcut. Here's the sample code he provided:
 
 ```
 {
    "id": {
        "keycode": 190,
        "name": "KEY_F20",
        "notes": ""
    },
    "commands": ["pt-brightness -d"]
},
```

As an additional note, it appears this method uses `showkey` for capturing key numbers. `190` is the brightness down key with `showkey`, but with `xev` it's 199.

 
 # Extra messages
With the included pt-device-manager your Raspbian desktop gets scaled up, resulting in some blurry icons. Mike (thanks again) suggested a few ways to disable scaling.

A permanent method is to install `pt-hub` with this command:

```
sudo apt install --no-install-recommends pt-hub
```

This won't install the desktop messaging service, so it appears you won't get important low battery warnings.

A short-term fix to enable the messaging service, but disable scaling is to do the following:

Back up these files:
* /etc/xdg/lxpanel/default/panels/panel
* /usr/share/raspi-ui-overrides/gtk.css
* /etc/xdg/lxsession/LXDE-pi/desktop.conf
* /etc/xdg/pcmanfm/LXDE-pi/desktop-items-0.conf
* /usr/share/lxterminal/lxterminal.conf
* /home/pi/.config/lxpanel/LXDE-pi/panels/panel
* /home/pi/.config/gtk-3.0/gtk.css
* /home/pi/.config/lxsession/LXDE-pi/desktop.conf
* /home/pi/.config/pcmanfm/LXDE-pi/desktop-items-0.conf
* /home/pi/.config/lxterminal/lxterminal.conf

Install the hub software:

`sudo apt install pt-hub`

Disable pt-desktop:

`sudo systemctl disable pt-desktop`

Again, thanks to Mike for commenting on this repo and
 
 # Conclusion
 Thanks to @rricharz for the original code to do shortcuts for the Pi-Top brightness.
 
 Thanks to the pi-top team for finally making some improvements for open-sourcing their code and allowing the Pi-Top to work on normal Raspbian. Having open-source code opens the gate for advanced users tinkering with their Pi-Tops.
 
 Thanks to @m-roberts for making an issue and addressing some concerns I had. 

# Typos? Confusing documentation? Issues?
Submit a PR or issue! I'm actively working on my Python project so I don't have all the time in the world to maintain this repo.

This was a hacked-up repo made at night to make brightness keys and shortcut keys work.
