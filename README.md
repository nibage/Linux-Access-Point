
# Create simple accesspoint on Debian / Ubuntu / Mint #

## Prerequisities ##

* You need to have installed hostapd and isc-dhcp-server

```
sudo apt-get update
sudo apt-get install hostapd isc-dhcp-server
```

* After successful configuration listed below

enable_ap - create accesspoint
enable_wifi - destroy accesspoint and permit normal connection to wifis


## Example configuration ##

* Hostapd

My wireless interface ```wlp2s0``` and ethernet ```enp1s0```

In

```
/etc/hostapd/hostapd.conf

```

Put the following lines, if the file does not exist, create it

interface=wlp2s0

driver=nl80211

ssid=WLAN_sd

hw_mode=g

channel=6

macaddr_acl=0

auth_algs=1

ignore_broadcast_ssid=0

wpa=3

wpa_passphrase=PASSWORD

wpa_key_mgmt=WPA-PSK

wpa_pairwise=TKIP

rsn_pairwise=CCMP

* DHCPd

For dhcpd we need to configure two files

in 

```
/etc/default/isc-dhcp-server
```

put this one liner

INTERFACES="wlp2s0"

and to

```
/etc/dhcp/dhcpd.conf
```

option domain-name "www.yoursite.com";

option domain-name-servers 8.8.8.8,  8.8.4.4;

default-lease-time 86400;

max-lease-time 604800;

log-facility local7;

subnet 192.168.1.0 netmask 255.255.255.0 {

range 192.168.1.1 192.168.1.255;

option routers 192.168.1.1;

option subnet-mask 255.255.255.0;

option broadcast-address 192.168.1.255;

option domain-name-servers 8.8.8.8, 8.8.4.4;

}

You should then be able to run source scripts


