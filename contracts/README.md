# Liquidation bot

Arbitrage  with Compound III => uses Uniswap flash loans to purchase discounted collateral assets from underwater accounts

1. Absorbs collateral positions.
2. Borrows base token from given Uniswap pool using flashswap functionality.
3. Buys discounted collateral from protocol.
4. Exchanges collateral assets into base token using other Uniswap pools.
5. Pays back flash loan.
6. Sends profit in base token to the caller of Liquidator contract.


Uniswap Flash Swaps: [uniswap/flash-swaps](https://docs.uniswap.org/protocol/guides/flash-integrations/inheritance-constructors).
