Building Ducatuscoin
====================

This documentation assumes the use of Ubuntu. Our miners currently run on Ubutun 14.04;
your mileage may vary if you choose to use a different Linux distro or version.

# Install Required Libraries

There are a number of required libraries to install Ducatuscoin. It is best to install in
this recommended order; including bitcoind in the first batch may prevent all necessary
libraries from being installed.

```bash
sudo apt-get update
sudo apt-get install -y ntp git build-essential libssl-dev libdb-dev libdb++-dev libboost-all-dev libqrencode-dev libevent-dev autoconf libtool libboost-all-dev wget software-properties-common python-software-properties

sudo add-apt-repository -y ppa:bitcoin/bitcoin
sudo apt-get update -y
sudo apt-get install -y bitcoind git libdb4.8-dev libdb4.8++-dev

```

# Install Univalue

```bash
git clone https://github.com/jgarzik/univalue
cd univalue
./autogen.sh
./configure
sudo make install
```

# Install Additional Libraries
```bash
sudo apt-get install --yes make pkg-config bsdmainutils libminiupnpc-dev libzmq3-dev libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler
```

# Download Ducatuscore and build the node software
```bash
git clone https://github.com/Ducatus/ducatuscoin-core
cd ducatuscoin-core
aclocal
./autogen.sh
autoreconf -i
autoconf
./configure --with-system-univalue --with-gui=no --with-qrencode=no --disable-tests
make
sudo make install
```

# Running the node software

The simplest way to start from scratch with the command line client, which will automatically sync the blockchain and create a wallet, is to just run this command (without arguments) :

```bash
 ducatuscoind
```

# Interacting with the node 

Once the node is running, you may interact with it using the `ducatuscoin-cli` command.

Look at the status of your node synchronization:
```bash
ducatuscoin-cli getblockchaininfo
```

Create an account and receiving address:
```bash
ducatuscoin-cli getnewaddress <int>
```

Mine Duactuscoin (generate hashes). Note that the recommended approach to mine Ducatuscoin is to use a standard miner such as cgminer, cudaminer, or cpuminer with the [Ducatus member pool](http://network.ducatus.net/beta/mining-pool/):
```bash
ducatuscoin-cli generate <int>
```

For more information:
```bash
ducatuscoin-cli help
```
