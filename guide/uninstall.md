<img align="right" src="https://github.com/galaxysollector/woa-r3q/blob/main/r3q.png" width="350" alt="Windows 11 running on r3q">

# Running Windows on the SAMSUNG GALAXY A90 5G SM-A908N

## Uninstalling Windows

### Prerequisites
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Modded TWRP](https://github.com/galaxysollector/woa-r3q/releases/tag/Recovery)

### Boot into the modded TWRP
> Flash it with Odin if you haven't already

#### Unmount all partitions
Go to TWRP > Mount > and unmount all partitions

### Running parted
```cmd
adb shell /sbin/parted /dev/block/sda
```

#### Printing the current partition table
> Parted will print the list of partitions
```cmd
print
```

#### Removing Windows partitions
> Replace **$** with the actual number of the partitions
>
> Do this for every partition after **omr**
```cmd
rm $
```

#### Recreating the userdata partition
```cmd
mkpart userdata ext4 9304MB 128GB
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

## Finished!

















































