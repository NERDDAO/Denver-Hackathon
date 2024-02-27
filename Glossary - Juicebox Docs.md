[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/glossary//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/glossary/)
- [中文](/zh/dev/learn/glossary/)

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
    
- [Extensions](#)
    
- [Resources](#)
    
- [Frontend](/dev/frontend/)
    
- [Deprecated](#)
    

- [](/)
- Learn
- Glossary

# Glossary

|Term|Preview|
|---|---|
|**Project**|Each Juicebox project is represented as an NFT (ERC-721), managed in the [`JBProjects`](/dev/api/contracts/jbprojects/) contract. The owner of this NFT is specified when the project is being created. Ownership over this NFT is used to enforce permissions needed to access several project-oriented transactions. Like any other NFT, ownership can be transferred from the original owner to any other address, such as a multi-sig wallet, voting contract, or burn address.<br><br>[Learn more](/dev/learn/glossary/project/)|
|**Funding cycle**|A project is expressed in terms of funding cycles. A funding cycle outlines the time-locked rules according to which a project wishes to operate. It is represented as a [`JBFundingCycle`](/dev/api/data-structures/jbfundingcycle/) data structure, and managed by the [`JBFundingCycleStore`](/dev/api/contracts/jbfundingcyclestore/) contract.<br><br>[Learn more](/dev/learn/glossary/funding-cycle/)|
|**Tokens**|The Juicebox protocol keeps track of tokens for each project. When a payment is made to a project, the protocol mints tokens for a specified beneficiary according to the rules of the project's current funding cycle.<br><br>Tokens are managed in the [`JBTokenStore`](/dev/api/contracts/jbtokenstore/) contract. Projects can optionally call its [`issueFor(...)`](/dev/api/contracts/jbtokenstore/write/issuefor/) transaction to issue an ERC-20 to represent their token. Once issued, anyone with a project's tokens can claim them from the protocol's internal accounting mechanism into their wallet to use around Web3.<br><br>Projects can also bring their own token, so long as it adheres to the [`IJBToken`](/dev/api/interfaces/ijbtoken/) interface and uses 18 decimal fixed point accounting.<br><br>[Learn more](/dev/learn/glossary/tokens/)|
|**Overflow**|The [`JBFundAccessConstraintsStore`](/dev/api/contracts/jbfundaccessconstraintsstore/) contract has a [`distributionLimitOf(...)`](/dev/api/contracts/jbfundaccessconstraintsstore/#distributionlimitof) property which denotes how much funds a project can pull from its treasury to distribute to its preprogrammed payout splits during each funding cycle. Any funds in the treasury in excess of the current distribution limit is considered overflow. A project's overflow can be reclaimed by its community by redeeming tokens. A project can specify treasury funds or assets held outside of Juicebox contracts by attaching a [`IJBFundingCycleDataSource`](/dev/api/interfaces/ijbfundingcycledatasource/) to its funding cycles.<br><br>[Learn more](/dev/learn/glossary/overflow/)|
|**Discount rate**|[`JBFundingCycle`](/dev/api/data-structures/jbfundingcycle/) data structures have a `weight` property that is automatically derived from multiplying the `weight` of the previous funding cycle by the `discountRate` of the previous cycle. The weight property can then be used to determine how many project tokens are distributed per unit of payment received during the funding cycle, or for any other functionality implement through a funding cycle's data source and delegates. A project can also customize its funding cycle's weight manually.<br><br>[Learn more](/dev/learn/glossary/discount-rate/)|
|**Redemption rate**|[`JBFundingCycle`](/dev/api/data-structures/jbfundingcycle/) data structures configured through the [`JBController3_1`](/dev/api/contracts/or-controllers/jbcontroller3_1/) contract have a `redemptionRate` metadata property that can be used to determine how much overflowed funds can be reclaimed by redeeming project tokens, or for any other functionality implemented in a funding cycle's data source and delegates.<br><br>[Learn more](/dev/learn/glossary/redemption-rate/)|
|**Reserved tokens**|[`JBFundingCycle`](/dev/api/data-structures/jbfundingcycle/) data structures configured through the [`JBController3_1`](/dev/api/contracts/or-controllers/jbcontroller3_1/) contract have a `reservedRate` metadata property which specifies the percentage of tokens minted as a result of newly received payments that should be reserved for distribution to preprogrammed reserved token splits.<br><br>[Learn more](/dev/learn/glossary/reserved-tokens/)|
|**Splits**|A Split is used to send a percent of a total amount to a preprogrammed address, Juicebox project, contract that inherits from [`IJBSplitAllocator`](/dev/api/interfaces/ijbsplitallocator/), or sender of the transaction causing the distribution to splits. Splits are represented with [`JBSplit`](/dev/api/data-structures/jbsplit/) data structures, and managed by the [`JBSplitsStore`](/dev/api/contracts/jbsplitsstore/). A split does not hold information about what is being split, it's simply a structure organizable into groups that maps a receiver to a percentage.<br><br>[Learn more](/dev/learn/glossary/splits/)|
|**Split allocator**|A project can preconfigure splits to be directed to any contract that adheres to [`IJBSplitAllocator`](/dev/api/interfaces/ijbsplitallocator/) whose `allocate(...)` transaction will be called when tokens are distributed.<br><br>[Learn more](/dev/learn/glossary/split-allocator/)|
|**Ballot**|[`JBFundingCycle`](/dev/api/data-structures/jbfundingcycle/) data structures have a ballot property which is the address of a contract that adheres to the [`IJBFundingCycleBallot`](/dev/api/interfaces/ijbfundingcycleballot/) interface. This contract specifies the conditions that must be met for any proposed funding cycle reconfiguration to take effect.<br><br>A ballot contract can be written to incorporate strict community voting requirements in order to make funding cycle changes, or to simply add a required buffer period between when a change is proposed and when it can take effect.<br><br>[Learn more](/dev/learn/glossary/ballot/)|
|**Payment terminal**|A project can be configured to use any contract that adheres to [`IJBPaymentTerminal`](/dev/api/interfaces/ijbpaymentterminal/) to manage its inflows and outflows of token funds. It can set its terminals using [`JBDirectory.setTerminalsOf(...)`](/dev/api/contracts/jbdirectory/write/setterminalsof/), and if it uses multiple tokens to manage funds for the same token, it can set the primary one where other Web3 contracts should send funds to using [`JBDirectory.setPrimaryTerminalOf(...)`](/dev/api/contracts/jbdirectory/write/setprimaryterminalof/).<br><br>[Learn more](/dev/learn/glossary/payment-terminal/)|
|**Data source**|[`JBFundingCycle`](/dev/api/data-structures/jbfundingcycle/) data structures configured through the [`JBController3_1`](/dev/api/contracts/or-controllers/jbcontroller3_1/) contract have a `dataSource` metadata property which is the address of a contract that adheres to the [`IJBFundingCycleDataSource3_1_1`](/dev/api/interfaces/ijbfundingcycledatasource3_1_1/) interface.<br><br>Including a data source allows projects to customize what happens when a payment is attempted to the project during a funding cycle, and what happens when a token is attempted to be redeemed during a funding cycle.<br><br>[Learn more](/dev/learn/glossary/data-source/)|
|**Delegate**|When a project receives a payment, its funding cycle's data source can specify the address of a contract that adheres to the [`IJBPayDelegate3_1_1`](/dev/api/interfaces/ijbpaydelegate3_1_1/) whose `didPay(...)` transaction will be called once [`JBPayoutRedemptionPaymentTerminal3_1_1.pay(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#pay) has been executed.<br><br>Similarly, when a project's tokens are being redeemed, its funding cycle's data source can specify the address of a contract that adheres to the [`IJBRedemptionDelegate3_1_1`](/dev/api/interfaces/ijbredemptiondelegate3_1_1/) whose `didRedeem(...)` transaction will be called once [`JBPayoutRedemptionPaymentTerminal3_1_1.redeemTokensOf(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#redeemtokensof) has been executed.<br><br>These can be used by projects to customize what happens when it receives payments and when someone redeems its tokens.<br><br>[Learn more](/dev/learn/glossary/delegate/)|
|**NFT Rewards**|A project can use the NFT Rewards delegate if it wishes to distribute NFTs of any number of tiers to addresses who contribute during a particular set of funding cycles. These NFTs can then be used for redemptions instead of the standard project tokens if the project chooses to.<br><br>[Learn more](/dev/learn/glossary/nft-rewards/)|
|**Token Store**|The [`JBTokenStore`](/dev/api/contracts/jbtokenstore/) contract manages project token balances, minting, and burning for all projects on a version of the protocol. It must adhere to the [`IJBTokenStore`](/dev/api/interfaces/ijbtokenstore/) interface, and its address can be found by reading a project's [`JBController3_1.tokenStore`](/dev/api/contracts/or-controllers/jbcontroller3_1/#tokenstore).<br><br>[Learn more](/dev/learn/glossary/token-store/)|
|**Operator**|Addresses can give permissions to any other address to take specific actions throughout the Juicebox ecosystem on their behalf. These addresses are called Operators, and are managed through the [`JBOperatorStore`](/dev/api/contracts/jboperatorstore/) contract.<br><br>[Learn more](/dev/learn/glossary/operator/)|

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/glossary/README.md)

[

Previous

Risks

](/dev/learn/risks/)[

Next

Ballot

](/dev/learn/glossary/ballot/)