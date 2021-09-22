# pylons-testnet

- Go version: [v1.16+](https://golang.org/dl/)
- Pylonsd version: [v0.1.0](https://github.com/Pylons-tech/pylons/releases)

## GenTx Generation

1. Initialize the pylons directories and create the local genesis file with the correct
   chain-id

   ```shell
   $ pylonsd init <monikername> --chain-id=pylons-testnet
   ```

2. Create a local key pair in the Keybase

   ```shell
   $ pylonsd keys add <key-name> --keyring-backend=os
   ```

3. Add your account to your local genesis file with a given amount and the key you
   just created.

   ```shell
   $ pylonsd add-genesis-account $(pylonsd keys show <key-name> -a --keyring-backend=os) 1000000ubedrock
   ```

4. Create the gentx ()

   ```shell
   $ pylonsd gentx <key-name>     \ 
      1000000ubedrock --moniker=<monikername> \ 
      --pubkey $(pylonsd tendermint show-validator) \    
      --keyring-backend=os                          \
      --chain-id=pylons-testnet                     
   ```
