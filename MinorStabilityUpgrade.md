# pylons-testnet-2

- Go version: [v1.17+](https://golang.org/dl/)
- Pylonsd version: [v0.4.1](https://github.com/Pylons-tech/pylons/releases/tag/v0.4.1)

         ensure GOPATH is set properly to point to the go directory of your Go installation: GOPATH = $HOME/go
         ensure PATH is set properly to point to the bin folder of your Go installation: PATH = $GOPATH/bin
         pylonsd binary(link above or from 'make install' on repo clone/source) should be put in Go's bin folder

## Minor Upgrade

         Get this upgrade done as quickly as possible: few seconds to a minute 

1. Stop your node, get the new pylonsd version [v0.4.1](https://github.com/Pylons-tech/pylons/releases/tag/v0.4.1) and `make install` the pylonsd binary

 
 
2. Run pylonsd version to verify the version is correct.  please reach out if the version is wrong.

   ```shell
   $ pylonsd version
   ``` 

3. Run pylonsd start

   ```shell
    $ pylonsd start

   ```

   
  Optional: If your node is stopped for too long, more than a few minutes, you may be jailed on restart. If jailed, request 10,000ubedrock on the channel, and self-delegate it to unjail.


    Self-delegate 10000ubedrock 

   ```shell
   $ pylonsd tx staking delegate pylovaloperxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx 10000ubedrock --from=<key-name> --broadcast-mode=async --chain-id=pylons-testnet -y
   ```
 
