# pinebook.edid
Generate EDID firmware for the early 14" pinebook model with the 1366x768 panel missing its EDID

# useage

Compile and generate the file.

```bash
javac -d out src/nz/net/foobar/pinebook/EDID.java
java -cp out nz.net.foobar.pinebook.EDID > pinebook.edid.bin
```

Copy the file to `/lib/firmare/edid`.

Configure `armbianEnv.txt` with:

```
extraargs=drm.edid_firmware=edid/pinebook.edid.bin
disp_mode=800x480
edid=0
```

Re-generate `boot.scr`:

```
mkimage -C none -A arm -T script -d /boot/boot.cmd /boot.scr
```

The default display_mode appears to be `1920x1080p60` in https://github.com/armbian/build/blob/c9ab99a84ba5f61b6c1be0ab028671b9fc9b8667/config/bootscripts/boot-sunxi.cmd#L12 which will not work on the non-HD panels.

