[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/build/treasury-extensions/data-source//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/build/treasury-extensions/data-source/)
- [中文](/zh/dev/build/treasury-extensions/data-source/)

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
- Data source

On this page

# Data source

Before implementing, learn about data sources [here](/dev/learn/glossary/data-source/). Also see [`juice-delegate-template`](https://github.com/mejango/juice-delegate-template).

#### Specs[​](#specs "Direct link to Specs")

A contract can become a treasury data source by adhering to [`IJBFundingCycleDataSource3_1_1`](/dev/api/interfaces/ijbfundingcycledatasource3_1_1/):

```
interface IJBFundingCycleDataSource3_1_1 is IERC165 {  function payParams(    JBPayParamsData calldata data  )    external    view    returns (      uint256 weight,      string memory memo,      JBPayDelegateAllocation3_1_1[] memory delegateAllocations    );  function redeemParams(    JBRedeemParamsData calldata data  )    external    view    returns (      uint256 reclaimAmount,      string memory memo,      JBRedemptionDelegateAllocation3_1_1[] memory delegateAllocations    );}
```

There are two functions that must be implemented, `payParams(...)` and `redeemParams(...)`. Either one can be left empty if the intent is to only extend the treasury's pay functionality or redeem functionality.

##### Pay[​](#pay "Direct link to Pay")

When extending the pay functionality with a data source, the protocol will pass a [`JBPayParamsData`](/dev/api/data-structures/jbpayparamsdata/) to the `payParams(...)` function:

```
struct JBPayParamsData {  IJBPaymentTerminal terminal;  address payer;  JBTokenAmount amount;  uint256 projectId;  uint256 currentFundingCycleConfiguration;  address beneficiary;  uint256 weight;  uint256 reservedRate;  string memo;  bytes metadata;}
```

```
struct JBTokenAmount {  address token;  uint256 value;  uint256 decimals;  uint256 currency;}
```

Using these params, the data source's `payParams(...)` function is responsible for either reverting or returning a few bits of information:

- `weight` is a fixed point number with 18 decimals that the protocol can use to base arbitrary calculations on. For example, payment terminals based on the [`JBPayoutRedemptionPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/), such as [`JBETHPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jbethpaymentterminal3_1_1/)'s and [`JBERC20PaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jberc20paymentterminal3_1_1/)'s, use the `weight` to determine how many project tokens to mint when a project receives a payment (see [the calculation](/dev/api/contracts/jbsingletokenpaymentterminalstore3_1_1/#recordpaymentfrom)). By default, the protocol will use the `weight` of the project's current funding cycle, which is provided to the data source function in `JBPayParamsData.weight`. Increasing the weight will mint more tokens and decreasing the weight will mint fewer tokens, both as a function of the amount paid. Return the `JBPayParamsData.weight` value if no altered functionality is desired.
- `memo` is a string emitted within the [`Pay`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#pay) event and sent along to any `delegate` that this function also returns. By default, the protocol will use the `memo` directly passed in by the payer, which is provided to this data source function in `JBPayParamsData.memo`. Return the `JBPayParamsData.memo` value if no altered functionality is desired.
- `delegateAllocations` is an array containing delegates, amounts to send them, and metadata to pass to them.
    - `delegateAllocations.delegate` is the address of a contract that adheres to [`IJBPayDelegate3_1_1`](/dev/api/interfaces/ijbpaydelegate3_1_1/) whose `didPay(...)` function will be called once the protocol finishes its standard payment routine. Check out [how to build a pay delegate](/dev/build/treasury-extensions/pay-delegate/) for more details. If the same contract is being used as the data source and the pay delegate, return `address(this)`. Return the zero address if no additional functionality is desired.
    - `delegateAllocations.amount` is the amount of tokens to send to the delegate.
    - `delegateAllocations.metadata` is the metadata to pass to the delegate.

The `payParams(...)` function can also revert if it's presented with any conditions it does not want to accept payments under.

The `payParams(...)` function has implicit permission to [`JBController3_1.mintTokensOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#minttokensof) for the project.

##### Redeem[​](#redeem "Direct link to Redeem")

When extending redeem functionality with a data source, the protocol will pass a [`JBRedeemParamsData`](/dev/api/data-structures/jbredeemparamsdata/) to the `redeemParams(...)` function:

```
struct JBRedeemParamsData {  IJBPaymentTerminal terminal;  address holder;  uint256 projectId;  uint256 currentFundingCycleConfiguration;  uint256 tokenCount;  uint256 totalSupply;  uint256 overflow;  JBTokenAmount reclaimAmount;  bool useTotalOverflow;  uint256 redemptionRate;  uint256 ballotRedemptionRate;  string memo;  bytes metadata;}
```

Using these params, the data source's `redeemParams(...)` function is responsible for either reverting or returning a few bits of information:

- `reclaimAmount` is the amount of tokens in the treasury that the terminal should send out to the redemption beneficiary as a result of burning the amount of project tokens tokens specified in `JBRedeemParamsData.tokenCount`, as a fixed point number with the same amount of decimals as `JBRedeemParamsData.decimals`. By default, the protocol will use a reclaim amount determined by the standard protocol bonding curve based on the redemption rate the project has configured into its current funding cycle, which is provided to the data source function in `JBRedeemParamsData.reclaimAmount`. Return the `JBRedeemParamsData.reclaimAmount` value if no altered functionality is desired.
- `memo` is a string emitted within the [`RedeemTokens`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#redeemtokensof) event and sent along to any `delegate` that this function also returns. By default, the protocol will use the `memo` passed in directly by the redeemer, which is provided to this data source function in `JBRedeemParamsData.memo`. Return the `JBRedeemParamsData.memo` value if no altered functionality is desired.
- `delegateAllocations` is an array containing delegates, amounts to send them, and metadata to pass to them.
    - `delegateAllocations.delegate` is the address of a contract that adheres to [`IJBRedemptionDelegate3_1_1`](/dev/api/interfaces/ijbredemptiondelegate3_1_1/) whose `didRedeem(...)` function will be called once the protocol finishes its standard redemption routine (but before the reclaimed amount is sent to the beneficiary). Check out [how to build a redemption delegate](/dev/build/treasury-extensions/redemption-delegate/) for more details. If the same contract is being used as the data source and the redemption delegate, return `address(this)`. Return the zero address if no additional functionality is desired.
    - `delegateAllocations.amount` is the amount of tokens to send to the delegate.
    - `delegateAllocations.metadata` is the metadata to pass to the delegate.

The `redeemParams(...)` function can also revert if it's presented with any conditions it does not want to accept redemptions under.

#### Attaching[​](#attaching "Direct link to Attaching")

New data source contracts should be deployed independently. Once deployed, its address can be configured into a project's funding cycle metadata to take effect while that funding cycle is active. Additionally, the metadata's `useDataSourceForPay` and/or `useDataSourceForRedeem` should be set to `true` if the respective data source hook should be referenced by the protocol.

#### Examples[​](#examples "Direct link to Examples")

```
import '@openzeppelin/contracts/token/ERC721/ERC721.sol';import '@jbx-protocol/contracts-v2/contracts/interfaces/IJBFundingCycleDataSource.sol';contract AllowlistDataSource is IJBFundingCycleDataSource {  error NOT_ALLOWED();  mapping(address => bool) allowed;  function payParams(JBPayParamsData calldata _data)    external    view    override    returns (      uint256 weight,      string memory memo,      IJBPayDelegate delegate    )  {    if (!allowed[_data.payer]) revert NOT_ALLOWED();    // Forward the recieved weight and memo, and use no delegate.    return (_data.weight, _data.memo, IJBPayDelegate(address(0)));  }  // This is unused but needs to be included to fulfill IJBFundingCycleDataSource.  function redeemParams(JBRedeemParamsData calldata _data)    external    pure    override    returns (      uint256 reclaimAmount,      string memory memo,      IJBRedemptionDelegate delegate    )  {    // Return the default values.    return (_data.reclaimAmount.value, _data.memo, IJBRedemptionDelegate(address(0)));  }}
```

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/build/treasury-extensions/data-source.md)

[

Previous

Ballot

](/dev/build/treasury-extensions/ballot/)[

Next

Pay delegate

](/dev/build/treasury-extensions/pay-delegate/)

- [Specs](#specs)
    - [Pay](#pay)
    - [Redeem](#redeem)
- [Attaching](#attaching)
- [Examples](#examples)