[Skip to main content](#__docusaurus_skipToContent_fallback)

[

![Juicebox Logo](https://docs.juicebox.money/dev/learn/glossary/redemption-rate//img/logo/main-logo-black.svg)

](/)[Docs](/dev/)[Project Creators](/user/)[JuiceboxDAO](/dao/)

[Blogs](/blogs/)

- [For Project Creators](/blog/)
- [Updates](/updates/)
- [Town Halls](/town-hall/)
- [Miscellaneous](/misc/)

[English](#)

- [English](/dev/learn/glossary/redemption-rate/)
- [中文](/zh/dev/learn/glossary/redemption-rate/)

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
- Redemption rate

On this page

# Redemption rate

#### What everyone needs to know[​](#what-everyone-needs-to-know "Direct link to What everyone needs to know")

- The redemption rate determines what proportion of treasury assets can be reclaimed by a token holder by redeeming their tokens.
- By default, all treasury assets that are considered overflow can be reclaimed by token holders. This can be modified using [data source](/dev/learn/glossary/data-source/) extensions.
- A project's redemption rate and extensions can be reconfigured each funding cycle.
- A redemption rate of 100% is linear, meaning a holder with 10% of the token supply can redeem all of their tokens for 10% of available treasury assets.
- A redemption rate of 0% will completely disable redemptions, meaning tokens cannot be redeemed.
- A redemption rate of `x`% where 0% < `x` < 100% will leave some assets in the treasury to share between those who wait longer to redeem. The smaller the `x`, the fewer assets can be reclaimed (_see note below_).
- A project can set a different redemption rate that takes effect only when the project's current funding cycle has an active [ballot](/dev/learn/glossary/ballot/).
- Redemptions incur a JBX membership fee when the redemption rate (or [ballot](/dev/learn/glossary/ballot/) redemption rate) is less than 100%. This fee can be set anywhere between 0% and 5%.

Redemption when 0% < x < 100%

With a redemption rate of 50%, a holder with 10% of the token supply can redeem their tokens for _slightly more_ than 5% of available treasury assets.

The other ~5% will remain in the treasury, thereby increasing the redemption value of everyone else's tokens by increasing the ratio of assets to tokens. This encourages holders to redeem later than others – the first holders to redeem will receive the fewest assets in return.

The reason that slightly more than 5% of assets would be returned: a redemption rate of 0% < `x`% < 100% allows for redemptions along a _bonding curve_. Specifically, the formula is:

![](https://docs.juicebox.money/dev/learn/glossary/redemption-rate/data:image/png;base64,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)

Where:

- **r** is the redemption rate (from 0 to 1),
- **o** is the _overflow_, or the funds not being paid out from the treasury that funding cycle,
- **s** is the current token supply, and
- **x** is the amount of tokens being redeemed

Here is an example bonding curve with an overflow of 100 ETH, a total supply of 200 tokens, and a redemption rate of 71.7%. The X axis represents the number of tokens being redeemed, and the Y axis represents the ETH that would be returned. You can try [editing the variables yourself](https://www.desmos.com/calculator/sp9ru6zbpk).

#### What you'll want to know if you're building[​](#what-youll-want-to-know-if-youre-building "Direct link to What you'll want to know if you're building")

- Token holders can redeem their tokens by calling [`JBPayoutRedemptionPaymentTerminal3_1_1.redeemTokensOf(...)`](/dev/api/contracts/or-payment-terminals/or-abstract/jbpayoutredemptionpaymentterminal3_1_1/#redeemtokensof).
- A redemption rate can be specified in a funding cycle through the [`JBController3_1.launchProjectFor(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#launchprojectfor) or [`JBController3_1.reconfigureFundingCyclesOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#reconfigurefundingcyclesof) transactions.
- A ballot redemption rate can be specified in a funding cycle through the [`JBController3_1.launchProjectFor(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#launchprojectfor) or [`JBController3_1.reconfigureFundingCyclesOf(...)`](/dev/api/contracts/or-controllers/jbcontroller3_1/#reconfigurefundingcyclesof) transactions, which will override the standard redemption rate if there is currently a [reconfiguration ballot active](/dev/learn/glossary/ballot/).

[Edit this page](https://github.com/jbx-protocol/juice-docs/blob/main/docs/dev/learn/glossary/redemption-rate.md)

[

Previous

Project

](/dev/learn/glossary/project/)[

Next

Reserved tokens

](/dev/learn/glossary/reserved-tokens/)

- [What everyone needs to know](#what-everyone-needs-to-know)
- [What you'll want to know if you're building](#what-youll-want-to-know-if-youre-building)