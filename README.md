# Mail-Server
# 組員
B1042011張芳瑜

B1042033余詩涵

B1042070張瑀芹
# Mail
* Mail介紹

* Mail安裝
# Mail介紹
# Mail安裝
-更新
```shell
sudo apt update
```
-安裝bind9
```shell
sudo apt install bind9
```

```shell
ifconfig
```

```shell
sudo nano /var/cache/bind/db.test
```

```shell
sudo named-checkzone test.com. /var/cache/bind/db.test
```

```shell
sudo nano /etc/bind/named.conf.default-zones
```

```shell
sudo nano /etc/bind/named.conf.options
```

```shell
sudo systemctl restart bind9
```


```shell
sudo apt install postfix
```

```shell
sudo apt install mailutils
```

```shell
mail
```

```shell
sudo useradd -m -s /bin/bash dog
```

```shell
sudo passwd dog
```

```shell
mail dog
```
cc

```shell
sudo apt update
```
