---
description: Differences between Mainnet Alchemix and other Layer 2 chains
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

# ⛓️ Alchemix on L2

Alchemix primarily operates on the Ethereum Mainnet, but also maintains additional deployments on Optimism and Arbitrum. ALCX and alAssets in Layer 2 chains are sometimes referred to as ‘xalAssets’, as they are not technically identical to the Mainnet assets. Below are the key differences between Mainnet components and their Layer 2 counterparts:

<figure><img src="../.gitbook/assets/ALCX-Std-logo_Thick (5).png" alt="" width="80"><figcaption><p>ALCX</p></figcaption></figure>

## ALCX <a href="#alcx" id="alcx"></a>

ALCX can only be minted on the Ethereum Mainnet. Any amount of ALCX may be bridged to Arbitrum or Optimism through the Everclear (prev Connext) bridge. When ALCX is bridged from Mainnet, it is locked in a lockbox contract and xALCX (Layer 2 ALCX) is minted on the Layer 2 chain. To bridge back, xALCX may be burned on the Layer 2 chain to claim ALCX from the lockbox on Mainnet. So long as the system behaves as expected, there would be no reason that xALCX on any Layer 2 could not be burned/bridged to claim equivalent ALCX on Mainnet.

<figure><img src="../.gitbook/assets/PlainLine_01.png" alt=""><figcaption></figcaption></figure>

<div align="center">

<figure><img src="../.gitbook/assets/alETH_thick (2).png" alt="" width="80"><figcaption><p>alETH</p></figcaption></figure>

</div>

## alAssets <a href="#alassets" id="alassets"></a>

Like xALCX, alUSD, and alETH can be locked/bridged in any quantity on/from Mainnet to earn equivalent credit to mint xalUSD and xalETH (Layer 2 alUSD and Layer 2 alETH). Additionally, xalUSD and xalETH can be minted on Arbitrum and Optimism by taking a self-repaying loan. Lastly, bridging xalAssets between L2s is unlimited, but bridging xalAssets to Mainnet can only be done up to the extent that the corresponding alAsset has been bridged from Mainnet to any L2.

For example, assuming no other bridging had ever taken place: if you were to bridge 10 alUSD from Mainnet to Optimism, and then someone else were to take an alUSD loan and bridge 10 OP-xalUSD from Optimism to Mainnet, you would no longer be able to bridge any xalUSD back from Optimism to Mainnet (someone else would have used the liquidity you created). However, you would be able to bridge your 10 OP-xalUSD from Optimism to Arbitrum. Ultimately, xalAssets are backed by a mix of Mainnet alAssets (through bridging) and the yield sources of that specific chain. OP-xalUSD is backed by Optimism future yield and alUSD bridged from Mainnet. Mainnet alUSD is only backed by Mainnet future yield.

This system helps create more liquidity on L2 chains while ensuring that the primary Alchemix deployment (Mainnet) is insulated from the L2 chains. In that manner, xalAssets should generally be expected to have an equivalent or lesser value than Mainnet alAssets as bridging from Mainnet to L2s (and between L2s) is unrestricted while bridging from L2s to Mainnet is liquidity-based.

<figure><img src="../.gitbook/assets/PlainLine_01.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/vaults.png" alt="" width="80"><figcaption><p>Alchemists</p></figcaption></figure>

## Alchemists <a href="#alchemists" id="alchemists"></a>

Loans on L2 chains behave the same as on Mainnet, but each chain has unique yield strategies.

<figure><img src="../.gitbook/assets/PlainLine_01.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/transmuter_thin.png" alt="" width="80"><figcaption><p>Transmuter</p></figcaption></figure>

## Transmuter <a href="#transmuter" id="transmuter"></a>

The Transmuter behaves the same on L2 chains, where xalAssets can be redeemed over time at a 1:1 rate for the underlying assets. The flow to the Transmuter is based on the yield for each chain. Note that users can bridge alAssets from mainnet to obtain xalAssets on an L2 and deposit them to the Transmuter.

<figure><img src="../.gitbook/assets/PlainLine_01.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/farm_thin.png" alt="" width="80"><figcaption><p>Elixir AMO</p></figcaption></figure>

## Elixir AMO <a href="#elixir-amo" id="elixir-amo"></a>

Where present, the AMO functions the same way on L2s as it does on Mainnet. The backing is held in the alAsset liquidity pool and can be withdrawn single-sided as alAssets to increase the price, as dictated by governance. On some L2s, the AMO exists as a multisig rather than a contract.

<figure><img src="../.gitbook/assets/PlainLine_01.png" alt=""><figcaption></figcaption></figure>

## Appendix - Everclear Bridge <a href="#appendix-connext-bridge" id="appendix-connext-bridge"></a>

Alchemix uses the xERC20 + Lockbox standard pioneered by Everclear (prev Connext). Currently, Everclear is also the only whitelisted bridge. Bridging alAssets and ALCX is secured through Everclear's cross-chain message system through the Arbitrum and Optimism canonical bridges. Everclear has the right to pause their system. If bridging is ever paused for an unreasonable amount of time, Alchemix has the option to whitelist another bridging service to provide cross-chain messaging such that bridging can continue between chains. Because of this system, Alchemix is not exclusively dependent on Everclear for bridging services. The bridge contracts on each chain are owned by Alchemix, with the intent to turn ownership over to veALCX.

{% hint style="info" %}
For detailed information see this guide to learn how to [bridge assets to other chains](../resources/guides/bridging-assets-to-other-chains.md).
{% endhint %}

<figure><img src="../.gitbook/assets/header_02_test.png" alt=""><figcaption></figcaption></figure>

