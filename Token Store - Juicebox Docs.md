[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/glossary/token-store//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/glossary/token-store/)
- [中文](/zh/dev/learn/glossary/token-store/)

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
- Token Store

On this page

# Token Store

#### What everyone needs to know[​](#what-everyone-needs-to-know "Direct link to What everyone needs to know")

- A token store contract manages project token balances, as well as minting and burning.
- All projects using the protocol share a token store (within one protocol version). It is a [core protocol contract](/dev/learn/architecture/) – for Juicebox, this is [`JBTokenStore`](/dev/api/contracts/jbtokenstore/).
- [`JBTokenStore`](/dev/api/contracts/jbtokenstore/) contains several useful read methods: [`JBTokenStore.balanceOf(...)`](/dev/api/contracts/jbtokenstore/read/balanceof/) returns a holder's total token balance for a project (including claimed and unclaimed tokens), and [`JBTokenStore.totalSupplyOf(...)`](/dev/api/contracts/jbtokenstore/read/totalsupplyof/) returns a project token's total supply (also including claimed and unclaimed tokens).
- Project owners can call [`JBTokenStore.issueFor(...)`](/dev/api/contracts/jbtokenstore/write/issuefor/) to issue a claimable ERC-20 for their project token.

#### What you'll want to know if you're building[​](#what-youll-want-to-know-if-youre-building "Direct link to What you'll want to know if you're building")

- A token store is a [core protocol contract](/dev/learn/architecture/) which must adhere to the [`IJBTokenStore`](/dev/api/interfaces/ijbtokenstore/) interface.
- A project's token store address can be accessed via [`JBController3_1.tokenStore`](/dev/api/contracts/or-controllers/jbcontroller3_1/#tokenstore).
- Projects do not typically interact directly with [`JBTokenStore`](/dev/api/contracts/jbtokenstore/), instead using methods on the project's controller. For new projects, this is [`JBController3_1`](/dev/api/contracts/or-controllers/jbcontroller3_1/).

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/glossary/token-store.md)

[

Previous

Splits

](/dev/learn/glossary/splits/)[

Next

Tokens

](/dev/learn/glossary/tokens/)

- [What everyone needs to know](#what-everyone-needs-to-know)
- [What you'll want to know if you're building](#what-youll-want-to-know-if-youre-building)