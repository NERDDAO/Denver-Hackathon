[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/glossary/payment-terminal//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/glossary/payment-terminal/)
- [中文](/zh/dev/learn/glossary/payment-terminal/)

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
- Payment terminal

On this page

# Payment terminal

#### What everyone needs to know[​](#what-everyone-needs-to-know "Direct link to What everyone needs to know")

- A project can be configured to use any contract(s) that adheres to [`IJBPaymentTerminal`](/dev/api/interfaces/ijbpaymentterminal/) to manage its inflows and outflows of token funds.
- Each payment terminal can have a unique distribution limit and overflow allowance.
- Each payment terminal can behave differently when it receives payments.

#### What you'll want to know if you're building[​](#what-youll-want-to-know-if-youre-building "Direct link to What you'll want to know if you're building")

- A project can set its terminals using [`JBDirectory.setTerminalsOf(...)`](/dev/api/contracts/jbdirectory/write/setterminalsof/).
- If a project uses multiple terminals to manage funds for the same token, it can set the primary one (where other Web3 contracts should send funds to) using [`JBDirectory.setPrimaryTerminalOf(...)`](/dev/api/contracts/jbdirectory/write/setprimaryterminalof/).
- To pay a project with a certain token, get its preferred payment terminal using [`JBDirectory.primaryTerminalOf(...)`](/dev/api/contracts/jbdirectory/read/primaryterminalof/). If no terminal is returned, the project is not currently accepting the specified token.

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/glossary/payment-terminal.md)

[

Previous

Overflow

](/dev/learn/glossary/overflow/)[

Next

Project

](/dev/learn/glossary/project/)

- [What everyone needs to know](#what-everyone-needs-to-know)
- [What you'll want to know if you're building](#what-youll-want-to-know-if-youre-building)