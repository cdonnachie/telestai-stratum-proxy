# telestai-stratum-proxy
Allows you to mine directly to your own local wallet/node with any mining software that uses the stratum protocol.

If you are a windows user and are not familiar with python, a walk-through and auto installer is avaliable for a (hopefully) easy install. See [here](#windows).

## *Important Note 1*
This is not pool software and is meant for solo-mining. All proceeds go to the address of the first miner that connects.

## *Important Note 2*
Mining software will only send a share when it has found a block. No shares for long periods of time is normal behavior.

## Table of Contents  
- [Setup](#setup)
- [Node Requirements](#node)
- [Usage](#usage)
- [Help](#help)

<a name="setup"/>

## Setup:

1. Requires python 3.8+
2. Run `python3 -m pip install -r requirements.txt`
  - Note that the pysha3 module will need to be compiled so you need some kind of C compiler installed. Alternatively, a precompiled `.whl` is avaliable in `windows/python_modules`.

<a name="windows"/>

#### For Windows:
A bat file is avaliable to auto install python and dependencies and generate another bat file to run the stratum.
1. Ensure your node is configured [as required](#node).
2. (Re)start your node (the qt wallet works).
3. Download this repo (https://github.com/cdonnachie/telestai-stratum-proxy/archive/refs/heads/main.zip)
4. Unzip the downloaded file
5. Open the unzipped folder
6. Open the `windows` folder
7. Double-click `generate_bat.bat`
8. After `generate_bat.bat` completes with no errors, go back to the previous folder.
9. Double-click `run.bat` to run the stratum proxy.

<a name="node"/>

## Node Requirements:

Requires the following `telestai.conf` options:
```
server=1
rpcuser=my_username
rpcpassword=my_password
rpcallowip=127.0.0.1
```
On *nix OS's this file is located at `~/.telestai` by default. On windows, this file is located at `%appdata%\Telestai`.

You may need to create the `telestai.conf` file and add those lines if it does not exist.

For testnet you can add `testnet=1` to your `telestai.conf`

note:
- Default Mainnet rpcport = `8766`
- Default Testnet rpcport = `18766`

Make sure you configure the rpcport on `telestai-stratum-proxy.py` accordingly.

<a name="usage"/>

## Usage:
The stratum proxy uses the following flags:
```
usage: telestai-stratum-proxy [-h] [--address ADDRESS] [--port PORT] [--rpcip RPCIP] [--rpcport RPCPORT] 
                 --rpcuser RPCUSER --rpcpass RPCPASS [-t] [-j] [-v] [--version]

Stratum proxy to solo mine to TELESTAI node.

options:
  -h, --help            show this help message and exit
  --address ADDRESS     the address to listen on, defaults to 127.0.0.1
  --port PORT           the port to listen on
  --rpcip RPCIP         the ip of the node rpc server to connect to.
  --rpcport RPCPORT     the port of the node rpc server to connect to.
  --rpcuser RPCUSER     the username of the node rpc server to connect to.
  --rpcpass RPCPASS     the password of the node rpc server to connect to.
  -t, --testnet         running on testnet
  -j, --jobs            show jobs in the log
  -v, --verbose, --debug
                        set log level to debug
  --version             show program's version number and exit
```
With this in mind we can run **testnet** from a local node with a miner:
```
python3 telestai-stratum-proxy.py --address 127.0.0.1 --port 54321 --rpcip 127.0.0.1  --rpcport 18766 --rpcuser my_username --rpcpassword my_password -j -t
```
**Testnet** with defaults
```
python3 telestai-stratum-proxy.py --rpcuser my_username --rpcpassword my_password -t
```
And for a local node on **mainnet** with a miner:
```
python3 telestai-stratum-proxy.py --address 127.0.0.1 --port 54321 --rpcip 127.0.0.1  --rpcport 8766 --rpcuser my_username --rpcpassword my_password -j
```
**Mainnet** with defaults
```
python3 telestai-stratum-proxy.py --rpcuser my_username --rpcpassword my_password
```

Connect to it with your miner of choise:

| status | miner | example |
| - | - | - |
| :heavy_check_mark: Works | T-rex | t-rex -a kawpow -o stratum+tcp://PROXY_IP:54325 -u YOUR_WALLET_ADDRESS -p x |
| :heavy_check_mark: Works | TeamRedMiner | teamredminer -o stratum+tcp://PROXY_IP:54325 -u YOUR_WALLET_ADDRESS -p x --eth_hash_report=on |
| :heavy_check_mark: Works | Gminer | miner --algo kawpow --server PROXY_IP:54325 --user YOUR_WALLET_ADDRESS --pass x |
| :heavy_check_mark: Works | kawpowminer | kawpowminer -P stratum+tcp://YOUR_WALLET_ADDRESS.worker@PROXY_IP:54325 |

<a name="help"/>

## Help:
@craigd9686 is avaliable on the community telestai server (https://discord.gg/HYQhTKseyZ)

Donate: 
  - TLS: TuSe7vmUq7WE5NBCPeewDEPPSUtPWk3XaC (My Telestai address)

@kralverde#0550 is avaliable on the community ravencoin server (https://discord.gg/jn6uhur)

Donate: 
  - RVN: RMriWfETGV97hskqH8TvSWVZb9idK6fkU6
  - BTC: bc1q9vs8ttd6sg8dvhwwqh5g6c5wjm0fwkfmq2lgff
