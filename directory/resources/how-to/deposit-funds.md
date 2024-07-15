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

# ⚡ Deposit funds

The unique thing about Alchemix loans is that they allow you to leverage your wealth without risk of liquidation. Another way to put this is that Alchemix allows you to borrow against an asset without carrying the risk of losing your collateral in the event of a market crash.

In order to setup a new loan, first visit the Vaults page on the website. Here you can see a list of available vaults where users can deposit any of the currently supported collateral assets.

<figure><img src="../../.gitbook/assets/wedqxsz.png" alt=""><figcaption></figcaption></figure>

Each vault displays the tokens used as collateral. Users are able to deposit these tokens in order to take a loan.

Let’s see how you can borrow against some of your ETH holdings with a new alETH loan.

First, click on the + button on the Yearn wETH vault. This will open the deposit section which offers you several deposit options.

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

Let’s go from the top. The LTV tells you how much you’re able to borrow against your deposit. 50% means you’ll be able to borrow a maximum of half the deposited amount.

In this example, the vault accepts wETH or yvwETH. Luckily there is a handy conversion tool built into the wETH vault that allows you to convert your ETH to wETH during the deposit.

All you need to do is click the toggle and the input box allows you to input the ETH amount you’d like to deposit.

Let’s input a value of 1 ETH.

Next, we have slippage. With certain vaults, (like the Yearn vaults) when you deposit collateral Alchemix will convert it into the Yearn equivalent. This is how Alchemix is able to earn yield on your deposit in the background. In this case it will exchange wETH to yvwETH for you. Because exchange rates fluctuate, your vault will receive a slightly different amount of yvwETH in return. This is usually minimal and not something you need to worry about. In order to protect our users, you are able to set your own slippage limits using the buttons provided, or specify a different amount here.

Now, you can press ‘deposit’ and authorize the transaction in your wallet. If it’s the first time you’ve deposited into one of our vaults, two transactions will need to be confirmed. The first is the token approval and the second will be the actual deposit.

Once your transaction has completed you’ll be able to see how much you’ve deposited in the vault.



<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

If you have any support queries, please contact our team in the official [Discord channel](https://alchemix-finance.gitbook.io/user-docs/resources).

Now let's look at how to take a Self-Repaying Loan in the next page.

<figure><img src="../../.gitbook/assets/header_02_test.png" alt=""><figcaption></figcaption></figure>
