[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/glossary/operator//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/glossary/operator/)
- [中文](/zh/dev/learn/glossary/operator/)

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
- [Glossary](/dev/learn/glossary/)
- Operator

On this page

# Operator

#### What everyone needs to know[​](#what-everyone-needs-to-know "Direct link to What everyone needs to know")

- An operator is an address that has been given permission to take one or more actions on another address's behalf.
- Several functions are only available to a project's owner, or to an operator address that the project's owner has set.
- Operator permissions are stored and managed in the [`JBOperatorStore`](/dev/api/contracts/jboperatorstore/), where they can be added or revoked at any time by the address being operated on behalf of.
- Operator permissions are expressed in terms of indexes defined in [`JBOperations`](/dev/api/libraries/jboperations/).
- Operator permissions apply to a specific domain namespace, which is used in the Juicebox ecosystem to allow addresses to give permissions that only apply to a specific project (where the domain is the project's ID). A domain of 0 is a wildcard domain, giving an operator access to an action across all domains.

#### What you'll want to know if you're building[​](#what-youll-want-to-know-if-youre-building "Direct link to What you'll want to know if you're building")

- Permission indexes can be found in [`JBOperations`](/dev/api/libraries/jboperations/), [`JBOperations2`](/dev/api/libraries/jboperations2/), and [`JBUriOperations`](/dev/extensions/juice-token-resolver/libraries/jburioperations/). See [Namespaces](/dev/build/namespace/#operator-indices) for a list.
- Any address can give an operator permissions to take one or more actions on its behalf by sending a transaction to [`JBOperatorStore.setOperator(...)`](/dev/api/contracts/jboperatorstore/write/setoperator/). To set multiple operators in the same transaction, use [`JBOperatorStore.setOperators(...)`](/dev/api/contracts/jboperatorstore/write/setoperators/).
- Access can be revoked from an operator through the same operations as above by sending an array of permissions that does not include those you wish to revoke.
- Permission for each operation is stored in a bit within an `uint256`. If the bit is 1, the permission is enabled for the particular operator within the particular domain. Otherwise it is disabled.
- [`JBOperatorStore.hasPermission(...)`](/dev/api/contracts/jboperatorstore/read/haspermission/) and [`JBOperatorStore.hasPermissions(...)`](/dev/api/contracts/jboperatorstore/read/haspermissions/) can be used to check if an operator has a particular permission.

#### Operatable functionality[​](#operatable-functionality "Direct link to Operatable functionality")

For each project, the following functions can only be accessed by either the address that owns the project's NFT or by operator addresses explicitly allowed by the address that owns the project's NFT. Operators are only valid in the context of a particular owner – if the NFT changes hands, the operators for the project must be set again by the new owner.

An address can set operators for its project with [`JBOperatorStore.setOperator(...)`](/dev/api/contracts/jboperatorstore/write/setoperator/), using the indexes from the [`JBOperations`](/dev/api/libraries/jboperations/) library. An Operator's permissions depend on the specific parameters the admin allows them. Each of the following functions can be called by the admin, and also by any operator that has been granted permission to call the function by the admin.

- [`JBController3_1.launchFundingCyclesFor(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#launchfundingcyclesfor)
- [`JBController3_1.reconfigureFundingCyclesOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#reconfigurefundingcyclesof)
- [`JBController3_1.mintTokensOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#minttokensof)
- [`JBTokenStore.issueFor(...)`](/dev/api/contracts/jbtokenstore/write/issuefor/)
- [`JBController3_1.setFor(...)`](/dev/api/contracts/jbtokenstore/write/setfor/)
- [`JBController3_1.migrate(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#migrate)
- [`JBPayoutRedemptionPaymentTerminal3_1_1.useAllowanceOf(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#useallowanceof)
- [`JBPayoutRedemptionPaymentTerminal3_1_1.migrate(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#migrate)
- [`JBPayoutRedemptionPaymentTerminal3_1_1.processFees(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#processfees)
- [`JBProjects.setMetadataOf(...)`](/dev/api/contracts/jbprojects/write/setmetadataof/)
- [`JBSplitsStore.set(...)`](/dev/api/contracts/jbsplitsstore/write/set/)
- [`JBDirectory.setControllerOf(...)`](/dev/api/contracts/jbdirectory/write/setcontrollerof/)
- [`JBDirectory.setTerminalsOf(...)`](/dev/api/contracts/jbdirectory/write/setterminalsof/)
- [`JBDirectory.setPrimaryTerminalOf(...)`](/dev/api/contracts/jbdirectory/write/setprimaryterminalof/)

The following transactions can be used by token holders or operator addresses explicitly allowed by the address that owns the tokens. If the tokens change hands, the operators must be set again by the new holder.

- [`JBController3_1.burnTokensOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#burntokensof)
- [`JBPayoutRedemptionPaymentTerminal3_1_1.redeemTokensOf(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#redeemtokensof)
- [`JBTokenStore.claimFor(...)`](/dev/api/contracts/jbtokenstore/write/claimfor/)
- [`JBTokenStore.transferFrom(...)`](/dev/api/contracts/jbtokenstore/write/transferfrom/)

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/glossary/operator.md)

[

Previous

NFT Rewards

](/dev/learn/glossary/nft-rewards/)[

Next

Overflow

](/dev/learn/glossary/overflow/)

- [What everyone needs to know](#what-everyone-needs-to-know)
- [What you'll want to know if you're building](#what-youll-want-to-know-if-youre-building)
- [Operatable functionality](#operatable-functionality)