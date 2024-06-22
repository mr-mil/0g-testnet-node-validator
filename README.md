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
