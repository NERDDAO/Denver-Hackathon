[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/build/getting-started//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/build/getting-started/)
- [中文](/zh/dev/build/getting-started/)

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
        
    - [Utilities](#)
        
    - [Namespaces & IDs](/dev/build/namespace/)
    - [Contract Examples](/dev/build/examples/)
- [API](#)
    
    - [Data Structures](#)
        
    - [Enums](#)
        
    - [Libraries](#)
        
    - [Interfaces](#)
        
    - [Contracts](/dev/api/contracts/)
        
        - [JBProjects](/dev/api/contracts/jbprojects/)
            
        - [JBTokenStore](/dev/api/contracts/jbtokenstore/)
            
        - [JBFundingCycleStore](/dev/api/contracts/jbfundingcyclestore/)
            
        - [JBSplitsStore](/dev/api/contracts/jbsplitsstore/)
            
        - [JBPrices](/dev/api/contracts/jbprices/)
            
        - [JBOperatorStore](/dev/api/contracts/jboperatorstore/)
            
        - [JBToken](/dev/api/contracts/jbtoken/)
            
        - [JBDirectory](/dev/api/contracts/jbdirectory/)
            
        - [JBFundAccessConstraintsStore](/dev/api/contracts/jbfundaccessconstraintsstore/)
        - [JBSingleTokenPaymentTerminalStore3_1](/dev/api/contracts/jbsingletokenpaymentterminalstore3_1/)
        - [JBSingleTokenPaymentTerminalStore3_1_1](/dev/api/contracts/jbsingletokenpaymentterminalstore3_1_1/)
        - [| Payment terminals](#)
            
        - [| Controllers](#)
            
        - [| Price Feeds](#)
            
        - [| Ballots](#)
            
        - [| Utilities](#)
            
        - [| Abstract](#)
            
- [Extensions](#)
    
- [Resources](#)
    
- [Frontend](/dev/frontend/)
    
- [Deprecated](#)
    

- [](/)
- Build
- Getting started

On this page

# Getting started

info

If you're interested in building a Juicebox smart contract, see the `juice-contract-template` [GitHub Repository](https://github.com/jbx-protocol/juice-contract-template). If you need any help, join our [Discord server](https://discord.gg/juicebox).

#### Import[​](#import "Direct link to Import")

Add the protocol files to the project.

```
# command linenpm install @jbx-protocol/juice-contracts-v3/
```

If referencing from typescript:

```
const contract = require(`@jbx-protocol/juice-contracts-v3/deployments/${network}/${contractName}.json`)
```

If referencing from a contract:

```
import '@jbx-protocol/juice-contracts-v3/contracts/[file-path].sol'
```

#### Now what[​](#now-what "Direct link to Now what")

From here, you can build the following:

[Basics](/dev/build/basics/): Interact with the protocol's basic functionality. Useful for building front-ends.

[Pay a project](/dev/build/utilities/project-payer/): Deploy or inherit from a contract that makes it easy to forward funds to Juicebox projects.

[Split payments](/dev/build/utilities/splits-payer/): Deploy or inherit from a contract that makes it easy to forward funds to groups of splits whose members are either addresses, Juicebox projects, or arbitrary contracts that inherit from [`IJBSplitAllocator`](/dev/build/treasury-extensions/split-allocator/).

[Program a treasury](/dev/build/programmable-treasury/): Get familiar with the configurable properties available when launching a project.

[Program project permissions](/dev/build/project-nft/): Build custom Juicebox Project NFT logic to create your own project access controls.

[Program treasury extensions](/dev/build/treasury-extensions/): Create custom contractual rules defining what happens when a project receives funds, and under what conditions funds can leave the treasury during a funding cycle.

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/build/getting-started.md)

[

Previous

Tokens

](/dev/learn/glossary/tokens/)[

Next

Basics

](/dev/build/basics/)

- [Import](#import)
- [Now what](#now-what)