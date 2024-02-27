[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/architecture//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/architecture/)
- [中文](/zh/dev/learn/architecture/)

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
    
- [Extensions](#)
    
- [Resources](#)
    
- [Frontend](/dev/frontend/)
    
- [Deprecated](#)
    

- [](/)
- Learn
- Architecture

On this page

# Architecture

info

See [JuiceboxDAO's Protocol Evolution: Navigating Updates and Enhancements](https://jango.eth.limo/31469E9F-8C0D-49E9-8003-0077674708A6/).

The protocol is made up of 7 core contracts and 3 surface contracts.

- Core contracts store all the independent components that make the protocol work.
- Surface contracts glue core contracts together and manage funds. Anyone can write new surface contracts for projects to use.

#### Core contracts[​](#core-contracts "Direct link to Core contracts")

The first two core contracts are self explanatory. They store the core opinionated components of the protocol.

- [`JBTokenStore`](/dev/api/contracts/jbtokenstore/) manages token minting and burning for all projects.
- [`JBFundingCycleStore`](/dev/api/contracts/jbfundingcyclestore/) manages funding cycle configurations and scheduling. Funding cycles are represented as a [`JBFundingCycle`](/dev/api/data-structures/jbfundingcycle/) data structure.

The next few are a little more generic. They don't know anything specific to the ecosystem, and are open for use by other protocols or future extensions.

- [`JBProjects`](/dev/api/contracts/jbprojects/) manages and tracks ownership over projects, which are represented as ERC-721 tokens.
    
    The protocol uses this to enforce permissions needed to access several project-oriented transactions.
    
- [`JBSplitsStore`](/dev/api/contracts/jbsplitsstore/) stores information about how arbitrary distributions should be split. The information is represented as a [`JBSplit`](/dev/api/data-structures/jbsplit/) data structure.
    
    The surface contracts currently use these to split up payout distributions and reserved token distributions.
    
- [`JBPrices`](/dev/api/contracts/jbprices/) manages and normalizes price feeds of various currencies.
    
    The protocol uses this to allow projects to do their accounting in any number of currencies, but manage all funds in ETH or other assets regardless of accounting denomination.
    
- [`JBOperatorStore`](/dev/api/contracts/jboperatorstore/) stores operator permissions for all addresses. Addresses can give permissions to any other address to take specific indexed actions on their behalf, while confining the permissions to an arbitrary number of domain namespaces.
    
    The protocol uses this to allow project owners and token holders to give other EOAs or contracts permission to take certain administrative actions on their behalf. This is useful for encouraging a composable ecosystem where proxy contracts can perform actions on an address's behalf as a lego block.
    
- [`JBDirectory`](/dev/api/contracts/jbdirectory/) keeps a reference of which terminal contracts each project is currently accepting funds through, and which controller contract is managing each project's tokens and funding cycles.
    

#### Surface contracts[​](#surface-contracts "Direct link to Surface contracts")

There are currently 3 surface contracts that manage how projects manage funds and define how all core contracts should be used together. Anyone can write new surface contracts for projects to use.

- [`JBController3_1`](/dev/api/contracts/or-controllers/jbcontroller3_1/) stitches together funding cycles and project tokens, allowing for restricted control, accounting, and token management.
- [`JBPayoutRedemptionPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/) manages all inflows ([`pay`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#pay), [`addToBalanceOf`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#addtobalanceof)) and outflows ([`distributePayoutsOf`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#distributepayoutsof), [`useAllowanceOf`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#useallowanceof), [`redeemTokensOf`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#redeemtokensof)) of funds. This is an abstract implementation that can be used by any number of payment terminals, such as [`JBETHPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jbethpaymentterminal3_1_1/)'s and [`JBERC20PaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jberc20paymentterminal3_1_1/)'s.
- [`JBSingleTokenPaymentTerminalStore3_1_1`](/dev/api/contracts/jbsingletokenpaymentterminalstore3_1_1/) manages accounting data on behalf of payment terminals that manage balances of only one token type.

The abstract [`JBPayoutRedemptionPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/) implements the [`IJBPaymentTerminal`](/dev/api/interfaces/ijbpaymentterminal/) interface to provide outflow mechanics, and [`JBETHPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jbethpaymentterminal3_1_1/) and [`JBERC20PaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jberc20paymentterminal3_1_1/) in-turn extend the [`JBPayoutRedemptionPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/) to provide scoped inflow/outflow environments for specific tokens. Projects are welcome to roll their own [`IJBPaymentTerminal`](/dev/api/interfaces/ijbpaymentterminal/) implementations to accept funds through. This can be useful to accept other tokens as payment, bypass protocol fees, or attempt some other funky design. A project can add/remove terminals from the core [`JBDirectory`](/dev/api/contracts/jbdirectory/) contract using [`JBDirectory.setTerminalsOf(...)`](/dev/api/contracts/jbdirectory/write/setterminalsof/) if its current funding cycle is configured to allow doing so.

Likewise, a project can bring its own contract to serve as its controller. A project's controller is the only contract that has direct access to manipulate its tokens and funding cycles. A project can set its controller from the core [`JBDirectory`](/dev/api/contracts/jbdirectory/) contract using [`JBDirectory.setControllerOf(...)`](/dev/api/contracts/jbdirectory/write/setcontrollerof/) if its current funding cycle is configured to allow doing so.

#### Bonus utility contracts[​](#bonus-utility-contracts "Direct link to Bonus utility contracts")

- [`JBETHERC20ProjectPayer`](/dev/api/contracts/or-utilities/jbetherc20projectpayer/) provides utilities to pay a project. Inheriting this contract is useful for contracts that wish to route funds to a treasury while specifying the token beneficiary, memo, and other contextual information alongside. Instances of this contract can also be deployed as stand-alone addresses that will forward funds received directly to a project's treasury.
- [`JBETHERC20ProjectPayerDeployer`](/dev/api/contracts/or-utilities/jbetherc20projectpayerdeployer/) provides a function to deploy new stand-alone [`JBETHERC20ProjectPayer`](/dev/api/contracts/or-utilities/jbetherc20projectpayer/)s.
- [`JBETHERC20SplitsPayer`](/dev/api/contracts/or-utilities/jbetherc20splitspayer/) provides utilities to pay a group of splits. Inheriting this contract is useful for contracts that wish to route funds to a group of splits while specifying contextual information alongside. Instances of this contract can also be deployed as stand-alone addresses that will forward funds received directly to a group of splits.
- [`JBETHERC20SplitsPayerDeployer`](/dev/api/contracts/or-utilities/jbetherc20splitspayerdeployer/) provides a function to deploy new stand-alone [`JBETHERC20SplitsPayer`](/dev/api/contracts/or-utilities/jbetherc20splitspayer/)s.
- [`JBProjectHandles`](/dev/deprecated/v2/contracts/or-utilities/jbprojecthandles/) lets project owners attach an ENS name as a project handle. Front ends can use a project's handle in place of its project ID, and indexers can use events to make the Juicebox project directory searchable and filterable.

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/architecture/README.md)

[

Previous

Overview

](/dev/learn/overview/)[

Next

Payment Terminals

](/dev/learn/architecture/terminals/)

- [Core contracts](#core-contracts)
- [Surface contracts](#surface-contracts)
- [Bonus utility contracts](#bonus-utility-contracts)