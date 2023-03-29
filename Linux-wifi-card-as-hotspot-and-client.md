---  
share: true  
tag: public  
---  
# Linux wifi card as hotspot and client  
~~~  
# to make wifi card work as hotspot while also beeing connected  
sudo iw phy phy0 interface add wlan0_st type managed addr 1c:4d:70:a5:c5:86   
sudo iw phy phy0 interface add wlan0_ap type managed addr 1c:4d:70:a5:c5:87  
ip link  
iw wlp2s0 link  
# to prepare for connection without network manager  
wpa_passphrase ZTE_FC7CAD 12564023 |tee ZTE_wpa_supplicant  
cat ZTE_wpa_supplicant   
sudo service NetworkManager status  
sudo service NetworkManager stop  
sudo service NetworkManager status  
ip link  
sudo ip link set wlan0_st up  
sudo wpa_supplicant -c ZTE_wpa_supplicant -i wlan0_st &  
sudo dhclient wlan0_st  
ping 8.8.8.8  -c 3   
# setup vpn to us  
curl https://downloads.nordcdn.com/configs/files/ovpn_legacy/servers/us5726.nordvpn.com.tcp443.ovpn | tee nordvpn.openvpn  
echo -e "41XmatQDRV1oiBetbCb4aZAb\nWYLtf8Jio3QPdtN4XhZNMu9j" |tee nordvpn.pass  
curl ipinfo.io/json  
sudo openvpn --config nordvpn.openvpn --auth-user-pass nordvpn.pass &  
curl ipinfo.io/json  
# setup hotspot  
# hostapd conf  
echo "interface=wlan0_ap  
ssid=vizio_test  
wpa_passphrase=viziohack  
driver=nl80211  
country_code=SI  
hw_mode=g  
wpa=2  
auth_algs=1  
channel=1  
wpa_key_mgmt=WPA-PSK  
" > hostapd.conf  
# starting hostapd  
ip addr  
sudo hostapd hostapd.conf &  
apnet=192.168.7  
ap=wlan0_ap  
sudo ip addr add $apnet.1/24 dev $ap  
# might neet to call sudo systemctl stop systemd-resolved if port 53 is used  
# and change nameserver in /etc/resolv.conf to 8.8.8.8 or soemthing similar  
sudo  dnsmasq --interface=$ap --dhcp-range=$apnet.100,$apnet.199  
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward  
sudo iptables -t nat -A POSTROUTING -s $apnet.0/24 ! -d $apnet.0/24 -j MASQUERADE  
# setting up mitm  
sudo iptables -t nat -A PREROUTING -i $ap -p tcp -j REDIRECT --to-port 8080  
mitmproxy --mode transparent --showhost --intercept ~q --ignore-hosts ""  
~/Applications/mitmproxy --mode transparent --showhost --intercept ~q --save-stream-file log.txt --ignore-hosts "gstatic.com|google.com|support.supportview.com|netflix.com|amazonaws.com|images.vizio.com"  
  
~~~