# WireGuard
Ubuntu 21 &lt;---> Mikrotik 7.x

--------------------------------


sudo apt install wireguard

sudo su -
cd /etc/wireguard
umask 077
wg genkey > privatekey
wg pubkey < privatekey > publickey
wg genkey | tee privatekey | wg pubkey > publickey


### Ubuntu

sudo cat /etc/wireguard/wg0.conf

[Interface]
Address = 10.4.4.4/24
SaveConfig = true
ListenPort = 40741
FwMark = 0xca6c
PrivateKey = 4MPwC55Of....

[Peer]
PublicKey = qojTFvaZo8Lk18PbCQ.....
AllowedIPs = 0.0.0.0/0
Endpoint = [IP WAN]:13231
PersistentKeepalive = 10


### Mikrotik

/ip add address=10.4.4.1/24 interface=wireguard-TMask

/interface/wireguard> print 
Flags: X - disabled; R - running 
 0  R name="wireguard-TMask" mtu=1420 listen-port=13231 
      private-key="6NS+gy2aa4aWG....." 
      public-key="qojTFvaZo8Lk18P...."

/interface/wireguard/peers> print 
Columns: INTERFACE, PUBLIC-KEY, ENDPOINT-ADDRESS, ENDPOINT-PORT, ALLOWED-ADDRESS
# INTERFACE        PUBLIC-KEY                                    ENDPOIN  E  ALLOWED-A
0 wireguard-TMask  +DvsrxyWDsCGPWEKrqRdj72....  0.0.0.0  0  0.0.0.0/0



#### Run



# Start
wg-quick up wg0

# Stop
wg-quick down wg0

# Status
wg
