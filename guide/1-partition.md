<img align="right" src="https://github.com/galaxysollector/woa-r3q/blob/main/r3q.png" width="350" alt="Windows 11 running on r3q">

# Running Windows on the SAMSUNG GALAXY A90 5G SM-A908N

## Partitioning your device

### Prerequisites
- A brain (most important of all)

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [TWRP](https://github.com/galaxysollector/woa-r3q/releases/download/Recovery/twrp.img)

- [Stock Recovery](https://github.com/galaxysollector/woa-r3q/releases/download/Recovery/stockrecovery.img)


### Notes
> [!WARNING]  
> Do not run the same command twice unless specified.
> 
> DO NOT REBOOT YOUR PHONE! If you think you made a mistake, ask for help in the [Telegram chat](https://t.me/woa_msmnile_issues).
> 
> Do not run all commands at once, execute them in order!
>
> YOU CAN BREAK YOUR DEVICE WITH THE COMMANDS BELOW IF YOU DO THEM WRONG!!!

### Flash the modded TWRP
> If you have the official TWRP installed, flash it through there. Otherwise use Odin.

#### Unmount all partitions
Go to TWRP > Mount > and unmount all partitions

#### Running parted
```cmd
adb push parted /sbin && adb shell "chmod +x /sbin/parted" && adb shell /sbin/parted /dev/block/sda
```

#### Printing the current partition table
> Parted will print the list of partitions, userdata should be the last partition in the list.
```cmd
print
```

#### Removing userdata
> Replace **$** with the number of the **userdata** partition, which should be **33**
```cmd
rm $
```

#### Creating ESP partition
```cmd
mkpart esp fat32 9304MB 10GB
```

#### Creating Windows partition
> Replace **74GB** with the value you want to be allocated to Windows
```cmd
mkpart win ntfs 10GB 74GB
```

#### Creating WinPE partition
> [!Note]
> This is optional

> Replace **74GB** with the end value of Windows
>
> Replace **87GB** with the end value you want WinPE to have
```cmd
mkpart pe fat32 74GB 87GB
```

#### Recreating userdata
> Replace **74GB** with the end value of the Windows or WinPE partition you created above
```cmd
mkpart userdata ext4 74GB 128GB
```

#### Make ESP bootable
> Replace **$** with the number of the **ESP** partition, which should be **33**
```cmd
set $ esp on
```

#### Exit parted
```cmd
quit
```

#### Format data
Flash stock recovery, reboot recovery, go to the Wipe menu and press Format Data,
then type `yes`.
Reboot to download, flash twrp, boot recovery.

### Check if Android still starts
Restart the phone, and see if Android still works

## [Next step: Installing Windows](2-install.md)

















