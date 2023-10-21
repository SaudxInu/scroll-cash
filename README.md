# Scroll Cash

Scroll Cash is a non-custodial Ethereum privacy solution based on zkSNARKs. It improves transaction privacy by breaking the on-chain link between the recipient and destination addresses. It uses a smart contract that accepts ETH deposits that can be withdrawn by a different address. Whenever ETH is withdrawn by the new address, there is no way to link the withdrawal to the deposit, ensuring complete privacy.

To make a deposit user generates a secret and sends its hash (called a commitment) along with the deposit amount to the Tornado smart contract. The contract accepts the deposit and adds the commitment to its list of deposits.

Later, the user decides to make a withdrawal. To do that, the user should provide a proof that he or she possesses a secret to an unspent commitment from the smart contract’s list of deposits. zkSnark technology allows that to happen without revealing which exact deposit corresponds to this secret. The smart contract will check the proof and transfer deposited funds to the address specified for withdrawal. An external observer will be unable to determine which deposit this withdrawal came from.

The contract addresses are listed below.

- **ETHScrollCash** (Main/Entry Point Contract): 0x15579a94E6896204Ded100CB29aD7dDe0bB1F0C1
- Hasher: 0x3B29e0Ceb0EF42d428f2f0762c15bc15F66D7aae
- Verifier: 0xA4933c0475D014212210909089dBe25e7539D83D

## Requirements

1. `node v11.15.0`
2. `npm install -g npx`

## Usage

### Testing

1. `npm install`
2. `cp .env.example .env`
3. `npm run download`
4. `npx ganache-cli`
5. `npm run test`

### Initialization

1. `cp .env.example .env`
2. `npm run download`

### Ganache

1. Make sure you complete steps from Initialization
2. `ganache-cli -i 1337`
3. `npm run migrate:dev`
4. `./cli.js test`
5. `./cli.js --help`

### Scroll Sepolia

Example:

```bash
node src/cli.js deposit ETH 0.1 --rpc https://misty-boldest-friday.scroll-testnet.quiknode.pro/xxxx/
```

> Your note: tornado-eth-0.1-534351-0xa1d91bc6e5cd1413d980a68978ddda759d7d6456fbdfd70f226ed24d41286d7d63e869da9400aaca6fdedc8ab1a2721b35c218f16ab01c21288f586fefdd
>
> Tornado ETH balance is 0
>
> Sender account ETH balance is 0.686153504755413117
>
> Submitting deposit transaction
>
> Tornado ETH balance is 0.1
>
> Sender account ETH balance is 0.585057035955328799

```bash
node src/cli.js withdraw tornado-eth-0.1-534351-0xa1d91bc6e5cd1413d980a68978ddda759d7d6456fbdfd70f226ed24d41286d7d63e869da9400aaca6fdedc8ab1a2721b35c218f16ab01c21288f586fefdd 0x1bc996F1A9af4F7b90e703D8e0c13995442d13EF --rpc https://misty-boldest-friday.scroll-testnet.quiknode.pro/xxxx/
```

> Getting current state from tornado contract
>
> Generating SNARK proof
>
> Proof time: 6.270s
>
> Submitting withdraw transaction
>
> The transaction hash is 0x549e9e6bf8cf0673beb1d77bb492d75d03c151b58a88edb9dbb1c7309c8e6bd7
>
> Done

## Deploy ETH Scroll Cash

1. `cp .env.example .env`
2. `npx truffle migrate --network scrollSepolia --reset --f 2 --to 4`

## Credits

Special thanks to [Tornado Cash](https://github.com/tornadocash).

> **_NOTE:_** Scroll Cash is a fork of [Tornado Cash](https://tornado.cash/audits/TornadoCash_whitepaper_v1.4.pdf) on Scroll.
