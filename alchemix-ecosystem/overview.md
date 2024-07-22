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

# 🔮 Overview

## How does Alchemix work? <a href="#what-does-alchemix-do" id="what-does-alchemix-do"></a>

Picture a bank where you deposit your assets and watch them grow via interest.&#x20;

Now imagine that in addition to earning interest, the bank allows you to access an instant credit line without the burden of interest payments or liquidation risks, and the interest you earn repays your debt automatically.

Alchemix is like your personal DeFi bank that you control - where deposited assets generate yield that automatically pays off any debt accrued and increases your credit.

With Alchemix, your collateral becomes your credit card, allowing you to spend a portion of your assets upfront, all while your accrued interest effortlessly repays any borrowed amounts over time.



> _**There's no interest on the debt.**_
>
> _**There are no monthly payments to make.**_
>
> _**There are no liquidations.**_



Alchemix offers an innovative DeFi protocol that provides self-repaying, interest-free, non-liquidating loans - giving you the freedom to do more with your capital.

{% hint style="info" %}
For detailed information and to learn how it works, see [Components](overview.md#the-components-of-alchemix), [How-to](../resources/how-to/), and [Guides and Explainers.](../resources/guides/)
{% endhint %}

<figure><img src="../.gitbook/assets/PlainLine_01.png" alt=""><figcaption></figcaption></figure>

## How to use Alchemix <a href="#how-do-i-use-it" id="how-do-i-use-it"></a>

<figure><img src="../.gitbook/assets/01_02 (1).png" alt=""><figcaption><p><strong>The Alchemical Flow.</strong> This graph shows the series of steps users take when using Alchemix.</p></figcaption></figure>

{% hint style="info" %}
Alchemix currently accepts diverse collateral types which are used to mint alAssets and take out loans. Keep up to date with all of the current yield strategies and liquidity incentives on the [Alchemix Statistics page](https://alchemix-stats.com/).
{% endhint %}

**Step 1: Deposit, Earn & Borrow**

* **Deposit:** Users can select a yield strategy and then deposit collateral (e.g., stablecoins or ETH) into that strategy, which will start harvesting yield with your deposit.
* **Borrow:** Users can choose to borrow up to the maximum collateral value. The borrow limit is determined by the collateral-to-debt ratio (defined as the collateral value over the loan value). The maximum allowed is a 2:1 collateral-to-debt ratio, which means users can borrow up to 50% of the quantity of the collateral in alAssets.&#x20;
* **Synthetic Assets:** alAssets are tokens that represent debt and the market price of alAssets fluctuates since it represents the future yield of the borrowed amount. The protocol treats alAssets as being equivalent to the underlying assets when borrowing and repaying debt

**Step 2: Market Swap**

* **Convert:** Swap alAssets to any other token via a DEX or DEX Aggregator. By design, alAssets can be priced at some discount relative to the underlying asset, so it is recommended to check the price of the alAsset before initiating a loan repayment. The discount can be viewed as the up-front cost to access your future yield today. alAssets can also be used directly on some DeFi protocols.
* **Spend:** You can do anything with the loan: buy more crypto, book a vacation, cash out savings, or any other way to spend money. Because there are no forced liquidations in Alchemix, you do not have to worry about being forced to repay your loan to avoid liquidation like many other lending protocols.&#x20;
* **Wait:** The user's chosen collateral yield strategy will go to work earning interest on the full initial deposit. The harvested yield token is used to pay down their debt automatically over time.

**Step 3: Withdraw & Repay**

* **Withdraw:** At any time, users can withdraw the principal amount (the amount deposited). The limits to withdrawals depend on the collateral-to-debt ratio. As long as a 2:1 ratio is maintained, users have two options: they can either wait for the yield from the chosen strategy to pay down the debt over time with the interest harvested, or they can use their deposited collateral to resolve their debt and self-liquidate.
* **Repay:** Users can repay their loans at any time with the respective alAsset or with the underlying asset. Users can also repay their debt at a discount by buying alAssets when they are trading lower on the broader market than when the loan was taken out.

<figure><img src="../.gitbook/assets/02_03.png" alt=""><figcaption><p><strong>The Components of Alchemix.</strong> This graph shows the Alchemical Flow along with the components of the platform. Users interact with a diverse group of smart contracts in order to interact with Alchemix.</p></figcaption></figure>

## Learn more about Alchemix

> * [guides](../resources/guides/ "mention")
> * [how-to](../resources/how-to/ "mention")

<figure><img src="../.gitbook/assets/PlainLine_01.png" alt=""><figcaption></figcaption></figure>

## The Components of Alchemix

<figure><img src="../.gitbook/assets/vaults.png" alt="" width="80"><figcaption><p>Alchemist</p></figcaption></figure>

### Alchemist

The Alchemists handle collateral deposits, issue synthetic assets, and manage yield strategies. There is one Alchemist for each alAsset on each chain.

_Read more -_ [_**Alchemist**_](https://alchemix-finance.gitbook.io/user-docs/components/alchemist)

<figure><img src="../.gitbook/assets/alUSD_thick.svg" alt="" width="75"><figcaption><p>alUSD, an alAsset</p></figcaption></figure>

### alAssets

alAssets are tokens that represent future yield. They can be used for market swaps, transmuting, liquidity provision, and loan repayments.

_Read more -_ [_**alAssets**_](https://alchemix-finance.gitbook.io/user-docs/components/alassets)&#x20;

<figure><img src="../.gitbook/assets/transmuter_thin.png" alt="" width="80"><figcaption><p>Transmuter</p></figcaption></figure>

### Transmuter

The Transmuter converts synthetic alAssets to their underlying assets on a 1:1 basis by gradually releasing yield from Alchemists to alAsset token stakers.

_Read more -_ [_**Transmuter**_](https://alchemix-finance.gitbook.io/user-docs/components/transmuter)

<figure><img src="../.gitbook/assets/farm_thin.png" alt="" width="80"><figcaption><p>Elixir AMO</p></figcaption></figure>

### Elixir AMO

The Elixir AMO (Automatic Market Operator) deposits surplus funds from the Transmuter into external liquidity pools, which supports alAsset prices and generates additional protocol revenue. The Elixir also has the flexibility to withdraw alAssets for price stabilization.

_Read more -_ [_**Elixir AMO**_](https://alchemix-finance.gitbook.io/user-docs/components/elixir-amo)

<figure><img src="../.gitbook/assets/Untitled design (1).png" alt="" width="125"><figcaption><p>Alchemix DAO</p></figcaption></figure>

### AlchemixDAO&#x20;

The Alchemix DAO is empowered by the governance token ALCX, which grants holders governance rights to signal their desires that help shape the protocol's direction and resource utilization.

_​Read more -_ [_**Alchemix DAO**_](https://alchemix-finance.gitbook.io/user-docs/alchemix-dao/alchemix-dao)&#x20;

<figure><img src="../.gitbook/assets/ALCX-Std-logo_Thick (5).png" alt="" width="80"><figcaption><p>ALCX</p></figcaption></figure>

### ALCX Token

ALCX serves as both the governance and incentive token for Alchemix, facilitating community decision-making and rewarding liquidity providers within the ecosystem.

_Read more - ​_[_**ALCX Token**_](https://alchemix-finance.gitbook.io/user-docs/alchemix-dao/alcx-token-distribution)&#x20;

<figure><img src="../.gitbook/assets/header_02_test.png" alt=""><figcaption></figcaption></figure>
