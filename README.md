# pylons-testnet

- Go version: [v1.17+](https://golang.org/dl/)
- Pylonsd version: [v0.3.1](https://github.com/Pylons-tech/pylons/releases/tag/v0.3.1)

         ensure GOPATH is set properly to point to the go directory of your Go installation: GOPATH = $HOME/go
         ensure PATH is set properly to point to the bin folder of your Go installation: PATH = $GOPATH/bin
         pylonsd binary(link above or from 'make install' on repo clone/source) should be put in Go's bin folder

## GenTx Generation

1. Initialize the pylons directories and create the local genesis file with the correct
   chain-id

   ```shell
   $ pylonsd init <moniker-name> --chain-id=pylons-testnet
   ```

2. Create a local key pair in the Keybase

   ```shell
   $ pylonsd keys add <key-name> --keyring-backend=os
   ```
   We recommend that you save the mnemonic generated to be able to recover your account in the future if it gets lost.  

3. Add your account to your local genesis file with a given amount and the key you
   just created.

   ```shell
   $ pylonsd add-genesis-account $(pylonsd keys show <key-name> -a --keyring-backend=os) 1000000ubedrock
   ```

4. Create the gentx ()

   ```shell
   $ pylonsd gentx <key-name> 1000000ubedrock --moniker="<moniker-name>" --pubkey $(pylonsd tendermint show-validator) --keyring-backend=os --chain-id=pylons-testnet --output-document ./gentxs/<moniker-name>.json                    
   ```

5. The previous step created a <monikername>.json file to the gentxs directory of this project. Now, you have to **commit and 
push it** to the pylons-testnet repository. 

   ```shell
    $ git add gentxs/<moniker-name>.json
    $ git commit -m "created gentx for <moniker-name>"
    $ git push origin main

   ```
   We recommend that you save the mnemonic generated to be able to recover your account in the future if it gets lost.  

## Joining the Network 

1. On receiving joining notification, run create validator

   ```shell
   $ pylonsd tx staking create-validator \
         --amount=1000000ubedrock \
         --pubkey=$(pylonsd tendermint show-validator) \
         --moniker=<moniker> \
         --chain-id=pylons-testnet \
         --commission-rate="0.10" \
         --commission-max-rate="0.20" \
         --commission-max-change-rate="0.01" \
         --min-self-delegation="1000000" \
         --gas="auto" \
         --from=<key_name>
   
   ```

2. Self-delegate 1000000ubedrock 

   ```shell
   $ pylonsd tx staking delegate pylovaloperxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx 1000000ubedrock --from=<key-name> --broadcast-mode=async --chain-id=pylons-testnet -y
   ```
 
