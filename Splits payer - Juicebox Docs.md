[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/build/utilities/splits-payer//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/build/utilities/splits-payer/)
- [中文](/zh/dev/build/utilities/splits-payer/)

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
- Splits payer

On this page

# Splits payer

[`JBETHERC20SplitsPayer`](/dev/api/contracts/or-utilities/jbetherc20splitspayer/) contracts make it easy to route funds to a group of splits from other contracts or within inheriting contracts. This is useful for routing funds to a number of Juicebox project treasuries and other addresses within other contracts such as an NFT marketplaces.

The [`JBETHERC20SplitsPayer`](/dev/api/contracts/or-utilities/jbetherc20splitspayer/) can be inherited from any contract to facilitate internal transactions to split groups in ETH or any ERC-20, assuming the projects in the split group are using a payment terminal that accepts the tokens. They can also be deployed as standalone splits payer copies using [`JBSplitsPayerDeployer`](/dev/api/contracts/or-utilities/jbetherc20splitspayerdeployer/).

#### Inheriting JBSplitsPayer[​](#inheriting-jbsplitspayer "Direct link to Inheriting JBSplitsPayer")

Inheriting from [`JBETHERC20SplitsPayer`](/dev/api/contracts/or-utilities/jbetherc20splitspayer/) will give a contract access to a public [`JBSplitsPayer.pay(...)`](/dev/api/contracts/or-utilities/jbetherc20splitspayer/#pay) function, a public [`JBSplitsPayer.addToBalanceOf(...)`](/dev/api/contracts/or-utilities/jbetherc20splitspayer/#addtobalanceof) function, and two functions [`JBSplitsPayer._payToSplits(...)`](/dev/api/contracts/or-utilities/jbetherc20splitspayer/#_paytosplits) and [`JBSplitsPayer._payTo(...)`](/dev/api/contracts/or-utilities/jbetherc20splitspayer/#_payto). These can be used from within the contract to route funds to a group of splits while specifying where leftover funds should go. Use the internal function if the inheriting contract has already handled receiving the funds being forwarded.

Follow instructions in [Getting started](/dev/build/getting-started/) to import the `JBSplitsPayer` files into a project.

```
function pay(  uint256 _projectId,  address _token,  uint256 _amount,  uint256 _decimals,  address _beneficiary,  uint256 _minReturnedTokens,  bool _preferClaimedTokens,  string calldata _memo,  bytes calldata _metadata) public payable virtual override nonReentrant {}
```

```
function addToBalanceOf(  uint256 _projectId,  address _token,  uint256 _amount,  uint256 _decimals,  string calldata _memo,  bytes calldata _metadata) public payable virtual override nonReentrant {}
```

```
function _payToSplits(  uint256 _splitsProjectId,  uint256 _splitsDomain,  uint256 _splitsGroup,  address _token,  uint256 _amount,  uint256 _decimals) internal virtual returns (uint256 leftoverAmount) {}
```

```
function _payTo(  JBSplit[] memory _splits,  address _token,  uint256 _amount,  uint256 _decimals,  address _defaultBeneficiary) internal virtual returns (uint256 leftoverAmount) { ... }
```

If your contract does not wish to route payments received via the native `receive` interaction to a group of splits, all default constructor arguments can be left as null values. The contract will revert any payment received.

#### Deploying splits payers[​](#deploying-splits-payers "Direct link to Deploying splits payers")

Instances of the [`JBETHERC20SplitsPayer`](/dev/api/contracts/or-utilities/jbetherc20splitspayer/) contract can also be deployed as standalone forwarders of payments to split groups. A new splits payer can be deployed using [`JBSplitsPayerDeployer.deploySplitsPayer(...)`](/dev/api/contracts/or-utilities/jbetherc20splitspayerdeployer/#deploysplitspayer).

```
function deploySplitsPayer(  uint256 _defaultSplitsProjectId,  uint256 _defaultSplitsDomain,  uint256 _defaultSplitsGroup,  IJBSplitsStore _splitsStore,  uint256 _defaultProjectId,  address payable _defaultBeneficiary,  bool _defaultPreferClaimedTokens,  string memory _defaultMemo,  bytes memory _defaultMetadata,  bool _defaultPreferAddToBalance,  address _owner) external override returns (IJBSplitsPayer splitsPayer) { ... }
```

Or using [`JBSplitsPayerDeployer.deploySplitsPayerWithSplits(...)`](/dev/api/contracts/or-utilities/jbetherc20splitspayerdeployer/#deploysplitspayerwithsplits).

```
function deploySplitsPayerWithSplits(    uint256 _defaultSplitsProjectId,    JBSplit[] memory _defaultSplits,    IJBSplitsStore _splitsStore,    uint256 _defaultProjectId,    address payable _defaultBeneficiary,    bool _defaultPreferClaimedTokens,    string memory _defaultMemo,    bytes memory _defaultMetadata,    bool _defaultPreferAddToBalance,    address _owner) external override returns (IJBSplitsPayer splitsPayer) { ... }
```

#### Examples[​](#examples "Direct link to Examples")

```
import '@openzeppelin/contracts/token/ERC721/ERC721.sol';import '@jbx-protocol/contracts-v2/contracts/JBETHERC20SplitsPayer.sol';contract NFTSplitsPayer is ERC721, JBETHERC20SplitsPayer {  JBSplits[] splits;  constructor(JBSplits[] memory _splits, IJBDirectory _directory, address _owner) JBETHERC20ProjectPayer(0, address(0), false, "", bytes(0), false, _directory, _owner) {    splits = _splits;  },  // Minting an NFT routes funds to a group of splits, and mints project tokens for msg.sender for splits that route to project treasuries.  function mint(uint256 _tokenId,) external payable override {    _mint(msg.sender, _tokenId);    uint256 _numSplits = splits.length;    JBSplits[] memory _splitsWithBeneficiary;    // Set the msg.sender to be the beneficiary of all project tokens resulting from splits that route to project treasuries.    for (uint256 _i; _i < _numSplits; _i++)  {      JBSplit _split = _splits[_i];      if (_split.projectId != 0) _split.beneficiary = msg.sender;      _splitsWithBeneficiary.push(_split);    }    _payTo(_splitsWithBeneficiary, JBTokens.ETH, msg.value, 18, msg.sender);  }}
```

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/build/utilities/splits-payer.md)

[

Previous

Project payer

](/dev/build/utilities/project-payer/)[

Next

Namespaces & IDs

](/dev/build/namespace/)

- [Inheriting JBSplitsPayer](#inheriting-jbsplitspayer)
- [Deploying splits payers](#deploying-splits-payers)
- [Examples](#examples)