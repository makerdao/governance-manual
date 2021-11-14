# On-chain Governance 


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