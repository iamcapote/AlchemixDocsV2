---
cover: ../.gitbook/assets/header_02_test.png
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

# 🧪 Elixir AMO

The Elixir AMO is a liquidity management tool designed to take advantage of the funds built up by the Transmuter. Excess underlying assets in the Transmuter are sent to third-party liquidity pools via the Elixir AMO to rebalance the alAsset price and generate yield.

The Elixir AMO removes assets from the liquidity pool when they fall below a target price, stabilizing the alAssets. The Elixir AMO enhances the sustainability of the Alchemix protocol by generating additional revenue streams and providing an additional lever for managing the system.

<figure><img src="../.gitbook/assets/01_02 (5).png" alt=""><figcaption></figcaption></figure>

## Key Features

### **Automated Market Operator**

The Elixir AMO automates liquidity management by deploying excess funds from the Transmuter into yield strategies, effectively rebalancing liquidity pools.



### **Price Stabilization**

The Elixir AMO can withdraw alAssets to stabilize prices when they fall below the target price, helping to mitigate volatility and increase stability.



### **Revenue Generation**

Deposits into liquidity pools to generate additional revenue for the protocol.



### **Flexible Withdrawal Mechanism**

The Elixir AMO offers the flexibility to withdraw alAssets and remove them from circulation when necessary, providing faster-acting influence over the alAsset supply than the Transmuter alone can offer.



### **Sustainability**

By enhancing alAsset management and generating additional revenue streams, the Elixir AMO contributes to the long-term sustainability of the Alchemix ecosystem.

<figure><img src="../.gitbook/assets/PlainLine_01.png" alt=""><figcaption></figcaption></figure>

## How it works

1. **Transmuter Accumulation:** Excess funds accumulate in the Transmuter.
2. **Transfer to Elixir AMO:** When significant, these funds are deployed to the Elixir AMO.
3. **Elixir AMO Deposits:** The Elixir AMO deposits the funds into corresponding liquidity pools, rebalancing the pools and increasing the alAsset prices.
4. **Yield Generation:** Yield generated from these deposits (such as CRV, CVX, or similar) creates additional revenue for the protocol.
5. **Removing Assets:** The AMO can also remove alAssets from circulation as a faster-acting method of influencing alAsset supply and price.

{% hint style="info" %}
For detailed information on how it works, see [The AMO: The Elixir](../resources/guides/the-amo-the-elixir.md).
{% endhint %}

<figure><img src="../.gitbook/assets/header_02_test.png" alt=""><figcaption></figcaption></figure>
