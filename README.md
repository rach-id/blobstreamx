# Blobstream X

![Blobstream X](https://pbs.twimg.com/media/F85boT-bYAAF1hM?format=jpg&name=4096x4096)

Implementation of zero-knowledge proof circuits for [Blobstream](https://docs.celestia.org/developers/blobstream), Celestia's data availability solution for Ethereum.

## Overview

Blobstream X's core contract is `BlobstreamX`, which stores commitments to ranges of data roots from Celestia blocks. Users can query for the validity of a data root of a specific block height via `verifyAttestation`, which proves that the data root is a leaf in the Merkle tree for the block range the specific block height is in.

## Request BlobstreamX Proofs

### Request Proofs from the Succinct Platform

Add env variables to `.env`, following the `.env.example`. You do not need to fill out the local configuration, unless you're planning on doing local proving.

Run `BlobstreamX` script to request updates to the specified light client continuously. For the cadence of requesting updates, update `LOOP_DELAY_MINUTES`.

In `/`, run

```shell
cargo run --bin blobstreamx --release
```

### [Generate & Relay Proofs Locally](https://hackmd.io/@succinctlabs/HJE7XRrup)

## BlobstreamX Contract Overview

### Contract Deployment

To deploy the `BlobstreamX` contract:

1. Get the genesis parameters for a `BlobstreamX` contract from a specific Celestia block.

```shell
cargo run --bin genesis -- --block <genesis_block>
```

2. Add .env variables to `contracts/.env`, following `contracts/.env.example`.
3. Initialize `BlobstreamX` contract with genesis parameters. In `contracts`, run

```shell
forge install

source .env

forge script script/Deploy.s.sol --rpc-url $RPC_URL --private-key $PRIVATE_KEY --broadcast --verify --verifier etherscan --etherscan-api-key $ETHERSCAN_API_KEY
```

### Succinct Gateway Prover Whitelist

#### Set Whitelist Status

Set the whitelist status of a functionID to Default (0), Custom (1) or Disabled (2).

```shell
cast calldata "setWhitelistStatus(bytes32,uint8)" <YOUR_FUNCTION_ID> <WHITELIST_STATUS>
```

#### Add Custom Prover

Add a custom prover for a specific functionID.

```shell
cast calldata "addCustomProver(bytes32,address)" <FUNCTION_ID> <CUSTOM_PROVER_ADDRESS>
```

### Deployed contracts

You can interact with the Blobstream X contracts today. The
Blobstream X Solidity smart contracts are currently deployed on
the following chains:

| Contract     | EVM network      | Contract address                                                                                                                | Attested data on Celestia |
| ------------ | ---------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| Blobstream X  | Ethereum Mainnet          | [`Not yet deployed`](https://etherscan.io/address/0xTODO) | [Mainnet Beta](https://docs.celestia.org/nodes/mainnet) |
| Blobstream X | Arbitrum One | [`0xA83ca7775Bc2889825BcDeDfFa5b758cf69e8794`](https://arbiscan.io/address/0xA83ca7775Bc2889825BcDeDfFa5b758cf69e8794#events)  | [Mainnet Beta](https://docs.celestia.org/nodes/mainnet) |
| Blobstream X | Base           | [`0xA83ca7775Bc2889825BcDeDfFa5b758cf69e8794`](https://basescan.org/address/0xA83ca7775Bc2889825BcDeDfFa5b758cf69e8794#events)  | [Mainnet Beta](https://docs.celestia.org/nodes/mainnet) |
| Blobstream X  | Sepolia          | [`0xf0c6429ebab2e7dc6e05dafb61128be21f13cb1e`](https://sepolia.etherscan.io/address/0xf0c6429ebab2e7dc6e05dafb61128be21f13cb1e#events) | [Mocha testnet](https://docs.celestia.org/nodes/mocha-testnet) |
| Blobstream X | Arbitrum Sepolia           | [`0xc3e209eb245Fd59c8586777b499d6A665DF3ABD2`](https://sepolia.arbiscan.io/address/0xc3e209eb245Fd59c8586777b499d6A665DF3ABD2#events)  | [Mocha testnet](https://docs.celestia.org/nodes/mocha-testnet) |
| Blobstream X | Base Sepolia           | [`0xc3e209eb245Fd59c8586777b499d6A665DF3ABD2`](https://sepolia.basescan.org/address/0xc3e209eb245Fd59c8586777b499d6A665DF3ABD2#events)  | [Mocha testnet](https://docs.celestia.org/nodes/mocha-testnet) |

For more information, please refer to the [documentation](https://docs.celestia.org/developers/blobstream). And if you're planning on building a rollup that uses Blobstream, check out the [blobstream rollups](https://docs.celestia.org/developers/blobstream-rollups) docs.
