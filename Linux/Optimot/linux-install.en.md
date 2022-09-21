# Linux Installation

## Ubuntu Desktop
### symbol file
With sudo priviledges add the following xkb section at the end of the file `/usr/share/X11/xkb/symbols/fr`
```c
partial alphanumeric_keys
xkb_symbols "optimot_ergo" {
    ...
};
```
### lst files
Then in `/usr/share/X11/xkb/rules/base.lst` we need to add 
```lst
optimot_ergo    fr: French (Optimot, clavier Ergo)
```
after the `!variant` section.
The same needs to be done in `/usr/share/X11/xkb/rules/evdev.lst`

### xml files
Then in `/usr/share/X11/xkb/rules/base.xml` the following section need to be added in the `variantlist` of the `layout` "fr"
```xml
        <variant>
          <configItem>
            <name>optimot_ergo</name>
            <description>French (Optimot, clavier Ergo)</description>
          </configItem>
        </variant>
```
The same needs to be done in `/usr/share/X11/xkb/rules/evdev.xml`

## From the console
To register the xkb from the console and use it on the current session :
```bash
$ xkbcomp -w0 Optimot.xkb $DISPLAY
```
Then the keyboard layout should be available.

## Compose
The XCompose content file could be added into `/usr/share/X11/locale/en_US.UTF-8/Compose`.
But the more convenient way to use it is by coping the compose file as is in the user home directory as `.XCompose`:
```bash
$ cp ./XCompose ~/.XCompose 
```

## Registering
Once done launch:
```bash
$ sudo dpkg-reconfigure xkb-data
```
and reboot the machine


## Credits
Thanks to @TrucTruc for the help on those instructions