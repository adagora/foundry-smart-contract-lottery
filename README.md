## Proveably Random Raffle Contracts

## What we want it to do?

1. Users can enter by paying for a ticket

- The ticket fees are going to go to the winner during the draw

2. After X period of time, the lottery will automatically draw a winner

- And this will be done programmatically

3. Using chainlink VRF & Chainlink Automation

- Chailink VRF -> Randomness
- Chainlink Automation -> Time based trigger

## Deployment to a testnet or mainnet

1. Setup environment variables You'll want to set your SEPOLIA_RPC_URL and
   PRIVATE_KEY as environment variables. You can add them to a .env file,
   similar to what you see in .env.example.

PRIVATE_KEY: The private key of your account (like from metamask). NOTE: FOR
DEVELOPMENT, PLEASE USE A KEY THAT DOESN'T HAVE ANY REAL FUNDS ASSOCIATED WITH
IT.

SEPOLIA_RPC_URL: This is url of the sepolia testnet node you're working with.
You can get setup with one for free from Alchemy Optionally, add your
ETHERSCAN_API_KEY if you want to verify your contract on Etherscan.

Get testnet ETH Head over to faucets.chain.link and get some testnet ETH. You
should see the ETH show up in your metamask.

2.Deploy

```bash
make deploy ARGS="--network sepolia"
```

This will setup a ChainlinkVRF Subscription for you. If you already have one,
update it in the scripts/HelperConfig.s.sol file. It will also automatically add
your contract as a consumer.

3. Register a Chainlink Automation Upkeep You can follow the documentation if
   you get lost.
   https://docs.chain.link/chainlink-automation/compatible-contracts

Go to automation.chain.link and register a new upkeep. Choose Custom logic as
your trigger mechanism for automation.

## Scripts

Using cast deployed locally example:

```bash
cast send <RAFFLE_CONTRACT_ADDRESS> "enterRaffle()" --value 0.1ether --private-key <PRIVATE_KEY> --rpc-url $SEPOLIA_RPC_URL
```

or, to create a ChainlinkVRF Subscription:

```bash
make createSubscription ARGS="--network sepolia"
```

## Testing

```bash
forge test
forge test --coverage
```
