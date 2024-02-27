[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/build/treasury-extensions/split-allocator//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/build/treasury-extensions/split-allocator/)
- [中文](/zh/dev/build/treasury-extensions/split-allocator/)

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
- Split allocator

On this page

# Split allocator

Before implementing, learn about allocators [here](/dev/learn/glossary/split-allocator/), and splits [here](/dev/learn/glossary/splits/).

#### Specs[​](#specs "Direct link to Specs")

A contract can become a split allocator by adhering to [`IJBSplitAllocator`](/dev/api/interfaces/ijbsplitallocator/):

```
interface IJBSplitAllocator {  function allocate(JBSplitAllocationData calldata _data) external payable;}
```

When extending payout distribution or reserved token distribution functionality with an allocator, the protocol will pass a [`JBSplitAllocationData`](/dev/api/data-structures/jbsplitallocationdata/) to the `allocate(...)` function:

```
struct JBSplitAllocationData {  address token;  uint256 amount;  uint256 decimals;  uint256 projectId;  uint256 group;  JBSplit split;}
```

```
struct JBSplit {  bool preferClaimed;  bool preferAddToBalance;  uint256 percent;  uint256 projectId;  address payable beneficiary;  uint256 lockedUntil;  IJBSplitAllocator allocator;}
```

The `msg.sender` to the allocator will either be the payment terminal that facilitated the payout distribution, or the controller that facilitated the reserved tokens distribution.

In payment terminals based on the [`JBPayoutRedemptionPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/), such as [`JBETHPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jbethpaymentterminal3_1_1/)'s and [`JBERC20PaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jberc20paymentterminal3_1_1/)'s, the allocator hook gets called while the payouts are being distributed to splits. [View the docs](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1/#_distributetopayoutsplitsof).

- If the allocation is coming from an ETH payment terminal such as [`JBETHPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jbethpaymentterminal3_1_1/), the ETH will be included in the call to `allocate(...)`.
- If the allocation is coming from an ERC20 payment terminal such as [`JBERC20PaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jberc20paymentterminal3_1_1/), the tokens will be pre-approved for the allocator contract to transfer them to it. Make sure to initiate the transfer, and make sure to not leave allocated tokens stuck in the allocator contract.
- If the allocation is coming from a controller such as [`JBController3_1`](/dev/api/contracts/or-controllers/jbcontroller3_1/) distributing reserved tokens, the tokens will be minted pre-distributed to the allocator's address. If the split's `preferClaimed` property is `true` and the project has a token a contract attached, the tokens will be minted directly to the allocator contract. Otherwise, they will be allocated in the [`JBTokenStore`](/dev/api/contracts/jbtokenstore/) as unclaimed tokens from which the allocator can then [`claimFor(...)`](/dev/api/contracts/jbtokenstore/write/claimfor/) itself or [`transferFrom(...)`](/dev/api/contracts/jbtokenstore/write/transferfrom/) itself to another address. Make sure to not leave allocated tokens stuck in the allocator contract or unclaimed in the [`JBTokenStore`](/dev/api/contracts/jbtokenstore/) contract.

#### Attaching[​](#attaching "Direct link to Attaching")

New allocator contracts should be deployed independently. Once deployed, its address can be configured into a project's payout splits or reserved token splits so that any distribution triggered while the funding cycle is active sends the relevant token to the allocator contract's `allocate(...)` hook.

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/build/treasury-extensions/split-allocator.md)

[

Previous

Redemption delegate

](/dev/build/treasury-extensions/redemption-delegate/)[

Next

Project payer

](/dev/build/utilities/project-payer/)

- [Specs](#specs)
- [Attaching](#attaching)