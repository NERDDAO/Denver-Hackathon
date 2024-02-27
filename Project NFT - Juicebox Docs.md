[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/build/project-nft//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/build/project-nft/)
- [中文](/zh/dev/build/project-nft/)

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
- Project NFT

On this page

# Project NFT

Anyone can build on the [`JBProjects`](/dev/api/contracts/jbprojects/) NFT contract. This allows developers to write new contracts which use [`JBProjects`](/dev/api/contracts/jbprojects/) NFTs to manage permissions in a standardized way, and allows any project using Juicebox payment terminals to access your contracts, and vice versa.

#### Create a project[​](#create-a-project "Direct link to Create a project")

Instead of calling [`JBController3_1.launchProjectFor(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#launchprojectfor) to create a project, configure its first funding cycle, and attach payment terminals and a juicebox controller contract to it in the same transaction, `JBProjects` can be minted independently to represent ownership over projects with subsequent capabilities attached later on.

To create a project, call [`JBProjects.createFor(...)`](/dev/api/contracts/jbprojects/write/createfor/). The [`JBProjectMetadata`](/dev/api/data-structures/jbprojectmetadata/) structure allows arbitrary metadata to be mapped to any namespace domain. [juicebox.money](https://juicebox.money) metadata uses a domain of 0 to store its formatted metadata.

```
function createFor(address _owner, JBProjectMetadata calldata _metadata)  external  override  returns (uint256 projectId) { ... }
```

```
struct JBProjectMetadata {  string content;  uint256 domain;}
```

View project info

Launching a project will mint a new NFT in the [`JBProjects`](/dev/api/contracts/jbprojects/) contract. The owner can be found using [`JBProjects.ownerOf(...)`](https://docs.openzeppelin.com/contracts/4.x/api/token/erc721#IERC721-ownerOf-uint256-).

```
function ownerOf(uint256 _projectId) external returns (address owner) { ... }
```

The project's metadata can be found using [`JBProjects.metadataContentOf(...)`](/dev/api/contracts/jbprojects/properties/metadatacontentof/).

```
function metadataContentOf(uint256 _projectId, uint256 _domain)  external  view  returns (string memory) { ... }
```

Once a project has been created, new metadata can be added by calling [`JBProjects.metadataContentOf(...)`](/dev/api/contracts/jbprojects/properties/metadatacontentof/).

```
function setMetadataOf(uint256 _projectId, JBProjectMetadata calldata _metadata)  external  override  requirePermission(ownerOf(_projectId), _projectId, JBOperations.SET_METADATA) { ... }
```

The project can set a new token URI by calling [`JBProjects.setTokenUriResolver(...)`](/dev/api/contracts/jbprojects/write/settokenuriresolver/).

```
function setTokenUriResolver(IJBTokenUriResolver _newResolver) external override onlyOwner { ... }
```

#### Attaching application-specific functionality[​](#attaching-application-specific-functionality "Direct link to Attaching application-specific functionality")

Project owners can configure their first funding cycle for their `JBProject`, attach payment terminals, and set all other standard Juicebox project properties by calling [`JBController3_1.launchFundingCyclesFor(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#launchfundingcyclesfor).

Most Juicebox protocol contracts are generic utilities for any `JBProject` owner, meaning stored data tends to me mapped from project IDs, and functionality that affects a project tends to be exposed only to the project's owner or a operator address specified by the project's owner.

```
function launchFundingCyclesFor(  uint256 _projectId,  JBFundingCycleData calldata _data,  JBFundingCycleMetadata calldata _metadata,  uint256 _mustStartAtOrAfter,  JBGroupedSplits[] calldata _groupedSplits,  JBFundAccessConstraints[] memory _fundAccessConstraints,  IJBPaymentTerminal[] memory _terminals,  string calldata _memo)  external  virtual  override  requirePermission(projects.ownerOf(_projectId), _projectId, JBOperations.RECONFIGURE)  returns (uint256 configuration) { ... }
```

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/build/project-nft.md)

[

Previous

Basics

](/dev/build/basics/)[

Next

Programmable treasury

](/dev/build/programmable-treasury/)

- [Create a project](#create-a-project)
- [Attaching application-specific functionality](#attaching-application-specific-functionality)