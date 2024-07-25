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

# 🖥️ Development of New Adapters

Technical contributions to the Alchemix ecosystem can come in many forms, including:

* Token adapters for new yield sources
* Integration with other DeFi protocols
* Alchemix-specific tools and utilities

However, to integrate any new smart contracts into an AlchemixV2 debt system, some governance actions will be required. Contributors should use the following procedures to guide them as they prepare to build and integrate code into the Alchemix ecosystem.



## Token Adapters

Alchemix token adapters are standardized methods used to interact with different yield-bearing assets or vaults. Alchemix uses token adapters to integrate and manage the various assets seamlessly.

The following details the steps are necessary for integrating a new adapter into the Alchemix V2 protocol.

### Token Adapter Governance Process <a href="#token-adapter-governance-process" id="token-adapter-governance-process"></a>

There are three steps, including 2 separate AIPs (Alchemix Improvement Proposals), needed to get an adapter approved and connected in an Alchemix V2 debt system. The first AIP is technically optional, as both AIPs could be condensed into a single AIP if the integration developer is comfortable putting in the development work upfront without pre-approval.

The [Community Governance Process](https://alchemix-finance.gitbook.io/user-docs/alchemix-dao/the-alchemix-dao/governance-process) details the general governance steps that should be followed for each AIP.

#### _Step 1 - Propose the new yield source for integration, and request grant funding._ <a href="#step-1" id="step-1"></a>

The purpose of this step is for the integrator/proposer to verify that the Alchemix DAO wants to integrate the proposed yield strategy. Additionally, the integrator/proposer can request a pre-approved grant of ALCX tokens, to be paid out when the Adapter is deployed in step 2.

A template for Step 1 proposals will be provided in the future.

#### _Step 2 - Write, deploy, and verify the ITokenAdapter compliant adapter. See Technical Requirements below at the end of section._ <a href="#step-2" id="step-2"></a>

#### _Step 3 - Propose integration of the new yield source using the new adapter._ <a href="#step-3" id="step-3"></a>

The following parameters need to be approved in at least one of the two AIPs:

* Target network (eg. ETH Mainnet, Optimism, etc…)
* Yield bearing asset name & address (include Etherscan & Github links)
* Collateral asset name & address (include Etherscan & Github links)
* [Maximum Loss](https://alchemix-finance.gitbook.io/v2/docs/alchemistv2#setmaximumloss) is expressed in basis points (eg., 50 for 0.5%) [more info](https://github.com/alchemix-finance/v2-foundry/blob/master/src/interfaces/alchemist/IAlchemistV2AdminActions.sol#L49)
* Deposit cap (expressed in units of underlying collateral) [more info](https://github.com/alchemix-finance/v2-foundry/blob/master/src/interfaces/alchemist/IAlchemistV2AdminActions.sol#L49)
* Credit unlock blocks (how long after a harvest does it take for the yield to be distributed to depositors) [more info](https://github.com/alchemix-finance/v2-foundry/blob/master/src/interfaces/alchemist/IAlchemistV2AdminActions.sol#L49)

The following needs to be approved as well, once development and deployment are complete:

* Adapter name & address
  * include Etherscan link
  * include Github link to solidity code in the [v2-foundry repo](https://github.com/alchemix-finance/v2-foundry)
  * include Github link to deployment artifacts in [deployments repo](https://github.com/alchemix-finance/deployments)
* Multisig transaction details that should be executed by the Alchemix dev multisig, detailed [here](https://alchemix-fi.atlassian.net/wiki/spaces/AL/pages/679608321/Adapter+Integration#Dev-Multisig-Transactions)

NOTE: To be clear, all of the above bullet points only need to be approved ONCE by governance. It is up to the builder whether or not they want pre-approval before creating and deploying the new adapter, or if they want to make a single AIP for approval once the adapter is built, deployed, and verified.



<figure><img src="../../../.gitbook/assets/PlainLine_01.png" alt=""><figcaption></figcaption></figure>

## Technical Requirements <a href="#technical-requirements" id="technical-requirements"></a>

1. Build a token adapter that is compliant with the [**ITokenAdapter** interface](https://github.com/alchemix-finance/v2-foundry/blob/master/src/interfaces/ITokenAdapter.sol), along with a set of unit & integration tests, and make a PR against the master branch of the [Alchemix V2 Repo](https://github.com/alchemix-finance/v2-foundry).
2. Once the Pull Request is approved and merged by the core team, you can deploy the contract to the target network.
3. Make a pr against the master branch of the [deployments repo](https://github.com/alchemix-finance/deployments) that includes the artifacts from the deployment (.json file containing, at a minimum, the **abi** & **address** of the deployed adapter).



## Dev Multisig Transactions <a href="#dev-multisig-transactions" id="dev-multisig-transactions"></a>

Relevant addresses for already-deployed Alchemix contracts can be found in the [deployments repo](https://github.com/alchemix-finance/deployments).



## **Enable a new adapter**

1. TARGET\_ALCHEMIST\_ADDRESS.addYieldToken(YIELD\_TOKEN\_ADDRESS, (ADAPTER\_ADDRESS, MAXIMUM\_LOSS, MAXIMUM\_EXPECTED\_VALUE, CREDIT\_UNLOCK\_BLOCKS));
   1. YIELD\_TOKEN\_ADDRESS = the address of the yield token being integrated
   2. ADAPTER\_ADDRESS = the address of the newly deployed adapter
   3. MAXIMUM\_LOSS = the maximum loss value (in bps) from the AIP
   4. MAXIMUM\_EXPECTED\_VALUE = the deposit cap value (in units of underlying collateral) from the AIP
   5. CREDIT\_UNLOCK\_BLOCKS = the credit unlock blocks value from the AIP
2. TARGET\_ALCHEMIST\_ADDRESS.setYieldTokenEnabled(YIELD\_TOKEN\_ADDRESS, true);
   1. YIELD\_TOKEN\_ADDRESS = the address of the yield token being integrated



## **Upgrade an adapter**

(If the newly deployed adapter is an upgraded adapter for an existing yield token)

1. TARGET\_ALCHEMIST\_ADDRESS.setTokenAdapter(YIELD\_TOKEN\_ADDRESS, ADAPTER\_ADDRESS);
   1. YIELD\_TOKEN\_ADDRESS = the address of the yield token being integrated
   2. ADAPTER\_ADDRESS = the address of the newly deployed adapter



## **Create a harvest job for the Alchemix Keeper**

1. HARVEST\_RESOLVER\_ADDRESS.addHarvestJob(true, YIELD\_TOKEN\_ADDRESS, ALCHEMIST\_ADDRESS, MINIMUM\_HARVEST\_AMOUNT, MINIMUM\_DELAY, SLIPPAGE\_BPS);
   1. details on these parameters can be found [here](https://github.com/alchemix-finance/v2-foundry/blob/master/src/keepers/HarvestResolver.sol#L92)
   2. MINIMUM\_HARVEST\_AMOUNT should be set to a value that can be expected to be harvested every 1-2 days
   3. MINIMUM\_DELAY should be set to 1-2 days

<figure><img src="../../../.gitbook/assets/header_02_test.png" alt=""><figcaption></figcaption></figure>
