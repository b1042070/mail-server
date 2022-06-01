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
- 將網路改為橋接介面卡

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

<img width="686" alt="螢幕擷取畫面 2022-06-02 004631" src="https://user-images.githubusercontent.com/106367137/171457622-84bf5e69-bd6b-4e65-a9c6-f81d0db82aee.png">

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
<img width="484" alt="螢幕擷取畫面 2022-06-02 002410" src="https://user-images.githubusercontent.com/106367137/171453467-0e1a4b49-c525-4b15-ab2a-7137815a1cc7.png">

```shell
sudo named-checkzone test.com. /var/cache/bind/db.test
```
<img width="456" alt="螢幕擷取畫面 2022-06-02 000834" src="https://user-images.githubusercontent.com/106367137/171450098-74f158a8-4d22-433c-ad61-bb5912ffb3e6.png">

```shell
sudo nano /etc/bind/named.conf.default-zones
```
在檔案中加入此內容
```properties
zone "test.com." {
       type master;
       file "db.test";
};
```

<img width="535" alt="螢幕擷取畫面 2022-06-02 004451" src="https://user-images.githubusercontent.com/106367137/171457295-5495684e-a11c-4c48-89c7-c27f98a10f97.png">

```shell
sudo nano /etc/bind/named.conf.options
```
0.0.0.0 改成 8.8.8.8 並將斜線刪除

<img width="534" alt="螢幕擷取畫面 2022-06-02 004147" src="https://user-images.githubusercontent.com/106367137/171456610-0afc967b-e0f4-4eac-8c56-a6597c70f906.png">

<img width="534" alt="螢幕擷取畫面 2022-06-02 004231" src="https://user-images.githubusercontent.com/106367137/171456752-125ebc3b-9de5-45d7-85b8-df84dfdaf80b.png">

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
