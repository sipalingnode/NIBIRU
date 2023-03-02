<p style="font-size:14px" align="right">
<a href="https://t.me/autosultan_group" target="_blank">Join our telegram <img src="https://user-images.githubusercontent.com/50621007/183283867-56b4d69f-bc6e-4939-b00a-72aa019d1aea.png" width="30"/></a>
</p>
<p align="center">
  <img height="300" height="auto" src="https://user-images.githubusercontent.com/109174478/209359981-dc19b4bf-854d-4a2a-b803-2547a7fa43f2.jpg">
</p>

# Nibiru Task 3 Oracle

## Install binary
```
curl -s https://get.nibiru.fi/pricefeeder! | bash
```
## Import Wallet
```
nibid keys add pricefeeder-wallet --recover
```
## Export Wallet
```
export FEEDER_MNEMONIC="isi_pharse_walletlu"
```
## Install Service
```
export CHAIN_ID="nibiru-itn-1"
export GRPC_ENDPOINT="localhost:39090"
export WEBSOCKET_ENDPOINT="ws://localhost:39657/websocket"
export EXCHANGE_SYMBOLS_MAP='{ "bitfinex": { "ubtc:uusd": "tBTCUSD", "ueth:uusd": "tETHUSD", "uusdt:uusd": "tUSTUSD" }, "binance": { "ubtc:uusd": "BTCUSD", "ueth:uusd": "ETHUSD", "uusdt:uusd": "USDTUSD", "uusdc:uusd": "USDCUSD", "uatom:uusd": "ATOMUSD", "ubnb:uusd": "BNBUSD", "uavax:uusd": "AVAXUSD", "usol:uusd": "SOLUSD", "uada:uusd": "ADAUSD", "ubtc:unusd": "BTCUSD", "ueth:unusd": "ETHUSD", "uusdt:unusd": "USDTUSD", "uusdc:unusd": "USDCUSD", "uatom:unusd": "ATOMUSD", "ubnb:unusd": "BNBUSD", "uavax:unusd": "AVAXUSD", "usol:unusd": "SOLUSD", "uada:unusd": "ADAUSD" } }'
export VALIDATOR_ADDRESS=$(nibid keys show wallet --bech val -a)

sudo tee /etc/systemd/system/pricefeeder.service<<EOF
[Unit]
Description=Nibiru Pricefeeder
Requires=network-online.target
After=network-online.target

[Service]
Type=exec
User=$USER
Group=$USER
ExecStart=/usr/local/bin/pricefeeder
Restart=on-failure
ExecReload=/bin/kill -HUP $MAINPID
KillSignal=SIGTERM
PermissionsStartOnly=true
LimitNOFILE=65535
Environment=CHAIN_ID='$CHAIN_ID'
Environment=GRPC_ENDPOINT='$GRPC_ENDPOINT'
Environment=WEBSOCKET_ENDPOINT='$WEBSOCKET_ENDPOINT'
Environment=EXCHANGE_SYMBOLS_MAP='$EXCHANGE_SYMBOLS_MAP'
Environment=FEEDER_MNEMONIC='$FEEDER_MNEMONIC'
Environment=VALIDATOR_ADDRESS='$VALIDATOR_ADDRESS'

[Install]
WantedBy=multi-user.target
EOF
```
## Restart Service
```
sudo systemctl daemon-reload && \
sudo systemctl enable pricefeeder && \
sudo systemctl start pricefeeder
```
## Cek Log
```
journalctl -fu pricefeeder
```
**Kalo Sukses Output akan seperti dibawah ini**
```
Feb 27 19:09:33 pricefeeder[3632198]: {"level":"info","voting-period-height":405780,"tx-hash":"8FC418510A2BBFEF6E2FF17108B5D1C909B14DC0AFB22129A73C7373E649329F","time":1677521373,"message":"successfully forwarded prices"}
Feb 27 19:09:48 pricefeeder[3632198]: {"level":"info","voting-period":{"Height":405790},"time":1677521388,"message":"new voting period"}
Feb 27 19:09:48 pricefeeder[3632198]: {"level":"info","voting-period-height":405790,"vote":{"salt":"337","exchange_rates":"(unibi:unusd,0.066667000000000000)|(ubtc:unusd,23296.630000000000000000)|(ueth:unusd,1628.900000000000000000)|(uatom:unusd,12.760000000000000000)|(ubnb:unusd,301.740800000000000000)|(uusdc:unusd,0.999900000000000000)|(uusdt:unusd,1.000100000000000000)|(unibi:uusd,0.066667000000000000)|(ubtc:uusd,23314.000000000000000000)|(ueth:uusd,1629.900000000000000000)|(uatom:uusd,12.760000000000000000)|(ubnb:uusd,301.740800000000000000)|(uusdc:uusd,0.999900000000000000)|(uusdt:uusd,1.000100000000000000)","feeder":"nibi1w9d0u9ln9tx9dnn5qku9977jn2rtrupxxx0lrn","validator":"nibivaloper195w5wxp8hgqgz7schdukq7u5kadc2tnrsc00a0"},"time":1677521388,"message":"prepared vote message"}
Feb 27 19:09:50 pricefeeder[3632198]: {"level":"info","voting-period-height":405790,"tx-hash":"ACB94C8421AE056468BDAAE68655D86CEB87FB6881A526A31A7A2E98234C8D13","time":1677521390,"message":"successfully forwarded prices"}
Feb 27 19:10:05 pricefeeder[3632198]: {"level":"info","voting-period":{"Height":405800},"time":1677521405,"message":"new voting period"}
Feb 27 19:10:05 pricefeeder[3632198]: {"level":"info","voting-period-height":405800,"vote":{"salt":"3334","exchange_rates":"(unibi:unusd,0.066667000000000000)|(ubtc:unusd,23296.680000000000000000)|(ueth:unusd,1628.780000000000000000)|(uatom:unusd,12.760000000000000000)|(ubnb:unusd,301.740800000000000000)|(uusdc:unusd,0.999900000000000000)|(uusdt:unusd,1.000100000000000000)|(unibi:uusd,0.066667000000000000)|(ubtc:uusd,23296.680000000000000000)|(ueth:uusd,1628.780000000000000000)|(uatom:uusd,12.760000000000000000)|(ubnb:uusd,301.740800000000000000)|(uusdc:uusd,0.999900000000000000)|(uusdt:uusd,1.000100000000000000)","feeder":"nibi1w9d0u9ln9tx9dnn5qku9977jn2rtrupxxx0lrn","validator":"nibivaloper195w5wxp8hgqgz7schdukq7u5kadc2tnrsc00a0"},"time":1677521405,"message":"prepared vote message"}
Feb 27 19:10:06 pricefeeder[3632198]: {"level":"info","voting-period-height":405800,"tx-hash":"1E85AD6307DD8D734AAB6565CC57FB09F0EA0F7CFE0B8EE8AB50FC8A08B4111A","time":1677521406,"message":"successfully forwarded prices"}
Feb 27 19:10:22 pricefeeder[3632198]: {"level":"info","voting-period":{"Height":405810},"time":1677521422,"message":"new voting period"}
Feb 27 19:10:22 pricefeeder[3632198]: {"level":"info","voting-period-height":405810,"vote":{"salt":"9672","exchange_rates":"(unibi:unusd,0.066667000000000000)|(ubtc:unusd,23310.000000000000000000)|(ueth:unusd,1630.010000000000000000)|(uatom:unusd,12.760000000000000000)|(ubnb:unusd,301.737500000000000000)|(uusdc:unusd,0.999900000000000000)|(uusdt:unusd,1.000000000000000000)|(unibi:uusd,0.066667000000000000)|(ubtc:uusd,23307.000000000000000000)|(ueth:uusd,1629.200000000000000000)|(uatom:uusd,12.760000000000000000)|(ubnb:uusd,301.737500000000000000)|(uusdc:uusd,0.999900000000000000)|(uusdt:uusd,1.000000000000000000)","feeder":"nibi1w9d0u9ln9tx9dnn5qku9977jn2rtrupxxx0lrn","validator":"nibivaloper195w5wxp8hgqgz7schdukq7u5kadc2tnrsc00a0"},"time":1677521422,"message":"prepared vote message"}
Feb 27 19:10:23 pricefeeder[3632198]: {"level":"info","voting-period-height":405810,"tx-hash":"24B3B16FB8B6B047885928FB6A254D7B0B44E17E0DC6AF37B1F077F78C7099A9","time":1677521423,"message":"successfully forwarded prices"}
```

**Atau kalian  bisa cek di explorer :** https://explorer.kjnodes.com/nibiru-testnet
