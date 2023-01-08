## Bootable USB

#### Bootable USB with ISO
```
###### PART 1 - open the command window #############
open CMD (command window) as administrator (rightclick - run as administrator)
click allow if the question comes up
Run command in the command window:

###### PART 2 - make the USB a bootable disk and format it #############
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


###### PART 3 - copy your files from the ISO to the USB #############
# On windows 7 using WinCDEmu (skip is windows 10 or 11)
Install WinCDEmu if not installed (https://wincdemu.sysprogs.org/)

Rightclick on the iso file
choose "select drive letter & mount"
choose eg R:
copy all files from R: to the USB drive (maybe got F:, E: or D: when running the command assign above - look in your file system)
```
