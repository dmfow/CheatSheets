## Bootable USB

#### Bootable USB with ISO
pen CMD (command window) as administrator (rightclick - run as administrator)
click allow if the question comes up
Run command in the command window:
```
diskpart
list disk

# !!!!!!!!!!!!!!! Do this command with care, or you can crash end erase you computer !!!!!!!!!!!!!!!!!!!!!!
select disk X (exchange X to your disk number)

clean
create partition primary
select partition 1
active
format FS=fat32 quick
# OR
format FS=ntfs quick

assign
exit


# Copy the ISO files to the disk - using WinCDEmu
Install WinCDEmu if not installed (https://wincdemu.sysprogs.org/)
Rightclick on the iso file
choose "select drive letter & mount"
choose eg R:
copy all files from R: to the USB drive (maybe got F:, E: or D: when running the command assign above - look in your file system)
```
