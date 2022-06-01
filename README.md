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
- 更新
```shell
sudo apt update
```
- 安裝bind9
```shell
sudo apt install bind9
```
- 查詢IP
先將ubuntu網路設定改為橋接介面卡
```shell
ifconfig
```
-
```shell
sudo nano /var/cache/bind/db.test
```
```properties
$ORIGIN test.com.
$TTL 1D
@       IN SOA     ns1 root(
                1 ;serial
                1D ;refresh
                2H ;retry
                2W ;expire
                5H ;minimum
);
@       IN        NS ns1
ns1     IN        A 192.168.250.7
mail    IN        A 192.168.250.7
@       IN        MX 5 mail
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
