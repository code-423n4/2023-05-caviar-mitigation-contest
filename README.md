# Caviar Private Pools - Mitigation contest details
- Total Prize Pool: $8,100 USDC 
- [Warden guidelines for C4 mitigation reviews](https://code4rena.notion.site/Guidelines-for-Versus-mitigation-reviews-ed10fc5cfbf640bd8dcec66f38b343c4)
- Submit findings [using the C4 form](https://code4rena.com/contests/2023-05-caviar-private-pools-mitigation-contest/submit)
- Starts May 09, 2023 20:00 UTC
- Ends May 12, 2023 20:00 UTC

## Important note 

Each warden must submit a mitigation review for *every High and Medium finding* from the parent contest. **Incomplete mitigation reviews will not be eligible for awards.**

## Findings being mitigated

Mitigations of all High and Medium issues will be considered in-scope and listed here.

- [H-01: Royalty receiver can drain a private pool](https://github.com/code-423n4/2023-04-caviar-findings/issues/320)
- [H-02: PrivatePool owner can steal all ERC20 and NFT from user via arbitrary execution](https://github.com/code-423n4/2023-04-caviar-findings/issues/184)
- [H-03: Risk of silent overflow in reserves update](https://github.com/code-423n4/2023-04-caviar-findings/issues/167)

- [M-02: EthRouter can't perform multiple changes](https://github.com/code-423n4/2023-04-caviar-findings/issues/873)
- [M-03: Flash loan fee is incorrect in Private Pool contract](https://github.com/code-423n4/2023-04-caviar-findings/issues/864)
- [M-05: `EthRouter.sell`, `EthRouter.deposit`, and `EthRouter.change` functions can be DOS'ed for some ERC721 tokens](https://github.com/code-423n4/2023-04-caviar-findings/issues/776)
- [M-06: Flashloan fee is not distributed to the factory](https://github.com/code-423n4/2023-04-caviar-findings/issues/697)
- [M-08: Loss of funds for traders due to accounting error in royalty calculations](https://github.com/code-423n4/2023-04-caviar-findings/issues/596)
- [M-10: Incorrect protocol fee is taken when changing NFTs](https://github.com/code-423n4/2023-04-caviar-findings/issues/463)
- [M-11: Factory.create: Predictability of pool address creates multiple issues.](https://github.com/code-423n4/2023-04-caviar-findings/issues/419)
- [M-12: Prohibition to create private pools with the factory NFT](https://github.com/code-423n4/2023-04-caviar-findings/issues/353)
- [M-15: Pool tokens can be stolen via PrivatePool.flashLoan function from previous owner](https://github.com/code-423n4/2023-04-caviar-findings/issues/230)
- [M-17: The tokenURI method does not check if the NFT has been minted and returns data for the contract that may be a fake NFT.](https://github.com/code-423n4/2023-04-caviar-findings/issues/44)

## Overview of changes

All of the mitigations for each issue are isolated to their own pull requests. While each mitigation may work in isolation, we would also like a review of how the mitigations all work together (i.e. an overview of the whole codebase). Of particular concern is [the mitigation for H-02](https://github.com/outdoteth/caviar-private-pools/pull/2) and whether it makes sense or not.


## Mitigations to be reviewed

| URL | Mitigation of | Purpose | 
| ----------- | ------------- | ----------- |
| https://github.com/outdoteth/caviar-private-pools/pull/12 | H-01 | This fix ensures that the royalty amounts and royalty payments are now done in a single loop | 
| https://github.com/outdoteth/caviar-private-pools/pull/2 | H-02, M-15 | Adds a check in the `execute()` function that will revert if the target contract is the `baseToken` or `nft`. | 
| https://github.com/outdoteth/caviar-private-pools/pull/10 | H-03 | This fix uses openzeppelin's SafeCast library | 
| https://github.com/outdoteth/caviar-private-pools/pull/5 | M-02 | Adds a `baseTokenAmount` field to the Change input | 
| https://github.com/outdoteth/caviar-private-pools/pull/6 | M-03 | Exponentiates the changeFee to make sure that the flashFee amount is correct. |
| https://github.com/outdoteth/caviar-private-pools/pull/7 | M-05 | Fix is to skip the approval step if the pool has already been approved to transfer the NFTs from the EthRouter. |
| https://github.com/outdoteth/caviar-private-pools/pull/8 | M-06 | Adds the protocol fee to flashLoan fees. |
| https://github.com/outdoteth/caviar-private-pools/pull/11 | M-08 | This fix ensures that the royaltyAmount is only incremented if the recipient address is not zero. |
| https://github.com/outdoteth/caviar-private-pools/pull/13 | M-10 | Fix is to add a separate fee called protocolChangeFeeRate which can be much higher than protocolFeeRate. |
| https://github.com/outdoteth/caviar-private-pools/pull/9 | M-11 | This fix includes the msg.sender in the salt when creating the proxy deployment. |
| https://github.com/outdoteth/caviar-private-pools/pull/14 | M-12 | Adds a check to ensure that users cannot create pools with private pool nfts deposited. |
| https://github.com/outdoteth/caviar-private-pools/pull/19 | M-17 | Adds a revert if the token does not exist. |


## Out of Scope

### M-01: The buy function's mechanism enables users to acquire flash loans at a cheaper fee rate.

We chose not to fix [M-01](https://github.com/code-423n4/2023-04-caviar-findings/issues/885) because it's an edge case, and either way the user will still be charged a similar fee, assuming that the private pool owner has set reasonable fee rates.

### M-04: changeFeeQuote will fail for low decimal ERC20 tokens.

We chose not to fix [M-04](https://github.com/code-423n4/2023-04-caviar-findings/issues/858) because it's an edge case and does not occur in any of the major ERC20 tokens that we intend to support.

### M-07: Royalty recipients will not get fair share of royalties

We chose not to fix [M-07](https://github.com/code-423n4/2023-04-caviar-findings/issues/669) because it's already documented in the code that all NFTs are assumed to have the same price for royalty payments. assuming that the recipient is the same for each NFTs royalty payment (which it almost always is in practice) then this makes sense.

* NFT 1 is worth 1 ETH
* NFT 2 is worth 2 ETH

* (1 + 2) / 2 = 1.5 ETH
* 1 / 2 + 2 / 2 = 1.5 ETH

the output is the same. the additional complexity of individually calculating each price is not worth it.

### M-09: Malicious royalty recipient can steal excess eth from buy orders

We chose not to fix [M-09](https://github.com/code-423n4/2023-04-caviar-findings/issues/569) because it assumes that the royalty recipient (usually the owner of the collection) is malicious, and that the user has sent a significant amount of surplus eth. In which case their order could be sandwiched by MEV bots anyway.

### M-13: Transaction revert if the baseToken does not support 0 value transfer when charging changeFee

We chose not to fix [M-13](https://github.com/code-423n4/2023-04-caviar-findings/issues/278) because it's an edge case and does not occur in any of the major ERC20 tokens that we intend to support.

### M-14: The royaltyRecipient could not be prepare to receive ether, making the sell to fail

We chose not to fix [M-14](https://github.com/code-423n4/2023-04-caviar-findings/issues/263) because it's assumed the royalty recipients are generally honest actors (collection founders). If it's not the case then a private pool owner can turn off the payRoyalties flag and disable royalty payments. The worst case scenario here is a DOS on trades.

### M-16: PrivatePool.flashLoan() takes fee from the wrong address

We chose not to fix [M-16](https://github.com/code-423n4/2023-04-caviar-findings/issues/56) because it breaks consistency with how fees are handled for native ETH. For native ETH, the `msg.value` is checked. This implies that the `msg.sender` is paying the fee. Hence, for consistency, it also makes sense for the `msg.sender` to pay the fee for ERC20 tokens too.
