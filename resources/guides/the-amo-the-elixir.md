---
description: The Alchemix Algorithmic Market Operator
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

# ⚗️ The AMO: The Elixir

<figure><img src="../../.gitbook/assets/image (21).png" alt="" width="563"><figcaption></figcaption></figure>

When Alchemix was originally launched, it was never anticipated that the peg stability module, the Transmuter, would build up a significant backstop of funds. To take advantage of this, in the V1 deployment of Alchemix, reserves were deployed in Yearn. The yield was passed from these deposits to DAI and ETH depositors in Alchemix. This enabled us to have a killer feature — boosted yield, which at times, doubled the amount of interest paid to Alchemix depositors.

While building V2, it dawned on the Alchemix team that these DAI and ETH reserves could be more intelligently deployed in order to better benefit the Alchemix ecosystem. Instead of these assets passively making money elsewhere in DeFi, it makes much more sense to use these funds actively in the market to earn the protocol income and to better manage the prices of the alAssets.

#### Introducing the Alchemix Elixir <a href="#id-8ab1" id="id-8ab1"></a>

![](https://alchemix-finance.gitbook.io/\~gitbook/image?url=https:%2F%2F1843944683-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FzG9qcxzJ1K3kNTlZ81Xj%252Fuploads%252Fek0IvPNfsSNXWG2FjwfD%252FElixirQuoteBlock\_01.png%3Falt=media%26token=7e2a3b01-050d-45bc-9fcb-81f32ac3f47e\&width=768\&dpr=4\&quality=100\&sign=25ae0dbd662295b59a63344c10e6163b8b87659e353acfb820a2127027c4e0a4)

The Alchemix Elixir is a contract inspired by FRAX’s Algorithmic Market Operator (AMO). Their AMO allows them to expand and contract the supply of FRAX in LP pools, with FRAX3CRV LP being the most predominant. They mint and deposit FRAX when the token price is above their peg, and withdraw and burn FRAX when the token price is below their peg. They also farm with the LP in Convex, earning the protocol income in the process.

Through its own automations, the Alchemix Elixir takes a similar approach to market operations, with the exception that **Alchemix cannot mint alUSD into the LP pools** (thus maintaining the overcollateralized nature of alAssets)**.**

See below for a diagram that shows how funds flow through the market.

![](https://alchemix-finance.gitbook.io/\~gitbook/image?url=https:%2F%2F1843944683-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FzG9qcxzJ1K3kNTlZ81Xj%252Fuploads%252FIixliC4pWHrW3ZQnOlui%252FAMO\_Graphic.png%3Falt=media%26token=8f40fb81-e19a-4f45-b0af-f52507f37517\&width=768\&dpr=4\&quality=100\&sign=8cab3928107c510f893cbc270b29b27177af59d8648ee77780b12c7051a918fe)

The Elixir was jump-started by migrating the v1 Transmuter TVL to it. From there, the additional will receive additional funds only when the Transmuters build up surpluses. The Elixir contract will supply liquidity in the primary Curve liquidity pools for alUSD and alETH. By depositing excess DAI, USDC, USDT, and ETH into Elixir, liquidity is deepened and the prices of alAssets are made more stable.

Curve allows for single sided withdrawals and deposits, and bases the exchange price on the relative balance between the tokens in the LP pool. If a pool is overbalanced with alUSD or alETH, it means we are below 1 USD for alUSD and 1 ETH for alETH. Alchemix can increase the price of the alAsset by single-sided withdrawals of alUSD or alETH, thus rebalancing the pool and increasing the alAsset price closer to 1:1. These withdrawn alUSD and alETH tokens would be removed from circulation, with the potential to be redeployed to their Curve pool should the price of the alAsset increase to the point where it is able to support the addition of alUSD with a negligible effect on the price of the asset.

The next function of Elixir is to generate revenue and build long-term liquidity for the protocol. The Elixir will do this by making a liquidity-driving asset accumulation strategy. Liquidity-driving assets, such as CVX and CRV, give the DAO power to direct rewards from the corresponding protocols. The more liquidity driving assets are owned, the more Alchemix can sustainably incentivize the primary alAsset liquidity pools. Alchemix also typically bribes voters to vote for emissions to these pools - where typically every $1 input results in greater than $1 emitted to the liquidity pool. Given the Elixir tends to own a significant share of the liquidity pools, this can result in a significant amount of value returned to the DAO in the form of CRV, CVX, and other assets. The more CVX Alchemix votes with, the more ALCX is returned as a rebate for voting for the alAsset pools. So between this multiple and the Votium rebates, it greatly enhances the efficiency and longevity of ALCX emissions.

![](https://alchemix-finance.gitbook.io/\~gitbook/image?url=https:%2F%2F1843944683-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FzG9qcxzJ1K3kNTlZ81Xj%252Fuploads%252FQitn9F5FQ7w7ByFcwIZV%252FElixirQuoteBlock\_03.png%3Falt=media%26token=d07d2fcb-5af5-4881-b5c1-816796734cf4\&width=768\&dpr=4\&quality=100\&sign=b9bdd31ccb2c89bdc7bee0608c843a8f47fceed0d17d55ff5c35cb0e920fb1b7)

When Alchemix stakes its own Curve LPs on Convex, it receives CRV and CVX rewards. The Elixir is able to use these rewards to benefit the DAO, with the current approach explained [here](https://alchemix-finance.gitbook.io/user-docs/components/elixir-amo).

The Elixir is a significant upgrade to our peg stability module. The concentrated management of our protocol-controlled value aligns it more closely to our interests.

The ancient tomes of alchemy describe a mysterious fluid known as “Elixir”. It was thought to have the power to turn base metals into gold and even grant immortality. In that sense, the Alchemix Elixir is true to its name, with the peg-stability mechanisms and CVX flywheel bringing long-term price stability and sustainability to Alchemix alUSD and alETH. It’s a new era for Alchemix, and we’re happy to be bringing magic to DeFi yet again.

#### Contracts: <a href="#id-9c75" id="id-9c75"></a>

alUSD Elixir: **0x9735f7d3ea56b454b24ffd74c58e9bd85cfad31b**

alETH Elixir: **0xe761bf731A06fE8259FeE05897B2687D56933110**

<figure><img src="../../.gitbook/assets/header_02_test.png" alt=""><figcaption></figcaption></figure>
