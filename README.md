# Caviar Private Pools - Mitigation contest details
- Total Prize Pool: $8,100 USDC 
- [Warden guidelines for C4 mitigation reviews](https://code4rena.notion.site/Guidelines-for-Versus-mitigation-reviews-ed10fc5cfbf640bd8dcec66f38b343c4)
- Submit findings [using the C4 form](https://code4rena.com/contests/2023-05-caviar-mitigation-contest/submit)
- Starts TBD XXX XXX XX 20:00 UTC
- Ends TBD XXX XXX XX 20:00 UTC

## Important note 

Each warden must submit a mitigation review for *every High and Medium finding* from the parent contest. **Incomplete mitigation reviews will not be eligible for awards.**

[ ⭐️ SPONSORS ADD INFO HERE ]

## Findings being mitigated

Mitigations of all High and Medium issues will be considered in-scope and listed here.

- [H-01: Royalty receiver can drain a private pool](https://github.com/code-423n4/2023-04-caviar-findings/issues/320)
- [H-02: PrivatePool owner can steal all ERC20 and NFT from user via arbitrary execution](https://github.com/code-423n4/2023-04-caviar-findings/issues/184)
- [H-03: Risk of silent overflow in reserves update](https://github.com/code-423n4/2023-04-caviar-findings/issues/167)
- [M-01: The buy function's mechanism enables users to acquire flash loans at a cheaper fee rate.](https://github.com/code-423n4/2023-04-caviar-findings/issues/885)
- [M-02: EthRouter can't perform multiple changes](https://github.com/code-423n4/2023-04-caviar-findings/issues/873)
- [M-03: Flash loan fee is incorrect in Private Pool contract](https://github.com/code-423n4/2023-04-caviar-findings/issues/864)
- [M-04: `changeFeeQuote` will fail for low decimal ERC20 tokens](https://github.com/code-423n4/2023-04-caviar-findings/issues/858)
- [M-05: `EthRouter.sell`, `EthRouter.deposit`, and `EthRouter.change` functions can be DOS'ed for some ERC721 tokens](https://github.com/code-423n4/2023-04-caviar-findings/issues/776)
- [M-06: Flashloan fee is not distributed to the factory](https://github.com/code-423n4/2023-04-caviar-findings/issues/697)
- [M-07: Royalty recipients will not get fair share of royalties](https://github.com/code-423n4/2023-04-caviar-findings/issues/669)
- [M-08: Loss of funds for traders due to accounting error in royalty calculations](https://github.com/code-423n4/2023-04-caviar-findings/issues/596)
- [M-09: Malicious royalty recipient can steal excess eth from buy orders](https://github.com/code-423n4/2023-04-caviar-findings/issues/569)
- [M-10: Incorrect protocol fee is taken when changing NFTs](https://github.com/code-423n4/2023-04-caviar-findings/issues/463)
- [M-11: Factory.create: Predictability of pool address creates multiple issues.](https://github.com/code-423n4/2023-04-caviar-findings/issues/419)
- [M-12: Prohibition to create private pools with the factory NFT](https://github.com/code-423n4/2023-04-caviar-findings/issues/353)
- [M-13: Transaction revert if the baseToken does not support 0 value transfer when charging changeFee](https://github.com/code-423n4/2023-04-caviar-findings/issues/278)
- [M-14: The royaltyRecipient could not be prepare to receive ether, making the sell to fail](https://github.com/code-423n4/2023-04-caviar-findings/issues/263)
- [M-15: Pool tokens can be stolen via PrivatePool.flashLoan function from previous owner](https://github.com/code-423n4/2023-04-caviar-findings/issues/230)
- [M-16: `PrivatePool.flashLoan()` takes fee from the wrong address](https://github.com/code-423n4/2023-04-caviar-findings/issues/56)
- [M-17: The tokenURI method does not check if the NFT has been minted and returns data for the contract that may be a fake NFT.](https://github.com/code-423n4/2023-04-caviar-findings/issues/44)

## Overview of changes

Please provide context about the mitigations that were applied if applicable and identify any areas of specific concern.

## Mitigations to be reviewed

Wherever possible, mitigations should be provided in separate pull requests, one per issue. If that is not possible (e.g. because several audit findings stem from the same core problem), then please link the PR to all relevant issues in your findings repo. 

| URL | Mitigation of | Purpose | 
| ----------- | ------------- | ----------- |
| https://github.com/code4rena/sample-contracts/pull/XXX | H-01 | This mitigation does XYZ | 

## Out of Scope

Please list any High and Medium issues that were judged as valid but you have chosen not to fix.
