# pylons-testnet

- Go version: [v1.16+](https://golang.org/dl/)
- Pylonsd version: [v0.1.0](https://github.com/Pylons-tech/pylons/releases)

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
   We recommend you to save the mnemonic generated in order to recover your account if it lost.  

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
    $ git commit -m "created gentx to moniker <moniker-name>"
    $ git push origin main

   ```