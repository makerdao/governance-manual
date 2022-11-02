# On-chain Governance 
There are two main types of on-chain governance activities: Governance Polls and Executive Votes. 

### Governance Polls

Governance Polls occur on-chain and are used to measure the sentiment of MKR voters. Polls often run concurrently, allowing voters to participate in any number of them at the same time. Polls may have different formats like Binary Voting, [Instant Run-Off Voting](https://en.wikipedia.org/wiki/Ranked_voting), or [Approval Voting](https://en.wikipedia.org/wiki/Approval_voting) depending on the topic. The current schedule calls for polls to go live each week on Monday at 16:00 UTC.

MKR holders may be asked to:

- Determine governance and DAO processes outside the technical layer of the Maker Protocol.
- Form consensus on important community goals and targets.
- Determine which proposals should proceed to a future Executive Vote.
- Ratify governance proposals originating from MakerDAO Core Unit Facilitators.
- Determine which values certain system parameters should be set to before those values are then confirmed in an executive vote.
- Ratify risk parameters for new collateral types.

Here is [an example](https://vote.makerdao.com/polling/Qmeac95W?network=mainnet#poll-detail) of a governance poll on the Governance Portal.

#### How long is the voting period of a Governance Poll?
The voting period of a given Governance Poll varies. Recurring polls of the same type are usually standardized and have the same duration. The most common are three and fourteen day periods. Concurrently posted polls do not necessarily have the same voting periods.

#### Where can I find on-chain Governance Polls?
Live and historic polls can be found on the [polling page](https://vote.makerdao.com/polling) of the Governance Portal.

#### How can I create an on-chain Governance Poll?
The on-chain Governance Poll smart contracts are permissionless, meaning anyone can trigger a poll. However, there is no creation or voting UI provided for user-generated polls. Polls created by arbitrary Ethereum addresses **are not** displayed on the official governance portal.

Currently, only Governance Facilitators are able to put up polls that display on the official [Governance Portal](https://vote.makerdao.com), and they do so on behalf of the rest of MakerDAO. This helps to ensure a level of standardization and quality of presentation.

### Executive Votes
Executive Votes occur on-chain and can be accessed through the [executive page](https://vote.makerdao.com/executive) in the Governance Portal.

Executive Votes execute technical changes to the Maker Protocol. When active, each Executive Vote has a proposed set of changes being made to the Maker Protocol's smart contracts. Executive Votes use a Continuous Approval Voting model.

Executive Votes can occur at any time, but the current schedule calls for Executive Votes to go live on Wednesdays. The exact time varies but is almost always after 14:00 UTC.

Executive Votes can be used to do the following (among other things):
- Add or remove Vault types.
- Adjust system parameters.
- Replace modular smart contracts.

Here is [an example](https://vote.makerdao.com/executive/template-executive-vote-parameter-changes-wsteth-a-onboarding-october-22-2021?network=mainnet#proposal-detail) of an executive vote on the Governance Portal.

Anyone can create an on-chain Executive Vote using the MakerDAO governance contracts; however, there is no non-technical UI available to do this. Users can create proposals, also known as [slates](https://docs.makerdao.com/smart-contract-modules/governance-module/chief-detailed-documentation), through this [experimental portal](https://chief.makerdao.com/), or by interacting directly with the smart contracts.

Under the normal schedule, an Executive Vote's contents are determined collaboratively by relevant Core Units that consider changes that are both approved by governance and ready for safe implementation. Once the contents have been determined, the proposal smart contract is created by the Protocol Engineering Core Unit.

Regularly scheduled proposals created by the Protocol Engineering Core Unit have the following properties: 
* They execute a single set of changes exactly once. 
* They are deactivated for safety reasons if they have not been passed within 30 days.

#### How is the voting calculated?
Executive Votes are calculated through Continuous Approval Voting. In such a system, competing proposals may be introduced at any time.

An active proposal may be executed if it has more votes in its favor than any other proposal. If MKR token holders do not agree with a new proposal, then they should cast their votes for the inactive proposal with the most vote-weight (usually the last proposal to successfully pass.)

The highest vote-weight proposal is sometimes referred to as the 'hat' proposal.

There are three aspects to consider about Continuous Approval Voting:
- Vote-weight present on the 'hat' proposal sets the 'victory threshold' for new proposals.
- Vote-weight may move from the 'hat' proposal to any new proposal, this both reduces the 'victory threshold' _and_ contributes to the new proposal's vote-weight.
- Vote-weight is meant to remain in the system on the 'hat' proposal to help secure it from any "rogue" proposals.

### Auditability

#### New votes
The public is encouraged to self-audit the code for each vote. There is an accessible guide on how to do so [here](governance/executive-audit.md). 

#### Voting record
The voter's current vote is displayed on a given proposal page in the [Governance Portal](https://vote.makerdao.com/). Historical voting records are also available on the governance portal.

>Page last reviewed: 2022-10-25  
>Next review due: 2023-10-25  

