
1. Download geth and mainnet using wget from the link below
	https://github.com/bnb-chain/bsc/releases/tag/v1.1.8 - Where v1.1.8 is the current latest version (as of 8th March 2022)

2. Make the geth_linux downloaded executable
3. Unzip the mainnet
4. move config.toml and genesis.json to the root folder
5. run the command ./geth_linux --datadir ./mainnet init genesis.json to generate genesis
6. Download the latest snapshot from https://github.com/bnb-chain/bsc-snapshots by using the command below
```
wget -q -O - <snapshot URL> | tar -I lz4 -xvf -
```

7. Replacing the <snapshot URL> with "THE_URL_TO_THE_LATEST_GETH"   (quotation marks included)
8. Once downloaded extract it. It will be extracted to the server folder on the downloaded folder. 
9. Delete the chaindata and triecache data from the datadir folder (mainnet) if it already exists to sync afresh. Use the commands provided below
10. Move the chaindata and triecache data of the downloaded snapshot to your datadir (mainnet) using  the commands below

```
rm -rf mainnet/geth/chaindata
rm -rf mainnet/geth/triecache
mv server/data-seed/geth/chaindata mainnet/geth/chaindata
mv server/data-seed/geth/triecache mainnet/geth/triecache
```

11. After moving the snapshot data, start the geth using the command below.

```
./geth_linux --config ./config.toml --datadir ./mainnet --cache 100000 --rpc.allow-unprotected-txs --txlookuplimit 0 --http --maxpeers 100 --ws --syncmode=full --snapshot=false --diffsync
```

< br>
Note:
	- Geth syncing should be run in a screen session to ensure the process continues even after the ssh session is closed 
	- If you are using the latest snapshot and notice that the age more than 2 years, most likely you have an eror in you sync setup
		- The first place to troubleshoot in such an issue is check that you have initailised the gennesis config correctly. Make sure that the datadir when initialisng the genesis config is correct.
	- In case you want to make a change to the the config.toml file or any other config file, just stop the node sync by control + C. After making the change start the node again with the command for starting the node. The change will pick up
	- The ip address for the websocket is not include in the config.toml. You need to manually add it



HAPPY SYNCING
