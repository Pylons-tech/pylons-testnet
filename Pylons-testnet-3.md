# pylons-testnet-3 Testnet

- Go version: [v1.17+](https://golang.org/dl/)
- Pylonsd version: [v0.4.2](https://github.com/Pylons-tech/pylons/releases/tag/v0.4.2)

         ensure GOPATH is set properly to point to the go directory of your Go installation: GOPATH = $HOME/go
         ensure PATH is set properly to point to the bin folder of your Go installation: PATH = $GOPATH/bin
         pylonsd binary(link above or from 'make install' on repo clone/source) should be put in Go's bin folder

## Testnet Restart - Pylons Testnet 3

1. Get the proper version (v0.4.2) and `make install` the pylonsd binary
   ```bash
   git clone https://github.com/Pylons-tech/pylons
   git checkout <latest-version>
   make install
   ``` 
2. Run pylonsd version to verify the version is correct (0.4.2).  please reach out if the version is wrong.

   ```bash
   pylonsd version
   ``` 

3. Run pylonsd unsafe-reset-all, remove genesis and pylonsd init

   ```bash
   pylonsd unsafe-reset-all
   rm -r $HOME/.pylons/config/genesis.json
   pylonsd init --chain-id=pylons-testnet-3
   ```

4. Download the correct genesis.json file (  and copy the file to ~/.pylons/config/genesis.json

   ```bash
   wget https://raw.githubusercontent.com/Pylons-tech/pylons-testnet/main/genesis.json -O ~/.pylons/config/genesis.json
   ```
   Also you can use the below command to download the genesis:
   ```bash
   curl http://95.214.55.4:26657/genesis | jq .result.genesis > genesis.json 
   ```
   
5. Run pylonsd validate-genesis .  Please reach out if there are issues

   ```bash
   pylonsd validate-genesis

   ```
   
6. Add peers to your config.json file then post your peer to the validator chat, and clear any old seeds in the config file.

   ```bash
   PEERS="25e7ef64b41a636e3fb4e9bb1191b785e7d1d5cc@46.166.140.172:26656,2c50b8171af784f1dca3d37d5dda5e90f1e1add8@95.214.55.4:26656,4f90babf520599ffe606157b0151c4c9bc0ec23f@194.163.172.115:26666,ebecc93e7865036fbdf8d3d54a624941d6e41ba1@104.200.136.57:26656,022ee5a5231a5dec014841394f8ce766d657cff5@95.214.53.132:26156,a6972be573807d34f28a337c0f7d599e0014be80@161.97.99.247:26656,515ffd755a92a47b56233143f7c25481dbe99f94@161.97.99.251:26606"

   sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.pylons/config/config.toml
   ```

7. Run pylonsd with systemd

   ```bash
   sudo tee /etc/systemd/system/pylonsd.service > /dev/null <<EOF  
   [Unit]
   Description=Pylons Daemon
   After=network-online.target

   [Service]
   User=$USER
   ExecStart=$(which pylonsd) start
   Restart=always
   RestartSec=3
   LimitNOFILE=infinity

   [Install]
   WantedBy=multi-user.target
   EOF
   sudo -S systemctl daemon-reload
   sudo -S systemctl enable pylonsd
   sudo -S systemctl restart pylonsd

   ```

8. Check the balance of your pyloxxxxx address. Please reach out to be funded from the faucet if you do not have funds (1,000,000ubedrock). Paste your pyloxxxxx address on the validator chat and request funds if you do not have. Beware to not get jailed because bedrock tokens from the faucet given to unjail you will be deducted from your incentivized bedrock tokens.

   ```bash
   pylonsd query bank balances <delegator-addresss>

   ```
   
9. Create your validator.

   ```bash
   pylonsd tx staking create-validator \
     --amount=1000000ubedrock \
     --pubkey=$(pylonsd tendermint show-validator) \
     --moniker=<moniker> \
     --chain-id=pylons-testnet-3 \
     --commission-rate="0.10" \
     --commission-max-rate="0.20" \
     --commission-max-change-rate="0.01" \
     --min-self-delegation="1000000" \
     --gas="auto" \
     --gas-adjustment="1.5" \
     --from=<key-name>

   ```
10. Self-delegate 1000000ubedrock 

   ```bash
   pylonsd tx staking delegate pylovaloperxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx 1000000ubedrock --from=<key-name> --broadcast-mode=async --chain-id=pylons-testnet-3 -y
   ```
 
