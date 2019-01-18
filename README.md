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

## Test
TBD
