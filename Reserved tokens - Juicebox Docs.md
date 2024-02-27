[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/glossary/reserved-tokens//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/glossary/reserved-tokens/)
- [中文](/zh/dev/learn/glossary/reserved-tokens/)

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
- Reserved tokens

On this page

# Reserved tokens

#### What everyone needs to know[​](#what-everyone-needs-to-know "Direct link to What everyone needs to know")

- Reserved tokens allow a project to guarantee that a percentage of all newly minted tokens from payments will be reserved to a preprogrammed list of [`JBSplit`](/dev/api/data-structures/jbsplit/)s. This percentage is referred to as the _reserved rate_.
- A project's reserved rate and reserved token splits can be reconfigured each funding cycle.
- Reserved token splits can be routed to addresses, the owners of other Juicebox projects, to contracts that adhere to the [`IJBSplitAllocator`](/dev/api/interfaces/ijbsplitallocator/) interface, or to the address that sent the [`JBController3_1.distributeReservedTokensOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#distributereservedtokensof) transaction.
- Reserved tokens do not get minted automatically when a new payment is received. Instead, they must be explicitly distributed during the funding cycle which contains the reserved rate and splits that should be applied. If a funding cycle's reserved rate or splits change before the allocation is distributed, the new values will apply.

#### What you'll want to know if you're building[​](#what-youll-want-to-know-if-youre-building "Direct link to What you'll want to know if you're building")

- A reserved rate can be specified in a funding cycle through the [`JBController3_1.launchProjectFor(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#launchprojectfor) or [`JBController3_1.reconfigureFundingCyclesOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#reconfigurefundingcyclesof) transactions.
- Distributing currently allocated reserved tokens is done by calling [`JBController3_1.distributeReservedTokensOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#distributereservedtokensof). Doing so will distribute the allocation according to the current funding cycle's reserved rate.

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/glossary/reserved-tokens.md)

[

Previous

Redemption rate

](/dev/learn/glossary/redemption-rate/)[

Next

Split allocator

](/dev/learn/glossary/split-allocator/)

- [What everyone needs to know](#what-everyone-needs-to-know)
- [What you'll want to know if you're building](#what-youll-want-to-know-if-youre-building)