# Cosmovisor and Service Management

=====================================

We encourage the use of [systemd](https://systemd.io) in addition to [cosmovisor](https://docs.cosmos.network/master/run-node/cosmovisor.html), a cosmos binary supervisor, to manage your `pylonsd` process.

First, download [cosmovisor](https://docs.cosmos.network/master/run-node/cosmovisor.html):


Setup a `cosmovisor` user and directory:

```
$ useradd --no-create-home --shell /bin/false cosmovisor
$ mkdir  $HOME/cosmovisor

```

Create the genesis directory and copy the `pylonsd` binary:

```

$ mkdir -p $HOME/cosmovisor/genesis/bin
$ cp  $(which pylonsd)  $HOME/cosmovisor/genesis/bin
$ cp  $(which cosmovisor)  $HOME/cosmovisor
$ chown -R cosmovisor:cosmovisor $HOME/cosmovisor

```

Create a [systemd](https://systemd.io) service in `/etc/systemd/system/cosmovisor.service` with the following definition:


```
1 [Unit]
2 Description=Cosmovisor Process Manager
3 After=network.target
4
5 [Service]
6 User=root
7 Group=root
8 Type=simple
9 Environment="DAEMON_NAME=pylonsd"
10 Environment="DAEMON_HOME=$HOME"
11 Environment="DAEMON_RESTART_AFTER_UPGRADE=true"
12 Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=true"
13 Environment="UNSAFE_SKIP_BACKUP=false"
14 ExecStart=$HOME/cosmovisor/cosmovisor start ...
15 Restart=on-failure
16 LimitNOFILE=4096
17
18 [Install]
19 WantedBy=multi-user.target


```
Reload [systemd](https://systemd.io) and start the `cosmovisor` service:


```
$ sudo systemctl daemon-reload
$ sudo systemctl start cosmovisor
```


Finally, verify the `cosmovisor` service is running and healthy and enable it:


```
$ sudo systemctl status cosmovisor
$ sudo systemctl enable cosmovisor
```


Only set `DAEMON_ALLOW_DOWNLOAD_BINARIES=true` if you're running a full-node or non-validator. Validators are encouraged to download or build the upgraded binaries ahead of time and verify they are correct.
