## Download and "Burn" ISO to USB

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
```

### Connect to Network
```
## requires iw and wpa_supplicant(for encryption)

## get info

$ iw dev
$ iw dev wlan0 link

## scan for APs

$ iw dev wlan0 scan
```
