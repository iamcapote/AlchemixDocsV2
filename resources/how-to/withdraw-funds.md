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

# 🍀 Withdraw funds

When you want to move your funds back into your wallet you’ll need to call the ‘withdraw’ function.

Something to bear in mind is that you can only withdraw funds that exceed the collateral requirements of any outstanding loans you have.

For example, if you have borrowed 50% of your deposit of a loan with a 50% loan-to-value ratio then you won’t be able to withdraw any funds unless you either repay your debt or liquidate it with your deposit.

In the previous guide, we liquidated our loan which releases the funds to be withdrawn.

Click the + button next to the vault you want to withdraw from and click the 'Withdraw' tab. You’ll notice the choice to receive the standard or yield bearing asset, in this example wETH or yvwETH.

<figure><img src="../../.gitbook/assets/image (17) (1).png" alt=""><figcaption></figcaption></figure>

Since we want ETH in our wallet following the withdrawal, we will toggle the wETH/ETH switch. The system will conveniently withdraw wETH and convert it to ETH for us.

In this case, we will choose ‘max’ since we want to completely exit the vault.

Like the liquidate and deposit functions, withdraw adds slippage protection control to allow users to limit the slippage as the system converts assets to unwind your position.

<figure><img src="../../.gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>

Click ‘Withdraw’ and confirm the transactions in your wallet.

When you’ve successfully withdrawn you’ll see your updated balance reflected in your wallet.

If you have any support queries, please contact our team on the official [Discord channel](https://alchemix-finance.gitbook.io/user-docs/resources)

<figure><img src="../../.gitbook/assets/header_02_test.png" alt=""><figcaption></figcaption></figure>
