### Install docker
```
apt update && apt list --upgradable && apt upgrade -y
```
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```
```
apt-cache policy docker-ce
```
```
sudo apt install docker-ce
```

### Install node
```
docker login -u public -p glpat-XvZ6bPe48rFGZ5z14Fxz registry.waterfall.network
```
```
docker pull registry.waterfall.network/waterfall/protocol/docker:2-rc1
```
### run node
```
docker run --platform linux/amd64 --name wf -d --rm -p 4000:4000 -p 13000:13000 -p 12000:12000/udp -p 30303:30303 -p 9545:9545 -p 9546:9546 -v $PWD/.wf/logs:/opt/wf/data/logs -v $PWD/.wf/gwat:/opt/wf/data/gwat -v $PWD/.wf/coordinator:/opt/wf/data/coordinator registry.waterfall.network/waterfall/protocol/docker:2-rc1
```
note : ` akan generate file ./wf & anda bisa costum port disini `
### status node
```
docker exec -it wf /opt/wf/sh/status.sh
```
note : `tunggu hingga ada keterangan synced membutuhkan waktu seharian`
### menjadi validator
[klik ini untuk request faucet](https://faucet.rc1.waterfall.network/)

Tambahkan network secara manual di metamask 
* Network Name: `Waterfall RC1 Network`
* RPC URL: `https://rpc.rc1.waterfall.network/`
* Chain ID: `8601151`
* Currency symbol: `WATER`
* Block Explorer URL: `https://explorer.rc1.waterfall.network`

note : `pergi ke menu pengaturan-advanced di metamask dan centang menu SHOW-HEX`
* membuat worker
```
docker exec -it wf /opt/wf/sh/add.sh (wallet address)
```
* deposit worker
note :` anda bisa membuat banyak worker`
```
docker exec -it wf /opt/wf/sh/deposit.sh 0
```
akan ada output seperti ini

`
  To: 0x0cEF9cA60360F957b65ecE8B1CB716718229277f`
  
  `
  Value: 3200 WATER`

  `
  Data: 0xf401af0558f9814d8ff52b15904bc76fcde0d4b694e5f01b5ffeab025bab6edc168422a1164d45cf4a9d58653ff3be4d4866072cb086a41ad80e13946aa8767cd9077e60115a072cb086a41ad80e13946aa8767cd9077e60115a86b45006fffc948a0f00aa32346c2e34bfc0e17355bac46a112fe1df3d3d30b2b2aff5fe39e0a1ba7e4791c062015da00baa85b394ab485d815ea7036694fbe5e73d4008ff68fc5afb219c62f778d94a1e5e7eda2b6db32c76dc9d7833c8378d
`
pergi ke metamask kirim ke address tersebut
