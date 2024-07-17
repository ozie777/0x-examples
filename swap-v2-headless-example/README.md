# Swap v2 headless example (viem)

A headless example of how to use 0x Swap API v2 /permit2/price and /permit2/quote using [viem](https://viem.sh/)

Demonstrates the following on Base mainnet:

1. Build price params (sell 0.1 USDC → buy WETH) Fetch price.
2. Check token approval
3. Build quote params (sell 0.1 USDC → buy WETH). Fetch quote.
4. Send transaction.

> [!WARNING]  
> This is a demo, and is not ready for production use. The code has not been audited and does not account for all error handling. Use at your own risk.

#### Requirements

- Install [Bun](https://bun.sh/) (v1.1.0+)
- An Ethereum private key
- Setup a wallet with min 0.1 USDC and some ETH for gas

## Usage

1. Create an `.env` file and setup the required environment variables (your Etheruem private keys & 0x API key).

```sh
cp .env.example .env
```

2. Install dependencies

```sh
bun install
```

3. Run the script with either

```sh
# Run the script once
bun run index.ts
```

or

```sh
# Run the script in watch mode. Code automatically recompiles and re-executes upon changes.
bun --watch index.ts

```

4. Here is an example of the output. It fetches a `price` (sell 0.1 USCD → WETH), approves token allowance (if not already granted), fetches a `quote`, and submits the transaction, and shows the transaction hash:

```
Fetching price to swap 0.1 USDC for WETH
https://api.0x.org/swap/permit2/price?chainId=8453&sellToken=0x833589fcd6edb6e08f4c7c32d4f71b54bda02913&buyToken=0x4200000000000000000000000000000000000006&sellAmount=100000
priceResponse:  {
  blockNumber: "16891368",
  buyAmount: "32749774604489",
  buyToken: "0x4200000000000000000000000000000000000006",
  fees: {
    integratorFee: null,
    zeroExFee: {
      amount: "150",
      token: "0x833589fcd6edb6e08f4c7c32d4f71b54bda02913",
      type: "volume",
    },
    gasFee: null,
  },
  gas: "183866",
  gasPrice: "2500000",
  issues: {
    allowance: null,
    balance: null,
    simulationIncomplete: false,
    invalidSourcesPassed: [],
  },
  liquidityAvailable: true,
  minBuyAmount: "32422276858444",
  route: {
    fills: [
      {
        from: "0x833589fcd6edb6e08f4c7c32d4f71b54bda02913",
        to: "0x4200000000000000000000000000000000000006",
        source: "BaseSwap",
        proportionBps: "10000",
      }
    ],
    tokens: [
      {
        address: "0x833589fcd6edb6e08f4c7c32d4f71b54bda02913",
        symbol: "USDC",
      }, {
        address: "0x4200000000000000000000000000000000000006",
        symbol: "WETH",
      }
    ],
  },
  sellAmount: "99850",
  sellToken: "0x833589fcd6edb6e08f4c7c32d4f71b54bda02913",
  totalNetworkFee: "490472989917",
}
USDC already approved for Permit2
Fetching quote to swap 0.1 USDC for WETH
quoteResponse:  {
  blockNumber: "16891369",
  buyAmount: "32749774604489",
  buyToken: "0x4200000000000000000000000000000000000006",
  fees: {
    integratorFee: null,
    zeroExFee: {
      amount: "150",
      token: "0x833589fcd6edb6e08f4c7c32d4f71b54bda02913",
      type: "volume",
    },
    gasFee: null,
  },
  issues: {
    allowance: null,
    balance: null,
    simulationIncomplete: false,
    invalidSourcesPassed: [],
  },
  liquidityAvailable: true,
  minBuyAmount: "32422276858444",
  permit2: {
    type: "Permit2",
    hash: "0xd5a381b2d7270d8f8693441a3ca33f06480eb7a05117b0117c53fc518942f6b9",
    eip712: {
      types: {
        PermitTransferFrom: [
          {
            name: "permitted",
            type: "TokenPermissions",
          }, {
            name: "spender",
            type: "address",
          }, {
            name: "nonce",
            type: "uint256",
          }, {
            name: "deadline",
            type: "uint256",
          }
        ],
        EIP712Domain: [
          {
            name: "name",
            type: "string",
          }, {
            name: "chainId",
            type: "uint256",
          }, {
            name: "verifyingContract",
            type: "address",
          }
        ],
        TokenPermissions: [
          {
            name: "token",
            type: "address",
          }, {
            name: "amount",
            type: "uint256",
          }
        ],
      },
      domain: {
        name: "Permit2",
        chainId: 8453,
        verifyingContract: "0x000000000022d473030f116ddee9f6b43ac78ba3",
      },
      message: {
        permitted: {
          token: "0x833589fcd6edb6e08f4c7c32d4f71b54bda02913",
          amount: "100000",
        },
        spender: "0x55873e4b1dd63ab3fea3ca47c10277655ac2dce0",
        nonce: "2241959297937691820908574931991586",
        deadline: "1720572385",
      },
      primaryType: "PermitTransferFrom",
    },
  },
  route: {
    fills: [
      {
        from: "0x833589fcd6edb6e08f4c7c32d4f71b54bda02913",
        to: "0x4200000000000000000000000000000000000006",
        source: "BaseSwap",
        proportionBps: "10000",
      }
    ],
    tokens: [
      {
        address: "0x833589fcd6edb6e08f4c7c32d4f71b54bda02913",
        symbol: "USDC",
      }, {
        address: "0x4200000000000000000000000000000000000006",
        symbol: "WETH",
      }
    ],
  },
  sellAmount: "99850",
  sellToken: "0x833589fcd6edb6e08f4c7c32d4f71b54bda02913",
  totalNetworkFee: "490472989917",
  transaction: {
    to: "0x55873e4b1dd63ab3fea3ca47c10277655ac2dce0",
    data: "0x1fff991f00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000a09984987dddf5ad699c63dbe500000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000003000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000001e000000000000000000000000000000000000000000000000000000000000003400000000000000000000000000000000000000000000000000000000000000144c1fb425e00000000000000000000000055873e4b1dd63ab3fea3ca47c10277655ac2dce0000000000000000000000000833589fcd6edb6e08f4c7c32d4f71b54bda0291300000000000000000000000000000000000000000000000000000000000186a00000000000000000000000000000000000006e898131631616b1779bad70bc2200000000000000000000000000000000000000000000000000000000668dd9e100000000000000000000000000000000000000000000000000000000000000c00000000000000000000000000000000000000000000000000000000000000041ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000012438c9c147000000000000000000000000833589fcd6edb6e08f4c7c32d4f71b54bda02913000000000000000000000000000000000000000000000000000000000000000f000000000000000000000000833589fcd6edb6e08f4c7c32d4f71b54bda02913000000000000000000000000000000000000000000000000000000000000002400000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000000044a9059cbb000000000000000000000000ad01c20d5886137e056775af56915de824c8fce50000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000c4103b48be0000000000000000000000004d2a422db44144996e855ce15fb581a477dbb947000000000000000000000000833589fcd6edb6e08f4c7c32d4f71b54bda029130000000000000000000000000000000000000000000000000000000000002710000000000000000000000000ab067c01c7f5734da168c699ae9d23a4512c9fdb000000000000000000000000000000000000000000000000000000000000190000000000000000000000000000000000000000000000000000001d7ce64b824c00000000000000000000000000000000000000000000000000000000",
    gas: "183866",
    gasPrice: "2500000",
    value: "0",
  },
}
Signed permit2 message from quote response
Transaction hash: 0xcb9ec3b8ef7002f9fa232fa23f16a0ba365a1c1d48580f420977a1b20c86ab78
See tx details at https://basescan.org/tx/0xcb9ec3b8ef7002f9fa232fa23f16a0ba365a1c1d48580f420977a1b20c86ab78
```