# Shielding

## Purpose of Shielding

By handing out the shield, NFT Watch DAO confirms that an NFT collection:

- is NOT violating the [Code of Conduct](./code-of-conduct.md)
- passes the [Basic Check](./shielding.md#basic-check)

*Note: Shielding is only targeting NFT collections, not individual accounts!*

## Shielding Fee
The shielding fee is introduced for several reasons:

1. Drive Guard interest which will lead to sustainability of the platform
1. Give back to the community:
    - Buy SOON SPOT NFTs to promote shielded collections
    - Host giveaways
    - ...
1. Encourage NFT marketplaces to adopt NFT Watch DAO
1. Provide added friction to scammers

Currently, NFT Watch DAO charges a fee of `10000.0000 XPR` for shielding.

The fee distribution is defined as follows:

- 50% Guard that performs the review and creats the shielding report
- 40% NFT Watch DAO
- 10% NFT Marketplace where the shielding request has been submitted

The fee as well as the percentage based distribution are defined in the [globals](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=globals)-table of the [Smart Contract](./smart-contract.md). Both can be adjusted anytime by the admins of the [nftwatchdao](https://explorer.xprnetwork.org/account/nftwatchdao) account via MultiSig proposal.

## Basic Check

The [Guards](./guards.md) will usually only shield NFT collections that pass the basic check requirements

### Requirements

An NFT collection needs to meet following requirements:

- age of first mint > 1 month
- min. 25 unique NFTs
- min. 10 unique buyers (transfers/airdrops are not counted)

## How does the shielding process look like?

### 1. Request Shielding

#### Providing the Shielding Fee
The exact shielding fee of currently `10000.0000 XPR` needs to be sent by the requester to the nftwatchdao account ***upfront*** with the memo `shielding`.

*Note: The token transfer action with the memo can be included in the same transaction. An NFT marketplace can propose such transaction accordingly.*

#### Calling the `reqshielding` action
Any community member request an NFT collection to be shielded by calling the [`reqshielding`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&action=reqshielding) action on the [Smart Contract](./smart-contract.md#public). This can be done directly via the explorer interface or via some independent UI, e.g. the interface of an NFT marketplace that utilizes NFT Watch DAO.

#### Skipping the Basic Check (Exceptions & Special Treatments)
In certain edge cases you might want to skip the Basic Check. In such cases you should consult with the [Guards](./guards.md) before doing so.

Potential cases, where skipping is possible:

- NFT collections of creators that already have another shielded NFT collection.
- NFT collections that are closely related to already shielded NFT collections, e.g.:
    - Secondary NFT collections that provide utility such as discounts, requests for custom creations, ...
    - NFT collections that have been distributed as an airdrop for an NFT collection that has already been shielded.
- NFT collections that might be attractive for scammers to be copied. A prominent example for this case are the [Proton DEX Keys](https://soon.market/collections/353512453544), where scammers unfortunately were able to collect funds of some community members before shielding existed.

*Note: Guards might also be willing to add the shield to such collections directly, without the need for a shielding request.*

### 2. Review (Basic Check & Report Creation) 

One of the [Guards](./guards.md) will:

1. Perform a Basic Check on the proposed NFT collection
1. Create a report according to the [Report Template](https://docs.google.com/spreadsheets/d/1iSVNuCF7yMAfQfR6yZ1VLHVxWM6PFCtaySH5Nf34rRw/edit#gid=0)
1. Publish the report (Google Drive + IPFS)
1. Confirm/Reject the shielding request by providing the IPFS Hash/CID of the published report to make it verifiable and to ensure it is tamper proof

### 3. Shielding / Rejection

- In case of shielding, a new entry will be added to the [`shielding`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=shielding)-table and the contract will log this action.
- In case of rejection, the shielding request will be deleted and the rejection will only be logged by the contract.