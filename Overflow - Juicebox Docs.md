[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/glossary/overflow//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/glossary/overflow/)
- [中文](/zh/dev/learn/glossary/overflow/)

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
- Overflow

On this page

# Overflow

#### What everyone needs to know[​](#what-everyone-needs-to-know "Direct link to What everyone needs to know")

- A project can set distribution limits from its treasury on a per funding cycle basis using [`JBController3_1.launchProjectFor(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#launchprojectfor) and [`JBController3_1.reconfigureFundingCyclesOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#reconfigurefundingcyclesof). These limits are stored in [`JBFundAccessConstraintsStore.distributionLimitOf(...)`](/dev/api/contracts/jbfundaccessconstraintsstore/#distributionlimitof). Any funds that are in the project's Juicebox treasury that it hasn't specified as distributable are considered overflow.
- Overflow serves as a project's runway since future funding cycles can tap into it within the bounds of the preconfigured distribution limits. Overflow can also serve as a refund or rebate mechanism, where everyone's net contribution price is pushed towards zero as volume outpaces what the project needs.
- By default, overflow also serves a means for allowing community members to exit with a portion of the treasury's funds in hand. Any funds in overflow are reclaimable by the project's community by redeeming community tokens along a bonding curve defined by the project's current [redemption rate](/dev/learn/glossary/redemption-rate/). Projects can override or extend this functionality using a custom [data source](/dev/learn/glossary/data-source/).
- Projects can manage how much money is in overflow (and therefore how much each member can exit with) either by adjusting its distribution limits or by using a custom redemption extension.
- A project can set overflow allowances from its treasury on a per-funding-cycle-configuration basis within the [`JBController3_1.launchProjectFor(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#launchprojectfor) and [`JBController3_1.reconfigureFundingCyclesOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#reconfigurefundingcyclesof) transactions. These allowances are stored in [`JBFundAccessConstraintsStore.overflowAllowanceOf(...)`](/dev/api/contracts/jbfundaccessconstraintsstore/#overflowallowanceof). A project's owner can distribute the project's funds from its overflow on-demand up until the preconfigured allowance. Overflow allowances do not reset each funding cycle, they last until a new funding cycle reconfiguration takes effect.

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/glossary/overflow.md)

[

Previous

Operator

](/dev/learn/glossary/operator/)[

Next

Payment terminal

](/dev/learn/glossary/payment-terminal/)

- [What everyone needs to know](#what-everyone-needs-to-know)