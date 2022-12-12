
# Otomatik PEER eklemek
```
cd testnet-public-tools/testnet-validator/
```
```
nano docker-compose.yaml
```
## Aşağıdaki bayrağı ekliyoruz. virgül ve boşluk bırakma kısmına dikkat etmeniz gerekli. Ctrl + x, y enter la kaydediyoruz 
```
"--bootnodes=$BOOTNODE1_ADDR,$BOOTNODE2_ADDR,$BOOTNODE3_ADDR",
 ```
 ![image](https://user-images.githubusercontent.com/99053148/207040355-afe41459-49dc-4b8a-8695-ec8b5811a022.png)

## Node'u kontrol ediyoruz

```
docker-compose logs -f --tail "100" 
```
