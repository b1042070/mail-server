# Mail-Server
## 組員
B1042011張芳瑜

B1042033余詩涵

B1042070張瑀芹
## Mail
* Mail介紹

* Mail安裝
## Mail介紹
## Mail安裝
### 將網路改為橋接介面卡
<img width="599" alt="1" src="https://user-images.githubusercontent.com/106367137/171447823-a085575b-1536-4cb3-83e4-b41d7b848e63.png">

- 更新
```shell
sudo apt update
```
- 安裝bind
```shell
sudo apt install bind9
```
- 查詢IP
```shell
ifconfig
```
![1654100004015](https://user-images.githubusercontent.com/106367137/171451126-e5d77c33-1ffd-427f-b682-e031582293ee.jpg)
- 配置 /var/cache/db.test
```shell
sudo nano /var/cache/bind/db.test
```
寫入此內容並將IP改為自己的
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
ns1     IN        A 192.168.111.37
mail    IN        A 192.168.111.37
@       IN        MX 5 mail
```
![1654099632873](https://user-images.githubusercontent.com/106367137/171449858-94a4d3f5-654f-4a63-b630-1618aec8377e.jpg)

```shell
sudo named-checkzone test.com. /var/cache/bind/db.test
```
<img width="456" alt="螢幕擷取畫面 2022-06-02 000834" src="https://user-images.githubusercontent.com/106367137/171450098-74f158a8-4d22-433c-ad61-bb5912ffb3e6.png">

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
