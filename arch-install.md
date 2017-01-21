## Download and "Burn" ISO to USB

```
## Verify UEFI/systemd-boot
$ ls /sys/firmware/efi/efivars

$ timedatectl set-ntp true


```
## Wireless


### Find Card / Check Card Status

```
$ lspci
$ lspci -k

## or if usb

$ dmesg | grep usbcore
```

### Check Logs (if necessary)

Possible Errors: 

- "SIOCSIFFLAGS: No such file or directory"

```
$ dmesg | grep firmware
$ dmesg | grep iwlwifi
```

### Attempt to Raise Interface

```
$ ip link
$ ip link set wlan0 up
$ ip r 
```

### Find the Network
```
## requires iw and wpa_supplicant(for encryption)

## get info

$ iw dev
$ iw dev wlan0 link

## scan for APs

$ iw dev wlan0 scan
$ iw dev wlan0 scan > aps.txt
$ cat aps.txt | grep keyword

```

### Connect to Network

```
$ wpa_supplicant -D nl80211,wext -i wlan0 -c <(wpa_passphrase "your_SSID" "your_key")

## after connecting sucessefully, run the command with -B flag to run it in the background

## get ip

$ dhcpcd wlan0

$ ping 8.8.8.8
$ ping google.com
```

Breakdown

-D: Driver Name ("driver1") or Driver Names ("driver1,driver2). This flag is usually not needed.
nl80211 is the netlink interface 802.11 driver for linux
wext, or The Wireless Extension (WE), is a generic API allowing a driver to expose to the user space, configuration and statistics specific to common Wireless LANs. As far as I know, it is being phased out.

-i: interface

-c: configuration file
In this case, we used the wpa_passphrase command to generate the config on the fly

If you sucessfully connect and then can't reconnect, attempt a restart if you don't want to continue debugging.


### Update

```
$ pacman -Syyu
```

## Partition Disks

### Using Fdisk
```
$ fdsik /dev/sdX
Command:
  ## create a new disk label (wipes partition)
  > o
  ## create a new partion
  > n
  ## with primary type
  > p
  ## first partion
  > 1
  ## first sector
  > 20148
  ## last sector
  > 512MiB
  > n
  > p
  > 2
  > XXXX
  > XXXX
  ## change type to linux lvm
  > t
  > 2
  > 8e
  > w
  
```

## Encryption

### READ THE MAN PAGE

```
$ cryptsetup --cipher aes-xts-plain --key-size 512 --hash sha256 --iter-time 5000 --use-random --verify-passphrase luksFormat /dev/sdX2

$ cryptsetup luksOpen /dev/sda2 lvm

$ pvcreate --data-alignment 1m /dev/mapper/lvm

$ vgcreate volgroup0 /dev/mapper/lvm

$ lvcreate -L 100GB volgroup0 -n lv_root

$ lvcreate -L 8G volgroup0 -n lv_swap

$ lvcreate l 100%FREE volgroup -n lv_home

$ modprobe dm_mod

$ vgscan
```

