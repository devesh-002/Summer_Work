## Install C-Lightning

### Update in 2022:

The lightning node installation process has changed a lot and has been made a bit easier for everyone to install. It can be installed simply by compiling the source code. 

Requirements: We'll be focussing on Ubuntu only hence the requirement is Ubuntu 15.10 or above. Along with this **pip3** and **Python3** is also needed 

 :warning: **WARNING:** You actually can run c-lightning on a pruned node. However, as the [Lightning repo](https://github.com/ElementsProject/lightning#pruning) notes, there may be issues. To make it work you have to ensure that your Lightning node is only ever trying to update info on blocks that your Bitcoin node has not pruned. To do so you must make sure (1) that your Bitcoin node is fully up to date before you start your Lightning node for the first time; and (2) that your Lightning node never falls too far behind your Bitcoin node (for a standard 550-block pruning, it can never be turned off for 4 or more days). So, you can do it, but it does introduce some danger, which isn't a good idea if you're running a production service. However for testing & installation purposes we can run the node on regtest mode using the file  contrib/startup_regtest.sh. The instructions and process for the same can be seen in the following chapters.

Now we can install the Lightining node using the following commands:

Install the dependencies:

```
sudo apt-get update
sudo apt-get install -y \
  autoconf automake build-essential git libtool libgmp-dev libsqlite3-dev \
  python3 python3-pip net-tools zlib1g-dev libsodium-dev gettext
pip3 install --upgrade pip
pip3 install --user poetry
```

Clone the lightining setup:

```
   git clone https://github.com/ElementsProject/lightning.git
   cd lightning
```

For development and testing :If you are a normal user please ignore this however for a developer who is working on C-Lightining, this is important to install. Given that we will also be focussing on developing and making changes in it, please note to install this properly

```
sudo apt-get install -y valgrind libpq-dev shellcheck cppcheck \
   libsecp256k1-dev jq
```

Build lightning:

```
poetry install
./configure
poetry run make
sudo make install
```

Run it:

```
  bitcoind &
    ./lightningd/lightningd &
    ./cli/lightning-cli help
```

