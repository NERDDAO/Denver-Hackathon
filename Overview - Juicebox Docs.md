[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/overview//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/overview/)
- [中文](/zh/dev/learn/overview/)

[Links](#)

- [Juicebox](https://juicebox.money)
- [Contact](https://juicebox.money/contact)
- [Discord](https://discord.gg/juicebox)
- [GitHub](https://github.com/jbx-protocol)
- [Telegram](https://t.me/jbx_eth)
- [Governance](https://jbdao.org)
- [Analytics](/dao/reference/analytics/)
- [Twitter](https://twitter.com/juiceboxETH)
- [YouTube](https://www.youtube.com/c/JuiceboxDAO/)
- [Newsletter](https://subscribepage.io/juicenews)
- [Podcast](https://anchor.fm/thejuicecast)

Search⌘K

- [Intro](/dev/)
- [Learn](#)
    
    - [Overview](/dev/learn/overview/)
    - [Architecture](/dev/learn/architecture/)
        
    - [Administration](/dev/learn/administration/)
    - [Risks](/dev/learn/risks/)
    - [Glossary](/dev/learn/glossary/)
        
- [Build](#)
    
    - [Getting started](/dev/build/getting-started/)
    - [Basics](/dev/build/basics/)
    - [Project NFT](/dev/build/project-nft/)
    - [Programmable treasury](/dev/build/programmable-treasury/)
    - [Treasury extensions](/dev/build/treasury-extensions/)
        
        - [Ballot](/dev/build/treasury-extensions/ballot/)
        - [Data source](/dev/build/treasury-extensions/data-source/)
        - [Pay delegate](/dev/build/treasury-extensions/pay-delegate/)
        - [Redemption delegate](/dev/build/treasury-extensions/redemption-delegate/)
        - [Split allocator](/dev/build/treasury-extensions/split-allocator/)
    - [Utilities](#)
        
    - [Namespaces & IDs](/dev/build/namespace/)
    - [Contract Examples](/dev/build/examples/)
- [API](#)
    
- [Extensions](#)
    
- [Resources](#)
    
- [Frontend](/dev/frontend/)
    
- [Deprecated](#)
    

- [](/)
- Learn
- Overview

On this page

# Overview

The Juicebox protocol is a framework for funding and operating projects openly on Ethereum. It lets you:

#### Deploy an NFT that represents ownership over a project[​](#deploy-an-nft-that-represents-ownership-over-a-project "Direct link to Deploy an NFT that represents ownership over a project")

Whichever address owns this NFT has administrative privileges to configure treasury parameters within the Juicebox ecosystem.

[Learn more about projects](/dev/learn/glossary/project/)

#### Configure funding cycles for a project[​](#configure-funding-cycles-for-a-project "Direct link to Configure funding cycles for a project")

Funding cycles define contractual constraints according to which the project will operate.

[Learn more about funding cycles](/dev/learn/glossary/funding-cycle/)  

The following properties can be configured into a funding cycle:

_Funding cycle properties_

##### Start timestamp[​](#start-timestamp "Direct link to Start timestamp")

The timestamp at which the funding cycle is considered active. Projects can configure the start time of their first funding cycle to be in the future, and can ensure reconfigurations don't take effect before a specified timestamp.

Once a funding cycle ends, a new one automatically starts right away. If there's an approved reconfiguration queued to start at this time, it will be used. Otherwise, a copy of the rolled over funding cycle will be used.

##### Duration[​](#duration "Direct link to Duration")

How long each funding cycle lasts (specified in seconds). All funding cycle properties are unchangeable while the cycle is in progress. In other words, any proposed reconfigurations can only take effect during the subsequent cycle.

If no reconfigurations were submitted by the project owner, or if proposed changes fail the current cycle's [ballot](#ballot), a copy of the latest funding cycle will automatically start once the current one ends.

A cycle with no duration lasts indefinitely, and reconfigurations can start a new funding cycle with the proposed changes right away.

##### Distribution limit[​](#distribution-limit "Direct link to Distribution limit")

The amount of funds that can be distributed out from the project's treasury during a funding cycle. The project owner can pre-program a list of addresses, other Juicebox projects, and contracts that adhere to [`IJBSplitAllocator`](/dev/api/interfaces/ijbsplitallocator/) to split distributions between. Treasury funds in excess of the distribution limit is considered overflow, which can serve as runway or be reclaimed by token holders who redeem their tokens.

Distributing is a public transaction that anyone can call on a project's behalf. The project owner can also include a split that sends a percentage of the distributed funds to the address who executes this transaction.

The protocol charges a [JBX membership fee](#jbx-membership-fee) on funds withdrawn from the network. There are no fees for distributions to other Juicebox projects.

Distribution limits can be specified in any currency that the [`JBPrices`](/dev/api/contracts/jbprices/) contract has a price feed for.

##### Overflow allowance[​](#overflow-allowance "Direct link to Overflow allowance")

The amount of treasury funds that the project owner can distribute on-demand.

This allowance does not reset per-funding cycle. Instead, it lasts until the project owner explicitly proposes a reconfiguration with a new allowance.

The protocol charges a [JBX membership fee](#jbx-membership-fee) on funds withdrawn from the network.

Overflow allowances can be specified in any currency that the [`JBPrices`](/dev/api/contracts/jbprices/) contract has a price feed for.

##### Weight[​](#weight "Direct link to Weight")

A number used to determine how many project tokens should be minted and transferred when payments are received during the funding cycle. In other words, weight is the exchange rate between the project token and a currency (defined by a [JBPayoutRedemptionPaymentTerminal3_1_1](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/)) during that funding cycle. Project owners can configure this directly, or allow it to be derived automatically from the previous funding cycle's weight and discount rate.

##### Discount rate[​](#discount-rate "Direct link to Discount rate")

The percent to automatically decrease the subsequent cycle's weight from the current cycle's weight.

The discount rate is not applied during funding cycles where the weight is explicitly reconfigured.

[Learn more about discount rates](/dev/learn/glossary/discount-rate/)

##### Ballot[​](#ballot "Direct link to Ballot")

The address of a contract that adheres to [`IJBFundingCycleBallot`](/dev/api/interfaces/ijbfundingcycleballot/), which can provide custom criteria that prevents funding cycle reconfigurations from taking effect.

A common implementation is to force reconfigurations to be submitted at least X days before the end of the current funding cycle, giving the community foresight into any misconfigurations or abuses of power before they take effect.

A more complex implementation might include on-chain governance.

[Learn more ballots](/dev/learn/glossary/ballot/)

##### Reserved rate[​](#reserved-rate "Direct link to Reserved rate")

The percentage of newly minted tokens that a project wishes to withhold for custom distributions. The project owner can pre-program a list of addresses, other Juicebox project owners, and contracts that adhere to [`IJBSplitAllocator`](/dev/api/interfaces/ijbsplitallocator/) to split reserved tokens between.

[Learn more about reserved rate](/dev/learn/glossary/reserved-tokens/)

##### Redemption rate[​](#redemption-rate "Direct link to Redemption rate")

The percentage of a project's treasury funds that can be reclaimed by community members by redeeming the project's tokens during the funding cycle.

A rate of 100% suggests a linear proportion, meaning X% of treasury overflow can be reclaimed by redeeming X% of the token supply.

[Learn more about redemption rates](/dev/learn/glossary/redemption-rate/)

##### Ballot redemption rate[​](#ballot-redemption-rate "Direct link to Ballot redemption rate")

A project can specify a custom redemption rate that only applies when a proposed reconfiguration is waiting to take effect.

This can be used to automatically allow for more favorable redemption rates during times of potential change.

##### Pause payments, pause distributions, pause redemptions, pause burn[​](#pause-payments-pause-distributions-pause-redemptions-pause-burn "Direct link to Pause payments, pause distributions, pause redemptions, pause burn")

Projects can pause various bits of its treasury's functionality on a per-funding cycle basis. These functions are unpaused by default.

##### Allow minting tokens, allow changing tokens, allow setting terminals, allow setting the controller, allow terminal migrations, allow controller migration[​](#allow-minting-tokens-allow-changing-tokens-allow-setting-terminals-allow-setting-the-controller-allow-terminal-migrations-allow-controller-migration "Direct link to Allow minting tokens, allow changing tokens, allow setting terminals, allow setting the controller, allow terminal migrations, allow controller migration")

Projects can allow various bits of treasury functionality on a per-funding cycle basis. These functions are disabled by default.

##### Hold fees[​](#hold-fees "Direct link to Hold fees")

By default, JBX membership fees are paid automatically when funds are distributed out of the ecosystem from a project's treasury. During funding cycles configured to hold fees, this fee amount is set aside instead of being immediately processed. Projects can get their held fees returned by adding the same amount of withdrawn funds back to their treasury. Otherwise, JuiceboxDAO or the project can process these held fees at any point to get JBX at the current rate.

This allows a project to withdraw funds and later add them back into their Juicebox treasury without incurring fees.  

This applies to both distributions from the distribution limit and from the overflow allowance.

##### Data source[​](#data-source "Direct link to Data source")

The address of a contract that adheres to [`IJBFundingCycleDataSource`](/dev/api/interfaces/ijbfundingcycledatasource/), which can be used to extend or override what happens when the treasury receives funds, and what happens when someone tries to redeem their project tokens.

[Learn more about data sources](/dev/learn/glossary/data-source/)

#### Mint tokens[​](#mint-tokens "Direct link to Mint tokens")

By default, a project starts with 0 tokens and mints them when its treasury receives contributions.  
A project can mint and distribute tokens on demand if its current funding cycle is configured to allow minting.  
By default, project tokens are not ERC-20s and thus not compatible with standard market protocols like Uniswap. At any time, you can issue ERC-20s that your token holders can claim. This is optional.

#### Burn tokens[​](#burn-tokens "Direct link to Burn tokens")

Anyone can burn a project's tokens if the project's current funding cycle isn't configured to paused burning.

#### Bring-your-own token[​](#bring-your-own-token "Direct link to Bring-your-own token")

A project can bring its own token, as long as it adheres to [`IJBToken`](/dev/api/interfaces/ijbtoken/) and uses fixed point accounting with 18 decimals.  

This allows a project to use ERC-721's, ERC-1155's, or any other custom contract that'll be called upon when the protocol asks to mint or burn tokens.  

A project can change its token during any of its funding cycles that are explicitly configured to allow changes.  

By default, the protocol provides a transaction for projects to deploy [`JBToken`](/dev/api/contracts/jbtoken/) ERC-20 tokens.

#### Splits[​](#splits "Direct link to Splits")

A project can pre-program token distributions to splits. The destination of a split can be an Ethereum address, the project ID of another project's Juicebox treasury (the split will allow you to configure the beneficiary of that project's tokens that get minted in response to the contribution), to the `allocate(...)` function of any contract that adheres to [`IJBSplitAllocator`](/dev/api/interfaces/ijbsplitallocator/), or to the address that initiated the transaction that distributes tokens to the splits.

[Learn more about splits](/dev/learn/glossary/splits/)  
[Learn more about allocators](/dev/learn/glossary/split-allocator/)

#### JBX membership fee[​](#jbx-membership-fee "Direct link to JBX membership fee")

All funds distributed by projects from their treasuries to destinations outside of the Juicebox ecosystem (i.e. distributions that do not go to other Juicebox treasuries) will incure a protocol fee. Redemptions from projects using [`JBETHPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jbethpaymentterminal3_1_1/) incur fees if the redemption rate (or ballot redemption rate) is less than 100%. This fee is sent to the JuiceboxDAO treasury which runs on the Juicebox protocol itself (project ID of 1), triggering the same functionality as a payment directly to JuiceboxDAO (by default, minting JBX for the fee payer according to JuiceboxDAO's current funding cycle configuration) from an external source.  

This fee is adjustable by JuiceboxDAO, with a max value of 5%.  

Any funds sent from one juicebox treasury to another via splits do not incur fees.

#### Custom treasury strategies[​](#custom-treasury-strategies "Direct link to Custom treasury strategies")

Funding cycles can be configured to use an [`IJBFundingCycleDataSource`](/dev/api/interfaces/ijbfundingcycledatasource/), [`IJBPayDelegate`](/dev/api/interfaces/ijbpaydelegate/), and [`IJBRedemptionDelegate`](/dev/api/interfaces/ijbredemptiondelegate/) to extend or override the default protocol's behavior that defines what happens when an address tries to make a payment to the project's treasury, and what happens when someone tries to redeem the project tokens during any particular funding cycle.

[Learn more about data sources](/dev/learn/glossary/data-source/)  
[Learn more about delegates](/dev/learn/glossary/delegate/)

#### Accept multiple tokens[​](#accept-multiple-tokens "Direct link to Accept multiple tokens")

A project can specify any number of payment terminal contracts where it can receive funds denominated in various tokens. This allows projects to create distinct rules for accepting ETH, any ERC-20, or any asset in general.

Anyone can roll their own contract that adheres to [`IJBPaymentTerminal`](/dev/api/interfaces/ijbpaymentterminal/) for projects to use, and a project can migrate funds between terminals that use the same token as it wishes.

#### Forkability and migratability[​](#forkability-and-migratability "Direct link to Forkability and migratability")

A project can migrate its treasury's controller to any other contract that adheres to [`IJBController3_1`](/dev/api/interfaces/ijbcontroller3_1/). This allows a project to evolve into updated or custom treasury dynamics over time as it wishes.

#### Operators[​](#operators "Direct link to Operators")

Addresses can specify other addresses that are allowed to operate certain administrative treasury transactions on its behalf.  

[Learn more about operators](/dev/learn/glossary/operator/)

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/overview.md)

[

Previous

Intro

](/dev/)[

Next

Architecture

](/dev/learn/architecture/)

- [Deploy an NFT that represents ownership over a project](#deploy-an-nft-that-represents-ownership-over-a-project)
- [Configure funding cycles for a project](#configure-funding-cycles-for-a-project)
    - [Start timestamp](#start-timestamp)
    - [Duration](#duration)
    - [Distribution limit](#distribution-limit)
    - [Overflow allowance](#overflow-allowance)
    - [Weight](#weight)
    - [Discount rate](#discount-rate)
    - [Ballot](#ballot)
    - [Reserved rate](#reserved-rate)
    - [Redemption rate](#redemption-rate)
    - [Ballot redemption rate](#ballot-redemption-rate)
    - [Pause payments, pause distributions, pause redemptions, pause burn](#pause-payments-pause-distributions-pause-redemptions-pause-burn)
    - [Allow minting tokens, allow changing tokens, allow setting terminals, allow setting the controller, allow terminal migrations, allow controller migration](#allow-minting-tokens-allow-changing-tokens-allow-setting-terminals-allow-setting-the-controller-allow-terminal-migrations-allow-controller-migration)
    - [Hold fees](#hold-fees)
    - [Data source](#data-source)
- [Mint tokens](#mint-tokens)
- [Burn tokens](#burn-tokens)
- [Bring-your-own token](#bring-your-own-token)
- [Splits](#splits)
- [JBX membership fee](#jbx-membership-fee)
- [Custom treasury strategies](#custom-treasury-strategies)
- [Accept multiple tokens](#accept-multiple-tokens)
- [Forkability and migratability](#forkability-and-migratability)
- [Operators](#operators)