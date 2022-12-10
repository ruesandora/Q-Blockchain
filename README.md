<h1 align="center"> Q Blockchain </h1>


## İhtiyacımız olanlar ve notlar:

* Bana sorularınız ve yardım ihtiyacınız için: [Telegram](https://t.me/+H_ecre-MCCg4ZTA0)
* Q Blockchain'i ödülsüz testnetinden beri takip ediyorum
* Burada yapılanlar kayıt gibi düşünün. Kayıt 31 Aralık'ta biter, Testnet 1 Ocak'ta başlar, 31 Mart'a kadar sürer
* Yani 4 ay 20 gün çalıştırmak demek, yüksek bir süre, ekip makalesinde bunu ödüllerle karşılayacağını söylüyor
* Ben garanti olduğunu düşünmüyorum, risk size kalmış, bu testnete katılıp katılmamak tamamen kişisel fikrinizdir
* Testnet bitince KYC olacakmış.
* Ödül dönemi kilit detayları var [makale](https://medium.com/q-blockchain/q-blockchain-validator-onboarding-program-part-1-validator-incentivized-testnet-567ef6e4002e) Katılmanın ne kadar mantıklı olduğunu siz seçin.
* Hem vakit hemde malum hastalıklardan ötürü rehber kısa ve öz hazırlandı (rehber 4 kez test edildi)
* Bu vakit darlığından ve hastalığımdan ötürü rehberin paylaşıldığı ilk gün grupta aktif olamayacağım.
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

## Peer ekleme ( eşleşemıyorsanız bir türlü olmadıysa son çare )
```
screen -a -r q
```
```
cd testnet-public-tools/testnet-validator/
```
```
docker-compose exec testnet-validator-node geth attach /data/geth.ipc
```
```
admin.addPeer('enode://e974d9354ababd356a6bfecbb03a59d14ab715ffa02d431c6accfc5de250e9c8c345817bd5687c119a04df78f1a4673e97877ea5775fa84270d311dac4a2eca7@128.199.213.70:30313')
admin.addPeer('enode://e974d9354ababd356a6bfecbb03a59d14ab715ffa02d431c6accfc5de250e9c8c345817bd5687c119a04df78f1a4673e97877ea5775fa84270d311dac4a2eca7@128.199.213.70:30313')
admin.addPeer('enode://b1d45b83e8ca1e1bb7ec71a59d3f02d67ab56175e068042e41c446f6445c8b0c677d0b34a454c1214081ea047a812156e55c35779c2c3528db84c91fde5688e5@149.102.137.123:30313')
admin.addPeer('enode://e5bdbfd84f6462a01fcc877953f8ef931dd1f58ea1acf77993f0004d09c64fea3064410c7f0ec3eb7ab3c1ff091330d63dae80ced1dd3beab324a68a29072291@3.125.235.53:30305')
admin.addPeer('enode://e5bdbfd84f6462a01fcc877953f8ef931dd1f58ea1acf77993f0004d09c64fea3064410c7f0ec3eb7ab3c1ff091330d63dae80ced1dd3beab324a68a29072291@3.125.235.53:30315')
admin.addPeer('enode://d176da7ae3104a95c5e99d427441df0ebc123dba2d54ead39edd13a43f55b8ff023759535e68e062c75b7e95126abe992c6e1e35ddc398b2412cad915f2106b0@3.71.94.49:30303')
admin.addPeer('enode://d176da7ae3104a95c5e99d427441df0ebc123dba2d54ead39edd13a43f55b8ff023759535e68e062c75b7e95126abe992c6e1e35ddc398b2412cad915f2106b0@3.71.94.49:30313')
admin.addPeer('enode://1d43093b84ebf356a96886e869ac58c15eeb88c28dbdad0a54a045309267ac4d3f753369fccc3b5e70e2d02b7ea7b8c4998e3b5995003e0548aee6007b9c339a@18.194.123.154:30304')
admin.addPeer('enode://1d43093b84ebf356a96886e869ac58c15eeb88c28dbdad0a54a045309267ac4d3f753369fccc3b5e70e2d02b7ea7b8c4998e3b5995003e0548aee6007b9c339a@18.194.123.154:30314')
admin.addPeer('enode://85d6f24920a0f552a5e0360366d18fb1234880c4370f257abc09e8ec762173fb3c4b1b14a7af9a23a8c31751b3ba2905d6a98fb436dfe3092644527a89046977@3.68.108.12:30303')
admin.addPeer('enode://ec40af9079c53e880f7e783ae5053b18d1f8bb8cd55b2dfbbfa3b7e1f5256c724ef7e22f23f785c2f119fbb7930769540e3c01c711c6ae26c83690b941a4886c@85.215.92.83:30303')
admin.addPeer('enode://e974d9354ababd356a6bfecbb03a59d14ab715ffa02d431c6accfc5de250e9c8c345817bd5687c119a04df78f1a4673e97877ea5775fa84270d311dac4a2eca7@128.199.213.70:30313')
admin.addPeer('enode://aa72b8309fc09728e9516c92c4a37944a29267cbc45a6e9fac807bb020808f8d61abaf86a510aa28fa7bc288f0ef1613a6785e74963203d6aeef01aaef1bfec1@5.75.140.251:30313')
admin.addPeer('enode://9efb0f552e9d9217843f5d143bb32dbd8cf7bf4073e601dce20510fc9a4a1e728fcd8658078db19f79ccef14cd45f54743d90fa1e64a2365fc5d83d307457018@65.108.74.190:61439')
admin.addPeer('enode://c610793186e4f719c1ace0983459c6ec7984d676e4a323681a1cbc8a67f506d1eccc4e164e53c2929019ed0e5cfc1bc800662d6fb47c36e978ab94c417031ac8@79.125.97.227:53820')
admin.addPeer('enode://5510070fd564e8930705f1a79a7d290efbc9d18743de9fb27872acdcd0775d1a65cad4851e7855ec455cfb48e2f0caa48a6d300d540dd08f42b462615c12e661@159.223.22.223:58658')
admin.addPeer('enode://a3862c64d5d7e43f8cffce810d4ad00d20c2b34524df20be5c3e9a91f157a7ca532068e358e690453e3f339d5bdeab6a922d7a2a6243d4c89d4b64304360de1e@18.158.211.67:30303')
admin.addPeer('enode://9960a6b7fcc6bb46f89575906d8ef68d7b3f924c9f9a206afd8e9576936f9f6176656296f530f19ca4a61e723a1515966fd6baa2391e7555a46855ac94059bd1@80.158.48.29:4452')
admin.addPeer('enode://81cdc63a97e7e687aa8aa28b3d4c5b72f94ddb856956e01ea5943f960a12fa0ea536a3366cefa7a522377ded79b243e9accc65d7f159762bc6971aa317850c5b@18.202.219.33:30303')
admin.addPeer('enode://7a8ade64b79961a7752daedc4104ca4b79f1a67a10ea5c9721e7115d820dbe7599fe9e03c9c315081ccf6a2afb0b6652ee4965e38f066fe5bf129abd6d26df58@79.125.97.227:49128')
admin.addPeer('enode://8eff01a7e5a66c5630cbd22149e069bbf8a8a22370cef61b232179e21ba8c7b74d40e8ee5aa62c54d145f7fc671b851e5ccbfe124fce75944cf1b06e29c55c80@79.125.97.227:54000')
admin.addPeer('enode://9127cf39043562e0600b8baa7e192fd92bdb3bff573288312aa7e0336c79a4000844e8e8580e8efd64fbd99ade341bae1ea21835e4d1a777e579304b66b5acaf@185.170.115.95:30313')
admin.addPeer('enode://37793ae0218500896ad2fb0a2aff634e29198b9729f5a83d52963b941f8f0af938a72cb4b5d48cb201a2c63e7903f1d35ea8827a38d4f7f7dc5b4100e8645f50@35.156.94.184:52350')
admin.addPeer('enode://26ba8d1e2990c9c2b1c267dee1b3b292086d6d82c064a0d4d43266b5caa35d55a7dc96b92f550938158f47a35eeba90415f1fa2312670f3fdf7636110038acdb@34.125.78.43:30313')
admin.addPeer('enode://8eff01a7e5a66c5630cbd22149e069bbf8a8a22370cef61b232179e21ba8c7b74d40e8ee5aa62c54d145f7fc671b851e5ccbfe124fce75944cf1b06e29c55c80@79.125.97.227:54000')
admin.addPeer('enode://9127cf39043562e0600b8baa7e192fd92bdb3bff573288312aa7e0336c79a4000844e8e8580e8efd64fbd99ade341bae1ea21835e4d1a777e579304b66b5acaf@185.170.115.95:30313')
admin.addPeer('enode://37793ae0218500896ad2fb0a2aff634e29198b9729f5a83d52963b941f8f0af938a72cb4b5d48cb201a2c63e7903f1d35ea8827a38d4f7f7dc5b4100e8645f50@35.156.94.184:52350')
admin.addPeer('enode://9963c9a837719cd8c802b14eb510f060994f5d4f1bf36796ab6287f0a3886fcccb6c74cb90f7a63ff982d0c6adca112706632c17cdc8660f6089f9bf5300f5a9@80.158.48.29:61275')
admin.addPeer('enode://3b352d3349bfb0d1fac0fd703d0cc2e397fe9910d6a5fbe5077ff1ec46c50b261704d28de5e29c768e425b99f8acff605d00a0cf602425fac2a36a1505a26efb@36.69.120.50:53434')
admin.addPeer('enode://08cf0b8ce2194c327937a22b9706ce9dc8b061371a9744f5d5f0cdd5694f6e239f45bec218b9e9490f96253ccc921b5ee568c86558a2b56802ef4be3f6c9dc29@80.158.48.29:61278')
admin.addPeer('enode://e5bdbfd84f6462a01fcc877953f8ef931dd1f58ea1acf77993f0004d09c64fea3064410c7f0ec3eb7ab3c1ff091330d63dae80ced1dd3beab324a68a29072291@3.125.235.53:56056')
admin.addPeer('enode://d176da7ae3104a95c5e99d427441df0ebc123dba2d54ead39edd13a43f55b8ff023759535e68e062c75b7e95126abe992c6e1e35ddc398b2412cad915f2106b0@3.71.94.49:55678')
admin.addPeer('enode://1baa3388ce4a021a275d531b20e9b3de406fb7bd1ad36e1bb62443a0f826b0c9dd31535b94e0038f7fbc0018b596f270ea49d96b50c6537c6a51cf46df81df4e@38.242.158.186:30313')
admin.addPeer('enode://ba55bd0a6ced3874fd29b8614322022e97bf0c85b68886a794ca505b82370584f398ce589430b4e3ace1028c42592cebda83adeb9af0452fae7d04946c4f5821@185.170.115.95:30314')
admin.addPeer('enode://a1ea9b6606ed7087dfa2d4b166c7fee9a9a73da0a1d53aed5db7ab90f5c288ad3700a6d192994468493dfdadd691b19fdc479354d6d5aae0636016de5d9ae1a1@103.41.204.234:42672')
admin.addPeer('enode://13c71856486f1ec9374fd5382ec0e3c54312e902930f5d68105b81a099a70bdac1d26616c3e94a696cc531fe592aff4422901a945e770c39a09f889a91683eb4@116.203.236.62:30313')
admin.addPeer('enode://4493f390d9670a4c309a6a528865666a2949126a96a3ded5d2f2ce8a8d952b6c1c7e3cbcff4deb265f64246f23eb2e6668ad0c4e7abf1a38fb2a3b4e2382390a@85.215.92.83:39546')
admin.addPeer('enode://be98d563773d207ccf0fcd2658ce35f6ab75fc74b182d4f5679e53218e9955a6ae85d257d32c27dad77acee7c50a612c9ede0c396c256ab0a4661d39a31d0684@65.108.74.188:4838')
admin.addPeer('enode://a092ed0aa0c015414a6c68673d822f99eb5a02d5d9d8ada4f88f9361b61082bddb5f1506c2da0b7606bfbbe2f6ffed6982f94397e0c6cf19f3fca34124bcd00d@65.108.200.247:30399')
admin.addPeer('enode://ebb67ca8e6c042b48843486570dba7959704738e66930b322f96b9333792377e68ec992b29f3ce17116dec9ef3d0e7b5f00b1e1938374de298440c60f27cecc5@152.44.36.189:30303')
admin.addPeer('enode://7e5f6b7cf3e41d494b915c93029a8c6c057e414c153816b6090c07bb966ab4dbba4dae4d572dd2dffa98b080717dbec8a758146ffe19096589fbe6a0ce0586c1@157.90.36.57:55226')
admin.addPeer('enode://1d43093b84ebf356a96886e869ac58c15eeb88c28dbdad0a54a045309267ac4d3f753369fccc3b5e70e2d02b7ea7b8c4998e3b5995003e0548aee6007b9c339a@18.194.123.154:59508')
admin.addPeer('enode://81eeadb960551cbd0d13126543f5fb02bd67e943fae795a5f33ab5aecf60211a6fd065336496ffe224c83d40086b5ba8750c582e1f1f12fac7f3dd992ecafee8@65.108.74.180:56681')
admin.addPeer('enode://fd8e7d940530b528ee03f9a4b01d58a09f348c9bd9f14d42cfae76ad75917fc69af616b19815f53c7d9f4b6adf583734c09e4a1b8620569b75636d20e29a490e@16.162.25.16:30313')
admin.addPeer('enode://c7f5d4836146e88d8db3593e751ea6489830beb05835942ace6a377d95943220ae34e3c664ba5c8ee22c52b840fd82d397165e298ad74076aeddae8e09160892@161.97.69.121:30313')
admin.addPeer('enode://e8fff0b380227fadebb4cfca963023e311c6077b250f889bf703464b1cce1e236fd2e0176423c1c7e67b75584ad3098f6d72bf97a77ae65f41181353d3c97ddd@46.38.240.229:30313')
admin.addPeer('enode://58503f042a510ea5cbb8dbc6154639f4f1aa1aa30843549e0b0d92b28a9eb4c1bb2aa8eb29f98e4cd55f947ea42f6e7ebeba1671495f33435e994659526b56de@159.65.155.162:30313')
admin.addPeer('enode://8eff01a7e5a66c5630cbd22149e069bbf8a8a22370cef61b232179e21ba8c7b74d40e8ee5aa62c54d145f7fc671b851e5ccbfe124fce75944cf1b06e29c55c80@79.125.97.227:54000')
admin.addPeer('enode://9127cf39043562e0600b8baa7e192fd92bdb3bff573288312aa7e0336c79a4000844e8e8580e8efd64fbd99ade341bae1ea21835e4d1a777e579304b66b5acaf@185.170.115.95:30313')
admin.addPeer('enode://37793ae0218500896ad2fb0a2aff634e29198b9729f5a83d52963b941f8f0af938a72cb4b5d48cb201a2c63e7903f1d35ea8827a38d4f7f7dc5b4100e8645f50@35.156.94.184:52350')
admin.addPeer('enode://9963c9a837719cd8c802b14eb510f060994f5d4f1bf36796ab6287f0a3886fcccb6c74cb90f7a63ff982d0c6adca112706632c17cdc8660f6089f9bf5300f5a9@80.158.48.29:61275')
admin.addPeer('enode://a3706f4d11303863efdbf0bb4c72db279cd00b97ea52ccae0de1fbff7091c04ad56e4c8324663bf7fb73bb8267cfab3c014c1529bce58fed1f8e264081a5f996@74.208.49.41:30313')
admin.addPeer('enode://650604f674865abc49297f63678e7fee2ec0de5b513c67a212cb24493eab7ac055a6ab3d2a51b988be93c54801b1aeb05d5ffd50903e7f742908cb5abeee0d03@38.242.229.50:30313')
admin.addPeer('enode://58623247cdc169181e918156e77cd843fdcd32526db9041b7ac0c5b2723787ad4a6c1802e9f130073e7389d39adb4d91a7f4f1249dd6ff66f9eab9bac9d43f90@65.108.124.57:50303')
admin.addPeer('enode://26ba8d1e2990c9c2b1c267dee1b3b292086d6d82c064a0d4d43266b5caa35d55a7dc96b92f550938158f47a35eeba90415f1fa2312670f3fdf7636110038acdb@34.125.78.43:30313')
admin.addPeer('enode://8eff01a7e5a66c5630cbd22149e069bbf8a8a22370cef61b232179e21ba8c7b74d40e8ee5aa62c54d145f7fc671b851e5ccbfe124fce75944cf1b06e29c55c80@79.125.97.227:54000')
admin.addPeer('enode://9127cf39043562e0600b8baa7e192fd92bdb3bff573288312aa7e0336c79a4000844e8e8580e8efd64fbd99ade341bae1ea21835e4d1a777e579304b66b5acaf@185.170.115.95:30313')
admin.addPeer('enode://37793ae0218500896ad2fb0a2aff634e29198b9729f5a83d52963b941f8f0af938a72cb4b5d48cb201a2c63e7903f1d35ea8827a38d4f7f7dc5b4100e8645f50@35.156.94.184:52350')
admin.addPeer('enode://9963c9a837719cd8c802b14eb510f060994f5d4f1bf36796ab6287f0a3886fcccb6c74cb90f7a63ff982d0c6adca112706632c17cdc8660f6089f9bf5300f5a9@80.158.48.29:61275')
admin.addPeer('enode://3b352d3349bfb0d1fac0fd703d0cc2e397fe9910d6a5fbe5077ff1ec46c50b261704d28de5e29c768e425b99f8acff605d00a0cf602425fac2a36a1505a26efb@36.69.120.50:53434')
admin.addPeer('enode://08cf0b8ce2194c327937a22b9706ce9dc8b061371a9744f5d5f0cdd5694f6e239f45bec218b9e9490f96253ccc921b5ee568c86558a2b56802ef4be3f6c9dc29@80.158.48.29:61278')
admin.addPeer('enode://e5bdbfd84f6462a01fcc877953f8ef931dd1f58ea1acf77993f0004d09c64fea3064410c7f0ec3eb7ab3c1ff091330d63dae80ced1dd3beab324a68a29072291@3.125.235.53:56056')
admin.addPeer('enode://d176da7ae3104a95c5e99d427441df0ebc123dba2d54ead39edd13a43f55b8ff023759535e68e062c75b7e95126abe992c6e1e35ddc398b2412cad915f2106b0@3.71.94.49:55678')
admin.addPeer('enode://1baa3388ce4a021a275d531b20e9b3de406fb7bd1ad36e1bb62443a0f826b0c9dd31535b94e0038f7fbc0018b596f270ea49d96b50c6537c6a51cf46df81df4e@38.242.158.186:30313')
admin.addPeer('enode://ba55bd0a6ced3874fd29b8614322022e97bf0c85b68886a794ca505b82370584f398ce589430b4e3ace1028c42592cebda83adeb9af0452fae7d04946c4f5821@185.170.115.95:30314')
admin.addPeer('enode://a1ea9b6606ed7087dfa2d4b166c7fee9a9a73da0a1d53aed5db7ab90f5c288ad3700a6d192994468493dfdadd691b19fdc479354d6d5aae0636016de5d9ae1a1@103.41.204.234:42672')
admin.addPeer('enode://13c71856486f1ec9374fd5382ec0e3c54312e902930f5d68105b81a099a70bdac1d26616c3e94a696cc531fe592aff4422901a945e770c39a09f889a91683eb4@116.203.236.62:30313')
admin.addPeer('enode://4493f390d9670a4c309a6a528865666a2949126a96a3ded5d2f2ce8a8d952b6c1c7e3cbcff4deb265f64246f23eb2e6668ad0c4e7abf1a38fb2a3b4e2382390a@85.215.92.83:39546')
admin.addPeer('enode://be98d563773d207ccf0fcd2658ce35f6ab75fc74b182d4f5679e53218e9955a6ae85d257d32c27dad77acee7c50a612c9ede0c396c256ab0a4661d39a31d0684@65.108.74.188:4838')
admin.addPeer('enode://a092ed0aa0c015414a6c68673d822f99eb5a02d5d9d8ada4f88f9361b61082bddb5f1506c2da0b7606bfbbe2f6ffed6982f94397e0c6cf19f3fca34124bcd00d@65.108.200.247:30399')
admin.addPeer('enode://ebb67ca8e6c042b48843486570dba7959704738e66930b322f96b9333792377e68ec992b29f3ce17116dec9ef3d0e7b5f00b1e1938374de298440c60f27cecc5@152.44.36.189:30303')
admin.addPeer('enode://7e5f6b7cf3e41d494b915c93029a8c6c057e414c153816b6090c07bb966ab4dbba4dae4d572dd2dffa98b080717dbec8a758146ffe19096589fbe6a0ce0586c1@157.90.36.57:55226')
admin.addPeer('enode://1d43093b84ebf356a96886e869ac58c15eeb88c28dbdad0a54a045309267ac4d3f753369fccc3b5e70e2d02b7ea7b8c4998e3b5995003e0548aee6007b9c339a@18.194.123.154:59508')
admin.addPeer('enode://81eeadb960551cbd0d13126543f5fb02bd67e943fae795a5f33ab5aecf60211a6fd065336496ffe224c83d40086b5ba8750c582e1f1f12fac7f3dd992ecafee8@65.108.74.180:56681')
admin.addPeer('enode://fd8e7d940530b528ee03f9a4b01d58a09f348c9bd9f14d42cfae76ad75917fc69af616b19815f53c7d9f4b6adf583734c09e4a1b8620569b75636d20e29a490e@16.162.25.16:30313')
admin.addPeer('enode://c7f5d4836146e88d8db3593e751ea6489830beb05835942ace6a377d95943220ae34e3c664ba5c8ee22c52b840fd82d397165e298ad74076aeddae8e09160892@161.97.69.121:30313')
admin.addPeer('enode://e8fff0b380227fadebb4cfca963023e311c6077b250f889bf703464b1cce1e236fd2e0176423c1c7e67b75584ad3098f6d72bf97a77ae65f41181353d3c97ddd@46.38.240.229:30313')
```

son olarak ( exit ) yazıp enterlıyoruz
```
docker-compose logs -f --tail "100" 
```
## eşleşmeye bir diğer çözüm peer sız deneme
```
cd testnet-public-tools/testnet-validator/
```
```
nano docker-compose.yaml
```
```
"--bootnodes=$BOOTNODE1_ADDR",
 ```
yukrıdaki kısmı siliyoruz ctrl x y enter la kaydediyoruz 

```
docker-compose logs -f --tail "100" 
```





## Hastalıklar cirit atıyor, dikkat edin kendinize!
