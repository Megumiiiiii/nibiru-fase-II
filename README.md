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

