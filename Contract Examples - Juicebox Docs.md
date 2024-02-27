[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/build/examples//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/build/examples/)
- [中文](/zh/dev/build/examples/)

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
        
        - [Project payer](/dev/build/utilities/project-payer/)
        - [Splits payer](/dev/build/utilities/splits-payer/)
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
- Contract Examples

On this page

# Contract Examples

Simple contract examples which integrate with Juicebox. If you're building new Juicebox-related contracts, join our [Discord server](https://discord.gg/juicebox) for help!

## Pay[​](#pay "Direct link to Pay")

A simple contract which pays a project through their primary ETH terminal.

```
import '@jbx-protocol/juice-contracts-v3/contracts/interfaces/IJBDirectory.sol';import '@jbx-protocol/juice-contracts-v3/contracts/libraries/JBTokens.sol';contract MyBangarangApp {  // Keep a reference to the directory in which project's current payment terminal's can be found.  IJBDirectory directory;  // Keep a reference to the project ID that'll be paid.  uint256 projectId;  constructor(IJBDirectory _directory, uint256 _projectId) {    directory = _directory;    projectId = _projectId;  }  function doSomething() external payable {    // Get the payment terminal the project currently prefers to accept ETH through.    IJBPaymentTerminal _ethTerminal = directory.primaryTerminalOf(projectId, JBTokens.ETH);    _ethTerminal.pay{ value: msg.value }(      projectId, // pay the correct project.      amount, // pay the full amount sent to this function.      JBTokens.ETH, // assert that the payment is being made in ETH.      msg.sender, // send the msg.sender as the beneficiary of any tokens issued from the payment.      0, // if you know the amount of project tokens you expect to be receiving as a result of this payment, specify it here to ensure this happens accordingly. this can be useful if your expectations rely on an oracle calculation. set to 0 if you're ok getting whatever you get.      false, // set this to true if you know the project has issued ERC-20's, and you prefer receiving the ERC-20's directly instead of keeping the option to claim later.      "This is a test payment!!", // send a memo if you want,      bytes(0) // no need to send metadata. if you know the project is using an extension that requires more information to fulfill the operation -- such as NFT minting -- you'll want to add the appropriate formatted metadata here.    });  }}
```

## Read Balance[​](#read-balance "Direct link to Read Balance")

A simple contract which reads a project's balance in their primary ETH terminal.

```
import '@jbx-protocol/juice-contracts-v3/contracts/interfaces/IJBDirectory.sol';import '@jbx-protocol/juice-contracts-v3/contracts/interfaces/IJBETHPaymentTerminal.sol';import '@jbx-protocol/juice-contracts-v3/contracts/libraries/JBTokens.sol';contract JBProjectViewUtil {  // Keep a reference to the directory in which project's current payment terminal's can be found.  IJBDirectory directory;  constructor(IJBDirectory _directory, uint256 _projectId) {    directory = _directory;  }  function getETHBalance(uint256 _projectId) external returns (uint256) {    // Get the payment terminal the project currently prefers to accept ETH through.    IJBPaymentTerminal _ethTerminal = directory.primaryTerminalOf(projectId, JBTokens.ETH);    // Assumes the terminal is a IJBETHPaymentTerminal. If the terminal could be a lesser version, a ERC165 check should be done before casting.    return IJBETHPaymentTerminal(_ethTerminal).store().balanceOf(_ethTerminal, projectId);  }}
```

## Read Overflow[​](#read-overflow "Direct link to Read Overflow")

A simple project which reads a project's overflow in their primary ETH terminal. A project's [_Overflow_](/dev/learn/glossary/overflow/) is the funds it holds which aren't needed for the current funding cycle's payouts.

```
import '@jbx-protocol/juice-contracts-v3/contracts/interfaces/IJBDirectory.sol';import '@jbx-protocol/juice-contracts-v3/contracts/libraries/JBTokens.sol';contract JBProjectViewUtil {  // Keep a reference to the directory in which project's current payment terminal's can be found.  IJBDirectory directory;  constructor(IJBDirectory _directory, uint256 _projectId) {    directory = _directory;  }  function getETHBalance(uint256 _projectId) external returns (uint256) {    // Get the payment terminal the project currently prefers to accept ETH through.    IJBPaymentTerminal _terminal = directory.primaryTerminalOf(_projectId, JBTokens.ETH);    // Return a project's balance in excess of any commitments already made but not yet distributed.    return _terminal.currentEthOverflowOf(_projectId);  }}
```

[`IJBPaymentTerminal`](/dev/api/interfaces/ijbpaymentterminal/)s are required to report how much ETH's worth of tokens it holds for a project in excess of funds needed for the current funding cycle's payouts via [`IJBPaymentTerminal.currentEthOverflowOf(uint256 _projectId)`](/dev/api/interfaces/ijbpaymentterminal/). The terminal can be written to assume a conversion rate to ETH of 0, meaning it could have a balance of 10,000 shitcoins but still have an ETH overflow of 0.

This requirement allows for straightforwards calculation of a project's total redeemable balance for use in redemption calculations and custom [data sources](/dev/learn/glossary/data-source/).

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/build/examples.md)

[

Previous

Namespaces & IDs

](/dev/build/namespace/)[

Next

JBDidPayData

](/dev/api/data-structures/jbdidpaydata/)

- [Pay](#pay)
- [Read Balance](#read-balance)
- [Read Overflow](#read-overflow)