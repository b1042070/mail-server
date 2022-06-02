# Mail-Server
## 組員
B1042011張芳瑜

B1042033余詩涵

B1042070張瑀芹
## Mail
* Mail介紹
* Mail安裝
* 實作一 : Mail給ubuntu其他使用者
* 實作二 : Mail給Gmail帳號
## Mail介紹

<img width="353" alt="螢幕擷取畫面 2022-06-02 200756" src="https://user-images.githubusercontent.com/106367137/171626696-07cb0dbf-7b96-4c83-942a-b1897cf73651.png">

<img width="452" alt="螢幕擷取畫面 2022-06-02 201307" src="https://user-images.githubusercontent.com/106367137/171626718-1f452c51-2bb4-4ed6-9f7c-6c9c7c59e8fa.png">

<img width="449" alt="螢幕擷取畫面 2022-06-02 201330" src="https://user-images.githubusercontent.com/106367137/171626729-1c5398ca-38d8-4050-ba41-83c1295d4be3.png">

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

- 添加新區域bind配置
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

- 重啟bind
```shell
sudo systemctl restart bind9
```

- 安裝postfix
```shell
sudo apt install postfix
```
<img width="461" alt="螢幕擷取畫面 2022-06-02 005705" src="https://user-images.githubusercontent.com/106367137/171459429-4442cad2-5ae8-4f5e-b0a2-3999ce9415d3.png">

設定套件

<img width="461" alt="螢幕擷取畫面 2022-06-02 005737" src="https://user-images.githubusercontent.com/106367137/171459522-34f555d0-44e3-42b0-b24d-5798c8685dc0.png">

設定域名

<img width="460" alt="螢幕擷取畫面 2022-06-02 005816" src="https://user-images.githubusercontent.com/106367137/171459644-11e639cf-58e9-4e96-8528-46a6f08abfe6.png">

- 安裝 mailutils
```shell
sudo apt install mailutils
```

- 添加用戶
```shell
sudo useradd -m -s /bin/bash dog
```

- 更改用戶密碼

```shell
sudo passwd dog
```

<img width="350" alt="螢幕擷取畫面 2022-06-02 010418" src="https://user-images.githubusercontent.com/106367137/171460737-3c430d47-3831-4004-a5c2-f5971d8e2fc9.png">

<img width="515" alt="螢幕擷取畫面 2022-06-02 010505" src="https://user-images.githubusercontent.com/106367137/171460817-93c37f70-b7af-4197-96a8-9c4d7ca1a3af.png">

## 實作一:Mail給ubuntu其他使用者
```shell
mail dog
```
Cc為寄件者

Subject為主旨

接著為信件內容

輸入完畢後ctrl+d送出

<img width="465" alt="螢幕擷取畫面 2022-06-02 010842" src="https://user-images.githubusercontent.com/106367137/171461647-4acc184e-7b6e-464d-bece-e297f1730f1f.png">

- 查看郵件是否寄出 
```shell
mail
```

![1654106164338](https://user-images.githubusercontent.com/106367137/171471228-42b5d54c-90b8-4c19-b1aa-6ccbce2c9c52.jpg)

- 登出切換用戶預覽郵件

```shell
mail
```

<img width="407" alt="螢幕擷取畫面 2022-06-02 011938" src="https://user-images.githubusercontent.com/106367137/171464682-3cef5874-2ff9-47ab-892b-db050b61727e.png">

- 按下Enter查看郵件內容

<img width="464" alt="螢幕擷取畫面 2022-06-02 012050" src="https://user-images.githubusercontent.com/106367137/171464884-bb3ceb79-bd16-4959-aff9-ee28c91f7320.png">

## 實作二:Mail給Gmail帳號

```shell
mail (自己或其他的mail)
```

![1654106422698](https://user-images.githubusercontent.com/106367137/171472371-5bba2c37-69b8-4d59-bec8-7680c3dcd849.jpg)


```shell
mail
```

![1654106534448](https://user-images.githubusercontent.com/106367137/171472392-c3c1e605-faf5-4e2d-9be7-1562ff547e15.jpg)


- 查看是否收到郵件(需要去垃圾郵件查看)

<img width="413" alt="螢幕擷取畫面 2022-06-02 012741" src="https://user-images.githubusercontent.com/106367137/171466114-e05adec9-0d89-4f81-b8a3-ae9178051939.png">

## 參考資料

[ https://dywang.csie.cyut.edu.tw/dywang/linuxserver/node67.html#:~:text ](https://dywang.csie.cyut.edu.tw/dywang/linuxserver/node67.html#:~:text)

[ https://www.hostinger.com/tutorials/how-to-install-and-setup-mail-server-on-ubuntu/ ](https://www.hostinger.com/tutorials/how-to-install-and-setup-mail-server-on-ubuntu/)





