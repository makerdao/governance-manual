
# Voting and MakerDAO
MakerDAO is a decentralized autonomous organization whose governance process controls various aspects of the protocol. This guide is for anyone who wishes to participate in the governance process through voting.

Voting requires MKR tokens. MKR holders have the sole authority to enact changes to the system through voting. Off-chain voting takes place on the [Maker Forum](https://forum.makerdao.com) and on-chain voting takes place on the [Governance Portal](https://vote.makerdao.com/). 

Voting is calculated by a weighted voting system, where voting power is proportional to the amount of MKR tokens cast. For example, if 50 stakeholders hold a total of 600 MKR and vote for proposal A, while 100 stakeholders hold a total of 400 MKR and vote for proposal B, then Proposal A would win with 60% of the vote. The number of stakeholders who voted for a proposal does not change the result.



---


---



## On-chain Governance 
### Governance Polls
Governance Polls occur on-chain and are used to measure the sentiment of MKR voters. They can be accessed through the the [polling page](https://vote.makerdao.com/polling) in the Governance Portal.

Polls often run concurrently, allowing voters to participate in any number of them at the same time and some use [instant run-off](https://en.wikipedia.org/wiki/Ranked_voting), so you can select multiple options.

The current schedule calls for polls to go live on a weekly basis every Monday at 16:00 UTC.

MKR holders may be asked to:

- Determine governance and DAO processes outside the technical layer of the Maker Protocol.
- Form consensus on important community goals and targets.
- Measure sentiment on potential Executive Vote proposals.
- Ratify governance proposals originating from the MakerDAO forum signal threads.
- Determine which values certain system parameters should be set to before those values are then confirmed in an executive vote.
- Ratify risk parameters for new collateral types as presented by Risk Teams.

Here is [an example](https://vote.makerdao.com/polling/Qmeac95W?network=mainnet#poll-detail) of a governance poll on the Governance Portal:

#### How long is the voting period of a Governance Poll?
The voting period of a given Governance Poll varies. Recurring polls of the same type are usually standardized and have the same duration.

The most common are three and seven day periods. Concurrently running polls do not necessarily have the same voting periods.

#### Where can I find on-chain Governance Polls?
Live polls can be found on the [polling page](https://vote.makerdao.com/polling) of the Governance Portal. Historic poll data can be found at the [Maker Governance Analytics Dashboard](https://mkrgov.science/).

User risks can be mitigated by using small test amounts beforehand and by thoroughly checking which addresses one is interacting with.

#### How to create an on-chain Governance Poll?
Anyone can create an on-chain Governance Poll using the polling smart contract, however, there is no UI provided to do this yet.

Currently, only the elected Governance Facilitators are able to put up polls that display on the [Governance Portal](https://vote.makerdao.com). Polls created by arbitrary Ethereum addresses **are not** displayed.

In the future, the MKR token holders or any third parties may want to develop special UIs or other voting frontends.



### Executive Votes
Executive Votes occur on-chain and can be accessed through the [executive page](https://vote.makerdao.com/executive) in the Governance Portal.

Executive Votes execute technical changes to the Maker Protocol. When active, each Executive Vote has a proposed set of changes being made on the Maker Protocol's smart-contracts.

Unlike the other types of votes, Executive Votes use a Continuous Approval Voting model.

Executive Vote can occur at any time, however the current schedule calls for Executive Votes to go live on Fridays 12pm EST, 9am PST, 14:00 UTC.

Executive Votes can be used to:

- Add or remove collateral types.
- Add or remove Vault types.
- Adjust global system parameters.
- Adjust Vault-specific parameters.
- Replace modular smart contracts.

Anyone can create an on-chain Executive Vote using the MakerDAO governance contracts, however, there is no non-technical UI available to do this.

Users can create proposals, also known as [slates](https://docs.makerdao.com/smart-contract-modules/governance-module/chief-detailed-documentation), through this [experimental portal](https://chief.makerdao.com/), or by interacting directly with the smart contracts.

Here is [an example](https://vote.makerdao.com/executive/template-executive-vote-parameter-changes-wsteth-a-onboarding-october-22-2021?network=mainnet#proposal-detail) of an executive vote on the Governance Portal:


#### How is the voting calculated?
Executive votes are calculated through Continuous Approval voting. In such a system, competing proposals may be introduced any time. Proposals remain active for a period of 30 days or until they get executed, whichever is earlier. After this, they become inactive proposals but remain eligible for votes. 

An active proposal is executed if it has more votes in its favor than the any single inactive proposal. If MKR token holders do not agree with a new proposal, then they may cast their votes for any inactive proposal, implying that they support the current state of the system. To revert a change in the system an entirely new proposal must be put forth. It is impossible to reactivate a proposal, once it is inactive. 

There are three aspects to consider with regard to Continuous Approval Voting:

- A vote for any inactive proposal creates a barrier for new proposals, since new proposals need to surpass the voting weight of the inactive proposal with the largest amount of MKR voting for it.
- Votes are meant to remain in the system continuously in order to prevent bad proposals from passing easily.
- The more votes there are on the current state of the system, the more secure the system generally is from any "rogue" proposals.

With Continuous Approval Voting, the continuity of staked votes challenges and reinforces the status quo of the system through movements of the majority of votes between the current state (most recent successful proposal) and new proposals.



### Auditability
#### With regard to new votes
The public is encouraged to self-audit the code for each vote. There is an accessible guide on how to do so [here.](https://github.com/blimpa/maker-operational-manual/tree/0fa13385ea5d0f81640f54a58ba46c759fe926a7/learn/governance/audit-exec-spells/README.md) 


#### With regard to a user's voting record
The voter's current vote is displayed on a given proposal page in the [Governance Portal](https://vote.makerdao.com/). Another alternative is to check third-party tools like [mkrgov.science](https://mkrgov.science) that collect voting data and even offer a [voting history lookup tool](https://mkrgov.science/voting-history).




---


---


## Off-Chain Governance
Off-chain governance supports on-chain governance by providing a process for gathering feedback prior to proposing on-chain votes and making decisions that don't require on-chain voting.

### Forum Signal Threads
Forum Signal Thread occur in the [Maker Forum](https://forum.makerdao.com/) to measure the sentiment of the public governance community. Anyone can create a signal thread to get feedback on their ideas to take action on an issue or improve the MakerDAO community.

Forum Signal Threads are used to:

- Measure community sentiment about issues affecting the MakerDAO ecosystem.
- Determine consensus that something needs to be done in response to a perceived issue.
- Determine consensus for a concrete action to be taken in response to a perceived issue.


Signal threads may contain one or more polls as determined by the original poster of the thread and issues may have one or more signal threads relating to them. Consider creating a summary thread if you happen to see this arise.

A guide to the signaling process is [here](https://forum.makerdao.com/t/guide-to-the-signaling-process/9400). A basic example of a Forum Signal Thread can be found [here](https://forum.makerdao.com/t/signal-request-should-we-increase-the-scd-debt-ceiling/506)

### Forum Signal Threads vs Forum Polls
A Forum Signal Thread is created with the intention of gathering consensus around an issue and moving that issue to an on-chain Governance Poll.

Forum polls can be used to measure community sentiment about anything and their use is encouraged. There are no guidelines on the general use of forum polls other than courtesy and common sense.

### Active Forum Polls
Once a forum signal thread has been active for several weeks and voted on by a reasonable number of community members, the creator of the signal thread will decide whether to refine the signal thread and post a new one or request that the Governance Facilitator push it to an on-chain governance poll.

If the Governance Facilitator agrees that the issue outlined in the signal thread is ready to go on-chain, then the Governance Facilitator will create an on-chain Governance Poll in the form specified by the community consensus created in the signal thread.



---


---


## Practical guide to on-chain voting
This section explains how users can vote using their MKR. 

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
