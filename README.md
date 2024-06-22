# 0g-testnet-node-validator
<h1>Complete Guide to Node Validator of the 0Gravity Project</h1>
<h2>Recommended System :</h2>
<ul>
<li>RAM 16GB</li>
<li>CPU 4 Core</li>
<li>Disk +500GB SSD</li>
<li>OS Ubuntu 20 or 22</li>
</ul>

<h3>1. Dependecies :</h3>

```
sudo apt update && \
sudo apt install curl git jq build-essential gcc unzip wget lz4 -y
```

<h3>2. Install GO :</h3>

```
cd $HOME && \
ver="1.21.3" && \
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz" && \
sudo rm -rf /usr/local/go && \
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz" && \
rm "go$ver.linux-amd64.tar.gz" && \
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile && \
source $HOME/.bash_profile && \
go version
```

<h3>3. Install 0G :</h3>

```
git clone -b v0.1.0 https://github.com/0glabs/0g-chain.git
./0g-chain/networks/testnet/install.sh
source .profile
```

```
mkdir -p $HOME/.0gchain/cosmovisor/genesis/bin
mv /root/go/bin/0gchaind $HOME/.0gchain/cosmovisor/genesis/bin/
```

```
sudo ln -s $HOME/.0gchain/cosmovisor/genesis $HOME/.0gchain/cosmovisor/current -f
sudo ln -s $HOME/.0gchain/cosmovisor/current/bin/0gchaind /usr/local/bin/0gchaind -f
```

```
go install cosmossdk.io/tools/cosmovisor/cmd/cosmovisor@v1.5.0
```

<h3>4. Create Public Node Service File :</h3>

```
sudo tee /etc/systemd/system/0gchaind.service > /dev/null << EOF
[Unit]
Description=0gchaind node service
After=network-online.target

[Service]
User=$USER
ExecStart=$(which cosmovisor) run start
Restart=on-failure
RestartSec=10
LimitNOFILE=65535
Environment="DAEMON_HOME=$HOME/.0gchain"
Environment="DAEMON_NAME=0gchaind"
Environment="UNSAFE_SKIP_BACKUP=true"
Environment="PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:$HOME/.0gchain/cosmovisor/current/bin"

[Install]
WantedBy=multi-user.target
EOF
```

```
sudo ln -s $HOME/.0gchain/cosmovisor/genesis $HOME/.0gchain/cosmovisor/current -f
sudo ln -s $HOME/.0gchain/cosmovisor/current/bin/0gchaind /usr/local/bin/0gchaind -f
```

```
sudo systemctl daemon-reload
sudo systemctl enable 0gchaind.service
```

<h3>5. Initiate Node :</h3>

```
0gchaind config chain-id zgtendermint_16600-1
0gchaind config keyring-backend os
0gchaind config node tcp://localhost:16657
```

In the code below, instead of NODE_NAME, enter your desired name for the node and then execute the command:

```
0gchaind init NODE_NAME --chain-id zgtendermint_16600-1
```
