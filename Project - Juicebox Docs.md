[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/glossary/project//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/glossary/project/)
- [中文](/zh/dev/learn/glossary/project/)

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
- Project

On this page

# Project

#### What everyone needs to know[​](#what-everyone-needs-to-know "Direct link to What everyone needs to know")

- Each project within the Juicebox protocol is represented as an ERC-721 NFT.
- Whoever is the owner of a project's NFT has access to [admin functionality](/dev/learn/glossary/operator/) for that project within the protocol, which ultimately gives it control over the project's funds.

#### What you'll want to know if you're building[​](#what-youll-want-to-know-if-youre-building "Direct link to What you'll want to know if you're building")

- Projects can be created either within the context of Juicebox with a call to [`JBController3_1.launchProjectFor(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#launchprojectfor) which also configures its funding cycle properties and sets it up to receive payments, or by itself with a call to [`JBProjects.createFor(...)`](/dev/api/contracts/jbprojects/write/createfor/). The `launchProjectFor(...)` transaction calls `createFor(...)` as part of its routine.
- A project can accommodate arbitrary metadata for any number of domains that can be updated by the project owner at any time using the [`JBProject.setMetadataOf(...)`](/dev/api/contracts/jbprojects/write/setmetadataof/) transaction. This can be used by clients to store a reference to metadata stored on IPFS (or anywhere else). The protocol does not define standards for this metadata. A project's current metadata for any particular domain can be found by reading from [`JBProject.metadataContentOf(...)`](/dev/api/contracts/jbprojects/properties/metadatacontentof/).
- Look through the [`JBProjects`](/dev/api/contracts/jbprojects/) contract for a complete list of relevant read functions, write functions, and emitted events.

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/glossary/project.md)

[

Previous

Payment terminal

](/dev/learn/glossary/payment-terminal/)[

Next

Redemption rate

](/dev/learn/glossary/redemption-rate/)

- [What everyone needs to know](#what-everyone-needs-to-know)
- [What you'll want to know if you're building](#what-youll-want-to-know-if-youre-building)