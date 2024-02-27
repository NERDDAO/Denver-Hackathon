[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/build/treasury-extensions/redemption-delegate//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/build/treasury-extensions/redemption-delegate/)
- [中文](/zh/dev/build/treasury-extensions/redemption-delegate/)

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
- Redemption delegate

On this page

# Redemption delegate

Before implementing, learn about delegates [here](/dev/learn/glossary/delegate/). Also see [`juice-delegate-template`](https://github.com/mejango/juice-delegate-template).

#### Specs[​](#specs "Direct link to Specs")

A contract can become a treasury redemption delegate by adhering to [`IJBRedemptionDelegate3_1_1`](/dev/api/interfaces/ijbredemptiondelegate3_1_1/):

```
interface IJBRedemptionDelegate3_1_1 is IERC165 {  function didRedeem(JBDidRedeemData3_1_1 calldata data) external payable;}
```

When extending the redemption functionality with a delegate, the protocol will pass a [`JBDidRedeemData3_1_1`](/dev/api/data-structures/jbdidredeemdata3_1_1/) to the `didRedeem(...)` function:

```
struct JBDidRedeemData3_1_1 {    address holder;    uint256 projectId;    uint256 currentFundingCycleConfiguration;    uint256 projectTokenCount;    JBTokenAmount reclaimedAmount;    JBTokenAmount forwardedAmount;    address payable beneficiary;    string memo;    bytes dataSourceMetadata;    bytes redeemerMetadata;}
```

```
struct JBTokenAmount {  address token;  uint256 value;  uint256 decimals;  uint256 currency;}
```

The `msg.sender` to the delegate will be the payment terminal that facilitated the redemption.

In payment terminals based on the [`JBPayoutRedemptionPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/), such as [`JBETHPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jbethpaymentterminal3_1_1/)'s and [`JBERC20PaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jberc20paymentterminal3_1_1/)'s, the redemption delegate hook gets called _before_ the reclaimed amount is sent to the redemption beneficiary, but after all internal accounting has been updated. [View the docs](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#redeemtokensof).

Make sure to only allow trusted contracts to access the `didRedeem(...)` transaction.

#### Attaching[​](#attaching "Direct link to Attaching")

New delegate contracts should be deployed independently. Once deployed, its address can be returned from a data source hook. See [how to build a data source](/dev/build/treasury-extensions/data-source/) for more.

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/build/treasury-extensions/redemption-delegate.md)

[

Previous

Pay delegate

](/dev/build/treasury-extensions/pay-delegate/)[

Next

Split allocator

](/dev/build/treasury-extensions/split-allocator/)

- [Specs](#specs)
- [Attaching](#attaching)