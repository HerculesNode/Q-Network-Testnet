# QBlockChain Türkçe Kurulum Rehberi
<h1 align="center"> <img src="https://raw.githubusercontent.com/herculessx/Q-Network-Testnet/main/FhOBhnLXkAkp0Bk.jpg" width="650"></h1>
<h1 align="center"> QBlockChain-Testnet </h1>
<h1 align="center"> Selamlar,  QBlockChain-Testnet Teşvikli Testnet Kurulum rehberi by Hercules
</h1>



## 🟢 Ödül Programı

 * [Medium Detay](https://medium.com/q-blockchain/q-blockchain-validator-onboarding-program-part-1-validator-incentivized-testnet-567ef6e4002e)
 * [Ödül Kayıt Linki](https://itn.qdev.li/)
 
 <br> 
 Kayıt 30 Aralık 2022 tarihine kadar devam edecek Testnet Yaklaşık 3 ay sürecek 01 Ocak 2023 tarihinde başlayacak ve 31 Mart 2023'e kadar sürecek Linkteki adresten kayıt olmanız gerekiyor Kayıt olduktan sonra size bir isim verecek ve aşağıdaki işlemleri yapacaksınız Multi Yasak ve Discord adreslerine girmeniz gerekiyor.
 
 <br><br>

Kayıt sonrası size Örnek  : TN-Hercules-47d34 Böyle bir isim verecek ve bunu değiştirip nodeyi tekrar durdurup başlatmanız gerekiyor. 
 
<br>cd testnet-public-tools/testnet-validator/  
 
dizininde bulunan  docker-compose.yaml  dosyasındaki adınızı değiştireceksiniz. Stats explorer adresinde aşağıdaki gibi görünecek adresiniz

<br>

![image](https://user-images.githubusercontent.com/101635385/206707554-02792278-1508-40fc-a3d8-12a904561a83.png)

 




## 🟢 Güncelleme

18.11.2022 tarihli güncelleme En alttadır Kurulum sonrası güncellemeyi yapınız.



### Linkler:

 * [Telegram Yardım Kanalımız](https://t.me/QblockchainTurkey)
 * [QBlockChain Discord Kanalı](https://discord.gg/aYDmNjrsJC)
 * [QBlockChain Twitter Kanalı](https://twitter.com/QBlockchain)
 

## 🟢 Gerekli notlar:
### Explorer:
 * [Explorer](https://explorer.qtestnet.org/)
### Faucet:
 * [FAUCET](https://faucet.qtestnet.org/)
 

 * Testnet Teşvikli olduğunu söylüyorlar. Sitesinden inceleyebilirsiniz. 
 * 1- kurulum cd testnet-public-tools/testnet-validator/ dizininde yapılması gerekiyor. 
 * 2- Kurulum cd  testnet-public-tools/omnibridge-oracle/ dizininde yapılması gerekiyor.
 * 3- Kurulum cd  testnet-public-tools/omnibridge-ui/  dizininde yapılması gerekiyor.
 * 4- Kurulum cd  testnet-public-tools/omnibridge-alm/  dizininde yapılması gerekiyor.
 
 * 4 parti kurulumdan oluşuyor Önce Validatör kuruyoruz daha sonra Oracle kurulumu yapıyoruz.
 
 * `https://rpc.ankr.com/eth_rinkeby` Rinkeby Testnet RPC ekleyeceğiz


 ## 🟢 Kurulumlar:

 * 1 testnet-public-tools/testnet-validator/ <br>
 * 2 testnet-public-tools/omnibridge-oracle  <br>
 * 3 testnet-public-tools/omnibridge-ui <br>
 * 4 testnet-public-tools/omnibridge-alm <br>
 
 ## 🟢 Sistemi Gereksinimleri

Minimum Gerekinimler <br> 1 CPU <br> 3 GB RAM <br> 30 GB Disk Alanı
 


## 🟢 Sistemi Güncelleme
```shell
sudo apt update && sudo apt upgrade -y
```

## 🟢 Gerekli Kütüphanelerin Kurulması
```shell
apt install ca-certificates curl gnupg lsb-release git htop
```

## 🟢 Docker Kurulumu
```shell

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
apt-get update
apt-get install docker-ce docker-ce-cli containerd.io
docker version
```


## 🟢 Docker Compose Yüklenmesi
```shell
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)
curl -L "https://github.com/docker/compose/releases/download/"$VER"/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

## 🟢 1. KURULUM Q Network Dosyalarının İndirilmesi ve Kurulumu

## Q Network Dosyalarını İndiriyoruz
```
screen -S qnetwork
git clone https://gitlab.com/q-dev/testnet-public-tools
```

## 🟢 keystore Klasörü ve pwd.txt Dosyası Oluşturulması 
Aşağıdaki komutla `testnet-validator` dosyası içerisinde `mkdir keystore` klasörü ve onun içerisine de bize verilecek cüzdanımız için şifremizi yazacağımız `pwd.txt` dosyasını oluşturup bu doyasnın içerisine giriyoruz. Şifremizi yazıp `ctrl x y enter` ile kaydedip çıkıyoruz.

```
cd testnet-public-tools/testnet-validator/
mkdir keystore
cd keystore
touch pwd.txt
nano pwd.txt
```

## Cüzdan Oluşturma
```
cd
cd testnet-public-tools/testnet-validator/
docker-compose run --rm --entrypoint "geth account new --datadir=/data --password=/data/keystore/pwd.txt" testnet-validator-node

```

Yukarıdaki kodu girdikten sonra aşağıdaki gibi bir çıktı almanız gerekiyor. Eğer böyle bir çıktı aldıysanız, her şey yolundadır. 
```
Your new key was generated

Public address of the key:   0xb3FF24F818b0ff6Cc50de951bcB8f86b522aa  -  SİZE BÖYLE BİR MATEMASK ADRESİ VERECEK
Path of the secret key file: /data/keystore/UTC--2021-01-18T11-36-28.705754426Z--b3ff24f818b0ff6cc50de951bcb8f86b52287dac

- You can share your public address with anyone. Others need it to interact with you.
- You must NEVER share the secret key with anyone! The key controls access to your funds!
- You must BACKUP your key file! Without the key, it's impossible to access account funds!
- You must REMEMBER your password! Without the password, it's impossible to decrypt the key!
```

## Kurulumu Yapılandırma

`.env` dosyası içerisine giriyoruz.<br>


```
cd
cd testnet-public-tools/testnet-validator/
cp .env.example .env
nano .env
```
Dosyada aşağıdaki yerleri dolduruyoruz.
 - `METAMASK_ADRESI` bu bölümüme yukarıda size verilen cüzdan adresini başında `0x` olmadan yazıyorsunuz.
 - `IP_ADRESI` bölümüne sunucunuzun ip adresini yazıyorsunuz.
 - Son olarak `ctrl x y enter` tuşlayarak dosyayı kaydediyoruz.

<br>

<img src="https://raw.githubusercontent.com/herculessx/Q-Network-Testnet/main/0aa05732-9d25-4a52-a4e1-aae61c6c659c.png" width="650">

## Matemask Cüzdan aktarma

testnet-public-tools/testnet-validator/keystore/ Dizininde UTC ile başlayan bir json dosyası göreceksiniz bunu bilgisayarınıza indirin. 
<br> Daha sonra Matemask cüzdanınızı açın ve içine json olarak import edin
<br> daha Sonra bu cüzdanın private keyini alın.
<br> Aşağıdaki 2 . Kurulum `omnibridge-oracle`  Bölümünde bu private key lazım olacak.

<img src="https://raw.githubusercontent.com/herculessx/Q-Network-Testnet/main/utc.PNG" width="650">

## config.json Dosyasını Düzenleme
Dosya içerisine giriyoruz.
```
nano config.json
```
Aşağıdaki yerleri düzenliyoruz;
 - `METAMASK_ADRESI` bu bölümüme yukarıda size verilen cüzdan adresini başında `0x` olmadan yazıyorsunuz.
 - `SIFRE` bölümüne sifrenizi.
 - Son olarak `ctrl x y enter` tuşlayarak dosyayı kaydediyoruz.
```
 {
      "address": "METAMASK_ADRESI",
      "password": "SIFRE",<br>
      "keystoreDirectory": "/data",
      "rpc": "https://rpc.qtestnet.org"
    }
```

<br>
<img src="https://github.com/herculessx/Q-Network-Testnet/blob/main/conf.png" width="650">
<br>

## Validatore Stake Etme
Bu işlemi yapmadan önce [faucetten](https://faucet.qtestnet.org/) token istemeyi unutmayın. 
```
docker run --rm -v $PWD:/data -v $PWD/config.json:/build/config.json qblockchain/js-interface:testnet validators.js
```

## Validatorumuzu https://stats.qtestnet.org Adresine Ekleme
```
nano docker-compose.yaml
```
Dosya içerisinde aşağodaki bölümü düzenliyoruz;
* `VALIDATOR_ADINIZ` bu bölüme validator adımızı yazıyoruz.

Alttaki kodu komple kopyalayın ve docker-compose.yaml dosyasındaki ile değiştirin burada sadece VALİDATÖR-İSMİNİZ yazan kısmı değiştirip kaydedin. ctrl + x Yes diyip kaydedin

```
version: "3"

services:
  testnet-validator-node:
    image: $QCLIENT_IMAGE
    entrypoint: ["geth", "--ethstats=VALİDATOR-İSMİNİZ:qstats-testnet@stats.qtestnet.org", "--bootnodes=$BOOTNODE1_ADDR", "--datadir=/data", "--nat=extip:$IP", "--port=$EXT_PORT", "--unlock=$ADDRESS",  "--password=/data/keystore/pwd.txt", "--mine", "--miner.threads=1", "--syncmode=full", "--rpc.allow-unprotected-txs", "--testnet", "--verbosity=3", "--miner.gasprice=1"]
    volumes:
      - ./keystore:/data/keystore
      - ./additional:/data/additional
      - testnet-validator-node-data:/data
    ports:
      - $EXT_PORT:8545/tcp
      - $EXT_PORT:8545/udp
    restart: unless-stopped

volumes:
  testnet-validator-node-data:
```

## Node'u Başlatma
```
docker-compose up -d
```

## Loglara Bakma
```
docker-compose logs -f --tail "100"
```
<br>CTRL + A + D ile ana ekrana dönelim 

# 2. omnibridge-oracle Kurulumu
İşlemlere başlamadan önce `/testnet-public-tools/testnet-validator/keystore` dosyası içerisinde `UTC` ile başlayan dosyayı bilgisayarımıza kaydedip, cüzdanımızı metamaskta içe aktarıyoruz. Daha sonra cüzdanımızın `prviate key`'ini alıyoruz. Bu bize lazım olacak. 

## .env Dosyası Oluşturma
```
cd
cd testnet-public-tools/omnibridge-oracle/
cp .env.testnet .env
```
Dosya içerisine giriyoruz. (İsterseniz winscp vb. progamla da aaçıp düzenlemeleri yapabilirsiniz.)
```
nano .env
```
Değiştirilecek yerler;
 - 1 `ORACLE_VALIDATOR_ADDRESS` buraya size verilen matemask adresini yazın
 - 2 `ORACLE_VALIDATOR_ADDRESS_PRIVATE_KEY` bu bölüme metamask adresinizin private keyini yazıyoruz
 - 3 `COMMON_FOREIGN_RPC_URL` buraya `https://rpc.ankr.com/eth_rinkeby` yazıyoruz.

## omnibridge-oracle Çalıştırma
```
docker-compose up -d
screen -S oracle
docker-compose logs -f --tail "100"
```
<br> loglar akmaya başladığında `ctrl a + d` ile screen'den çıkıyoruz


# 3. OmniBridge-UI Kurulumu

## .env Dosyası Oluşturma

```
cd
cd testnet-public-tools/omnibridge-ui/
cp .env.testnet .env
```
Dosya içerisine giriyoruz. (İsterseniz winscp vb. progamla da aaçıp düzenlemeleri yapabilirsiniz.)
```
nano .env
```
Değiştirilecek yerler;
<br /> 1 - `REACT_APP_FOREIGN_RPC_URL` buraya `https://rpc.ankr.com/eth_rinkeby` yazıyoruz.<br>

## OmniBridge-UI Çalıştırma
```
docker-compose up -d
```

# 4. Omnibridge-ALM Kurulumu

## .env Dosyası Oluşturma
```
cd
cd testnet-public-tools/omnibridge-alm/
cp .env.testnet .env
```
Dosya içerisine giriyoruz. (İsterseniz winscp vb. progamla da aaçıp düzenlemeleri yapabilirsiniz.)
```
nano .env
```
Değiştirilecek yerler;
<br /> 1 - `PORT` varsayılan olarak 8090 oluyor ama siz sunucunuzun durumunda değiştirebilirsiniz ben 8091 yaptım <br>
<br /> 2 - `COMMON_FOREIGN_RPC_URL` buraya `https://rpc.ankr.com/eth_rinkeby` yazıyoruz<br>

## OmniBridge-ALM Çalıştırma
```
docker-compose up -d
```

<br>
Şimdilik bukadar. Teşekkürler 

 * Bu [adreste](https://stats.qtestnet.org/) validatör adınızı görmeniz gerekiyor<br />

🟢 - senkronize, çok sayıda peer var<br>
🟡 - senkronize ediliyor, birkaç peer var <br>
🔴 - henüz senkronize edilmedi / az sayıda peer var<br>


# 🟢 Güncelleme
1- Node'u Durdurma ve Birimi Silme

```
docker-compose down -v
```
<br>
2- En Son Yapılandırmaları İndirme

```
git pull
```
<br>
3- En Son Docker Containerı Çekme (ve üzerine yazma)

```
docker-compose pull
```
<br>

4- Yeni Yapılandırmalar ile Yeniden Başlatma
```
docker-compose up -d
```


## 🟢 ip kontrol
<BR>
http://IPADRESİNİZ:8080/
<img src="https://raw.githubusercontent.com/herculessx/Q-Network-Testnet/main/ip.png" width="650">
 
 
 ## 🟢 Güncelleme 07.12.2022  ( Bu tarihten sonra kurulum yaptıysanız güncelleme yapmanıza gerek yok )

```
cd testnet-public-tools/testnet-validator/

git stash && git pull

QCLIENT_IMAGE=qblockchain/q-client:1.2.2

docker-compose pull && docker-compose up -d

docker-compose logs -f --tail "100" 
```
 
## 🟢 Peer Sorunu yaşayanlar 
 
 Peer ile ilgil sorun yaşayanlar aşağıdaki adımları uygulayabilir .  ctrl + d ile ekrandan çıkabilirsiniz.
<br>
 ```
cd testnet-public-tools/testnet-validator/
docker-compose exec testnet-validator-node geth attach /data/geth.ipc
admin.addPeer('enode://<ADDRESS>')
```

Örnek : admin.addPeer('enode://f00f1f85184e2ac8a460f2a91076429bc08a4ad018e24d8e78b76813eff0cc15a7c8566eb9c4671f7ba99cfce1ae0ccc40c9ddae3e6b3948a482a3d3a0c82f0a@65.108.74.180:31776')
 
```
enode://8eff01a7e5a66c5630cbd22149e069bbf8a8a22370cef61b232179e21ba8c7b74d40e8ee5aa62c54d145f7fc671b851e5ccbfe124fce75944cf1b06e29c55c80@79.125.97.227:54000
enode://9127cf39043562e0600b8baa7e192fd92bdb3bff573288312aa7e0336c79a4000844e8e8580e8efd64fbd99ade341bae1ea21835e4d1a777e579304b66b5acaf@185.170.115.95:30313
enode://37793ae0218500896ad2fb0a2aff634e29198b9729f5a83d52963b941f8f0af938a72cb4b5d48cb201a2c63e7903f1d35ea8827a38d4f7f7dc5b4100e8645f50@35.156.94.184:52350
enode://9963c9a837719cd8c802b14eb510f060994f5d4f1bf36796ab6287f0a3886fcccb6c74cb90f7a63ff982d0c6adca112706632c17cdc8660f6089f9bf5300f5a9@80.158.48.29:61275
enode://3b352d3349bfb0d1fac0fd703d0cc2e397fe9910d6a5fbe5077ff1ec46c50b261704d28de5e29c768e425b99f8acff605d00a0cf602425fac2a36a1505a26efb@36.69.120.50:53434
enode://08cf0b8ce2194c327937a22b9706ce9dc8b061371a9744f5d5f0cdd5694f6e239f45bec218b9e9490f96253ccc921b5ee568c86558a2b56802ef4be3f6c9dc29@80.158.48.29:61278
enode://e5bdbfd84f6462a01fcc877953f8ef931dd1f58ea1acf77993f0004d09c64fea3064410c7f0ec3eb7ab3c1ff091330d63dae80ced1dd3beab324a68a29072291@3.125.235.53:56056
enode://d176da7ae3104a95c5e99d427441df0ebc123dba2d54ead39edd13a43f55b8ff023759535e68e062c75b7e95126abe992c6e1e35ddc398b2412cad915f2106b0@3.71.94.49:55678
enode://1baa3388ce4a021a275d531b20e9b3de406fb7bd1ad36e1bb62443a0f826b0c9dd31535b94e0038f7fbc0018b596f270ea49d96b50c6537c6a51cf46df81df4e@38.242.158.186:30313
enode://ba55bd0a6ced3874fd29b8614322022e97bf0c85b68886a794ca505b82370584f398ce589430b4e3ace1028c42592cebda83adeb9af0452fae7d04946c4f5821@185.170.115.95:30314
enode://a1ea9b6606ed7087dfa2d4b166c7fee9a9a73da0a1d53aed5db7ab90f5c288ad3700a6d192994468493dfdadd691b19fdc479354d6d5aae0636016de5d9ae1a1@103.41.204.234:42672
enode://13c71856486f1ec9374fd5382ec0e3c54312e902930f5d68105b81a099a70bdac1d26616c3e94a696cc531fe592aff4422901a945e770c39a09f889a91683eb4@116.203.236.62:30313
enode://4493f390d9670a4c309a6a528865666a2949126a96a3ded5d2f2ce8a8d952b6c1c7e3cbcff4deb265f64246f23eb2e6668ad0c4e7abf1a38fb2a3b4e2382390a@85.215.92.83:39546
enode://be98d563773d207ccf0fcd2658ce35f6ab75fc74b182d4f5679e53218e9955a6ae85d257d32c27dad77acee7c50a612c9ede0c396c256ab0a4661d39a31d0684@65.108.74.188:4838
enode://a092ed0aa0c015414a6c68673d822f99eb5a02d5d9d8ada4f88f9361b61082bddb5f1506c2da0b7606bfbbe2f6ffed6982f94397e0c6cf19f3fca34124bcd00d@65.108.200.247:30399
enode://ebb67ca8e6c042b48843486570dba7959704738e66930b322f96b9333792377e68ec992b29f3ce17116dec9ef3d0e7b5f00b1e1938374de298440c60f27cecc5@152.44.36.189:30303
enode://7e5f6b7cf3e41d494b915c93029a8c6c057e414c153816b6090c07bb966ab4dbba4dae4d572dd2dffa98b080717dbec8a758146ffe19096589fbe6a0ce0586c1@157.90.36.57:55226
enode://1d43093b84ebf356a96886e869ac58c15eeb88c28dbdad0a54a045309267ac4d3f753369fccc3b5e70e2d02b7ea7b8c4998e3b5995003e0548aee6007b9c339a@18.194.123.154:59508
enode://81eeadb960551cbd0d13126543f5fb02bd67e943fae795a5f33ab5aecf60211a6fd065336496ffe224c83d40086b5ba8750c582e1f1f12fac7f3dd992ecafee8@65.108.74.180:56681
enode://fd8e7d940530b528ee03f9a4b01d58a09f348c9bd9f14d42cfae76ad75917fc69af616b19815f53c7d9f4b6adf583734c09e4a1b8620569b75636d20e29a490e@16.162.25.16:30313
enode://c7f5d4836146e88d8db3593e751ea6489830beb05835942ace6a377d95943220ae34e3c664ba5c8ee22c52b840fd82d397165e298ad74076aeddae8e09160892@161.97.69.121:30313
enode://e8fff0b380227fadebb4cfca963023e311c6077b250f889bf703464b1cce1e236fd2e0176423c1c7e67b75584ad3098f6d72bf97a77ae65f41181353d3c97ddd@46.38.240.229:30313
enode://f00f1f85184e2ac8a460f2a91076429bc08a4ad018e24d8e78b76813eff0cc15a7c8566eb9c4671f7ba99cfce1ae0ccc40c9ddae3e6b3948a482a3d3a0c82f0a@65.108.74.180:31776
```
