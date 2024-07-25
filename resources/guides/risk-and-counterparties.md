---
description: >-
  A guide to the various counterparties that make up the Alchemix system and the
  risk each counterparty takes on.
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

# ⚠️ Risk & Counterparties

The purpose of this article is to go over the risks that various types of users of the Alchemix system take on when the system is functioning as intended. This list is not intended to be exhaustive, as certain risks are inherent to DeFi and Crypto in general, such as smart contract risk. For information about other types of risks, see [Multisig Admin Rights](https://alchemix-finance.gitbook.io/user-docs/alchemix-dao/the-alchemix-dao/governance-process/multisig-admin-rights), [Audits](https://alchemix-finance.gitbook.io/user-docs/resources/audits-and-reports), and [Vault Losses and Collateral De-pegging](https://alchemix-finance.gitbook.io/user-docs/resources/guides/vault-losses-and-collateral-de-pegging).

## Depositors (Borrowers) <a href="#depositors-borrowers" id="depositors-borrowers"></a>

Depositors provide collateral to the yield strategies in the Alchemists in order to take alAsset loans. Unless a depositor also wishes to act as a liquidity provider, they will typically swap their alAsset to another asset soon after taking the loan. Therefore, they are not exposed to the price of alAssets over time.

The primary risk a depositor takes on is risk of having funds deposited in the underlying yield strategy, through Alchemix. If the strategy they deposit experiences a loss that exceeds the `maximumLoss` (a variable set by governance), then the yield strategy will be paused. This means users may not make any deposits, may not liquidate or repay, and may not take a new loan with this strategy. Harvests will also be disabled. Lastly, users will be unable to withdraw collateral in the form of the underlying asset. Users will still be able to repay their loan and withdraw the yield token, however. For example if the `maximumLoss` was exceeded, a user could not withdraw DAI from a strategy that uses yDAI, but they would still be able to repay their loan with DAI to withdraw their yDAI collateral).

In the scenario of an underlying strategy suffering a majority loss of funds (ie, greater than 50% of the strategy), then the user would actually have bad debt with Alchemix (the value of their debt would exceed the value of their collateral). In this scenario, the user actually suffered less of a loss by using Alchemix.

Note some yield strategies may require selling yielded tokens to harvest yield. In this scenario, a temporary depeg of the value of the harvested token would result in the user experiencing reduced yield for the period of time the token remains depegged. For more an examples of the protocol handles collateral depeg events and vault losses, see [Vault Losses and Collateral De-pegging](https://alchemix-finance.gitbook.io/user-docs/resources/guides/vault-losses-and-collateral-de-pegging).

## Liquidity Providers / Transmuter Users <a href="#liquidity-providers-transmuter-users" id="liquidity-providers-transmuter-users"></a>

alAsset liquidity providers are exposed to price fluctuations of alAssets. They create the liquidity for users to sell their alAssets for other tokens. alAssets can only be redeemed for underlying collateral in three ways:

1. Loan repayment (instant, 1 alAsset = 1 asset)
2. Selling through a liquidity pool (instant, price will fluctuate)
3. Depositing in the Transmuter (timeline is uncertain, 1 alAsset = 1 asset)

A liquidity provider / alUSD holder that does not have an Alchemix position in a yield strategy does not have option 1 at their disposal. A liquidity provider has three primary steps to consider when providing liquidity:

1. Price / balance of liquidity pool when entering the pool
2. Yield earned from providing liquidity over the life of the liquidity provision
3. Price / balance of liquidity pool when leaving the pool

If the balance of the pool moves favorably for the LPer over time, they can earn yield as well as a net positive slippage from the difference between their exit and entry position. If the balance of the pool moves unfavorably, then the net negative slippage would be subtracted from the yield earned during their liquidity provision over time.

A user can hedge this exposure by using the Transmuter, or by being a depositor within Alchemix. If the alAsset pool shifts less favorably for the depositor/LPer, they can withdraw alUSD instead of stablecoins for a bonus positive slippage and repay their debt. They could also use the same approach with the Transmuter, at the opportunity cost of waiting for the collateral to flow into the Transmuter. See [Transmuter](https://alchemix-finance.gitbook.io/user-docs/alchemix-ecosystem/transmuter) and [The Transmuter, Elaborated](https://alchemix-finance.gitbook.io/user-docs/resources/guides/the-transmuter-elaborated) for more information on how the Transmuter distributes collateral to alAsset stakers.

Lastly, alAssets could become undercollateralized if a large enough loss of funds of an underlying yield strategy occurred, as detailed in the [Depositors (Borrowers)](risk-and-counterparties.md#depositors-borrowers) section.

## Alchemix DAO and ALCX Holders <a href="#alchemix-dao-and-alcx-holders" id="alchemix-dao-and-alcx-holders"></a>

As mentioned above, it is possible for bad debt to exist in Alchemix if a yield strategy suffers a significant loss of funds. Because ALCX liquidity and single staking pools are not locked, Alchemix cannot currently slash stakers to make the protocol whole. In the scenario of a full yield strategy loss above, the treasury could sell ALCX or other assets from the treasury to make the protocol whole if decided by governance, which would dilute ALCX holders.

<figure><img src="../../.gitbook/assets/header_02_test.png" alt=""><figcaption></figcaption></figure>
