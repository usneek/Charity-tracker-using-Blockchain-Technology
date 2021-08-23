# Charity-tracker-using-Blockchain-Technology
1. Unzip the charity-tracker.zip file attached.
2. You will find four nodes- charity, donor,external_entity &
service-provider and the genesis file, ‘clique genesis.json’ .
3. In the data folder of each node, permissions_config.toml is
present through which we provide permissions to the node.
4. To start charity node use the following command
besu --data-path=data --genesis-file=../cliqueGenesis.json
--permissions-nodes-config-file-enabled
--permissions-accounts-config-file-enabled
--rpc-http-enabled --rpc-http-api=ADMIN,ETH,NET,PERM,CLIQUE
--host-allowlist="*" --rpc-http-cors-origins="*"
(Make sure you provide the correct path of besu installed on your
pc).
5. To start donor node use the following command
besu --data-path=data --genesis-file=../cliqueGenesis.json
--permissions-nodes-config-file-enabled
--permissions-accounts-config-file-enabled
--rpc-http-enabled --rpc-http-api=ADMIN,ETH,NET,PERM,CLIQUE
--host-allowlist="*" --rpc-http-cors-origins="*"
--p2p-port=30304 --rpc-http-port=8546
6. To start service_provider node, use the following command
besu --data-path=data --genesis-file=../cliqueGenesis.json
--permissions-nodes-config-file-enabled
--permissions-accounts-config-file-enabled
--rpc-http-enabled --rpc-http-api=ADMIN,ETH,NET,PERM,CLIQUE

--host-allowlist="*" --rpc-http-cors-origins="*"
--p2p-port=30305 --rpc-http-port=8547
7. Start another terminal and use the perm_addNodesToAllowlist
JSON-RPC API method to add the nodes to the permissions
configuration file for each node.
Replace <EnodeNode1>, <EnodeNode2>, and <EnodeNode3> with the
enode URL displayed when starting each node.
Charity:
curl -X POST --data
'{"jsonrpc":"2.0","method":"perm_addNodesToAllowlist","param
s":[["<EnodeNode1>","<EnodeNode2>","<EnodeNode3>"]],
"id":1}' http://127.0.0.1:8545

Donor:
curl -X POST --data
'{"jsonrpc":"2.0","method":"perm_addNodesToAllowlist","param
s":[["<EnodeNode1>","<EnodeNode2>","<EnodeNode3>"]],
"id":1}' http://127.0.0.1:8546

Service Provider:
curl -X POST --data
'{"jsonrpc":"2.0","method":"perm_addNodesToAllowlist","param
s":[["<EnodeNode1>","<EnodeNode2>","<EnodeNode3>"]],
"id":1}' http://127.0.0.1:8547
8. Use the admin_addPeer JSON-RPC API method to add charity node
as a peer for donor and service provider node.
Replace <EnodeNode1> with the enode URL displayed when
starting charity node.

Donor:
curl -X POST --data
'{"jsonrpc":"2.0","method":"admin_addPeer","params":["<Enode
Node1>"],"id":1}' http://127.0.0.1:8546

Service provider:
curl -X POST --data
'{"jsonrpc":"2.0","method":"admin_addPeer","params":["<Enode
Node1>"],"id":1}' http://127.0.0.1:8547
9. Use cURL to call the JSON-RPC API net_peerCount method and
confirm the nodes are functioning as peers:
curl -X POST --data
'{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":
1}' localhost:8545
10. To add the private permissioned network on MetaMask:
a. Sign in to MetaMask.
b. After you sign in to MetaMask, connect to the private
network RPC endpoint:
i. In the MetaMask network list, select Custom RPC.
ii. In the New RPC URL field, enter the JSON-RPC HTTP
service endpoint displayed when you started the
private network.

Save the configuration and return to the MetaMask main screen.
Your current network is now set to the private network RPC node.
11. Import the accounts in MetaMask private network using their
private key addresses.

12. To monitor situation better, we will use Alethio Ethereum Lite
Explorer. Using addresses of nodes we can view the current
balance and change after every transaction.Use the command
docker run --rm -p 8080:80 -e APP_NODE_URL=http://localhost:8545
alethio/ethereum-lite-explorer
Open http://localhost:8080 in your browser to view the Lite
Explorer.
13. Make required transaction and view the changes reflected on
system.
14. Your private permissioned network has been set up and ready
to do transactions in a transparent manner.
15. To confirm permissioning, run the node named as external
entity in the folder. Check its peer count using the following
command
curl -X POST --data
'{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":
1}' localhost:8548
You will observe a net peer count of zero in it.
16. Press ctrl+C to stop the nodes.
  
  
  Please find the working demonstration of the project at:- [demo](https://drive.google.com/file/d/1tXW7WjSdg4eAtaFl9m8hOYzWNOA8X9R3/view?usp=sharing)
