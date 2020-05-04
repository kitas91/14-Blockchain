# 14-Blockchain
Creating the ZBank blockchain 

Step 1: Create nodes:

Node 1 = zeus
Node 2 = poseidon


Step 2: Genesis 
./puppth to create genesis:

(ethereum) lucas@MacBookPro ~/Documents/Columbia/Blockcahin-Tools
$ ./puppeth
+-----------------------------------------------------------+
| Welcome to puppeth, your Ethereum private network manager |
|                                                           |
| This tool lets you create a new Ethereum network down to  |
| the genesis block, bootnodes, miners and ethstats servers |
| without the hassle that it would normally entail.         |
|                                                           |
| Puppeth uses SSH to dial in to remote servers, and builds |
| its network components out of Docker containers using the |
| docker-compose toolset.                                   |
+-----------------------------------------------------------+

Please specify a network name to administer (no spaces, hyphens or capital letters please)
> ares  

Sweet, you can set this via --network=ares next time!

INFO [05-04|15:26:12.249] Administering Ethereum network           name=ares
WARN [05-04|15:26:12.252] No previous configurations found         path=/Users/lucas/.puppeth/ares

What would you like to do? (default = stats)
 1. Show network stats
 2. Configure new genesis
 3. Track new remote server
 4. Deploy network components
> 2

What would you like to do? (default = create)
 1. Create new genesis from scratch
 2. Import already existing genesis
> 1

Which consensus engine to use? (default = clique)
 1. Ethash - proof-of-work
 2. Clique - proof-of-authority
> 2

How many seconds should blocks take? (default = 15)
> 

Which accounts are allowed to seal? (mandatory at least one)
> 0x zeus address 
> 0x poseidon address
> 0x

Which accounts should be pre-funded? (advisable at least one)
> 0x zeus address
> 0x poseidon address
> 0x

Should the precompile-addresses (0x1 .. 0xff) be pre-funded with 1 wei? (advisable yes)
> 

Specify your chain/network ID if you want an explicit one (default = random)
> 2020
INFO [05-04|15:28:41.477] Configured new genesis block 

What would you like to do? (default = stats)
 1. Show network stats
 2. Manage existing genesis
 3. Track new remote server
 4. Deploy network components
> 2

 1. Modify existing configurations
 2. Export genesis configurations
 3. Remove genesis configuration
> 2

Which folder to save the genesis specs into? (default = current)
  Will create ares.json, ares-aleth.json, ares-harmony.json, ares-parity.json
> 
INFO [05-04|15:29:16.498] Saved native genesis chain spec          path=ares.json
ERROR[05-04|15:29:16.498] Failed to create Aleth chain spec        err="unsupported consensus engine"
ERROR[05-04|15:29:16.499] Failed to create Parity chain spec       err="unsupported consensus engine"
INFO [05-04|15:29:16.502] Saved genesis chain spec                 client=harmony path=ares-harmony.json

What would you like to do? (default = stats)
 1. Show network stats
 2. Manage existing genesis
 3. Track new remote server
 4. Deploy network components
> ^C  # exit out

Step 3: Initiate (nodes) zeus & poseidon:

Zeus
$ ./geth init ares.json --datadir zeus
INFO [05-04|15:32:28.890] Maximum peer count                       ETH=50 LES=0 total=50
INFO [05-04|15:32:28.920] Allocated cache and file handles         database=/Users/lucas/Documents/Columbia/Blockcahin-Tools/zeus/geth/chaindata cache=16.00MiB handles=16
INFO [05-04|15:32:28.946] Writing custom genesis block 
INFO [05-04|15:32:28.953] Persisted trie from memory database      nodes=357 size=50.97KiB time=1.520459ms gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
INFO [05-04|15:32:28.954] Successfully wrote genesis state         database=chaindata hash=817bea…95e483
INFO [05-04|15:32:28.955] Allocated cache and file handles         database=/Users/lucas/Documents/Columbia/Blockcahin-Tools/zeus/geth/lightchaindata cache=16.00MiB handles=16
INFO [05-04|15:32:28.973] Writing custom genesis block 
INFO [05-04|15:32:28.981] Persisted trie from memory database      nodes=357 size=50.97KiB time=1.725939ms gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
INFO [05-04|15:32:28.982] Successfully wrote genesis state         database=lightchaindata hash=817bea…95e483

Poseidon
$ ./geth init ares.json --datadir poseidon
INFO [05-04|15:32:28.890] Maximum peer count                       ETH=50 LES=0 total=50
INFO [05-04|15:32:28.920] Allocated cache and file handles         database=/Users/lucas/Documents/Columbia/Blockcahin-Tools/zeus/geth/chaindata cache=16.00MiB handles=16
INFO [05-04|15:32:28.946] Writing custom genesis block 
INFO [05-04|15:32:28.953] Persisted trie from memory database      nodes=357 size=50.97KiB time=1.520459ms gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
INFO [05-04|15:32:28.954] Successfully wrote genesis state         database=chaindata hash=817bea…95e483
INFO [05-04|15:32:28.955] Allocated cache and file handles         database=/Users/lucas/Documents/Columbia/Blockcahin-Tools/zeus/geth/lightchaindata cache=16.00MiB handles=16
INFO [05-04|15:32:28.973] Writing custom genesis block 
INFO [05-04|15:32:28.981] Persisted trie from memory database      nodes=357 size=50.97KiB time=1.725939ms gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
INFO [05-04|15:32:28.982] Successfully wrote genesis state         database=lightchaindata hash=817bea…95e483


Step 4: Fire up the blockchain

Zeus:
$ ./geth --datadir zeus --unlock "0x zeus address" --mine --rpc --allow-insecure-unlock

Poseidon:
./geth --datadir poseidon --mine --port 30304 --bootnodes "zeus enode" --unlock "0x poseidon address"


Step 5: Create Network on MyCrypto
- "Change Network"
- "Add Custom Nodes"
- "Set Up Your Custom Node"
    - Node Name: Zeus
    - Network: Custom
    - Network Name: ares
    - Currency: ETH
    - Chain ID: 2020
    - URL: http://127.0.0.1.8545



