# Phase II

### Install Docker
Cek apakah sudah ada docker atau belum
```
docker version
```
Jika belum ada, install
```
sudo apt-get update && sudo apt install jq git && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin
```

### Install Rust
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

```
source "$HOME/.cargo/env"
```

### Install Wasm32
```
rustup target list --installed
rustup target add wasm32-unknown-unknown
```


### Clone
```
git clone https://github.com/CosmWasm/cosmwasm-examples
cd ~/cosmwasm-examples
git fetch
git checkout 44d6a256cd99e66849e550185c98671d4109d78b
cd contracts/erc20
```

### Compile
```
rustup default stable
cargo wasm 
```

- Next
```
sudo docker run --rm -v "$(pwd)":/code \
    --mount type=volume,source="$(basename "$(pwd)")_cache",target=/code/target \
    --mount type=volume,source=registry_cache,target=/usr/local/cargo/registry \
    cosmwasm/rust-optimizer:0.12.6
```
### Memulai deploy
```
cd artifacts
nibid tx wasm store cw_erc20.wasm  --from wallet --fees 100000unibi --gas auto --gas-adjustment 1.5 -b block -y
```

Output yang benar
<p align="left"><img height="auto" width="auto" src="https://github.com/Megumiiiiii/nibiru-fase-II/assets/98658943/00ee2f73-2dfe-4648-aaf1-f8bdffb66f6f"</p>

Copy dari `Code: 0` sampai `txhash: ` dan simpan di notepad
    
### Create Token
Copy `Code ID` dari output tadi, untuk membuat token
<p align="left"><img height="auto" width="auto" src="https://github.com/Megumiiiiii/nibiru-fase-II/assets/98658943/56c329e4-b99c-4631-ac3f-81cf4314ba72"</p>

Sesuikan `name` `symbol` `decimal`  `address_nibiru` `total_supply` `label` sesuka hati
    
```
nibid tx wasm instantiate CODE_ID_MU --admin Address_Nibiru  \
    '{"name":"Oben Coin","symbol":"OBEN","decimals":18,"initial_balances":[{"address":"Address_Nibiru","amount":"Total_Supply"}]}' \
    --amount 50000unibi  --label "Oben skem" --from wallet --fees 100000unibi --gas auto --gas-adjustment 1.5 -b block -y
````

Scroll output nya, akan ada `contract_address`
<p align="left"><img height="auto" width="auto" src="https://github.com/Megumiiiiii/nibiru-fase-II/assets/98658943/3cf6dd47-db70-403a-874b-e37ee2f7736b"</p>

### Cek Contract
```
 nibid query wasm contract Contract_AddressMu
```
<p align="left"><img height="auto" width="auto" src="https://github.com/Megumiiiiii/nibiru-fase-II/assets/98658943/c3ec7586-f5bd-435f-9f02-a9cd052166c2"</p>

    
    
### Cek Balance
```
nibid query wasm contract-state smart Contract_Address '{"balance":{"address":"Address_Nibiru"}}'
```
<p align="left"><img height="auto" width="auto" src="https://github.com/Megumiiiiii/nibiru-fase-II/assets/98658943/64d7a30c-43e5-4385-8d23-4893d2b347d1"</p>

    
    
### Test Send
```
nibid tx wasm execute Contract_Address '{"transfer":{"amount":"200","owner":"Address_Nibiru","recipient":"Address_Nibiru_Penerima"}}' --from wallet --gas auto --gas-adjustment 1.5 --fees 10000unibi -y
```
 
#

<div id="header" align="center">
  <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExMzNmZTIxZmE3ZmY3MzRiMDcwNDJhYTQ5ZmNlY2YxMWE1OWIyYmVkNSZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/mVBlqOD4ra9jQiI3cC/giphy.gif" height="125" width="420"/>
</div>
