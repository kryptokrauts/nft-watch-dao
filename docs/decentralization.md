# Decentralization

NFT Watch DAO always aimed to be as decentralized as possible. Right now, all decisions are taken on [Discord](https://discord.gg/KtVVaYy6b3) as described.

In the future however, all decisions will be taken on-chain!

The team behind Soon.Market is currently working together with the NFT Watch DAO to define how the current processes can be handled on-chain.

## Considerations

A Smart Contract will be developed, that will be able to manage the lists of shielded and blacklisted NFT collections. There are some considerations that need to be discussed and the goal is to move on with the most simple and effective solution as possible.

### Usage of MultiSig Permissions

The permission system of [Antelope](https://antelope.io) is impressive!

- [Guard](./roles.md#guard) MultiSig responsibilities would be to:
    - control the owner & active key of [nftwatch](https://www.protonscan.io/account/nftwatch)
    - add/remove accounts for the Voter role in the custom permission
    - add/remove accounts to the Guard MultiSig
    - change the threshold needed to execute Guard MultiSig decisions
    - change the threshold needed for custom permissions to execute a proposed MultiSig decision of Voters
- [Voter](./roles.md#voter) MultiSig responsibility would be to:
    - control a custom permission (child of active key of [nftwatch](https://www.protonscan.io/account/nftwatch)) that is allowed to approve an NFT collection to get shielded

### Oracles

In order to perform various checks, NFT Watch DAO should consider to rely on trusted oracles.

The oracles could support Guards by automating tasks to determine if:

- an NFT collection passes the [Basic Check](./shielding.md#basic-check)
- an account is eligible to become a [Voter](./roles.md#voter)

### Shielding Expiration

It might make sense to let shielding expire because it is likely that NFT collections lose support from the community. A new shielding vote to keep the shield could be automatically triggered e.g. every 3 months and if it does not pass, the shield will be removed.

### Generative Art Indicator

It might make sense to provide an indicator for an NFT collection whether it is generative art or not. This would allow NFT marketplaces to consume the information and act accordingly.

### Yellow Tier Information

In case a Yellow Tier Vote was performed on an NFT collection and it passed, the info might be useful for the community. Adding information about such cases and the related NFT collections of the potential knock-off might be valuable for many members of the community.

## Open questions

- How to handle Yellow Tier Votes which are currently anonymous?
    - An off-chain anonymous voting procedure where Guards confirm the decisions on-chain might be needed as we cannot provide a ZKP solution in short term.
- What is the maximum amount of accounts that can be added to a custom permission controled via MultiSig?
- Are multiple custom (MultiSig) permissions needed to handle the process as envisioned?
- What's the best and most efficient way to govern the threshold of different (custom) MultiSig permissions?