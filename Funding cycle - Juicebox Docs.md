[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/glossary/funding-cycle//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/glossary/funding-cycle/)
- [中文](/zh/dev/learn/glossary/funding-cycle/)

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
- Funding cycle

On this page

# Funding cycle

#### What everyone needs to know[​](#what-everyone-needs-to-know "Direct link to What everyone needs to know")

- Projects can configure funding cycles to create rules to follow over set amounts of time.
- A funding cycle's parameters can't be changed while it is in progress, but the project owner can propose reconfigurations to an upcoming cycle at any time.
- Funding cycles roll over automatically. If there is a reconfiguration in place and it has been approved by the current cycle's [ballot](/dev/learn/glossary/ballot/), it will be used. Otherwise, a copy of the current funding cycle will be used with an updated `start` time and discounted `weight`.
- The mechanics of each project can vary dramatically depending on how its funding cycles are configured over time. [Become familiar with how projects work](/dev/learn/glossary/project/) to get a better understanding of how these decisions can be made.

#### What you'll want to know if you're building[​](#what-youll-want-to-know-if-youre-building "Direct link to What you'll want to know if you're building")

- A funding cycle is represented as a [`JBFundingCycle`](/dev/api/data-structures/jbfundingcycle/) data structure.
- It is possible to create funding cycles that allow for total flexibility, total rigidity, or anything in between. Flexibility can be useful for rapid experimentation and evolution, whereas rigidity can be useful for dependability and trust. Anyone can configure a project's first funding cycle alongside creating the project with a call to [`JBController3_1.launchProjectFor(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#launchprojectfor), and the project's owner can issue a reconfiguration to subsequent funding cycles with a call to [`JBController3_1.reconfigureFundingCyclesOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#reconfigurefundingcyclesof).
- If a project has a current funding cycle, it can be found by reading from [`JBFundingCycleStore.currentOf(...)`](/dev/api/contracts/jbfundingcyclestore/read/currentof/). A project's upcoming funding cycle can be found by reading from [`JBFundingCycleStore.queuedOf(...)`](/dev/api/contracts/jbfundingcyclestore/read/queuedof/). The funding cycles that carry each original configuration can be found by reading from [`JBFundingCycleStore.get(...)`](/dev/api/contracts/jbfundingcyclestore/read/get/). [`JBController3_1.currentFundingCycleOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#currentfundingcycleof) and [`JBController3_1.queueFundingCycleOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#queuedfundingcycleof) can also be used to get a reference to the funding cycle's metadata alongside.
- A funding cycle's [`ballot`](/dev/learn/glossary/ballot/) property is useful for setting rules by which any proposed reconfiguration to subsequent cycles must adhere. This is useful for community oriented projects as it can prevent a project owner from maliciously updating an upcoming cycle's configuration moments before it begins without the broader community's consent. A funding cycle's ballot status, which is a [`JBBallotState`](/dev/api/enums/jbballotstate/) enumeration, can be found by reading from [`JBFundingCycleStore.currentBallotStateOf(...)`](/dev/api/contracts/jbfundingcyclestore/read/currentballotstateof/).
- Look through the [`JBFundingCycleStore`](/dev/api/contracts/jbfundingcyclestore/) contract for a complete list of relevant read functions, write functions, and emitted events. Several properties of [`JBController3_1`](/dev/api/contracts/or-controllers/jbcontroller3_1/) and [`JBSingleTokenPaymentTerminalStore3_1`](/dev/api/contracts/jbsingletokenpaymentterminalstore3_1/) also store information relative to funding cycle configurations.

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/glossary/funding-cycle.md)

[

Previous

Discount rate

](/dev/learn/glossary/discount-rate/)[

Next

Hold fees

](/dev/learn/glossary/hold-fees/)

- [What everyone needs to know](#what-everyone-needs-to-know)
- [What you'll want to know if you're building](#what-youll-want-to-know-if-youre-building)