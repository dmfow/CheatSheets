## Mixed

#### NSlookup
```
nslookup www.bbc.co.uk

nslookup
>
> type=mx
> www.bbc.co.uk
> quit



nslookup
>
> debug
> www.bbc.co.uk
> quit

```





## USB

#### Can't access a USB
```
# In the commmand (maybe as admin)
> Diskpart
DISKPART> select disk 2
DISKPART> clean
"DiskPart has encountered an error: Access is denied."
DISKPART> attribute disk clear readonly
DISKPART> clean
DISKPART> format fs=ntfs quick
DISKPART> exit
```


#### Bootable USB with ISO (this procedure does not work with all boot systems)
```
###### PART 1 - open the command window #############
open CMD (command window) as administrator (rightclick - run as administrator)
click allow if the question comes up
Run command in the command window:

###### PART 2 - make the USB a bootable disk and format it #############
diskpart
list disk

# ------- Do this command with care, or you can crash and erase you computer ------------
# !
# !
select disk X (exchange X to your disk number in the "list disk")
# !
# !
# ---------------------------------------------------------------------

clean
create partition primary
select partition 1
active
format FS=ntfs quick
# OR (UEFI support for fat32)
format FS=fat32 quick

assign
exit


# OR (fat/fat16)
clean
create part primary size=4000
active
format FS=fat quick
assign
exit


###### PART 3 - copy your files from the ISO to the USB #############
# On windows 7 using WinCDEmu (skip is windows 10 or 11)
Install WinCDEmu if not installed (https://wincdemu.sysprogs.org/)

Rightclick on the iso file
choose "select drive letter & mount"
choose eg R:
# copy all files from R: to the USB drive 
xcopy *.* /s/e/f f:
  # (maybe got F:, E: or D: when running the command assign above - look in your file system)

right click in the R: drive and choose eject


```
