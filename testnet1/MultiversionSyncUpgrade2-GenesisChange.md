# Multiversion ReSync

These instructions are for validators who are currently jailed, still running Pylonsd v0.3.1 and have not upgraded to v0.3.2. Also, your node should not be running.

#### 1. Clear old data, Set halt-height to 121320 and Start Pylons v0.3.1 till halt-height. Steps are:

      pylonsd unsafe-reset-all
      nano .pylons/config/app.toml
Change halt-height=0 to 121320 and start your pylons v0.3.1 node to start syncing
      
      pylonsd start

Keep running until synced block height reaches 121320 and halts. After this, stop your node.


#### 2. Export genesis:

    pylonsd export &> 121320.pylons_testnet.json
    
#### 3. Backup old `~/.pylons folder

    cp ~/.pylons ~/pylons_backup
    

#### 4. Delete the data in ~/.pylons/data/ and delete the genesis.json in ~/.pylons/config in the .pylons folder (not the backup)

#### 5. Download the new pylonsd binary (v0.3.2), run `make install` on it.

    git clone https://github.com/Pylons-tech/pylons
    git checkout <latest-version>
    make install
    pylonsd version

  pylonsd version (should return v0.3.2)
  
#### 6. Move exported genesis (121320.pylons_testnet.json) to `~/.pylons/config` folder and rename it to genesis.json (replace the genesis.json)

    cp 121320.pylons_testnet.json .pylons/config/genesis.json

#### 7. Copy your priv_validator_key.json and node_key.json from the pylons_backup folder (`pylons_backup/config/`) to the new .pylons folder in the same location (`~/.pylons/config/`);

    cp pylons_backup/config/priv_validator_key.json ~/.pylons/config/priv_validator_key.json
    cp pylons_backup/config/priv_validator_key.json ~/.pylons/config/priv_validator_key.json

#### 8. Copy your priv_validator_state.json from the pylons_backup folder (`pylons_backup/data/priv_validator_state.json`) to the new .pylons folder in the same location (`~/.pylons/data/priv_validator_state.json`);

    cp pylons_backup/data/priv_validator_state.json ~/.pylons/data/priv_validator_state.json

#### 9. Copy your data folder from the pylons_backup folder (`pylons_backup/data`) to the data folder in the new .pylons folder in the same location (`~/.pylons/data`);

    cp -r pylons_backup/data ~/.pylons

#### 10. Copy the config.toml from the backup (pylons_backup) to the same location on the new: `~/.pylons/config folder`

    cp pylons_backup/config/config.toml ~/.pylons/config/config.toml

change (reset) the halt-height back to 0. 
#### 11. Start pylonsd
    pylonsd start
 

