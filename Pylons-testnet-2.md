# pylons-testnet-2

- Go version: [v1.17+](https://golang.org/dl/)
- Pylonsd version: [v0.4.0](https://github.com/Pylons-tech/pylons/releases/tag/v0.4.0)

         ensure GOPATH is set properly to point to the go directory of your Go installation: GOPATH = $HOME/go
         ensure PATH is set properly to point to the bin folder of your Go installation: PATH = $GOPATH/bin
         pylonsd binary(link above or from 'make install' on repo clone/source) should be put in Go's bin folder

## Testnet Restart

1. Get the proper version (v0.4.0) and `make install` the pylonsd binary
 ```shell
    git clone https://github.com/Pylons-tech/pylons
    git checkout <latest-version>
    make install
 ``` 
2. Run pylonsd version to verify the version is correct.  please reach out if the version is wrong.

   ```shell
   $ pylonsd version
   ``` 

3. Run pylonsd unsafe-reset-all, remove genesis and pylonsd init

   ```shell
   $ pylonsd unsafe-reset-all
   $ rm -r $HOME/.pylons/config/genesis.json
   $ pylonsd init --chain-id=pylons-testnet-2
   ```

4. Download the correct genesis.json file (  and copy the file to ~/.pylons/config/genesis.json

   ```shell
     https://github.com/Pylons-tech/pylons-testnet/blob/main/genesis.json
   ```
   you can use the below command to download the genesis:
 ```shell
         wget https://raw.githubusercontent.com/Pylons-tech/pylons-testnet/main/genesis.json?token=<git-token>
 ```
5. Run pylonsd validate-genesis .  Please reach out if there are issues

   ```shell
    $ pylonsd validate-genesis

   ```
   
6. Add the Peers in `~/.pylons/config/config.toml and post your peer to the validator chat, and clear any old seeds in the config file.

   ```shell
    Peers: 
        ae3c6f9285b613cadfa43326a38188029b6c81d4@161.97.78.75:26656
        e7754fa37be29b52eed809488460110f34e677a2@185.211.6.100:26656
        28d06fd011f0d84953f11170d2b2a859e7b0fbcc@194.163.154.64:26656
        0a0724b6421196e9e280fb48b039a69a577a56fb@161.97.178.48:26656
        25e7ef64b41a636e3fb4e9bb1191b785e7d1d5cc@46.166.140.172:26656

   ```

7. Run pylonsd start

   ```shell
    $ pylonsd start

   ```

8. Check the balance of your pyloxxxxx address. Please reach out to be funded from the faucet if you do not have funds (1,000,000ubedrock). Paste your pyloxxxxx address on the validator chat and request funds if you do not have.

   ```shell
    $ pylonsd query bank balances <delegator-addresss>

   ```
   
9. Create your validator.

   ```shell
    $ pylonsd tx staking create-validator \
      --amount=1000000ubedrock \
      --pubkey=$(pylonsd tendermint show-validator) \
      --moniker=<moniker> \
      --chain-id=pylons-testnet-2 \
      --commission-rate="0.10" \
      --commission-max-rate="0.20" \
      --commission-max-change-rate="0.01" \
      --min-self-delegation="1000000" \
      --gas="auto" \
      --gas-adjustment="1.5" \
      --from=<key-name>

   ```
10. Self-delegate 1000000ubedrock 

   ```shell
   $ pylonsd tx staking delegate pylovaloperxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx 1000000ubedrock --from=<key-name> --broadcast-mode=async --chain-id=pylons-testnet-2 -y
   ```
 
