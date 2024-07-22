---
description: A deeper dive into how the Transmuter functions
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

# ⚖️ The Transmuter, Elaborated

The Transmuter is actually composed of two separate components: The TransmuterBuffer and the Transmuter.

When funds enter the Transmuter, assuming there is at least a matching amount of the corresponding alAsset they will be immediately be claimable by users with alAssets staked in the Transmuter. The TransmuterBuffer sits between the Alchemist and Transmuter, limiting the available funds that are accessible for transmutation. The goal here is to delay the transmutability of funds so that the massive front-stop (ie, excess funds in the Transmuter buffer) cannot immediately be used to take advantage of extremely small (< 0.1%) arbitrage opportunities, thus burning protocol value for tiny gains. The longer the system can hold onto the front-stop, the longer it can supply liquidity and earn revenue through the Elixir/AMO, and the more Alchemist depositors Alchemix can sustain.

![](https://alchemix-finance.gitbook.io/\~gitbook/image?url=https:%2F%2Flh3.googleusercontent.com%2Fit5PpNg2lG56uV9LcAvPh0OEvw2OdMeUVGHdneY3wdUjEbNLZu7gM-pi7V\_KmWu7o2nVPVzAW\_-rpkAVVFRA0IyS1Ay\_OLLxdK05j912-351\_ArmzMqSJ4nsZVU-T0Lb6EauXS8XXoUNUchlbnK6fQ\&width=768\&dpr=4\&quality=100\&sign=e28ffadf2207873e8257a61726653775ca96eaed632c949fa00066dbd070ec1c)

### Transmuter Flowchart

In the Transmuter, user-exchanged and un-exchanged balances are updated in a stepwise manner, only when the exchange() function is called. The `exchange()` function sends the underlying asset (USDC, DAI, or USDT) to the Transmuter in exchange for the alUSD burned from the transmuter. The TransmuterBuffer receives a call to its `exchange()` function whenever `alchemist.harvest()`, `alchemist.liquidate()`, or `alchemist.repay()` are called - ie, whenever a yield harvest occurs, or when a user liquidates or repays their loan. `TransmuterBuffer.exchange()` will update the available amount of flow that is theoretically accessible by the transmuter, and subsequently call `Transmuter.exchange()` with the marginal amount of funds that need to be exchanged. Each Transmuter handles a single collateral type. Each TransmuterBuffer handles a single synthetic type, and all collateral types underlying that synthetic.

### Flow Rate <a href="#flow-rate" id="flow-rate"></a>

The flow rate is set by governance and is a per-second MAXIMUM rate of flow for funds to be sent from the TransmuterBuffer to the Transmuter. The main features of the flow are:

1. Flow-rate is constant and linear.
2. The flow-rate (measured in underlying collateral token per one second, ie 1 DAI/second) will continuously add to the available-flow (measured in the underlying collateral token, ie 1 DAI).
3. The available-flow is a measure of how much underlying collateral will immediately flow from the TransmuterBuffer to the Transmuter, upon a deposit to the TransmuterBuffer (ie, a call of the `exchange()` function). This means the available-flow can build up over time if the Transmuter flow-rate is being underutilized. A build-up of available flow makes it possible for the effective flow-rate over a period of time to exceed the flow-rate, thus ensuring the set flow-rate is acting as more of an average over time, rather than a hard cap.
4. Each underlying-token has its own flow-rate. The available-flow for a given underlying-token can exceed the total amount of funds denominated in that underlying-token (across all strategies) held by the transmuter-buffer in the Alchemist. However, when this is the case, the Transmuter will only be able to access the actual funds held by the Transmuter-buffer in the Alchemist (see Invariants 1 and 2)
   1. Figure 1 shows a scenario where available flow has exceeded the total buffered amount (total amount of underlying token controlled by the Transmuter buffer across all strategies in the alchemist).
   2. Figure 2 shows a scenario where the total buffered amount has exceeded the available flow.
   3. In both scenarios, the total amount exchanged to the Transmuter cannot surpass the lesser of the two values in question.
   4. In Figure 1, there will be an excess of available-flow. Should the flow of the underlying asset to the Transmuter increase beyond the defined flow-rate, the excess of available-flow would be used to absorb the faster rate (as described in Item 2 above).

![](https://alchemix-finance.gitbook.io/\~gitbook/image?url=https:%2F%2Flh5.googleusercontent.com%2FftZLKfzFyYJuB3s1EQyTGQP7oZsqJsTMNxfy8NsOwE9SIUlujL5Una48PwBVAMx5ydcngdoeRn0Nhdfghj5IH-\_P-G9fRaR83OLNsY-sIoEYEJyEl34aso1J1h3inyJ5yKNLcLTvtQSttit-6Y7ZmA\&width=768\&dpr=4\&quality=100\&sign=89dce485d70a6a1c338e83b640f8ef2ddd09d2f55a21e8166d5c4db6aca4b788)

Visualization of Transmuter Buffer Available Flow Scenarios

<figure><img src="../../.gitbook/assets/header_02_test.png" alt=""><figcaption></figcaption></figure>
