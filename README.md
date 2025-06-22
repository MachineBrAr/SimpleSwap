# SimpleSwap: A Uniswap V2-style AMM DEX

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Description

SimpleSwap is a decentralized exchange (DEX) smart contract built on the Ethereum blockchain. It functions as an Automated Market Maker (AMM) using the constant product formula (`x * y = k`), similar to Uniswap V2. The contract allows users to swap ERC-20 tokens, provide liquidity to earn fees, and remove their liquidity at any time.

This project is designed with security, clarity, and strict adherence to common interface standards as top priorities, making it a robust foundation for decentralized finance applications.

## Key Features & Design Philosophy

This contract was built to meet high standards of quality and security:

* **Security First**: Inherits from OpenZeppelin's battle-tested contracts, including `Ownable`, `Pausable`, `ReentrancyGuard`, and `Math`. This provides built-in protection against common vulnerabilities.
* **Uniswap V2 Model**: Implements the well-established constant product formula for token pricing and a standard 0.3% trading fee, which is distributed to liquidity providers.
* **Multi-Hop Swaps**: The `swapExactTokensForTokens` function supports routing trades through multiple liquidity pools to find the best possible price.
* **Slippage Protection**: All trading and liquidity functions include parameters (`amountOutMin`, `amountAMin`, etc.) to protect users from price volatility during transaction confirmation.
* **Deadline Protection**: All state-changing functions include a `deadline` parameter to prevent transactions from being maliciously held and executed later at an unfavorable price.
* **NatSpec Documentation**: The entire codebase is thoroughly documented using the Ethereum Natural Language Specification (NatSpec) format for maximum clarity and interoperability with developer tools.

## Contract Public Interface

The primary functions for interacting with the SimpleSwap DEX are:

* `addLiquidity`: Adds liquidity to a token pair pool and mints LP units for the provider.
* `removeLiquidity`: Burns LP units and allows the provider to withdraw their share of the underlying tokens.
* `swapExactTokensForTokens`: Swaps an exact amount of an input token for another. Returns an array containing the input amount and the final output amount.
* `getPrice`: A view function to get the spot price of one token in terms of another, scaled by `1e18`.
* `getAmountOut`: A pure function to calculate how many output tokens will be received for a given input amount and known reserves.
* `getAmountOutByTokens`: A helper view function that reads pool reserves directly to calculate the output of a potential swap.
* `getReserves`: A view function to retrieve the current liquidity reserves for a token pair.

## Development & Environment

This project is intended to be used with a standard Solidity development environment like Hardhat.

### Prerequisites

* [Node.js](https://nodejs.org/en/) (`>=18.0.0`)
* [NPM](https://www.npmjs.com/) or [Yarn](https://yarnpkg.com/)

### Getting Started

1.  **Clone the repository:**
    ```bash
    git clone <YOUR_REPOSITORY_URL>
    cd simpleswap-dex
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    ```

3.  **Create an environment file:**
    Create a `.env` file in the project root by copying the example file:
    ```bash
    cp .env.example .env
    ```
    Then, fill in the required values:
    ```
    # Your private key for deployment (e.g., from MetaMask)
    PRIVATE_KEY="YOUR_WALLET_PRIVATE_KEY"

    # RPC URL for the network you want to deploy to (e.g., from Infura or Alchemy)
    SEPOLIA_RPC_URL="[https://sepolia.infura.io/v3/YOUR_INFURA_PROJECT_ID](https://sepolia.infura.io/v3/YOUR_INFURA_PROJECT_ID)"

    # Your Etherscan API key for contract verification
    ETHERSCAN_API_KEY="YOUR_ETHERSCAN_API_KEY"
    ```

## Core Commands (Hardhat)

* **Compile Contracts:**
    ```bash
    npx hardhat compile
    ```

* **Run Tests:**
    *(Assuming tests are located in the `/test` directory)*
    ```bash
    npx hardhat test
    ```

* **Deploy Contract:**
    *(Assuming a deploy script is located at `scripts/deploy.js`)*
    ```bash
    npx hardhat run scripts/deploy.js --network sepolia
    ```

* **Verify on Etherscan:**
    After deployment, use the contract address printed to the console to verify it.
    ```bash
    npx hardhat verify --network sepolia <DEPLOYED_CONTRACT_ADDRESS>
    ```
    *(Constructor arguments, if any, should be added at the end).*

## License

This project is licensed under the MIT License. See the `SPDX-License-Identifier` in the contract file for details.
