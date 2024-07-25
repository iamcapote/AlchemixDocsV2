---
cover: ../../.gitbook/assets/header_02_test.png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 🏦 Vault Losses and Collateral De-pegging

Vault losses and collateral de-pegging events are two scenarios that can create a loss of alAsset backing, thus jeopardizing the health of the protocol. Vault losses are caused by the underlying yield strategy returning less of the underlying token than expected - for example, a strategy that is meant to earn 10% APR on ETH suddenly only being worth 0.9 ETH per 1 ETH deposited. Collateral de-pegging is caused by the underlying collateral being worth less than its expected value. This is only applicable to alUSD as it is the only alchemist that accepts multiple collateral types. For example, if USDT were to be worth $0.9 relative to DAI and USDC each being worth $1. This is not relevant to ETH as 1 ETH will always be worth 1 ETH.

Vault losses are handled automatically through the `maxloss()` parameter. Collateral de-pegging is handled manually through sentinels' ability to pause tokens (see [Multisig Admin Rights](https://alchemix-finance.gitbook.io/user-docs/alchemix-dao/the-alchemix-dao/governance-process/multisig-admin-rights)). See below for an example scenario where a yield-bearing asset experiences a 10% loss in underlying collateral, and another scenario where DAI drops to $0.80 relative to USDC and USDT.

### Vault Loss Scenario <a href="#vault-loss-scenario" id="vault-loss-scenario"></a>

**Scenario:** A yield-bearing asset experiences a loss in the underlying collateral. For this example, we will assume a 10% loss of DAI from the yvDAI vault that is unrecoverable.

After the transaction that causes the loss is committed to the chain, the `maxloss()` is triggered and the following happens:

* The following yvDAI Alchemist functions are automatically disabled:
  * `deposit()`
  * `depositUnderlying()`
  * `withdrawUnderlying()`
  * `withdrawUnderlyingFrom()`
  * `liquidate()`
  * `harvest()`
* The following yvDAI Alchemist functions are still useable:
  * `withdraw()`
  * `withdrawFrom()`
  * `repay()`
  * `mint()`
  * `burn()`

**Resolution:** In order to re-enable the disabled functions, the following needs to happen:

1. A proposal is created to call `snap()` on the Alchemist, targeting the yvDAI vault.
2. A vote takes place (we assume it passes)
3. `snap()` is called on the Alchemist, which accepts the 10% loss and resets the expected value of those yield tokens held in the Alchemist

**Damage:** The maximum damage is the total amount of funds lost from the vault. alUSD will still be overcollateralized and depositors will experience the loss, the same way they would experience the loss if they held the tokens outside of Alchemix or if they used `withdraw()` after `maxloss()` was triggered. The effective rate of yield flow to the transmuter buffer would also be slightly slower, as there would be slightly less collateral in the system earning yield relative to the alAsset supply. Note that if a loss of >50% were realized, this could lead to a loss in backing for alUSD.

While the risk of a vault losing collateral is low, the damage is still significant. However, Alchemix does not control the operations of 3rd party vaults, so the only way to minimize the risk is to carefully consider which yield-bearing strategies are added.

**Necessary Response Time:** The response time for this scenario does not need to be necessarily fast, because the functions that are affected by a vault loss will be automatically disabled. The team and the DAO should assess the loss to make sure that it is unrecoverable before taking the governance steps to remedy the situation by calling `snap()`.

### Collateral De-pegging <a href="#collateral-de-pegging" id="collateral-de-pegging"></a>

**Scenario:** One collateral token used by the Alchemist experiences a severe de-pegging against other collateral. For this example, we will assume DAI drops to 80 cents vs USDC & USDT. alUSD maintains its peg against USDC & USDT.

This de-pegging presents multiple arbitrage opportunities:

1. Users can buy DAI off the market, deposit it into the Alchemist, take a loan, and repeat this loop until the minting cap is reached.
2. Users can buy DAI off the market and use it to repay their loans until the repay cap is reached.
3. Users can liquidate their current yDAI position (paying off their outstanding debt at a discount), buy more DAI with their loan, deposit it into the Alchemist, take a loan, and repeat until the liquidation cap is reached.

These arbitrage opportunities will likely result in one or more of the mint / repay / liquidate caps being met.

**Resolution:** The only resolution that matters is getting DAI to reach peg again. This can take multiple avenues.

* The peg could re-stabilize on its own without any intervention.
* The collateral in question can be disabled by a sentinel or admin, buying the peg more time to re-stabilize. This would disable the following functions:
  * `deposit()`
  * `depositUnderlying()`
  * `repay()`
  * `liquidate()`

**Damage:** The de-pegging of DAI results in the price of the alAsset dropping towards the de-pegged asset. The sentinels exist to disable underlying tokens as soon as they experience a de-pegging event. The repay, liquidate, and mint caps are in place to limit the amount of de-pegging of the synthetic asset that can occur prior to sentinel action.

**Risk:** Given the interconnected nature of underlying collateral tokens and DeFi at large, there will likely be consistent, small arbitrage opportunities between collaterals and their pegged synthetics. In times of high volatility, these arbitrage opportunities can get exasperated as assets experience larger and longer de-pegging events. As a result, there is some risk that the repay/liquidate/mint caps get reached.

Note that if the peg does not restabilize, DAI would remain paused; there will be a loss in the backing of alUSD. The DAO will need to determine how to proceed in this scenario.

**Necessary Response Time:** The faster a sentinel can respond by disabling the de-pegged underlying token, the less the price of alAsset will be arbitraged down.

<figure><img src="../../.gitbook/assets/header_02_test.png" alt=""><figcaption></figcaption></figure>
