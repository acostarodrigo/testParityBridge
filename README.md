# testParityBridge
tests related to parity Bridge

## Network Thopology
Main network is a private parity Dev blockchain. Configured under ./private.
Private network is only a single node, node0.


Side network is a Proof of Authority parity blockchain. Configured under ./poa
PoA network is formed by two authorities, node0 and node1.

## Private dev blockchain


Network is started in the following way:

``` /private$ parity --config node0.toml --unlock 0x00bd138abd70e2f00903268f3db08f2d25677c9e --password password.txt ```

Account 0x00bd138abd70e2f00903268f3db08f2d25677c9e is the one defined at the bridge config file bridge_config.toml, as the authority address.

The authority address must exists in both networks and be unlocked for both parity clients.

To import this address into private blockchain execute:

``` parity --config node0.toml account import [PathToAccountFile] ```


## Proof of Authority blockchain

In a similar way, PoA blockchain can be started in the following way:

``` /poa$ parity --config node0.toml --unlock 0x00bd138abd70e2f00903268f3db08f2d25677c9e --password node.pwds ```


### Deploy parity Bridge contract

In a similar way, first deployment of contracts in both networks is executed by:

``` env RUST_LOG=info ../target/release/parity-bridge-deploy --config bridge_config.toml --database bridge.db ```

The output for my local environment was:

```
env RUST_LOG=info ../target/release/parity-bridge-deploy --config bridge_config.toml --database bridge.db
 INFO 2019-01-17T22:37:08Z: parity_bridge_deploy: Parsing cli arguments
 INFO 2019-01-17T22:37:08Z: parity_bridge_deploy: Loading config
 INFO 2019-01-17T22:37:08Z: parity_bridge_deploy: Starting event loop
 INFO 2019-01-17T22:37:08Z: parity_bridge_deploy: Establishing HTTP connection to main "http://localhost:8542"
 INFO 2019-01-17T22:37:08Z: parity_bridge_deploy: Establishing HTTP connection to side "http://localhost:8540"
 INFO 2019-01-17T22:37:08Z: parity_bridge_deploy: Deploying MainBridge contract
 INFO 2019-01-17T22:37:08Z: bridge::deploy: sending MainBridge contract deployment transaction and waiting for 0 confirmations...
 INFO 2019-01-17T22:37:08Z: bridge::send_tx_with_receipt: SendTransactionWithReceipt: got last block number 1
 INFO 2019-01-17T22:37:08Z: bridge::send_tx_with_receipt::inner: SendTransactionWithReceipt: sent transaction 0x9cbf…0096
 INFO 2019-01-17T22:37:09Z: bridge::block_number_stream: BlockNumberStream polling last block number
 INFO 2019-01-17T22:37:09Z: bridge::block_number_stream: BlockNumberStream: fetched last block number 2
 INFO 2019-01-17T22:37:09Z: bridge::send_tx_with_receipt::inner: SendTransactionWithReceipt: fetched confirmed block number 2
 INFO 2019-01-17T22:37:09Z: bridge::send_tx_with_receipt::inner: SendTransactionWithReceipt: got transaction receipt: 0x9cbf…0096
 INFO 2019-01-17T22:37:09Z: bridge::deploy: MainBridge deployment completed to 0xebd3944af37ccc6b67ff61239ac4fef229c8f69f
 INFO 2019-01-17T22:37:09Z: parity_bridge_deploy: Successfully deployed MainBridge contract
 INFO 2019-01-17T22:37:09Z: bridge::deploy: "deployment-main-ebd3944af37ccc6b67ff61239ac4fef229c8f69f" created
 INFO 2019-01-17T22:37:09Z: parity_bridge_deploy: Deploying SideBridge contract
 INFO 2019-01-17T22:37:09Z: bridge::deploy: sending SideBridge contract deployment transaction and waiting for 0 confirmations...
 INFO 2019-01-17T22:37:09Z: bridge::send_tx_with_receipt: SendTransactionWithReceipt: got last block number 2381
 INFO 2019-01-17T22:37:09Z: bridge::send_tx_with_receipt::inner: SendTransactionWithReceipt: sent transaction 0x01b4…326b
 INFO 2019-01-17T22:37:10Z: bridge::block_number_stream: BlockNumberStream polling last block number
 INFO 2019-01-17T22:37:10Z: bridge::block_number_stream: BlockNumberStream: fetched last block number 2382
 INFO 2019-01-17T22:37:10Z: bridge::send_tx_with_receipt::inner: SendTransactionWithReceipt: fetched confirmed block number 2382
 INFO 2019-01-17T22:37:10Z: bridge::send_tx_with_receipt::inner: SendTransactionWithReceipt: got transaction receipt: 0x01b4…326b
 INFO 2019-01-17T22:37:10Z: bridge::deploy: SideBridge deployment completed to 0xebd3944af37ccc6b67ff61239ac4fef229c8f69f
 INFO 2019-01-17T22:37:10Z: parity_bridge_deploy: Successfully deployed SideBridge contract
 INFO 2019-01-17T22:37:10Z: bridge::deploy: "deployment-side-ebd3944af37ccc6b67ff61239ac4fef229c8f69f" created
 INFO 2019-01-17T22:37:10Z: parity_bridge_deploy: 

main_contract_address = "0xebd3944af37ccc6b67ff61239ac4fef229c8f69f"
side_contract_address = "0xebd3944af37ccc6b67ff61239ac4fef229c8f69f"
main_deployed_at_block = 2
side_deployed_at_block = 2382
last_main_to_side_sign_at_block = 2
last_side_to_main_signatures_at_block = 2382
last_side_to_main_sign_at_block = 2382
```

## Test
TBD
