[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/glossary/tokens//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/glossary/tokens/)
- [中文](/zh/dev/learn/glossary/tokens/)

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
- Tokens

On this page

# Tokens

#### What everyone needs to know[​](#what-everyone-needs-to-know "Direct link to What everyone needs to know")

- By default, all payments that come in to a Juicebox project mint tokens. These tokens are distributed to a beneficiary specified by the payer, and to any addresses specified in the project's reserved token list. The amount of tokens minted depends on the amount paid and the `weight` (i.e. exchange rate) of the project's current funding cycle. Projects can override or extended this default behavior using [data sources](/dev/learn/glossary/data-source/).
- By default, the protocol allocates tokens to recipients using an internal accounting mechanism in [`JBTokenStore`](/dev/api/contracts/jbtokenstore/). These are fungible but do not conform to the ERC-20 standard, and as such cannot be composed with ecosystem ERC-20/ERC-721 marketplaces like AMMs and OpenSea. Their balances can be used for voting on various platforms.
- Projects can issue their own ERC-20 token directly from the protocol to use as its token. Projects can also bring their own token as long as it conforms to the [`IJBToken`](/dev/api/interfaces/ijbtoken/) interface and uses 18 decimal fixed point accounting. This makes it possible to use ERC-1155's or custom tokens.
- Once a project has issued a token, token holders can export tokens from the protocol's internal accounting mechanism in [`JBTokenStore`](/dev/api/contracts/jbtokenstore/) to their wallet to use across Web3. A project's owner can also force project tokens to be issued directly to the exported version. This bypasses the internal accounting mechanism, but slightly increases gas costs for transactions that requires tokens to be minted.
- By default, tokens can be [redeemed](/dev/learn/glossary/redemption-rate/) by holders to reclaim a portion of what's in the project's [overflow](/dev/learn/glossary/overflow/). The amount of overflow claimable is determined by the [`redemptionRate`](/dev/learn/glossary/redemption-rate/) of the project's current funding cycle. Projects can override or extend this default behavior. Redeeming tokens burns them, shrinking the total supply.
- A project owner can mint and distribute more of the project's tokens on demand. This behavior must be explicitly allowed on a per-funding cycle basis.
- A project can use its tokens however it wishes. It can be purely ceremonial, used for governance, used for airdrops, or whatever.

#### What you'll want to know if you're building[​](#what-youll-want-to-know-if-youre-building "Direct link to What you'll want to know if you're building")

- Tokens can be minted on-demand by project owners or their operators by calling [`JBController3_1.mintTokensOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#minttokensof). The ability to do so must be explicitly turned on via a funding cycle configuration metadata parameter.
- Tokens can be burned on-demand by holders by calling [`JBController3_1.burnTokensOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#burntokensof). The ability to do so can be turned off via a funding cycle configuration metadata parameter.

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/glossary/tokens.md)

[

Previous

Token Store

](/dev/learn/glossary/token-store/)[

Next

Getting started

](/dev/build/getting-started/)

- [What everyone needs to know](#what-everyone-needs-to-know)
- [What you'll want to know if you're building](#what-youll-want-to-know-if-youre-building)