# Smart Contract

The processes of NFT Watch DAO are governed through a Smart Contract that has been developed by [kryptokrauts](https://kryptokrauts.com), the team behind [Soon.Market](https://soon.market).

It is deployed on the account [nftwatchdao](https://explorer.xprnetwork.org/account/nftwatchdao) on [XPR Network](https://xprnetwork.org). The source code is available on [GitHub](https://github.com/kryptokrauts/xpr-contracts/blob/main/nftwatchdao/nftwatchdao.contract.ts).

## Secured via MultiSig

[XPR Network](https://xprnetwork.org) is running on [Antelope](https://antelope.io) technology, which ships with an advanced permission system. In order to ensure that the [nftwatchdao](https://explorer.xprnetwork.org/account/nftwatchdao#keys) is not controlled by one single entity, we decided to secure the account via MultiSig.

## Contract Actions

### Public
- [`report`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=report) to report NFT collections that violates the [Code of Conduct](./code-of-conduct.md)
    - Params: `collection`, `reporter`, `reason`
    - Reports will be stored in [`blacklistrep`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=blacklistrep)-table until reviewed by [Guards](./guards.md)
- [`reqshielding`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=reqshielding) to request shielding for a specific NFT collection
    - Params: `collection`, `requester`, `requestMarketplace`, `skipBasicCheck`, `skipReason`
    - Requires the [Shielding Fee](./shielding.md#shielding-fee) to be transferred upfront to nftwatchdao account with memo `shielding`
        - A certain percentage of the fee will automatically be distributed to the `requestMarketplace` account as defined in the [globals](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=globals)-table
    - Allows to tell Guards to skip the [Basic Check](./shielding.md#basic-check) with a valid reason which should be consulted with guards upfront!
    - Reports will be stored in [`shieldingreq`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=shieldingreq)-table until reviewed by [Guards](./guards.md)

### Guards Only
- [`addblacklist`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=addblacklist) to add NFT collections to the blacklist which haven't been reported before
    - Params: `collection`, `guard`, `comment`
    - A new entry will be added to the [`blacklist`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=blacklist)-table
    - The new blacklist entry will be logged
- [`confirmrep`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=confirmrep) to confirm a reported NFT collection to be added to the blacklist
    - Params: `collection`, `guard`, `comment`
    - The entry in the [`blacklistrep`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=blacklistrep)-table will be removed and a new entry will be added to the [`blacklist`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=blacklist)-table
    - The confirmation will be logged
- [`rejectreport`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=rejectreport) to reject a reported NFT collection to be added to the blacklist
    - Params: `collection`, `guard`, `comment`
    - The entry in the [`blacklistrep`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=blacklistrep)-table will be removed
    - The rejection will be logged
- [`delblacklist`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=delblacklist) to remove an NFT collection from blacklist
    - Params: `collection`, `guard`, `comment`
    - The entry in the [`blacklist`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=blacklist)-table will be removed
    - The deletion will be logged
- [`addshielding`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=addshielding) to add NFT collections to the shieldings without requiring a request
    - Params: `collection`, `guard`, `skipReason`, `reportCid`
    - This is mainly used for collections that have already been shielded before the contract existed
    - A new entry will be added to the [`shieldings`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=shieldings)-table
    - The new shielding will be logged
- [`confshield`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=confshield) to confirm shielding for a requested NFT collection
    - Params: `collection`, `guard`, `reportCid`
    - The entry in the [`shieldingreq`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=shieldingreq)-table will be removed and a new entry will be added to the [`shieldings`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=shieldings)-table
    - A certain percentage of the fee will automatically be distributed to the `guard` account as defined in the [globals](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=globals)-table
    - The new shielding will be logged
- [`rejectshield`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=rejectshield) to reject shielding for a requested NFT collection
    - Params: `collection`, `guard`, `reportCid`
    - The entry in the [`shieldingreq`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=shieldingreq)-table will be removed
    - A certain percentage of the fee will automatically be distributed to the `guard` account as defined in the [globals](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=globals)-table
    - The rejection will be logged
- [`delshielding`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=delshielding) to remove an NFT collections from shieldings
    - Params: `collection`, `guard`, `comment`
    - The entry in the [`shieldings`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=shieldings)-table will be removed
    - The deletion will be logged

### MultiSig Only
- [`addguard`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=addguard) to add an authorized guard
    - Params: `guard`
    - The guard will be added in the list of `authorizedGuards` in the [globals](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=globals)-table
- [`delguard`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=delguard) to remove an authorized guard
    - Params: `guard`
    - The guard will be removed from the list of `authorizedGuards` in the [globals](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=globals)-table
- [`addmarket`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=addmarket) to add an NFT marketplace that is eligible to allow their users to request shieldings
    - Params: `marketplace`
    - The marketplace will be added in the list of `marketplaces` in the [globals](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=globals)-table
- [`setshieldprc`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=setshieldprc) to change the price in XPR for shielding
    - Params: `xprPrice`
    - The `shieldingPrice` in the [globals](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=globals)-table will be updated
- [`setfeestruct`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=setfeestruct) to change the fee structure for rewarding guards & marketplaces
    - Params: `guard`, `dao`, `market`
    - The `shieldingGuardFee`, `shieldingDaoFee` & `shieldingMarketFee` will be updated in the [globals](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=globals)-table