# What is this?
This is the simple script allowing you to mount removable sdcard, formatted as Android Adopted Storage, on your linux PC. This script was inspired by this article https://nelenkov.blogspot.com/2015/06/decrypting-android-m-adopted-storage.html, but I've added uid/gid translation.

# Requirements
- Rooted Android smartphone/tablet etc
- Linux PC with installed bindfs package

# Obtaining decryption key
First, you need to get decryption key. It's stored in /data/misc/vold directory on your phone in file, named like expand_8838e738a18746b6e435bb0d04c15ccd.key If you have multiple files - try it all, until get the correct key (I suppost that it will be in the newest file).

I perfer to put phone into TWRP recovery mode and then do `adb pull /data/misc/vold` to get beforementioned directory contents.

Key file must be 16 bytes long.

Get key from it using command like `od -t x1 expand_8838e738a18746b6e435bb0d04c15ccd.key` (run this command on PC, not on phone), it will print 16 hexadecimal values like `0000000 00 01 02 03 04 05 06 07 08 09 0a 0b 0c 0d 0e 0f`. Remove first 7 zeroes and all spaces - this is will be your key.

# Obtaining partition UUID
Shut down your phone, insert sdcard into cardreader and execute `blkid` command. Find partition with name like "android_expand" and copy its partition UUID.

# Mounting
Create directory, where you will mount sdcard, open script and edit data in it (you have to set your key, partition uuid, path to mount directory and your uid/gid).

Run script as root: `./mount_adopted_storage mount`

# Unmounting
Just run `./mount_adopted_storage unmount`
