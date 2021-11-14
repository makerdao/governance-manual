# Practical guide to on-chain voting
### Single wallet voting
Single wallet voting is the simplest method of voting. The initial setup is more convenient and users who store MKR on MetaMask or other web wallets may find it to be the easiest way to start voting. Users deposit tokens directly into the voting contract by connecting their wallet to the Governance Portal. 

Single wallet voting can lead to security issues since every vote requires the wallet to be online. The single wallet setup also has another disadvantage - there are two different contracts that manage the two types of votes (Governance Polls and Executive Votes). MKR tokens cannot be used to vote on both simultaneously. 

### Linked wallet voting
The disadvantages of single wallet voting can be circumvented by the Voting Proxy contract. It assures that MKR owners can vote with the full weight of the MKR they own, both for Governance voting, and for Executive voting. Moreover, it improves security in the voting process by enabling MKR owners to participate in Maker Governance without having their most secure wallet (called the “cold wallet”) online for every vote. The MKR owner designates a so-called “hot wallet” that can be used only for voting, and transfers their MKR to the voting proxy contract. The designated “hot wallet” can then be used to lock up MKR in the voting system and draw MKR back to the cold wallet at a later time. These are the only actions the “hot wallet” can perform. It cannot send the MKR anywhere else, nor can it withdraw the MKR to its own wallet.

A guide to setting up the linked wallet can be found [here](https://makerdao.world/en/learn/governance/voting-setup/).

### Costs of voting
Voting requires a single transaction and typically costs a few cents per vote. The total amount varies depending on network congestion.

Setting up a linked-wallet Voting Contract takes four transactions for a total of approximately 1M gas. The cost of setting up a linked-wallet Voting Contract is split between the hot and cold wallets so please ensure both wallets contain Ether (ETH).


### Delegation
MKR holders may also delegate their MKR and allow the delegate to vote on their behalf. More information on delegation can be found [here](https://forum.makerdao.com/t/delegation-and-makerdao/9429) and a MKR holder's guide to delegation can be found [here](https://forum.makerdao.com/t/mkr-holder-s-guide-to-delegation/9602).

Anyone may choose to become a delegate. There are two types of delegates:
- Recognized delegates who are whitelisted, and must meet certain requirements in exchange for more visibility and prestige.
- Shadow delegates who are permissionless, with no requirements or responsibilities beyond that which they have agreed directly with those who delegate to them.

The requirements to become a recognized delegate are [here](https://forum.makerdao.com/t/recognised-delegate-requirements/9421). Note that setting up the contract and not fulfilling the remaining requirements automatically makes one a shadow delegate.
