<h1 align="center"> <img src="https://raw.githubusercontent.com/herculessx/Q-Network-Testnet/main/FhOBhnLXkAkp0Bk.jpg" width="650"></h1>
<h1 align="center"> QBlockchain-Testnet </h1>
<h1 align="center"> Selamlar,  QBlockChain-Testnet Teşvikli Testnet Kurulum rehberi by Hercules - Scannerx
</h1>

### 🟢 Linkler:

 * [Telegram Yardım Kanalımız](https://t.me/FortaDestek)
 * [QBlockchain Discord Kanalı](https://discord.gg/b5VXuvXN)
 * [QBlockchain Twitter Kanalı](https://twitter.com/QBlockchain)
 
  ### 🟢 Explorer:
 * [Explorer](https://explorer.qtestnet.org/)
 
 
 ### 🟢 Faucet:

 * [FAUCET](https://faucet.qtestnet.org/)
 
 
 ## 🟢 Gerekli notlar:

 * Testnet Teşvikli olduğunu söylüyorlar Sitesinden inceleyebilirsiniz. 
 * ilk işlem testnet-validator/ dizininde yapılması gerekiyor. Diğer kurulumlar ilgili dizinde
 * 4 parti kurulumdan oluştuyor Önce Validatör kuruyoruz daha sonra Oracle
 * https://app.infura.io/  sitesine üye oluyoruz goerli Testnet RPC linkini alacağız.

 ## 🟢 Kurulumlar:

 *1 /valitador . <br>
 *2 /omnibridge-oracle.  <br>
 *3 /omnibridge-ui. <br>
 *4 /omnibridge-alm <br>

 
 ## 🟢 Docker ve güncellemeler::

Eğer  Sunucunuzda Doker yoksa önce kurulum yapmanız gerekiyor 
<br>
```
apt update && apt upgrade
apt install git
apt install docker.io
apt install docker-compose
apt install ca-certificates curl gnupg lsb-release git htop
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
apt-get update
apt-get install docker-ce docker-ce-cli containerd.io
```

## 🟢 1. KURULUM Git clone çekiyoruz
```
screen -S qnetwork
git clone https://gitlab.com/q-dev/testnet-public-tools
```

## 🟢 ilgili klasöre giriyoruz
```
cd testnet-public-tools/testnet-validator/
```

## 🟢 Klasör oluşumu ve şifre

mkdir keystore  komutu ile klasör oluşturuyoruz <br> 
içine girip  pwd.txt dosyası oluşturuyoruz ve içine şifre yazıyoruz. <br> 
Bu size vereceği matemask adresinin şifresi olacak.


## 🟢 Key şifre komutu giriyoruz
```
docker run --entrypoint="" --rm -v $PWD:/data -it qblockchain/q-client:testnet geth account new --datadir=/data --password=/data/keystore/pwd.txt
```
Böyle Bir çıktı almanız lazım
Your new key was generated

Public address of the key:   0xb3FF24F818b0ff6Cc50de951bcB8f86b522aa  -  SİZE BÖYLE BİR MATEMASK ADRESİ VERECEK
Path of the secret key file: /data/keystore/UTC--2021-01-18T11-36-28.705754426Z--b3ff24f818b0ff6cc50de951bcb8f86b52287dac

- You can share your public address with anyone. Others need it to interact with you.
- You must NEVER share the secret key with anyone! The key controls access to your funds!
- You must BACKUP your key file! Without the key, it's impossible to access account funds!
- You must REMEMBER your password! Without the password, it's impossible to decrypt the key!


## 🟢 Kurulumu Yapılandırıyoruz
```
QCLIENT_IMAGE=qblockchain/q-client:testnet

ADDRESS=SİZE VERDİĞİ MATEMASK ADRESİNİ YAZIN  ( bir önceki komutta verdiği adresi yazıyoruz başında 0x olmayacak )

IP=İPADRESİNİZİ YAZIN

EXT_PORT=30313


BOOTNODE1_ADDR=enode://c610793186e4f719c1ace0983459c6ec7984d676e4a323681a1cbc8a67f506d1eccc4e164e53c2929019ed0e5cfc1bc800662d6fb47c36e978ab94c417031ac8@79.125.97.227:30304
BOOTNODE2_ADDR=enode://8eff01a7e5a66c5630cbd22149e069bbf8a8a22370cef61b232179e21ba8c7b74d40e8ee5aa62c54d145f7fc671b851e5ccbfe124fce75944cf1b06e29c55c80@79.125.97.227:30305
BOOTNODE3_ADDR=enode://7a8ade64b79961a7752daedc4104ca4b79f1a67a10ea5c9721e7115d820dbe7599fe9e03c9c315081ccf6a2afb0b6652ee4965e38f066fe5bf129abd6d26df58@79.125.97.227:30306
```
<br>
testnet-public-tools/testnet-validator/  Dizininde bulunan  " .env "  dosyasını açın ve yukarda girdiğiniz bilgiler varmı diye kontrol edin yoksa dosya üzerinden girin ve kaydedin.

<img src="https://raw.githubusercontent.com/herculessx/Q-Network-Testnet/main/0aa05732-9d25-4a52-a4e1-aae61c6c659c.png" width="650">



## 🟢 Matemask Cüzdan aktarma

testnet-public-tools/testnet-validator/keystore/ Dizininde UTC ile başlayan bir json dosyası göreceksiniz bunu bilgisayarınıza indirin. 
<br> Daha sonra Matemask cüzdanınızı açın ve içine json olarak import edin
<br> daha Sonra bu cüzdanın private keyini alın.
<br> Aşağıdaki 2 . Kurulum omnibridge-oracle  Bölümünde bu private key lazım olacak.

<img src="https://raw.githubusercontent.com/herculessx/Q-Network-Testnet/main/utc.PNG" width="650">




## 🟢 config dosyanızı düzenleyin config.json DOSYASI Aşağıdaki şekilde yapıp kaydedin

testnet-validator dizininde olduğunuzdan emin olun değilseniz  cd testnet-public-tools/testnet-validator/  komutunu kullanın daha sonar aşağıdan config dosyanızı açın <br>
nano config.json
<br> gerekli yerleri değiştirin ctrl +x y diyip kaydedin

 {<br>
      "address": "SİZE VERİLEN MATEMASK ADRESİ 0X OLMAYACAK BAŞINDA",<br>
      "password": "GİRDİĞİNİZ ŞİFRE",<br>
      "keystoreDirectory": "/data",<br>
      "rpc": "https://rpc.qtestnet.org"<br>
    }
<br>
<img src="https://github.com/herculessx/Q-Network-Testnet/blob/main/conf.png" width="650">
<br>
## 🟢 Doğrulayıcılar Sözleşmesine Pay Koy
```
docker run --rm -v $PWD:/data -v $PWD/config.json:/build/config.json qblockchain/js-interface:testnet validators.js
```


## 🟢 Doğrulayıcınızı https://stats.qtestnet.org adresine ekleyin

nano docker-compose.yaml ile ilgili dosyaya girin aşağıdaki kod ile komple değiştirin <> İşaretleri olmayacak  

<br>
Değiştirmeniz gereken yer VALİDATÖR-İSMİNİZ  değiştirip kaydedin
 
```
version: "3"

services:
  testnet-validator-node:
    image: $QCLIENT_IMAGE
    entrypoint: ["geth", "--ethstats=<VALİDATÖR-İSMİNİZ>:qstats-testnet@stats.qtestnet.org", "--bootnodes=$BOOTNODE1_ADDR", "--datadir=/data", "--nat=extip:$IP", "--port=$EXT_PORT", "--unlock=$ADDRESS",  "--password=/data/keystore/pwd.txt", "--mine", "--miner.threads=1", "--syncmode=full", "--rpc.allow-unprotected-txs", "--testnet", "--verbosity=3", "--miner.gasprice=1"]
    volumes:
      - ./keystore:/data/keystore
      - ./additional:/data/additional
      - testnet-validator-node-data:/data
    ports:
    - $EXT_PORT:$EXT_PORT/tcp
    - $EXT_PORT:$EXT_PORT/udp
    restart: unless-stopped

volumes:
  testnet-validator-node-data:
```


## 🟢 Düğümü Başlat
```
docker-compose up -d
```

Eğer komut çalışmaz ise bu komutu girip install yapın daha sonra tekrar başlatma komutunu girin
<br>
apt install docker-compose

## 🟢 Düğümü izle
```
docker-compose logs -f --tail "100"
```
<br>CTRL + A + D ile ana ekrana dönelim 


## 🟢 2 . Kurulum omnibridge-oracle
```
cd testnet-public-tools/omnibridge-oracle/
cp .env.testnet .env
```
<br> .env adında dosya oluşacak bunu açıyoruz ister nano .env  isterseniz direk programla açın  <br>

1 - ORACLE_VALIDATOR_ADDRESS  (buraya size verilen matemask adresini yazın ) <br>
2 - ORACLE_VALIDATOR_ADDRESS_PRIVATE_KEY  ( Matemask adresinin private keyi ) <br>
3 - COMMON_FOREIGN_RPC_URL  ( infura.io üye olup goerli testnet rpc alın forta kuranlar bilir ) örnek : https://goerli.infura.io/v3/0b15cc96dc0d <br>

```
docker-compose up -d
screen -S oracle
docker-compose logs -f --tail "100"
```
<br> loglar akmaya başladığında ctrl a + d ile çıkın


## 🟢 3 . Kurulum OmniBridge-UI
```
cd ../omnibridge-ui
cp .env.testnet .env
```
<br> .env adında dosya oluşacak bunu açıyoruz ister nano .env  isterseniz direk programla açın  <br>

1 - REACT_APP_FOREIGN_RPC_URL  ( infura.io üye olup goerli testnet rpc alın forta kuranlar bilir ) örnek : https://goerli.infura.io/v3/0b15cc96dc0d <br>

```
docker-compose up -d

```


## 🟢 4 . Kurulum Omnibridge-ALM
```
cd ../omnibridge-alm
cp .env.testnet .env
```
<br> .env adında dosya oluşacak bunu açıyoruz ister nano .env  isterseniz direk programla açın  <br>

1 - PORT  ( 8090 oluyor ama isterseniz değiştirin ben 8091 yaptım )  <br>
2 - COMMON_FOREIGN_RPC_URL  ( infura.io üye olup goerli testnet rpc alın forta kuranlar bilir ) örnek : https://goerli.infura.io/v3/0b15cc96dc0d <br>

```
docker-compose up -d

```


<br>
Şimdilik bukadar Teşekkürler 
<br>
https://stats.qtestnet.org/   
Burada validatör isminizi görmeniz lazım<br><br>

🟢 - senkronize, çok sayıda akranı var<br>
🟡 - senkronize ediliyor, bazı eşler var <br>
🔴 - henüz senkronize edilmedi / az sayıda eşe sahip<br>



## 🟢 Güncelleme Geldiğinde uygulanacak Komut

1- Geçerli kök düğümü durdurun ve birimi silin

```
docker-compose down -v
```
<br>
2- En son yapılandırmaları çekin

```
git pull
```
<br>
3- En son docker görüntülerini çekin (ve üzerine yazın)

```
docker-compose pull
```
<br>

4- Yeni yapılandırmalar ve resimlerle yeniden başlatın
```
docker-compose up -d
```


## 🟢 ip kontrol
<BR>
http://IPADRESİNİZ:8080/
<img src="https://raw.githubusercontent.com/herculessx/Q-Network-Testnet/main/ip.png" width="650">
 
 
 ## 🟢 Diğer Yapılması Gerekenler

 Aşağıdaki adresten borç verme borç alma işlemlerini yapın ayrıca validatör stake işlemlerini gerçekleştirin.
 <BR>
 https://hq.qtestnet.org/ 
<BR>

Buradan Qdai , QUSD , QBTC 
<BR>
    
Aşağıdaki Formu doldurun
https://docs.google.com/forms/u/0/d/e/1FAIpQLSeet42006F_SZGlJC8UmdLvL2DrgYzTMM2jun928kiHMmBXBQ/alreadyresponded
