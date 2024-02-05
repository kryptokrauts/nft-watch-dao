# Blacklisting

## How does the blacklisting process look like?

### 1. Report

Any community member can report an NFT collection that potentially violates the [Code of Conduct](./code-of-conduct.md) by calling the [`report`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Actions&account=nftwatchdao&scope=nftwatchdao&limit=100&table=globals&action=report)-action on the [Smart Contract](./smart-contract.md#public). This can be done directly via the explorer interface or via some independent UI, e.g. the interface of an NFT marketplace that utilizes NFT Watch DAO.

### 2. Guard Review

One of the [Guards](./guards.md) will perform a check on the reported NFT collection:

- If the NFT collection is a clear rip-off, [Guards](./guards.md) will confirm to put the NFT collection on the blacklist.
- If the NFT collection is assumed to be a knock-off, [Guards](./guards.md) will try to reach out to the creator or the team behind an NFT collection before taking a decision. This applies for NFT collections where IP issues or other controversal grey area issues are assumed.
- If no violation is detected, the report will be rejected by and no action will be taken.

Learn more about knock-offs in the [FAQ](./faq.md#what-is-the-difference-between-copy-paste-scams-and-knock-off-assumptions-why-are-they-treated-differently-how-does-nft-watch-dao-make-the-determination).


### 3. Blacklisting / Rejection

- In case of blacklisting, a new entry will be added to the [`blacklist`](https://explorer.xprnetwork.org/account/nftwatchdao?loadContract=true&tab=Tables&account=nftwatchdao&scope=nftwatchdao&limit=100&table=blacklist)-table and the contract will log this action.
- In case of rejection, the report will be deleted and the rejection will only be logged by the contract.