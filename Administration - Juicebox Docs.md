[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/administration//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/administration/)
- [中文](/zh/dev/learn/administration/)

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
- Administration

# Administration

The protocol has very minimal global governance. The following are the only global functions that can be accessed by a privileged administrating address, initially the [JuiceboxDAO multisig](https://gnosis-safe.io/app/eth:0xAF28bcB48C40dBC86f52D459A6562F658fc94B1e/home), a 9 of 14 multisig voted in by JBX members:

- **[`JBProjects.setTokenUriResolver(...)`](/dev/api/contracts/jbprojects/write/settokenuriresolver/)**  
    Allows the owner of the [`JBProjects`](/dev/api/contracts/jbprojects/) contract to provide and change the [`IJBTokenUriResolver`](/dev/api/interfaces/ijbtokenuriresolver/) used to resolve metadata for project NFTs in its [`tokenURI(...)`](/dev/api/contracts/jbprojects/read/tokenuri/) function.  
    
- **[`JBPrices.addFeedFor(...)`](/dev/api/contracts/jbprices/write/addfeed/)**  
    Allows the owner of the [`JBPrices`](/dev/api/contracts/jbprices/) contract to add new price feeds used to convert amounts denoted in one currency to another. Once added, a price feed cannot be removed.  
    
- **[`JBDirectory.setIsAllowedToSetFirstController(...)`](/dev/api/contracts/jbdirectory/write/setisallowedtosetfirstcontroller/)**  
    Allows the owner of the [`JBDirectory`](/dev/api/contracts/jbdirectory/) contract to add/remove addresses that can set a project's first controller on its behalf.  
    
- **[`JBETHPaymentTerminal3_1_1.setFee(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#setfee)**  
    Allows the owner of the [`JBETHPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jbethpaymentterminal3_1_1/) (or any other terminal inheriting from [`JBPayoutRedemptionPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/)) to change the protocol fee incurred when projects distribute their treasury funds outside of the protocol ecosystem or when funds are redeemed from a project with a redemption rate less than 100%. The max fee is 5%.  
    
- **[`JBETHPaymentTerminal3_1_1.setFeeGauge(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#setfeegauge)**  
    Allows the owner of the [`JBETHPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jbethpaymentterminal3_1_1/) (or any other terminal inheriting from [`JBPayoutRedemptionPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/)) to change the fee gauge used to provide fee discounts on a per-project basis.  
    
- **[`JBETHPaymentTerminal3_1_1.setFeelessAddress(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#setfeelessaddress)**  
    Allows the owner of the [`JBETHPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jbethpaymentterminal3_1_1/) (or any other terminal inheriting from [`JBPayoutRedemptionPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/)) to add/remove any other address used by other projects to/from a list of address to which distributed funds can be sent without incurring protocol fees, and from which funds can be added back to the project's balance without refunding held fees.
- **[`JBETHPaymentTerminal3_1_1.processFees(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_2/#processfees)**  
    Allows the owner of the [`JBETHPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/jbethpaymentterminal3_1_1/) (or any other terminal inheriting from [`JBPayoutRedemptionPaymentTerminal3_1_1`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/)) to process any project's [held fees](/dev/learn/glossary/hold-fees/).  
    

Ownership for each contract is managed independently and can be transferred to a new owner by the current owner.

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/administration.md)

[

Previous

Payment Terminals

](/dev/learn/architecture/terminals/)[

Next

Risks

](/dev/learn/risks/)