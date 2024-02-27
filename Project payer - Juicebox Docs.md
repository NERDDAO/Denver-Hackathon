[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/build/utilities/project-payer//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/build/utilities/project-payer/)
- [中文](/zh/dev/build/utilities/project-payer/)

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
- Utilities
- Project payer

On this page

# Project payer

[`JBETHERC20ProjectPayer`](/dev/api/contracts/or-utilities/jbetherc20projectpayer/) contracts make it easy to route funds to projects' treasuries from other contracts or within inheriting contracts. This is useful for routing funds to a Juicebox treasury within other contracts such as an NFT's minting function, or creating contracts that will automatically route any received funds to a project's treasury with preconfigured parameters to send along with the payment.

The [`JBETHERC20ProjectPayer`](/dev/api/contracts/or-utilities/jbetherc20projectpayer/) can be inherited from any contract to facilitate internal transactions to Juicebox treasuries in ETH or any ERC-20, assuming the project is using a payment terminal that accepts the tokens. They can also be deployed as standalone project payer copies using [`JBProjectPayerDeployer`](/dev/api/contracts/or-utilities/jbetherc20projectpayerdeployer/).

#### Inheriting JBProjectPayer[​](#inheriting-jbprojectpayer "Direct link to Inheriting JBProjectPayer")

Inheriting from [`JBETHERC20ProjectPayer`](/dev/api/contracts/or-utilities/jbetherc20projectpayer/) will give a contract access to a public [`JBProjectPayer.pay(...)`](/dev/api/contracts/or-utilities/jbetherc20projectpayer/#pay) function, a public [`JBProjectPayer.addToBalanceOf(...)`](/dev/api/contracts/or-utilities/jbetherc20projectpayer/#addtobalanceof) function, an internal [`JBProjectPayer._pay(...)`](/dev/api/contracts/or-utilities/jbetherc20projectpayer/#_pay) function, and an internal [`JBProjectPayer._addToBalanceOf(...)`](/dev/api/contracts/or-utilities/jbetherc20projectpayer/#_addtobalanceof) function. These can be used from within the contract to route funds to a Juicebox treasury while specifying all relevant parameters to contextualize the payment. Use the internal versions if the inheriting contract has already handled receiving the funds being forwarded.

Follow instructions in [Getting started](/dev/build/getting-started/) to import the `JBProjectPayer` files into a project.

```
function pay(  uint256 _projectId,  address _token,  uint256 _amount,  uint256 _decimals,  address _beneficiary,  uint256 _minReturnedTokens,  bool _preferClaimedTokens,  string calldata _memo,  bytes calldata _metadata) public payable virtual override {}
```

```
function addToBalanceOf(  uint256 _projectId,  address _token,  uint256 _amount,  uint256 _decimals,  string calldata _memo  bytes calldata _metadata) public payable virtual override {}
```

```
function _pay(  uint256 _projectId,  address _token,  uint256 _amount,  uint256 _decimals,  address _beneficiary,  uint256 _minReturnedTokens,  bool _preferClaimedTokens,  string memory _memo,  bytes memory _metadata) internal virtual {}
```

```
function _addToBalanceOf(  uint256 _projectId,  address _token,  uint256 _amount,  uint256 _decimals,  string memory _memo,  string memory _metadata) internal virtual  {}
```

If your contract does not wish to route payments received via the native `receive` interaction to a Juicebox treasury, all default constructor arguments can be left as null values. The contract will revert any payment received.

#### Deploying project payers[​](#deploying-project-payers "Direct link to Deploying project payers")

Instances of the [`JBETHERC20ProjectPayer`](/dev/api/contracts/or-utilities/jbetherc20projectpayer/) contract can also be deployed as stand-alone forwarders of payments to Juicebox treasuries. A new project payer can be deployed using [`JBProjectPayerDeployer.deployProjectPayer(...)`](/dev/api/contracts/or-utilities/jbetherc20projectpayerdeployer/#deployprojectpayer).

```
function deployProjectPayer(  uint256 _defaultProjectId,  address payable _defaultBeneficiary,  bool _defaultPreferClaimedTokens,  string memory _defaultMemo,  bytes memory _defaultMetadata,  bool _defaultPreferAddToBalance,  IJBDirectory _directory,  address _owner) external override returns (IJBProjectPayer projectPayer) { ... }
```

#### Examples[​](#examples "Direct link to Examples")

```
import '@openzeppelin/contracts/token/ERC721/ERC721.sol';import '@jbx-protocol/contracts-v2/contracts/JBETHERC20ProjectPayer.sol';contract NFTProjectPayer is ERC721, JBETHERC20ProjectPayer {  uint256 projectId;  constructor(uint256 _projectId, IJBDirectory _directory, address _owner) JBETHERC20ProjectPayer(0, address(0), false, "", bytes(0), false, _directory, _owner) {    projectId = _projectId;  },  // Minting an NFT routes funds to the juicebox treasury and mints project tokens for msg.sender. Use addToBalance if you don't want tokens minted.  function mint(uint256 _tokenId) external payable override {    _mint(msg.sender, _tokenId);    _pay(_projectId, JBTokens.ETH, msg.value, 18, msg.sender, 0, false, "I love buffalos", bytes(''));    // _addToBalance(_projectId, JBTokens.ETH, msg.value, 18, "I love buffalos", bytes(0));  }}
```

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/build/utilities/project-payer.md)

[

Previous

Split allocator

](/dev/build/treasury-extensions/split-allocator/)[

Next

Splits payer

](/dev/build/utilities/splits-payer/)

- [Inheriting JBProjectPayer](#inheriting-jbprojectpayer)
- [Deploying project payers](#deploying-project-payers)
- [Examples](#examples)