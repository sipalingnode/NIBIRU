<p style="font-size:14px" align="right">
<a href="https://t.me/autosultan_group" target="_blank">Join our telegram <img src="https://user-images.githubusercontent.com/50621007/183283867-56b4d69f-bc6e-4939-b00a-72aa019d1aea.png" width="30"/></a>
</p>
<p align="center">
  <img height="300" height="auto" src="https://user-images.githubusercontent.com/109174478/209359981-dc19b4bf-854d-4a2a-b803-2547a7fa43f2.jpg">
</p>

# TUTORIAL NIBIRU NODE
## Install Node
```
wget -O nibiru.sh https://raw.githubusercontent.com/sipalingnode/nibiru/main/nibiru.sh; chmod +x nibiru.sh; ./nibiru.sh
```
Snapshot From KJ89
```
sudo systemctl stop nibid
cp $HOME/.nibid/data/priv_validator_state.json $HOME/.nibid/priv_validator_state.json.backup
rm -rf $HOME/.nibid/data
```
```
curl -L https://snapshots.kjnodes.com/nibiru-testnet/snapshot_latest.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.nibid
mv $HOME/.nibid/priv_validator_state.json.backup $HOME/.nibid/data/priv_validator_state.json
```
```
sudo systemctl restart nibid && sudo journalctl -u nibid -f --no-hostname -o cat
```
## Import Wallet (Gunakan address yang udah submit di gleam)
```
nibid keys add wallet --recover
```
**Kemudian masukan pharse wallet kalian**

## Cek Status Node
```
nibid status 2>&1 | jq .SyncInfo
```
**Jika sudah FALSE boleh lanjut create validator. Jika masih TRUE tunggu sampe FALSE**

## Create Validator
```
nibid tx staking create-validator \
--amount 1000000unibi \
--pubkey $(nibid tendermint show-validator) \
--moniker "YOUR_MONIKER_NAME" \
--details "YOUR_DETAILS" \
--website "YOUR_WEBSITE_URL" \
--chain-id nibiru-itn-1 \
--commission-rate 0.05 \
--commission-max-rate 0.20 \
--commission-max-change-rate 0.01 \
--min-self-delegation 1 \
--from wallet \
--gas-adjustment 1.4 \
--gas auto \
--gas-prices 0.025unibi \
-y
```
|  kata kata |  Yang harus di edit |
| ------------ | ------------ |
| YOUR_MONIKER_NAME  | Nama Validator Lu  |
| YOUR_DETAILS | Deskripsi Node Bebas |
| YOUR_WEBSITE_URL  | Isi aja pake link twitter lu |

Done. Cek Explorer : https://explorer.kjnodes.com/nibiru-testnet
