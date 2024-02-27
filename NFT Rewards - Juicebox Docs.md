[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/glossary/nft-rewards//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/glossary/nft-rewards/)
- [中文](/zh/dev/learn/glossary/nft-rewards/)

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
- NFT Rewards

On this page

# NFT Rewards

#### What everyone needs to know[​](#what-everyone-needs-to-know "Direct link to What everyone needs to know")

- NFT Rewards can be attached to a project's funding cycles, allowing any payment made to the project to also qualify for the minting of an NFT along any number of tiers.
- Each project can deploy NFT rewards with customizable parameters. Each tier can be specified to have:
    - Contribution floor specified in ETH or USD, the minimum contribution necessary to mint an NFT from the tier.
    - Max quantity.
    - Reserved rate, specifying the number of NFTs from the tier that can be minted to a predefined beneficiary address as a proportion of NFTs minted to contributors.
    - Voting units, specifying a number to associate with NFTs from each tier that can be used in on-chain or off-chain governance.
    - A URI, overridable by a URI resolver that can return dynamic values for each unit with the tier.
    - A flag specifying if the contract's owner can manually mint from the tier on-demand.
    - A lock date, before which the tier must remain accessible.
- The NFT Rewards contract's owner can add and remove tiers on demand, subject to flags passed in at the time of its creation:
    - If the contract is set to lock reserved token changes, new tiers cannot have a reserved rate.
    - If the contract is set to lock voting unit changes, new tiers cannot have voting units.
    - If the contract is set to lock manual minting changes, new tiers cannot allow manual minting.
    - If the contract is set to have transfers pausable, a funding cycle metadata flag will determine if NFTs are transferable while the cycle is active.
- Incoming payments can directly specify any number of tiers to mint from within their [`JBDidPayData.metadata`](/dev/api/data-structures/jbdidpaydata/).
- If a payment received does not meet a minting threshold or is in excess of the minted tiers, the balance is stored as a credit which will be added to future payments and applied to mints at that time. A flag can also be passed alongside a payment to avoid accepting payments that aren't applied to mints in full.
- The NFT Rewards contract can be used for on-chain governance. At the time of the contract's creation, the deployer must specify if vote delegation should be accounted for across all tiers (compatible with Governor contracts), on a per-tier basis, or if there should not be any extra governance accounting affordances.

#### What you'll want to know if you're building[​](#what-youll-want-to-know-if-youre-building "Direct link to What you'll want to know if you're building")

- An project can be deployed with a new NFT Rewards contract attached using the [`JBTiered721DelegateProjectDeployer.launchProjectFor(...)`](/dev/extensions/juice-721-delegate/contracts/contract.JBTiered721DelegateProjectDeployer/#launchprojectfor) transaction.
- A project can be reconfigured with a new NFT Rewards contract using the [`JBTiered721DelegateProjectDeployer.reconfigureFundingCyclesOf(...)`](/dev/extensions/juice-721-delegate/contracts/contract.JBTiered721DelegateProjectDeployer/#reconfigurefundingcyclesof) transaction.
- An already-existing NFT rewards contract can be passed into the standard [`JBController3_1.launchProjectFor(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#launchprojectfor) and [`JBController3_1.reconfigureFundingCyclesOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#reconfigurefundingcyclesof) transactions in the funding cycle's metadata.

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/glossary/nft-rewards.md)

[

Previous

Hold fees

](/dev/learn/glossary/hold-fees/)[

Next

Operator

](/dev/learn/glossary/operator/)

- [What everyone needs to know](#what-everyone-needs-to-know)
- [What you'll want to know if you're building](#what-youll-want-to-know-if-youre-building)