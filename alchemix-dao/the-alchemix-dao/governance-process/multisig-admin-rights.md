---
cover: ../../../.gitbook/assets/header_02_test.png
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

# 🧙‍♂️ Multisig Admin Rights

## Multisig Admin Rights

### Access Control <a href="#access-control" id="access-control"></a>

#### Alchemist Contracts <a href="#alchemist-contracts" id="alchemist-contracts"></a>

Alchemist contracts for alUSD and alETH allow the user to create a debt position by depositing tokens as collateral and taking debt against the collateral by minting alUSD or alETH.

Each Alchemist Contract has the following privileged roles: Admin, Sentinel, and Keeper, with the following privileges:

1. **Admin**
   * Add tokens to the list of underlying and yield tokens supported by the Alchemist
   * Enable and disable tokens from this list
   * Add and remove sentinels and keepers
   * Transfer the admin role to a different address (must be accepted by the new admin)
   * Configure the Alchemist's parameters, including limits, fees, and the addresses of the Transmuter and protocol fee receiver
   * Reset ("snap") the expected value of a yield token to the current value. Since deposits, withdrawals of the underlying, and liquidations are blocked if the value of a yield token suddenly drops significantly below its expected value, this can prevent the contract from becoming unusable if the yield token doesn't recover, or takes too long to recover.
   * Disable or enable whitelisting requirements
2. **Sentinel**
   * Sentinels can disable (ie, pause) underlying and yield tokens. `pauseUnderlyingToken()` will disable `deposit()`, `depositUnderlying()`, `repay()`, and `liquidate()` functionality for the given underlying token. `pauseYieldToken()` will disable `deposit()`, `depositUnderlying()`, `withdraw()`, `withdrawUnderlying()`, `liquidate()` , and `harvest()`for the given yield token (ie, given yield strategy). See Pause Control below for more information.
3. **Keeper**
   * Keepers can trigger harvests of the yield tokens.

### Upgradeability <a href="#upgradeability" id="upgradeability"></a>

One major design choice of note in Alchemix v2 is upgradeability. All 3 major contracts (AlchemistV2, TransmuterV2, and TransmuterBuffer) are built to be used via upgradeable proxies. This entrusts the Alchemix DAO with the ability and responsibility to upgrade the functionality whenever needed.

### Pause Control <a href="#pause-control" id="pause-control"></a>

Sentinels have the ability to pause yield tokens should there be an issue. Admins may then unpause the tokens. When an underlying token is disabled, it should be noted that the `withdraw()`, `withdrawUnderlying()`, `repay()`, `mint()`, and `burn()` (ie, repay debt with alAssets) functions can still be called - allowing users to settle their debt and withdraw the yield token or underlying token.

Each accepted yield token has a configured maximum amount of loss that it can experience and still function normally. If the yield strategy loses more than the specified `maximumLoss`, then the yield strategy is paused automatically, meaning users may not make any deposits, may not liquidate or repay, and may not take a new loan with these strategies. Harvests will also be disabled. Lastly, users will be unable to withdraw collateral as the underlying asset. However, they will still be able to repay their loan and withdraw the yield token. For example, if the `maximumLoss` were exceeded, a user could not withdraw DAI from a strategy that uses yDAI. However, they could still repay their loan with DAI to withdraw their yDAI collateral.

Sentinels also have the ability to pause underlying tokens if issues arise. This applies only to alAssets with multiple underlying tokens, such as alUSD.If an underlying token is paused, the `deposit()`, `depositUnderlying()`, `liquidate()`, and `repay()` functions would be disabled for that token. Notably, debts may still be paid down by harvests and users may repay debt with alAssets or other underlying tokens and withdraw their funds.

### Multisigs, Timelock, and veALCX <a href="#multisigs-timelock-and-vealcx" id="multisigs-timelock-and-vealcx"></a>

The Alchemix Developer Multisig serves as the administrator for the Alchemix contracts and manages the protocol’s operational budget. Separately, the timelock multisig holds the majority of DAO-owned ALCX and owns the sweep functions of the AMO contracts (i.e., AMO funds can only be removed from the AMO contracts by the timelock multisig). The timelock is currently 600 seconds, reduced from 24 hours in response to the July 30th Curve Exploit. In the future, the timelock will likely be retired and all admin controls will be assigned to a mix of veALCX and the dev multisig, with a goal of shifting more power to veALCX and away from the dev multisig over time.

### More Information <a href="#more-information" id="more-information"></a>

For more in-depth information on admin controls and contract features, see the [v2 audit](https://github.com/runtimeverification/publications/blob/main/reports/smart-contracts/Alchemix\_v2.pdf) and [developer docs](https://alchemix-finance.gitbook.io/v2/).

<figure><img src="../../../.gitbook/assets/header_02_test (1).png" alt=""><figcaption></figcaption></figure>
