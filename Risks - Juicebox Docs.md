[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/risks//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/risks/)
- [中文](/zh/dev/learn/risks/)

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
- Risks

On this page

# Risks

The following are risks that everyone should be aware of before interacting with the protocol. The protocol's design exposes these risks in consequence to its normal operating procedures.

_Also see [Security & Audits](/dev/resources/security/)._

#### Smart contract risk[​](#smart-contract-risk "Direct link to Smart contract risk")

The protocol runs entirely on public smart contracts explained in detail throughout these docs. The Juicebox protocol is public infrastructure running well-known code, all consequences from interacting with networks running the protocol are borne by the entities who sign each transaction. The protocol works according to the specifications outlined in these docs to the extent the code is written and deployed correctly, which is a collective responsibility and not guaranteed. There is a major risk that this is not the case. Please do your own research.

#### Project owner risk[​](#project-owner-risk "Direct link to Project owner risk")

Ownership of each project on the Juicebox protocol belongs to the address possessing a [`JBProjects`](/dev/api/contracts/jbprojects/) NFT with a unique token ID, which also serves as the project's ID. The address that owns this token can reconfigure a project's funding cycles, which empower it to manipulate a project's finances both productively and maliciously.

- The following values can be reconfigured by a project's owner on a per-funding cycle basis:
    
    #### Setting a distribution limit and payout splits[​](#setting-a-distribution-limit-and-payout-splits "Direct link to Setting a distribution limit and payout splits")
    
    With a distribution limit of zero, all treasury funds belong to the community. Token holders can redeem their tokens to reclaim their share of the treasury at any time, according to the current funding cycle's redemption bonding curve rate.
    
    A non-zero distribution limit allocates a portion of the treasury for distribution to payout splits.
    
    A project owner can also change the split allocations that are bound by the funding cycle's distribution limit at any time, unless the split was explicitly locked until a specified date during its creation.
    
    🟢 **Used productively** this can be used to withdraw funds to a community safe, distribute funds to contributors, channel funds to other projects operating treasuries on the protocol, and more.  
    
    🔴 **Used maliciously** this can be used to rug the entire treasury into an arbitrary wallet.  
      
    
    #### Setting an overflow allowance[​](#setting-an-overflow-allowance "Direct link to Setting an overflow allowance")
    
    With an overflow allowance of zero, all treasury funds belonging to the community – funds in excess of the distribution limit – cannot be accessed by the project owner. The only way funds can leave the treasury is through token redemptions.
    
    A non-zero overflow allowance gives the project owner access to a portion of the community's funds for on-demand distribution to arbitrary addresses.
    
    🟢 **Used productively** this can be used to manage discretionary spending.  
    
    🔴 **Used maliciously** this can be used to rug the entire treasury into an arbitrary wallet.  
      
    
    #### Allowing token minting[​](#allowing-token-minting "Direct link to Allowing token minting")
    
    While token minting is not allowed, the only way for new project tokens to be minted and distributed is for the project to receive new funds into its treasury. Tokens will get minted in accordance to the current funding cycle's values.
    
    If token minting is allowed, an arbitrary number of tokens can be minted and distributed by the project owner, diluting the redemption value of all outstanding tokens.
    
    🟢 **Used productively** this can be used to premint tokens to members, or satisfy other agreed upon inflationary treasury strategies.  
    
    🔴 **Used maliciously** this can be used to mint extra tokens and redeem them to reclaim treasury funds into an arbitrary wallet, rugging the entire treasury.  
      
    
    #### Setting the funding cycle's weight[​](#setting-the-funding-cycles-weight "Direct link to Setting the funding cycle's weight")
    
    A funding cycle's weight determines how many tokens will be minted and distributed when a treasury receives funds. By default, a funding cycle has the same weight as the cycle that preceded it after applying the preceding cycle's discount rate.
    
    🟢 **Used productively** this can be used to manage how tokens are issued over time.  
    
    🔴 **Used maliciously** this can be used to manipulate token issuance, and rug the entire treasury into an arbitrary wallet.  
      
    
    #### Allowing changing of project tokens[​](#allowing-changing-of-project-tokens "Direct link to Allowing changing of project tokens")
    
    While changing tokens isn't allowed, the current project token will be used to satisfy redemptions and new issuance for the duration of the funding cycle.
    
    If changing tokens is allowed, a new token can replace the role of a previous token for new issuance and redemptions.
    
    🟢 **Used productively** this can be used to allow projects to augment a previous token strategy with a Juicebox treasury, detach a token from a Juicebox treasury, or create custom token mechanisms associated with its Juicebox treasury.  
    
    🔴 **Used maliciously** this can be used to cut off a community of token holders from their treasury while using the redemption of a new token to reclaim treasury funds into an arbitrary wallet.  
      
    
    #### Pause payments, pause distributions, pause redemptions, pause burn[​](#pause-payments-pause-distributions-pause-redemptions-pause-burn "Direct link to Pause payments, pause distributions, pause redemptions, pause burn")
    
    While each functionality isn't paused, the standard functionality will be accessible.
    
    If payments are paused to a project, the protocol will reject any inbound payments. If disitributions are paused for a project, the protocol will reject any request to distribute funds from the treasury. If redemptions are paused, the protocol will reject any request to redeem tokens. If burning is paused, the protocol will reject any request by token holders to burn their tokens.
    
    🟢 **Used productively** this can be used to allow projects to creatively tune how its treasury can be accessed.  
    
    🔴 **Used maliciously** this can be used to cut off a community of token holders from standard treasury functionality.  
      
    
    #### Custom treasury extensions[​](#custom-treasury-extensions "Direct link to Custom treasury extensions")
    
    If a project's funding cycles have no data source, delegate, split allocator, or ballot contracts attached, the consequences of each interaction with the protocol are predictable, consistent, and specified within these docs.
    
    If a project has attached a data source, delegate, split allocator, or ballot contract to a funding cycle, the protocol will access information from them and call functionality within them at specific moments during the execution of various transactions within the regular operation of the protocol.
    
    🟢 **Used productively** this can be used to customize what happens when a treasury receives funds, under what conditions funds can leave a treasury, and under what conditions reconfigurations can take effect.  
    
    🔴 **Used maliciously** this can be used to mint excess tokens, rug the entire treasury into an arbitrary wallet, trick users into compromising their individual wallets, create arbitrary unwanted and extractive behavior, or introduce smart contract bugs into otherwise productive extension designs. Do not interact with a project that is using an untrusted extension.  
      
    
    #### Add and remove payment terminals[​](#add-and-remove-payment-terminals "Direct link to Add and remove payment terminals")
    
    While setting payment terminals isn't allowed, a project can only receive funds and offer token redemptions from within the payment terminals it has already attached.
    
    If setting payment terminals is allowed, projects can begin managing inflows and outflows of funds from new contracts, or remove current contracts where they are doing so.
    
    🟢 **Used productively** this can be used to begin accepting new tokens into a treasury, or creating totally custom treasury behavior.  
    
    🔴 **Used maliciously** this can be used to cut off a community of token holders from their treasury, create arbitrary unwanted and extractive behavior, or introduce smart contract bugs. Do not interact with a projects using untrusted payment terminals.  
      
    
    #### Setting the controller[​](#setting-the-controller "Direct link to Setting the controller")
    
    While setting the controller isn't allowed, a project can only operate according to the rules of its currently set controller.
    
    If setting the controller is allowed, projects can bring new rules according to which it'll operate.
    
    🟢 **Used productively** this can be used to create totally custom treasury behavior.  
    
    🔴 **Used maliciously** this can be used to cut off a community of token holders from their treasury, create arbitrary unwanted and extractive behavior, or introduce smart contract bugs. Do not interact with a projects using an untrusted controller.  
      
    
    #### Migrating funds between terminals[​](#migrating-funds-between-terminals "Direct link to Migrating funds between terminals")
    
    While migrating funds between terminals isn't allowed, a project's funds in a terminal cannot be migrated to another terminal which may have alternate constraints.
    
    If migrating funds between terminals is allowed, a project can move its funds from one terminal to another.
    
    🟢 **Used productively** this can be used to move a treasury into a totally custom environment, or to trusted upgraded versions of the protocol.  
    
    🔴 **Used maliciously** this can be used to cut off a community of token holders from their treasury, create arbitrary unwanted and extractive behavior, or introduce smart contract bugs.  
      
    

#### Undistributed reserved rate risk[​](#undistributed-reserved-rate-risk "Direct link to Undistributed reserved rate risk")

info

This risk only applies to projects which have not yet upgraded to [`JBController3_1`](/dev/api/contracts/or-controllers/jbcontroller3_1/). Newly deployed projects don't have this risk.

If a project enters a funding cycle with a different reserved rate than the preceding cycle while still having outstanding reserved tokens to distribute, the quantity of distributable tokens will change to reflect the new reserved rate.

For example, if in FC#1 a project has a reserved rate of 10% and 9,000 tokens are minted, 1,000 tokens (10% of the total) are reserved to be distributed to the configured reserved token receivers. If FC#2 with a reserved rate of 50% begins without the reserved tokens having been distributed, there will now be 9,000 tokens (50% of the total) reserved to be distributed to the configured reserved token receivers.

Distributing reserved tokens is a public action – anyone can send a transaction to do this.

#### Price oracle risk[​](#price-oracle-risk "Direct link to Price oracle risk")

The protocol uses price oracles to normalize prices throughout the its standard operations. These oracles are smart contract mechanisms external to the core Juicebox protocol. Projects using multiple currencies for certain functionality bare the risk of these external oracle systems misreporting price values, or halting all together. To avoid this risk, projects should account distribution limits in the same currency as is being collected.

#### Large number risk[​](#large-number-risk "Direct link to Large number risk")

Under certain circumstances, token holders attempting to burn token amounts greater than (2^256 / 2) - 1, or 57896044618658097711785492504343953926634992332820282019728792003956564819968, will have their transactions reverted due to an arithmetic underflow.

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/risks.md)

[

Previous

Administration

](/dev/learn/administration/)[

Next

Glossary

](/dev/learn/glossary/)

- [Smart contract risk](#smart-contract-risk)
- [Project owner risk](#project-owner-risk)
- [Undistributed reserved rate risk](#undistributed-reserved-rate-risk)
- [Price oracle risk](#price-oracle-risk)
- [Large number risk](#large-number-risk)