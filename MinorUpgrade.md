# pylons-testnet

- Go version: [v1.17+](https://golang.org/dl/)
- Pylonsd version: [v0.3.2](https://github.com/Pylons-tech/pylons/releases/tag/v0.3.2)

         ensure GOPATH is set properly to point to the go directory of your Go installation: GOPATH = $HOME/go
         ensure PATH is set properly to point to the bin folder of your Go installation: PATH = $GOPATH/bin
         pylonsd binary(link above or from 'make install' on repo clone/source) should be put in Go's bin folder

## Minor Upgrade

         Target to get this upgrade done in 5 minutes or less and restart your node.

1. Stop your node, get the new pylonsd version (v0.3.2) and `make install` the pylonsd binary

 
 
2. Run pylonsd version to verify the version is correct.  please reach out if the version is wrong.

   ```shell
   $ pylonsd version
   ``` 

3. Run pylonsd start

   ```shell
    $ pylonsd start

   ```

   
  Optional: If your node is stopped for more than 5minutes you may be jailed on restart. If jailed, request 10,000ubedrock on the channel, and self-delegate it to unjail.


   ```
    Self-delegate 10000ubedrock 

   ```shell
   $ pylonsd tx staking delegate pylovaloperxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx 10000ubedrock --from=<key-name> --broadcast-mode=async --chain-id=pylons-testnet -y
   ```
 
