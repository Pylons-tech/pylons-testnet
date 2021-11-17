# Multiversion ReSync

These instructions are for validators who are currently jailed, still running Pylonsd v0.3.1 and have not upgraded to v0.3.2. Also, your node should not be running.


  
#### 1. Clear old data, set halt height to 220000. Start Pylons v0.3.1, sync till 220000 (before the initial halt of 230,991) and stop your node. Steps are:

      pylonsd unsafe-reset-all
      nano .pylons/config/app.toml
Change halt-height=0 to 220000 and start your pylons v0.3.1 node to start syncing. Note: you must use v0.3.1 for this step.
      
      pylonsd start
      
Keep running until synced block height reaches 220000 and halts as per setting. After this, stop your node.

if you halt before 220k, proceed to step 2.
    

#### 2. Download the new pylonsd binary (v0.3.2), run `make install` on it.

    git clone https://github.com/Pylons-tech/pylons
    git checkout v0.3.2
    make install
    pylonsd version

  pylonsd version (should return v0.3.2)
  
#### 3. change (reset) the halt-height back to 0. 
    
    nano .pylons/config/app.toml

Change halt-height=0    

#### 4. Start pylonsd
    pylonsd start
 

