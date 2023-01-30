
# How To Sync a BSC Node

### System requirements

- Desktop or laptop hardware running recent versions of Mac OS X, Windows, or Linux.
- 2TB of free disk space, accessible at a minimum read/write speed of 100 MB/s.
- 8 cores of CPU and 16 gigabytes of memory (RAM).
- A broadband Internet connection with upload/download speeds of at least 1 megabyte per second
Your full node has to run at least 4 hours per 24 hours in order to catch up with Binance Chain More hours will be better, run your node continuously for best results. </br></br></br>

> The specifications listed above are high end but will ensure you have a smooth sync process with fewer prunning. If you want the minimum specification requirements have a look here [Minimum System Requirements](https://docs.binance.org/guides/node/join-mainnet.html).

> Server recommendation: Hetzner AX61-NVMe 


</br>

### Sync Process

1. Download the latest geth and mainnet using wget from the link below
	[https://github.com/bnb-chain/bsc/releases](https://github.com/bnb-chain/bsc/releases) - the current version at the moment is v1.1.18 is the current latest version (as of 17th June 2022)
	
```
wget https://github.com/bnb-chain/bsc/releases/download/v1.1.18/geth_linux
```
```
wget https://github.com/bnb-chain/bsc/releases/download/v1.1.18/mainnet.zip
```


2. Make the geth_linux downloaded executable

```
chmod +x geth_linux
```
4. Unzip the mainnet.zip file. You may need to [install unzip](https://askubuntu.com/questions/86849/how-to-unzip-a-zip-file-from-the-terminal) if you dont have it in your machine 
```
unzip mainnet.zip
```
5. Generate the genesis block by runnin the command below 
```
./geth_linux --datadir ./mainnet init genesis.json
```
7. Download the latest snapshot from https://github.com/bnb-chain/bsc-snapshots by using the command below
```
wget -q -O - <snapshot URL> | tar -I lz4 -xvf -
```

7. Replacing the <snapshot URL> with "THE_URL_TO_THE_LATEST_SNAPSHOT"   (quotation marks included)
8. Once downloaded, it will be extracted to a folder named server folder on the downloaded folder. 
9. Delete the chaindata and triecache data from the datadir folder (mainnet) if it already exists to sync afresh. Use the commands provided below
```
rm -rf mainnet/geth/chaindata
rm -rf mainnet/geth/triecache
```
10. Move the chaindata and triecache data of the downloaded snapshot to your datadir (mainnet) using  the commands below

```
mv server/data-seed/geth/chaindata mainnet/geth/chaindata
mv server/data-seed/geth/triecache mainnet/geth/triecache
```

11. After moving the snapshot data, start the geth using the command below.

```
./geth_linux --config ./config.toml --datadir ./mainnet --cache 100000 --rpc.allow-unprotected-txs --txlookuplimit 0 --http --maxpeers 100 --ws --syncmode=full --snapshot=false --diffsync
```
<br ><br >
***Note***<br ><br >
	Geth syncing should be run in a screen session to ensure the process continues even after the ssh session is closed <br >
	- If you are using the latest snapshot and notice that the age more than 2 years, most likely you have an eror in you sync setup <br >
		- The first place to troubleshoot in such an issue is check that you have initailised the gennesis config correctly. Make sure that the datadir when initialisng the genesis config is correct. <br >
	- In case you want to make a change to the the config.toml file or any other config file, just stop the node sync by control + C. After making the change start the node again with the command for starting the node. The change will pick up <br >
	- The ip address for the websocket is not include in the config.toml. You need to manually add it <br >



							HAPPY SYNCING
