# Practical guide to on-chain voting
This section explains how users can vote using their MKR. 

### Single wallet voting
Single wallet voting is the simplest method of voting. The initial setup is more convenient and users who store MKR on MetaMask or other web wallets may find it to be the easiest way to start voting. Users deposit tokens directly into the voting contract by connecting their wallet to the Governance Portal. 

Single wallet voting can lead to security issues if a non-hardware wallet is used because every vote requires an interaction with the wallet.

### Linked wallet voting
The disadvantages of single wallet voting can be circumvented by the Voting Proxy contract. It improves security in the voting process by enabling MKR owners to participate in Maker Governance without using their most secure wallet (called the “cold wallet”) for voting. The MKR owner designates a so-called “hot wallet” that can be used only for voting, and transfers their MKR to the voting proxy contract. The designated “hot wallet” can then be used to lock up MKR in the voting system and draw MKR back to the cold wallet at a later time. These are the only actions the “hot wallet” can perform. It cannot send the MKR anywhere else, nor can it withdraw the MKR to its own wallet. Therefore, if the hot-wallet is compromised, the voter's MKR is not at risk.


### Costs of voting
Voting requires a single transaction and fees will vary based on the congestion of the Ethereum blockchain. 

Setting up a linked-wallet Voting Contract takes four transactions for a total of approximately 1 million gas. The cost of setting up a linked-wallet Voting Contract is split between the hot and cold wallets so users should ensure both wallets contain sufficient Ether (ETH) to pay for gas costs.

### Delegation
MKR holders may also delegate their MKR and allow the delegate to vote on their behalf. More information on delegation can be found [here](https://manual.makerdao.com/governance/what-is-delegation).

$eof$