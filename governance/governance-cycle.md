# Governance Cycle

MakerDAO's Governance Cycle defines the process through which Maker governance decisions are made. The Governance Cycle is split into the Monthly Governance Cycle and the Weekly Governance Cycle that are defined in MIP51 and MIP16 respectively.

## The Monthly Governance Cycle (MIP51)

By defining a a Monthly Governance Cycle MIP51 provides a predictable framework for Maker governance decisions.

### Governance Cycle Breakdown (MIP51c1)

The first Monday of each calendar month marks the beginning of the Monthly Governance Cycle.

Proposals submitted into the Monthly Governance Cycle must follow the guidelines defined in [MIP0](https://github.com/makerdao/mips/blob/master/MIP0/mip0.md).

*Time is inclusive and based on UTC (Coordinated Universal Time) and the Gregorian calendar*

**Week 1, Monday**
-   MIP Authors move their proposals to **Formal Submission** (Phase 5 described in [MIP0c3](https://github.com/makerdao/mips/blob/master/MIP0/mip0.md#mip0c3-the-mip-lifecycle)). This phase lasts for 3 days.
-   Proposals must be moved into the [formal submission](https://forum.makerdao.com/c/mips/fs/16) subcategory on the MakerDAO forums under the [Maker Improvement Proposal](https://forum.makerdao.com/c/mips/14) category (as defined in Phase 5 in [MIP0c3](https://github.com/makerdao/mips/blob/master/MIP0/mip0.md#mip0c3-the-mip-lifecycle)).
-   MIP Editors must be informed by MIP Authors of the status change via commonly used communications channels.

**Week 1, Thursday**
-  Governance Facilitators perform the **Submission Review** as part of the weekly Governance and Risk meeting and communicate which of the proposed MIPs are in accordance with guidelines (defined in the MIP0 Framework) and will continue to the Ratification Poll.
- The Governance Facilitators must come to consensus on whether each submission warrants moving forward to a Ratification Poll.
    - Governance Facilitators may consider blocking a proposal if they believe that moving forward to a Ratification Poll would negatively affect community cohesion.
    - If the Governance Facilitators prevent a proposal from moving to a Ratification Poll, they must clearly communicate their reasons for doing so via the official [forum](https://forum.makerdao.com).
    - In the event the Governance Facilitators abuse this power they should be removed from their positions via any method Maker Governance determines is appropriate.

**Week 2, Monday**
-   The Governance Facilitators publish the set of **Ratification Polls**. The format of these is defined in MIP51c2.
-   Ratification Polls are published to the [community GitHub](https://github.com/makerdao/community/tree/master/governance/polls), submitted on-chain and appear on the official [voting portal](https://vote.makerdao.com/).

**Week 4, Monday**
-   The Ratification polls conclude, and each proposal or set of proposals is marked as either Accepted or Rejected by the MIP Editors.

**Week 4, Thursday**
- The Governance Facilitators do a **Governance Cycle Review** as part of the weekly Governance and Risk meeting in which they summarize and discuss the Governance Cycle with the community.
- The Governance Facilitators also discuss the upcoming governance cycle and potential submissions with the community.

### Governance Cycle Overview
![Gov Cycle](https://user-images.githubusercontent.com/53664591/114054203-8c7de580-9887-11eb-90da-0431b051fff3.png)

---

### MIP51c2: Ratification Poll

Ratification Polls under the Monthly Governance Cycle must meet these requirements:
* **Duration:** 2 weeks
* **Minimum Positive Participation:** 10,000 MKR
* **Type:** Binary poll (yes/no/abstain)

Ratification Polls under the Monthly Governance Cycle must contain:
* Links to a *specific version* of a single proposal or set of related proposals (MIP Set) within the official MIPs GitHub.
* The Sentence and Paragraph summaries of each included proposal.

In order for a Ratification Poll to conclude successfully and the contained proposal(s) move to Accepted status, each of the following conditions must be true:
* `Yes` vote-weight must exceed `No` vote-weight when the poll closes.
* `Yes` vote-weight must exceed the `Minimum Positive Participation` value of 10,000 MKR when the poll closes.

---

### MIP51c3: Minimum Positive Participation Changes

The Minimum Positive Participation value defined in MIP51c2 may be modified via a successful polling vote under the Weekly Governance Cycle (MIP16).

If such a vote is successful, the MIP Editors will update MIP51c2 and the change will come into effect in the _following_ Monthly Governance Cycle.

The Minimum Positive Participation value may not be changed for Ratification Polls that are in progress under any circumstances.

---

### MIP51c4: Calendar Exceptions

Due to the multitude of cultural and religious holidays occurring in and around the month of December, there will be no Monthly Governance Cycle in the December of each year.

# The Weekly Governance Cycle (MIP16)

MIP16 defines and formalizes the Weekly Governance Cycle to provide a more predictable weekly framework for Maker governance decisions.
It complements the Monthly Governance Cycle ([MIP51](https://github.com/makerdao/mips/blob/master/MIP51/mip51.md)) by enabling recurring weekly decisions to be made that require quicker action.


### MIP16c1: Weekly Governance Cycle Definitions

- A **Weekly Poll** is a non-binding MKR poll that determines the weekly Executive Vote contents. In this context, a non-binding weekly poll refers to the fact that a weekly poll cannot change the system parameters independently; it merely dictates what will be included at the end of week in the Executive Vote.
- A **Non-Standard Weekly Poll** is a non-binding weekly poll that has arbitrary time-sensitive decisions that MKR holders have to make in a relatively short period of time. These polls are needed to be expedited through the Maker governance process via a separate vote. The use of non-standard weekly polls is dedicated to Facilitators, given that they have already established a high level of trust with the community. Furthermore, the use of non-standard weekly governance polls will be limited to situations where the weekly governance cycle is determined to operate too slowly to be usable.
- Facilitators that have been onboarded into [MIP38: DAO Primitives State](https://github.com/makerdao/mips/blob/master/MIP38/mip38.md) have been authorized by Maker Governance to efficiently interact with the weekly cycle to enable them to fulfill their Core Unit Mandate with as little friction as possible. Facilitators are authorized to submit non-standard Weekly polls that are related to their Core Unit Mandate and include logic in the weekly Executive Vote that is related to their Core Unit Mandate. If necessary, and if it is related to their Core Unit Mandate, Facilitators can skip the Non-Standard Weekly poll and include logic directly into the weekly Executive Vote.

---

### MIP16c2: Weekly Governance Cycle Breakdown


**Monday**

- Every Monday, the weekly cycle begins and includes standard recurring decisions proposed in the form of a weekly poll. The poll will run for three days ending Thursday before the Governance and Risk Call.

**Thursday**

- The weekly poll results will be reviewed on the Governance and Risk Call.

**Friday**

- Every Friday, given the Monday Weekly Governance Poll passes, the weekly polls are put up for an Executive Vote. The Weekly Executive vote has an expiration of one week.

### Overview of the Weekly Governance Cycle

![weekly_monthly-gov](https://github.com/makerdao/mips/blob/master/MIP16/weekly_governance_cycle.png?raw=true)

**Important Notes:**

- If a non-standard weekly poll ("signal request") has been proposed, it will also be put in the weekly poll. To create a non-standard weekly poll requires an urgent and apparent reason from a timing perspective to justify it. It is important to note that a non-standard weekly poll cannot be used for long-term decisions and requires consensus from the Governance Facilitators before it can be accepted and published.


## MakerDAO Calendar

Dates relevant to the Weekly and Monthly Governance Cycles as well as MakerDAO calls, events, polls, and more, can be found at [MakerDAO Calendar](https://calendar.google.com/calendar/u/0/embed?src=makerdao.com_3efhm2ghipksegl009ktniomdk@group.calendar.google.com&ctz=America/Los_Angeles).
