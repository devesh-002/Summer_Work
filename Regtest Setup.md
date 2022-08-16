# Regtest Setup

## Introduction

Before beginning our developer guide we will learn small tricks for setup. Lightning node as we know should support only testnet or mainnet. However if you are a beginner you might want to see it running immediately. To do this we have to run bitcoin core on regtest but the Lightining doesn't support it. If you try to run on regtest then it will show an error as:

```
Wrong network! Our Bitcoin backend is running on 'regtest', but we expect 'main'.
```

Hence to make it run we have various ways to do so. A very nice article is presented [here](https://medium.com/@bitstein/setting-up-a-bitcoin-lightning-network-test-environment-ab967167594a) but in C-Lightining we can do this even in much simpler ways. It is advised to configure it using the following command before going through the tutorial.

```
./configure --enable-developer
poetry run make
sudo make install
```

After building lightning again go through the tutorial. **Note** that the above commands might take time depending on previous builds and numbers.

## How to do in C-Lightning

If you dive in the codebase, you might find a file in contrib folder named ```startup_regtest.sh``` , path is ```contrib/startup_regtest.sh``` . Given this file run this in home directory where lightning node is present.

```
source contrib/startup_regtest.sh
```

As you might note, this is a bash script file which makes aliases like 

```start_ln:``` This can be used to start the lightning node with the number of nodes specified, by default it loads 2 lightning node setups. 

``ensure_bitcoind_funds:``  This is a supplement command and to use this for fund_nodes

```fund_nodes:``` transfer funds from one node to another node

``connect:`` Connect one lightning node to another, usage is ``connect  1 2``

 ```stop_ln:``` Stop the lightning setups

Now run the command ```start_ln 3``` . This will make 3 lightining nodes and you might get an output like:

```
Bitcoin Core starting
awaiting bitcoind...
Commands: 
	l1-cli, l1-log,
	l2-cli, l2-log,
	l3-cli, l3-log,
	bt-cli, stop_ln
```

each of the l```num```-cli  and l```num```-log is for the corresponding lightning node and interact with there cli and nodes. While running the command, you might encounter an error like:

```
error code: -18
error message:
No wallet is loaded. Load a wallet using loadwallet or create a new one with createwallet. (Note: A default wallet is no longer automatically created)
error code: -5
error message:
Error: Invalid address
[1] 97003
[2] 97050
[3] 97115
```

In the recent version of bitcoin-cli they have stopped providing the default wallet and you need to fix this by providing a rpcwallet for each of the lightning nodes using -rpcwallet for nodes/

For saving the aliases and ending the nodes use the command

```
stop_ln
```

This command stops the services and keeps the aliases.

Given we are equipped with this basic knowledge, we can now proceed to learn more about lightning node and its functioning.

