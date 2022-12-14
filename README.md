<h1 align="center"> Q Blockchain </h1>


## İhtiyacımız olanlar ve notlar:

* Bana sorularınız ve yardım ihtiyacınız için: [Telegram](https://t.me/+H_ecre-MCCg4ZTA0)
* Q Blockchain'i ödülsüz testnetinden beri takip ediyorum
* Burada yapılanlar kayıt gibi düşünün. Kayıt 31 Aralık'ta biter, Testnet 1 Ocak'ta başlar, 31 Mart'a kadar sürer
* Yani 4 ay 20 gün çalıştırmak demek, yüksek bir süre, ekip makalesinde bunu ödüllerle karşılayacağını söylüyor
* Ben garanti olduğunu düşünmüyorum, risk size kalmış, bu testnete katılıp katılmamak tamamen kişisel fikrinizdir
* Testnet bitince KYC olacakmış.
* Ödül dönemi kilit detayları var [makale](https://medium.com/q-blockchain/q-blockchain-validator-onboarding-program-part-1-validator-incentivized-testnet-567ef6e4002e) Katılmanın ne kadar mantıklı olduğunu siz seçin.
* Proje discordu: [Discord kanalı](https://discord.gg/pRkZRahJ)
* Repoyu sağ üstten forklayıp yıldızlamayı unutmayın!
* Eksik gördüklerinizi pull request yapmayı unutmayın!

## Sistem gereksinimleri:

* NOT: Bilgi yok, manuel olarak test ettim
* Hetzner kullandım.
* Varsa 3 CPU işlemci garanti olur.
```
2 CPU
2 RAM
```

## Değişkenleri ayarlıyoruz:

* Bir şifre belirleyin
```
PASSWORD=Şifrebelirle
```
* ŞİFRE yazan yeri düzenleyin
```
echo "export PASSWORD=ŞİFRE" $HOME/.bash_profile
source $HOME/.bash_profile
```

## Güncellemeleri tek tek yapınız

* Bazı güncellemelerde Y/N sorularında Y basıp ENTERLEYİN
```
sudo apt update
```
```
sudo apt upgrade
```
```
apt install docker-compose
```
```
apt install npm
```
```
apt install screen
```
```
sudo apt-get update && sudo apt install jq && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin
```

## Binary ve pwd oluşturuyoruz:

* Komutları tek tek giriniz
* Şifre kısmını düzenleyiniz

```
git clone https://gitlab.com/q-dev/testnet-public-tools.git
cd testnet-public-tools/testnet-validator/
mkdir keystore
cd keystore/
echo "ŞİFRE" >> pwd.txt
```

## Cüzdan oluşturup bilgileri kaydedlim:

* Oluşan 0xli cüzdanımıza token alalım: [Faucet](https://faucet.qtestnet.org/)

```
cd ..
docker run --entrypoint="" --rm -v $PWD:/data -it qblockchain/q-client:testnet geth account new --datadir=/data --password=/data/keystore/pwd.txt
```

## Yapılandırma dosyasını düzenleyeceğiz:

* address kısmına 0xli olmayan keyi girelim
* CTRL X Y ENTER ile çıkın sonra

```
cp .env.example .env
nano .env
```

![image](https://user-images.githubusercontent.com/101149671/206860212-79018b15-b65d-4291-8054-8785b0078153.png)

## Aynı işlem:

* addres ve password kısmını düzenleyin.
* address 0xsiz adres, şifrede yukarda belirlemiştik. 
* CTRL X Y ENTER ile çıkın sonra
```
nano config.json
```
![image](https://user-images.githubusercontent.com/101149671/206860284-853e9661-3f8a-4d0d-b343-9adf93ff62ea.png)

## Tokenlerimizi stakeleyelim

* Bu komut çalışmazsa yukarda yapılandırma dosyaları (`.env` ve `config.json`) eksik yapmışsınız demektir.

```
docker run --rm -v $PWD:/data -v $PWD/config.json:/build/config.json qblockchain/js-interface:testnet validators.js
```

## Şimdi private key oluşturuyoruz:
```
cd
cd testnet-public-tools
chmod +x run-js-tools-in-docker.sh
./run-js-tools-in-docker.sh
npm install
```
* Burada 0XLİCÜZDAN ve ŞİFRE kısmını düzenlemeyi unutmayın!
* Bu işlem sonunda PK adlı klasör oluşacak
* CTRL A D ile çıkın NPM içinden.
```
chmod +x extract-geth-private-key.js
node extract-geth-private-key 0XLİCÜZDAN ../testnet-validator/ ŞİFRE
```

## WinSCP veya Mobaxterm ile sunucunuza bağlanın:

* dosya `/root/testnet-public-tools/js-tools` içinde olacak
* İçine tıkladığımızda bize bir key vericek

![image](https://user-images.githubusercontent.com/101149671/206860533-1c06a2ed-4f60-42b9-95e6-2ad3429a5127.png)

## Şimdi bir Metamask cüzdanı lazım:

* Bunun için isterseniz testnet cüzdanı kullanın veya yeni cüzdan açın
* Sağ üstten profile tıklıyoruz ve hesabı içe aktar diyoruz
* Az önce PK klasöründen aldığımız keyi girip hesabı oluşturuyoruz

![image](https://user-images.githubusercontent.com/101149671/206860604-caebf5ca-f43d-4efd-9ce1-cf6a3e87fab2.png)

## Daha sonra [buradan](https://itn.qdev.li/) başvuruyoruz

* Testnet cüzdanınızı doğru olduğundan emin olun
* Böyle bir görsel alacaksınız:
![image](https://user-images.githubusercontent.com/101149671/206860707-60d24966-f27c-4348-90b1-1fd45428df8a.png)


## Burası kritik ve önemli:
```
cd
cd testnet-public-tools
cd testnet-validator
nano docker-compose.yaml
```

* geth'nin virgüne gelin boşluk bırakın
* " işareti ekleyip formda ki --ethstatslı komutu girin
* girdikten sonra bir daha " işareti ekleyip , ekleyin ve boşluk bırakın
* ÖRNEK:  `"geth", "--ethstats=ITN-RuesValidator-9:qstats-testnet@stats.qtestnet.org", ..`
* CTRL X Y ENTER ile çıkın

![image](https://user-images.githubusercontent.com/101149671/206860778-bd49a825-7c2c-4d68-b5c8-b7a3dd2a2cf4.png)

## Başlatıyoruz:
```
screen -S q
```
```
docker compose up -d
```
```
docker compose logs -f
```

## Explorerdan kontrol edelim:

* [Explorer](https://stats.qtestnet.org/) biraz yavaş ve ağır :)
* Rengibize göre:
* Yeşil olmak için bi yarım saat (tahmini) falan beklemek gerekiyor 
* Zamanla kırmızı-sarı-yeşil oluyorsunuz
```
🟢 - Eşleştin
🟡 - Eşleşiyor biraz bekle
🔴 - Eşleşme arıyor
```

-Explorerda kendi validatör adınızı bulmakta zorlanıyorsanız ctrl+f yaptıktan sonra kendi adınızı yazıp bulabilirsiniz. Ardından aşağıda işaretlediğim, kendi adınızın yanındaki dairenin üzerine geldiğinizde ''click to pin'' yazısına tıkladığınızda artık kendi adınızı en üstte görebileceksiniz :)

![kkk](https://user-images.githubusercontent.com/98269269/207414985-60d423e6-facb-4292-be91-999209e9fe29.png)


Eğer formu doldururken aşağıdaki hata ile karşılaşırsanız kullandığınız Identify adında değişiklik yapmanız veya adreslerinizi kontrol etmeniz gerekiyor. Kullandığınız karakterlerde değişiklik yaparak veya validatör adresinizi kontrol ederek bu sorunu çözebilirsiniz.

![dff](https://user-images.githubusercontent.com/98269269/207157285-76e4d6b2-bf65-4155-84b7-59f36fbae211.jpg)


## Hastalıklar cirit atıyor, dikkat edin kendinize!
