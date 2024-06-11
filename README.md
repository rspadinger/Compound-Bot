# Compound Liquidation Bot

A continuously running script that liquidates Compound III accounts that violate collateral requirements.

## Resources:

* Find current Comet borrower accounts : https://alchemy.com/
* Test liquidation txns before submitting them to the blockchain with Alchemy Transact: https://docs.alchemy.com/reference/transact-api-quickstart
* Notify - mined txn webhook: https://docs.alchemy.com/reference/mined-transaction-webhook
* Autocode webhook listens for the http request and sends an email via SendGrid to the liquidator: https://autocode.com 
* Compount Finance - Comet: https://github.com/compound-finance/comet
* Compound Comet Liquidation guide: https://www.comp.xyz/t/the-compound-iii-liquidation-guide/3452
 
## Install

```
yarn install
yarn build
```

### Autocode

Set up the webhook (`autocode/index.js`) after setting up the Alchemy Notify Mined Transaction Webhook: https://docs.alchemy.com/reference/mined-transaction-webhook.

### SendGrid

Send email alerts when a transaction is mined: https://sendgrid.com

## Liquidator Contract Deployments

The liquidator contract (`./contracts/OnChainLiquidator.sol`) is deployed and verified. Any caller of the contract can initalize a liquidation and receive the resulting excess base asset tokens if a liquidation transaction is successful.

```
arbitrum: '0x18A715c11Cf4ed6A0cf94FCc93a290d4b2d14dD7'
polygon: '0xbf4555f5c127479b225332cd5520cd54c68f814c'
mainnet: '0xC70e2915f019e27BAA493972e4627dbc0ED7a794'
```

## Test Run

This command will run the liquidation bot but it will not try to liquidate borrowers, it will use Alchemy Transact simulation to estimate the arbitrage transaction results using: https://docs.alchemy.com/reference/simulation-asset-changes 

Polygon example:

```
Provide the following .env variables: 

ALCHEMY_KEY="YOUR_ALCHEMY_API_KEY" \
DEPLOYMENT="usdc" \
LIQUIDATOR_ADDRESS="0xbf4555f5c127479b225332cd5520cd54c68f814c" \
USE_FLASHBOTS="false" \
ETH_PK="YOUR_PRIVATE_EVM_ACCOUNT_KEY" \
TESTRUN="true" \

npx hardhat run scripts/liquidation_bot/index.ts --network polygon
```

## Production Run

Same as above, simply remove the `TESTRUN` environment variable.

```
ALCHEMY_KEY="YOUR_ALCHEMY_API_KEY" \
DEPLOYMENT="usdc" \
LIQUIDATOR_ADDRESS="0xbf4555f5c127479b225332cd5520cd54c68f814c" \
USE_FLASHBOTS="false" \
ETH_PK="YOUR_PRIVATE_EVM_ACCOUNT_KEY" \

npx hardhat run scripts/liquidation_bot/index.ts --network polygon
```
