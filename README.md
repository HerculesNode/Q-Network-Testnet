<h1 align="center"> Q-Network-Testnet </h1>
<h1 align="center"> Selamlar,  Q-Network-Testnet Teşvikli Testnet Kurulum rehberi:
</h1>

### Linkler:

 * [Telegram Yardım Kanalımız](https://t.me/FortaDestek)
 * [Q Netwrok Discord Kanalı](https://discord.gg/b5VXuvXN)
 
  ### Explorer:
 * [Explorer](https://discord.gg/b5VXuvXN)
 
 
 ### Faucet:

 * [FAUCET](https://faucet.qtestnet.org/)
 
 
 ## Gerekli notlar:

 * Testnet Teşvikli olduğunu söylüyorlar Sitesinden inceleyebilirsiniz. 
 * Tüm işlemler testnet-validator/ dizininde yapılması gerekiyor.
 
 ## Docker ve güncellemeler::

```
apt update && apt upgrade
apt install ca-certificates curl gnupg lsb-release git htop
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
apt-get update
apt-get install docker-ce docker-ce-cli containerd.io
```

## Git clone çekiyoruz
```
git clone https://gitlab.com/q-dev/testnet-public-tools
```

## ilgili klasöre giriyoruz
```
cd testnet-public-tools/testnet-validator/
```

## Klasör oluşumu ve şifre

mkdir keystore  komutu ile klasör oluşturuyoruz <br> 
içine girip  pwd.txt dosyası oluşturuyoruz ve içine şifre yazıyoruz. <br> 
Bu size vereceği matemask adresinin şifresi olacak.


## Key şifre komutu giriyoruz
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


## Kurulumu Yapılandırıyoruz
```
QCLIENT_IMAGE=qblockchain/q-client:testnet

ADDRESS=SİZE VERDİĞİ MATEMASK ADRESİNİ YAZIN  ( bir önceki komutta verdiği adresi yazıyoruz başında 0x olmayacak )

IP=İPADRESİNİZİ YAZIN

EXT_PORT=30313


BOOTNODE1_ADDR=enode://c610793186e4f719c1ace0983459c6ec7984d676e4a323681a1cbc8a67f506d1eccc4e164e53c2929019ed0e5cfc1bc800662d6fb47c36e978ab94c417031ac8@79.125.97.227:30304
BOOTNODE2_ADDR=enode://8eff01a7e5a66c5630cbd22149e069bbf8a8a22370cef61b232179e21ba8c7b74d40e8ee5aa62c54d145f7fc671b851e5ccbfe124fce75944cf1b06e29c55c80@79.125.97.227:30305
BOOTNODE3_ADDR=enode://7a8ade64b79961a7752daedc4104ca4b79f1a67a10ea5c9721e7115d820dbe7599fe9e03c9c315081ccf6a2afb0b6652ee4965e38f066fe5bf129abd6d26df58@79.125.97.227:30306
```

## config dosyanızı düzenleyin config.json DOSYASI Aşağıdaki şekilde yapıp kaydedin

 {<br>
      "address": "SİZE VERİLEN MATEMASK ADRESİ",<br>
      "password": "GİRDİĞİNİZ ŞİFRE",<br>
      "keystoreDirectory": "/data",<br>
      "rpc": "https://rpc.qtestnet.org"<br>
    }


## Doğrulayıcılar Sözleşmesine Pay Koy
```
docker run --rm -v $PWD:/data -v $PWD/config.json:/build/config.json qblockchain/js-interface:testnet validators.js
```

## Düğümü Başlat
```
docker-compose up -d
```

## Düğümü izle
```
docker-compose logs -f --tail "100"
```
