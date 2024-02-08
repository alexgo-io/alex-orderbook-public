# STXDX Contracts
This project contains several Clarity smart contracts that enable decentralized trading of fungible and non-fungible tokens on the Stacks blockchain.

## Overview
The core components are:

- `stxdx-exchange-zero` - Implements the decentralized exchange functionality for trading tokens
- `stxdx-wallet-zero` - Holds user balances and processes deposits/withdrawals
- `stxdx-registry` - Maps user IDs and asset IDs to their respective principals
- `stxdx-sender-proxy` - Allows authorized users to submit transactions to the exchange
- `redstone-verify` - Library for verifying RedStone signatures

Together, these contracts allow users to trustlessly trade tokens in a decentralized manner, without requiring a centralized exchange operator. The registry provides efficient lookup of principals, the wallet holds user balances, the exchange facilitates trading, and the proxy allows delegated access.

## Contract Details
### stxdx-exchange-zero.clar
This contract implements the core exchange logic. Key functionality includes:

- Placing limit orders for trades
- Filling existing orders by matching compatible trades
- Getting status of open orders
- Cancelling unfilled orders
- Setting oracle price feeds for assets
- Orders are specified in terms of user IDs and asset IDs, which are resolved to principals via the registry.

### stxdx-wallet-zero.clar
The wallet holds balances of assets for different user accounts. It enables:

- Depositing asset tokens into the wallet
- Requesting withdrawals from the wallet
- Approving pending withdrawal requests
- Transferring balances between user accounts
- The wallet integrates with the registry to lookup user and asset principals. Withdrawals follow a 2-step process to provide security.

### stxdx-registry.clar
This simple registry contract maps user IDs and asset IDs to their respective principals. It allows efficient lookup of principals by ID instead of passing around full principals in transaction data.

### stxdx-sender-proxy.clar
This proxy contract allows authorized users to submit transactions to the exchange on behalf of other accounts. This provides a permissioned layer for delegated trading.

### redstone-verify.clar
General purpose signature verification library for validating RedStone signed payloads. Used by other contracts for verifying signatures from oracle price feeds.

## Usage
The main entrypoints are the exchange and wallet contracts. Users can trade tokens on the decentralized exchange via `stxdx-exchange-zero`, and deposit/withdraw via `stxdx-wallet-zero`.

The sender proxy allows delegated trading, while the registry is used internally for efficient data storage.

## License
This project is licensed under the BUSL license - see the LICENSE file for details.