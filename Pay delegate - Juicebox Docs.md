[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/build/treasury-extensions/pay-delegate//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/build/treasury-extensions/pay-delegate/)
- [中文](/zh/dev/build/treasury-extensions/pay-delegate/)

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
- Pay delegate

On this page

# Pay delegate

Before implementing, learn about delegates [here](/dev/learn/glossary/delegate/). Also see [`juice-delegate-template`](https://github.com/mejango/juice-delegate-template).

#### Specs[​](#specs "Direct link to Specs")

A contract can become a treasury pay delegate by adhering to [`IJBPayDelegate3_1_1`](/dev/api/interfaces/ijbpaydelegate3_1_1/):

```
interface IJBPayDelegate3_1_1 is IERC165 {  function didPay(JBDidPayData3_1_1 calldata data) external payable;}
```

When extending pay functionality with a delegate, the protocol will pass a [`JBDidPayData3_1_1`](/dev/api/data-structures/jbdidpaydata3_1_1/) to the `didPay(...)` function:

```
struct JBDidPayData3_1_1 {    address payer;    uint256 projectId;    uint256 currentFundingCycleConfiguration;    JBTokenAmount amount;    JBTokenAmount forwardedAmount;    uint256 projectTokenCount;    address beneficiary;    bool preferClaimedTokens;    string memo;    bytes dataSourceMetadata;    bytes payerMetadata;}
```

```
struct JBTokenAmount {  address token;  uint256 value;  uint256 decimals;  uint256 currency;}
```

The `msg.sender` to the delegate will be the payment terminal that facilitated the payment.

In payment terminals based on the [`JBPayoutRedemptionPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/), such as [`JBETHPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jbethpaymentterminal3_1_1/)'s and [`JBERC20PaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jberc20paymentterminal3_1_1/)'s, the pay delegate hook gets called _after_ the project's tokens have been minted and distributed. [View the docs](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#_pay).

Make sure to only allow trusted contracts to access the `didPay(...)` transaction.

#### Attaching[​](#attaching "Direct link to Attaching")

New delegate contracts should be deployed independently. Once deployed, its address can be returned from a data source hook. See [how to build a data source](/dev/build/treasury-extensions/data-source/) for more.

#### Examples[​](#examples "Direct link to Examples")

```
import '@openzeppelin/contracts/token/ERC721/ERC721.sol';import '@jbx-protocol/contracts-v2/contracts/interfaces/IJBFundingCycleDataSource.sol';import '@jbx-protocol/contracts-v2/contracts/interfaces/IJBPayDelegate.sol';import '@jbx-protocol/contracts-v2/contracts/structs/JBTokenAmount.sol';contract NFTPayDelegate is ERC721, IJBFundingCycleDataSource, IJBPayDelegate {  error INVALID_PAYMENT_EVENT();  IJBDirectory directory;  uint256 projectId;  JBTokenAmount contributionThreshold;  uint256 supply;  // This contract can be used as a funding cycle data source to ensure its didPay function is called once the payment has gone through.  function payParams(JBPayParamsData calldata _data)    external    view    override    returns (      uint256 weight,      string memory memo,      IJBPayDelegate delegate    )  {    // Forward the recieved weight and memo, and use this contract as a pay delegate.    return (_data.weight, _data.memo, IJBPayDelegate(address(this)));  }  // This is unused but needs to be included to fulfill IJBFundingCycleDataSource.  function redeemParams(JBRedeemParamsData calldata _data)    external    pure    override    returns (      uint256 reclaimAmount,      string memory memo,      IJBRedemptionDelegate delegate    )  {    // Return the default values.    return (_data.reclaimAmount.value, _data.memo, IJBRedemptionDelegate(address(0)));  }  constructor(IJBDirectory _directory, uint256 _projectId, JBTokenAmount _contributionThreshold, string calldata _name, string calldata _symbol) ERC721(_name, _symbol) {    directory = _directory;    projectId = _projectId;  },  // Called once the payment has gone through if the project's current funding cycle is using a data source that returns this delegate.  function didPay(JBDidPayData calldata _data) external override {    // Make sure the caller is a terminal of the project, and the call is being made on behalf of an interaction with the correct project.    if (      !directory.isTerminalOf(projectId, IJBPaymentTerminal(msg.sender)) ||      _data.projectId != projectId    ) revert INVALID_PAYMENT_EVENT();    // Make the contribution is being made in the expected token.    if (_data.amount.token != contributionThreshold.token) return;    // Make sure the values use the same number of decimals.    if (_data.amount.decimals < contributionThreshold.decimals) return;    // Make sure the threshold is met.    if (_data.amount.value < contributionThreshold.value) return;    uint256 _tokenId = ++supply;    _mint(_data.beneficiary, _tokenId);  }}
```

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/build/treasury-extensions/pay-delegate.md)

[

Previous

Data source

](/dev/build/treasury-extensions/data-source/)[

Next

Redemption delegate

](/dev/build/treasury-extensions/redemption-delegate/)

- [Specs](#specs)
- [Attaching](#attaching)
- [Examples](#examples)