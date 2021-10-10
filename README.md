# pylons-testnet

- Go version: [v1.17+](https://golang.org/dl/)
- Pylonsd version: [v0.1.3](https://github.com/Pylons-tech/pylons/releases/tag/v0.1.3)

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
