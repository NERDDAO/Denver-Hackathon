[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/build/treasury-extensions/ballot//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/build/treasury-extensions/ballot/)
- [中文](/zh/dev/build/treasury-extensions/ballot/)

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
- [Treasury extensions](/dev/build/treasury-extensions/)
- Ballot

On this page

# Ballot

Before implementing, learn about ballots [here](/dev/learn/glossary/ballot/).

#### Specs[​](#specs "Direct link to Specs")

A contract can become a funding cycle ballot by adhering to [`IJBFundingCycleBallot`](/dev/api/interfaces/ijbfundingcycleballot/):

```
interface IJBFundingCycleBallot {  function duration() external view returns (uint256);  function stateOf(    uint256 _projectId,    uint256 _configuration,    uint256 _start  ) external view returns (JBBallotState);}
```

There are two functions that must be implemented: `duration(...)` and `stateOf(...)`. The result of `duration(...)` is the number of seconds the ballot lasts for from the moment the reconfiguration is proposed. During this time, the protocol automatically interprets the ballot's state as [`JBBallotState.Active`](/dev/api/enums/jbballotstate/). The result of `stateOf(...)` returns the [`JBBallotState`](/dev/api/enums/jbballotstate/). If a configuration is approved and the duration has expired, the [`JBFundingCycleStore`](/dev/api/contracts/jbfundingcyclestore/) will use it as the project's current funding cycle when it becomes active. Otherwise, it will make a copy of the latest approved cycle to use.

When extending the pay functionality with a delegate, the protocol will pass a `projectId`, a `configuration`, and a `start` to the `stateOf(...)` function. `configuration` is the identifier of the funding cycle being evaluated, and also the unix timestamp in seconds of when the reconfiguration was proposed. `start` is the unix timestamp the reconfiguration is scheduled to start at if that reconfiguration is approved.

Once the `duration(...)` has expired, the returned value of `stateOf(...)` should no longer change.

#### Attaching[​](#attaching "Direct link to Attaching")

New ballot contracts should be deployed independently. Once deployed, its address can be configured into a project's funding cycle. The ballot will take effect while that funding cycle is active, and will be used for evaluating subsequent reconfigurations.

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/build/treasury-extensions/ballot.md)

[

Previous

Treasury extensions

](/dev/build/treasury-extensions/)[

Next

Data source

](/dev/build/treasury-extensions/data-source/)

- [Specs](#specs)
- [Attaching](#attaching)