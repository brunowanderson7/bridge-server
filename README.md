# EVM Bridge (ERC-20)
To access the Portuguese version, [click here](link)

## Description
EVM Bridge is a project that provides a bridge between blockchain networks using the Ethereum Virtual Machine (EVM). Its purpose is to facilitate the development and testing of interoperable tokens, enabling the transfer of value between different blockchains compatible with the EVM. Additionally, the project provides comprehensive documentation to assist developers in using the bridge and understanding its functionality.

## Features
 - ERC-20 token transfer between compatible networks.
 - Secure token burning process.
 - Scalable infrastructure for token transfers between blockchains.

## Project Overview

## EVM

## Server

## [contract-methods.js](link)

<details>
<summary>mintTokens</summary>

### `mintTokens(provider, contract, amount, address)`
Mint tokens in the provided contract. This function is responsible for creating new tokens and assigning them to a specific address.

- `provider`: The Ethereum provider used to interact with the blockchain.
- `contract`: The Ethereum contract used to interact with the blockchain.
- `amount`: The amount of tokens to be created.
- `address`: The address to which the tokens will be created.

<br/></details>


<details>
<summary>transferToEthWallet</summary>

### `transferToEthWallet(provider, contract, amount, address)`
Transfer tokens to the ETH wallet. This function allows the transfer of tokens from one address to another within the same blockchain.

- `provider`: The Ethereum provider used to interact with the blockchain.
- `contract`: The Ethereum contract used to interact with the blockchain.
- `amount`: The amount of tokens to be transferred.
- `address`: The address to which the tokens will be transferred.

<br/></details>


<details>
<summary>approveForBurn</summary>

### `approveForBurn(provider, contract, amount)`
Approve the token burn operation. This function grants permission for a specific amount of tokens to be burned.

- `provider`: The Ethereum provider used to interact with the blockchain.
- `contract`: The Ethereum contract used to interact with the blockchain.
- `amount`: The amount of tokens to be transferred.

<br/></details>


<details>
<summary>burnTokens</summary>

### `burnTokens(provider, contract, amount)`
Burn tokens from the wallet. This function destroys a specified amount of tokens, permanently removing them from circulation.

- `provider`: The Ethereum provider used to interact with the blockchain.
- `contract`: The Ethereum contract used to interact with the blockchain.
- `amount`: The amount of tokens to be transferred.

</details><br/>


## [event-watcher.js](link)

<details>
<summary>handleEthEvent</summary>

### `handleEthEvent(event, provider, contract)`
Handles events related to the Ethereum blockchain. It verifies token transfers in a contract and performs minting of the received tokens.

- `event`: The event related to the token transfer.
- `provider`: The Ethereum provider used to interact with the blockchain.
- `contract`: The Ethereum contract used to interact with the blockchain.

The `handleEthEvent` function is called when an event related to the source blockchain is triggered.

<br/></details>


<details>
<summary>handleDestinationEvent</summary>

### `handleDestinationEvent(event, provider, contract, providerDest, contractDest)`
Handles events related to the destination blockchain. It verifies token transfers in a destination contract and executes the burn and transfer back operations to the source chain.

- `event`: The event related to the token transfer.
- `provider`: The Ethereum provider used to interact with the Ethereum blockchain.
- `contract`: The Ethereum contract used to interact with the Ethereum blockchain.
- `providerDest`: The Ethereum provider used to interact with the destination blockchain.
- `contractDest`: The Ethereum contract used to interact with the destination blockchain.

The `handleDestinationEvent` function is called when an event related to the destination blockchain is triggered.

<br/></details>

## Web