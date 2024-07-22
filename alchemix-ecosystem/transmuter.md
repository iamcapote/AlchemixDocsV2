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

# ⚖️ Transmuter

The Transmuter is the primary mechanism for restoring alAsset prices and reducing supply by converting alAssets into their underlying assets.

The Transmuter achieves this by receiving all harvested yields and self-liquidations (i.e., repayments) while gradually releasing them to alAsset depositors to be redeemed via a time-based formula.

Users that deposit alAssets to the Transmuter will gradually be credited with the corresponding assets proportional to the amount of alAssets that they have deposited in the Transmuter.  The alAssets are burned when a user claims the transmuted token.&#x20;

For example, take a scenario where a user has deposited 100 alUSD into the Transmuter, which will start to convert the alUSD to DAI gradually. Once the 100 alUSD are fully redeemable for 100 DAI, the user can claim the corresponding 100 DAI, which will also burn the 100 alUSD.

<figure><img src="../.gitbook/assets/01_02 (4).png" alt=""><figcaption></figcaption></figure>

## Key Features

### **1:1 Asset Conversion**

Enables the conversion of alAssets to underlying assets at a 1:1 rate.



### **Minimum Estimate of Flow**

The transmutation rate is dictated by the average yield earned by depositors, which provides a baseline estimation for the flow of yield into the Transmuter. The rate of flow to the Transmuter is increased by self-liquidations and loan repayments.



### **Protocol Synergy**

Receiving funds from Alchemists and redirecting excess funds to the Elixir AMO optimizes the capital efficiency within the ecosystem.



### **Governance-Controlled Parameters**

Transmuter parameters are managed based on governance decisions, aligning with the ecosystem's evolving needs.



### **Stabilization of alAssets**

The Transmuter provides an efficient mechanism to stabilize the price of the alAsset.

<figure><img src="../.gitbook/assets/PlainLine_01.png" alt=""><figcaption></figcaption></figure>

## How it works

1. **Deposit:** Users deposit alAssets (like alUSD) into the Transmuter.&#x20;
2. **Accumulation & Exchange:** Overtime the underlying asset is accumulated in the Transmuter via yield harvest, self-liquidations, and loan repayments. The asset is proportionally allocated to users based on their alAsset deposit. For example, if a user deposits alUSD gradually the Transmuter will allocate DAI to be claimed by the user based on how much alUSD they have deposited.
3. **Claim:** Users claim the alAssets equivalent to their deposited tokens and burn the alAssets at a 1:1 ratio. In this example, if the user deposited 100 alUSD the user will burn their 100 alUSD deposits when they claim the 100 DAI equivalent.

Users who deposit alUSD in the Transmuter would gradually be credited with DAI proportional to their alUSD deposit. Once the user decides to withdraw DAI, an equivalent amount of their deposit alUSD is burned, completing the transmutation cycle.

<figure><img src="../.gitbook/assets/PlainLine_01.png" alt=""><figcaption></figcaption></figure>

## Conversion Flow

The flow rate at which these assets can be converted from alAssets (alUSD) into the underlying tokens (DAI) is limited to ensure that the system is not drained by minor arbitrages while creating a front-stop or excess pool of funds for conversions when the price of the alAsset diverges further from the underlying. If the excess funds are significant, they are sent to the [Elixir AMO](https://alchemix-finance.gitbook.io/user-docs/components/elixir-amo).

The minimum flow to the Transmuter may be estimated by the average yield earned by all depositors for the corresponding alAsset. Furthermore, repayments and self-liquidations are sent directly into the Transmuter, contributing to the conversion flow, which is part of the average yield.

{% hint style="info" %}
More information can be found in [the-transmuter-elaborated.md](../resources/guides/the-transmuter-elaborated.md "mention")
{% endhint %}

<figure><img src="../.gitbook/assets/header_02_test.png" alt=""><figcaption></figcaption></figure>
