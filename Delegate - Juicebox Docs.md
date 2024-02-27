[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/glossary/delegate//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/glossary/delegate/)
- [中文](/zh/dev/learn/glossary/delegate/)

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
- Delegate

On this page

# Delegate

#### What everyone needs to know[​](#what-everyone-needs-to-know "Direct link to What everyone needs to know")

- A delegate contract is a way of providing extensions to a treasury that augments the default [`JBPayoutRedemptionPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/) behavior.
- Pay delegates include a custom `didPay(...)` hook that will execute after all of the default protocol pay logic has successfully executed in the terminal contract. The hook is passed a bunch of contextual information via a [`JBDidPayData`](/dev/api/data-structures/jbdidpaydata/) data structure.
- Redemption delegates include a custom `didRedeem(...)` hook that will execute after all of the default protocol redeem logic has successfully executed in the terminal contract. The hook is passed a bunch of contextual information via a [`JBDidRedeemData`](/dev/api/data-structures/jbdidredeemdata/) data structure. The `didRedeem(...)` hook gets called before any reclaimed tokens are transferred out of the terminal contract.
- Each [`IJBPaymentTerminal`](/dev/api/interfaces/ijbpaymentterminal/) fork can leverage delegates in unique ways.

#### What you'll want to know if you're building[​](#what-youll-want-to-know-if-youre-building "Direct link to What you'll want to know if you're building")

- There are two types of delegates: [`IJBPayDelegate3_1_1`](/dev/api/interfaces/ijbpaydelegate3_1_1/)s and [`IJBRedemptionDelegate3_1_1`](/dev/api/interfaces/ijbredemptiondelegate3_1_1/)s. Any contract that adheres to these interfaces can be used as a delegate in a project's funding cycles.
- The funding cycle's [`dataSource`](/dev/learn/glossary/data-source/) specifies the active Delegate contracts.
- The [`IJBPayDelegate3_1_1`](/dev/api/interfaces/ijbpaydelegate3_1_1/)'s `didPay(...)` hook is triggered in [`JBPayoutRedemptionPaymentTerminal3_1_1._pay(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#_pay), and the [`IJBRedemptionDelegate`](/dev/api/interfaces/ijbredemptiondelegate/)'s `didRedeem(...)` hook is triggered in [`JBPayoutRedemptionPaymentTerminal3_1_1.redeemTokensOf(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#redeemtokensof).
- The redemption delegate hook is called before funds are dispersed.

[Get started building pay delegates](/dev/build/treasury-extensions/pay-delegate/).

[Get started building redemption delegates](/dev/build/treasury-extensions/redemption-delegate/).

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/glossary/delegate.md)

[

Previous

Data source

](/dev/learn/glossary/data-source/)[

Next

Discount rate

](/dev/learn/glossary/discount-rate/)

- [What everyone needs to know](#what-everyone-needs-to-know)
- [What you'll want to know if you're building](#what-youll-want-to-know-if-youre-building)