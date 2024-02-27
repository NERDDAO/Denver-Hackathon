[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/glossary/data-source//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/glossary/data-source/)
- [中文](/zh/dev/learn/glossary/data-source/)

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
        
        - [Payment Terminals](/dev/learn/architecture/terminals/)
    - [Administration](/dev/learn/administration/)
    - [Risks](/dev/learn/risks/)
    - [Glossary](/dev/learn/glossary/)
        
        - [Ballot](/dev/learn/glossary/ballot/)
        - [Data source](/dev/learn/glossary/data-source/)
        - [Delegate](/dev/learn/glossary/delegate/)
        - [Discount rate](/dev/learn/glossary/discount-rate/)
        - [Funding cycle](/dev/learn/glossary/funding-cycle/)
        - [Hold fees](/dev/learn/glossary/hold-fees/)
        - [NFT Rewards](/dev/learn/glossary/nft-rewards/)
        - [Operator](/dev/learn/glossary/operator/)
        - [Overflow](/dev/learn/glossary/overflow/)
        - [Payment terminal](/dev/learn/glossary/payment-terminal/)
        - [Project](/dev/learn/glossary/project/)
        - [Redemption rate](/dev/learn/glossary/redemption-rate/)
        - [Reserved tokens](/dev/learn/glossary/reserved-tokens/)
        - [Split allocator](/dev/learn/glossary/split-allocator/)
        - [Splits](/dev/learn/glossary/splits/)
        - [Token Store](/dev/learn/glossary/token-store/)
        - [Tokens](/dev/learn/glossary/tokens/)
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
- [Glossary](/dev/learn/glossary/)
- Data source

On this page

# Data source

#### What everyone needs to know[​](#what-everyone-needs-to-know "Direct link to What everyone needs to know")

- A data source contract is a way of providing extensions to a treasury that either override or augment the default [`JBPayoutRedemptionPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/) functionality.
- A data source contract can be used to provide custom data to the [`JBPayoutRedemptionPaymentTerminal3_1_1.pay(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#pay) transaction and/or the [`JBPayoutRedemptionPaymentTerminal3_1_1.redeemTokensOf(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#redeemtokensof) transaction.
- A data source is passed contextual information from the transactions, from which it can derive custom data for the protocol to use to affect subsequent behaviors in the pay and redeem transactions. Contextual information from the pay transaction is passed to the data source in the form of [`JBPayParamsData`](/dev/api/data-structures/jbpayparamsdata/) , and contextual information from the redeem transaction is passed to the data source in the form of [`JBRedeemParamsData`](/dev/api/data-structures/jbredeemparamsdata/).
- Data sources can revert under custom circumstances, which can be used to create a gated treasury, max token supply, min contribution amount, etc.
- A data source is responsible for specifying any [delegate](/dev/learn/glossary/delegate/) hooks that should be triggered after the core functionality of a [`pay(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#pay) or [`redeemTokensOf(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#redeemtokensof) transaction executes successfully.
- Each [`IJBPaymentTerminal`](/dev/api/interfaces/ijbpaymentterminal/) fork can leverage data sources in unique ways.

#### What you'll want to know if you're building[​](#what-youll-want-to-know-if-youre-building "Direct link to What you'll want to know if you're building")

- A data source must adhere to the [`IJBFundingCycleDataSource3_1_1`](/dev/api/interfaces/ijbfundingcycledatasource3_1_1/) interface.
- A data source contract can be specified in a funding cycle, along with flags that indicate if the funding cycle should `useDataSourceForPay` and/or `useDataSourceForRedeem`. These are set either in [`JBController3_1.launchProjectFor(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#launchprojectfor) or [`JBController3_1.reconfigureFundingCyclesOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#reconfigurefundingcyclesof).
- A funding cycle's data source is called upon in [`JBSingleTokenPaymentTerminalStore3_1_1.recordPaymentFrom(...)`](/dev/api/contracts/jbsingletokenpaymentterminalstore3_1_1/#recordpaymentfrom) and in [`JBSingleTokenPaymentTerminalStore3_1_1.recordRedemptionFor(...)`](/dev/api/contracts/jbsingletokenpaymentterminalstore3_1_1/#recordredemptionfor).
- A data source has implicit permissions to [`JBController3_1.mintTokensFor(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#minttokensfor) on a project's behalf.
- If a data source is not specified in a funding cycle, or if flags aren't explicitly set, default protocol data will be used.

[Get started building data sources](/dev/build/treasury-extensions/data-source/).

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/glossary/data-source.md)

[

Previous

Ballot

](/dev/learn/glossary/ballot/)[

Next

Delegate

](/dev/learn/glossary/delegate/)

- [What everyone needs to know](#what-everyone-needs-to-know)
- [What you'll want to know if you're building](#what-youll-want-to-know-if-youre-building)