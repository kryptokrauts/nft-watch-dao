# Decentralization

NFT Watch DAO always aimed to be as decentralized as possible. Right now, all decisions are taken on [Discord](https://discord.gg/KtVVaYy6b3) as described.

In the future however, all decisions will be taken on-chain & executed by an as trustless and decentralized process as possible.

The team behind Soon.Market is currently working together with the NFT Watch DAO to define how the current processes can be handled on-chain.

## Considerations

A Smart Contract will be developed, that will be able to manage the lists of shielded and blacklisted NFT collections. There are some considerations that need to be discussed and the goal is to move on with the most simple and effective solution as possible.

### Usage of MultiSig Permissions

The permission system of [Antelope](https://antelope.io) is impressive and just the right fit to be integrated in the development of our solution!

- [Guard](./roles.md#guard) MultiSig responsibilities:
    - Control the owner & active key of [nftwatch](https://www.protonscan.io/account/nftwatch)
    - Add/remove accounts for the Voter role in the custom permission
    - Add/remove accounts to the Guard MultiSig
    - Change the threshold needed to execute Guard MultiSig decisions after DAO Vote decisions
    - Change the threshold needed for custom permissions to execute proposed MultiSig decisions of Voters taken in DAO Votes
- [Voter](./roles.md#voter) MultiSig responsibilities:
    - Control a custom permission `shielding` (child of active key of [nftwatch](https://www.protonscan.io/account/nftwatch)) that is allowed to approve an NFT collection to get shielded
    - Control a custom permission `yellowtier` (child of active key of [nftwatch](https://www.protonscan.io/account/nftwatch)) that can participate in Yellow Tier Votes (there is some drawback in regards to anonymity, see [Open Questions](./decentralization.md#open-questions))
    - Control a custom permission `daoparams` (child of active key of [nftwatch](https://www.protonscan.io/account/nftwatch)) that can participate in DAO votes where changes of the params are proposed

*Note: If we have to leverage a Smart Contract where DAO params are defined for Yellow Tier Votes and DAO Votes, probably only one custom permission will be needed for the [Voters](./roles.md#voter). Unfortunately this would increase the effort of development a little bit.*

### Oracles

In order to perform various checks, NFT Watch DAO should consider to rely on trusted oracles.

The oracles could support Guards by automating tasks to determine if:

- An NFT collection passes the [Basic Check](./shielding.md#basic-check)
- An account is eligible to become a [Voter](./roles.md#voter)

Leveraging the power of oracles, the automated process is protecting the NFT collections from abusing of NFT Watch positions.

### Shielding Expiration

It might make sense to let shielding expire because it is likely that NFT collections lose support from the community. A new shielding vote to keep the shield could be automatically triggered e.g. every 3 months and if it does not pass, the shield will be removed.

### Generative Art Indicator

It might make sense to provide an indicator for an NFT collection whether it is generative art or not. This would allow NFT marketplaces to consume the information and act accordingly.

We might also consider to introduce different states (fully generative / mixed generative). The question here is how to determine if the art is fully generative or mixed generative. Guards would have to decide about this before starting the Shielding Vote.

### Yellow Tier Information

In case a Yellow Tier Vote was performed on an NFT collection and it passed, the info might be useful for the community. Adding information about such cases and the related NFT collections of the potential knock-off might be valuable for many members of the community.

Even if the Yellow Tier Vote passes and an NFT collection gets shielded afterwards, this information would still be available for the public.

### Parameters

There exist several parameters in NFT Watch DAO that are subject to change through DAO votes.

#### Basic Check

These are the current params which are used in the [Basic Check](./shielding.md#basic-check) of NFT collections:

- `first_mint_age` = 1 month
- `amount_nfts` = 25
- `unique_holders` = 10
- `unique_buyers` = 10

#### Voter Role

The following param is checked before a new [Voter](./roles.md#voter) is added to the MultiSig permission(s):

- `account_age` = 3 months

#### Voting

These params are considered for the actual votes and would be reflected in the threshold of the respective MultiSig permission:

- `shielding_vote_confirmations` = 21
- `yellow_tier_vote_confirmations` = to be discussed as it might not be easily applicable via MultiSig, see [Open Questions](./decentralization.md#open-questions)
- `dao_vote_confirmations` = to be discussed as it might not be easily applicable via MultiSig, see [Open Questions](./decentralization.md#open-questions)

The following param determines the duration for a shielded NFT collection before it expires:

- `shielding_expiration_time` = to be discussed (proposal: 3 months)

The following param determines the time for votes be active before they expire:

- `vote_expiration_time` = 1 week

*Note: This would be valid for all types of votes. If needed, different expiration times for different votes can be defined.*

The following param determines the timeout that is applied if a vote didn't reach enough upvotes / participants:

- `vote_timeout_period` = 1 month

*Note: If a Shielding Vote is not successful due to missing supporters, it can be proposed again once the timeout period has passed. The same timeout is applied for Yellow Tier Votes that failed due to a too low participation rate.*

## Open questions

- Can we use the default permission system of Antelope to cover various use-cases via MultiSig permissions?
    - It is definitely the most simple and efficient way to do it, but it has limitations in advanced decision making.
- What is the maximum amount of accounts that can be added to a custom permission controled via MultiSig?
    - Note: All Voters would have to be added to such custom permission.
- How to handle Yellow Tier Votes which are currently anonymous?
    - Note: An off-chain anonymous voting procedure where Guards confirm the decisions on-chain might be needed as we cannot provide a ZKP solution in short term.
- Can we perform all kinds of Votes (Shielding, Yellow Tier, DAO) in an upvote only approach to avoid having to implement custom logic for voting and 100% use the default MultiSig permission system provided by Antelope?
- What's the best and most efficient way to govern and use the threshold of different (custom) MultiSig permissions?
    - Do we need a Smart Contract or is a clever UI sufficient to handle this?
    - Is it possible and does it make sense to define the threshold for Yellow Tier Votes and DAO Votes in tables of a Smart Contract?
    - Can a Smart Contract easily look up which accounts are currently added in a custom permission and only allow accounts included in such permission to perform a certain action? (e.g. Vote for YES/NO)