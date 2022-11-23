# QBlockChain Türkçe Kurulum Rehberi
<h1 align="center"> <img src="https://raw.githubusercontent.com/herculessx/Q-Network-Testnet/main/FhOBhnLXkAkp0Bk.jpg" width="650"></h1>
<h1 align="center"> QBlockChain-Testnet </h1>
<h1 align="center"> Selamlar,  QBlockChain-Testnet Teşvikli Testnet Kurulum rehberi by Hercules
</h1>


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
 * ilk işlem testnet-validator/ dizininde yapılması gerekiyor. Diğer kurulumlar ilgili dizinde yapıyoruz.
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
cd $HOME/testnet-public-tools/testnet-validator/
docker run --entrypoint="" --rm -v $PWD:/data -it qblockchain/q-client:testnet geth account new --datadir=/data --password=/data/keystore/pwd.txt
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
testnet-public-tools/testnet-validator/  Dizininde bulunan  `.env` dosyasını açın ve yukarda girdiğiniz bilgiler varmı diye kontrol edin yoksa dosya üzerinden girin ve kaydedin.<br>


```
cd
cd testnet-public-tools/testnet-validator/
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

Dosya içerisinde ekleme yapılacak yer aşağıda mevcut. dosya içeriğini silip aşağıdaki kodu düzenleyerek dosyaya yapıştırabilirsiniz.

```
version: "3"

services:
  testnet-validator-node:
    image: $QCLIENT_IMAGE
    entrypoint: ["geth", "--ethstats=VALİDATOR-İSMİNİZ:qstats-testnet@stats.qtestnet.org", "--bootnodes=$BOOTNODE21_ADDR", "--datadir=/data", "--nat=extip:$IP", "--port=$EXT_PORT", "--unlock=$ADDRESS",  "--password=/data/keystore/pwd.txt", "--mine", "--miner.threads=1", "--syncmode=full", "--rpc.allow-unprotected-txs", "--testnet", "--verbosity=3", "--miner.gasprice=1"]
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
cd  $HOME/testnet-public-tools/omnibridge-oracle/
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
cd  testnet-public-tools/omnibridge-ui/
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
cd  $HOME/testnet-public-tools/omnibridge-alm/
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
 
 
 ## 🟢 Güncelleme 18.11.2022  ( Bu tarihten sonra kurulum yaptıysanız güncelleme yapmanıza gerek yok )

```
cd  testnet-public-tools/testnet-validator/

git stash && git pull

QCLIENT_IMAGE=qblockchain/q-client:1.2.1

git stash apply && docker-compose pull

docker-compose up -d

docker-compose logs -f --tail "100" 
```
 
