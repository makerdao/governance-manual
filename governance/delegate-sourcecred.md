# Delegate Engagement Compensation Mechanism

Engagement and discussion around governance decisions are extremely important for the long-term health of MakerDAO.

Recognized delegates are compensated for the quantity and quality of their engagements on the MakerDAO forum as judged by the rest of the community via the SourceCred mechanism.

### Cred Distribution

Delegates are excluded from payouts under the main SourceCred instance. However, we still use the Cred distribution across Recognized Delegates to assess their engagement with some operational modifications. 

1. A separate pool of funds exists to compensate Recognized Delegate engagement.
2. Rewards are distributed outside of the existing SourceCred instance.

Separating the delegate and community engagement budgets prevents Recognized Delegates from monopolizing the DAI distribution. It also maintains the dispersion and decentralization of the benefits that SourceCred offers to the community.

52,000 DAI annually is allocated to the Recognized Delegate reward pool. This breaks down to 1,000 DAI allocated to delegates per week based on their engagement in the MakerDAO forum.

### Cred Calculation

Cred for delegates is calculated using a custom algorithm based on raw weekly cred scores. 

This algorithm assesses the activity of the Delegates on a weekly basis, measuring cred earned from likes received, topic-post interactions, and post-reply interactions on the posts they have created during that week.

This is performed in a three-step process:
- First, the algorithm selects the week evaluated for a specific delegate.
- Then, it filters out all of the actions that are not relevant for the scope of this calculation (user mentions, inter-week cred interactions, and cred lost for likes given).
- Finally, it counts and stores the cred that is left in the selection.

This makes the calculation more biased toward direct delegate activity and recent quality contributions, so Delegates that contribute less (garner fewer likes, replies, and link-backs) will notice that the DAI they receive from SourceCred will be greatly reduced.

### Payout Process

Engagement compensation in DAI is calculated on a weekly basis and paid out to Recognized Delegates once a month.

Compensation calculations are transparent and located here: GovAlpha Observable.

Payouts are consolidated into a CSV file and distributed by GovAlpha from the GovAlpha multisig wallet.

Delegates' engagement performance will be published in each month's Delegates Round-up along with an overview of their activity within Maker Governance.

# Delegate Engagement Eligibility

## General Eligibility
**1.1** - Any Recognized Delegate with one or more official forum accounts is eligible to receive delegate engagement payouts for **one account only**.  
**1.2** - Recognized Delegates must opt in and confirm which forum account is accruing engagement payouts.  

## Monthly Eligibility
**2.1** - A Recognized Delegate is only eligible for engagement payouts in a given month if they meet the criteria in [MIP61](https://mips.makerdao.com/mips/details/MIP61#performance-modifier) to receive a non-zero amount of compensation for that month.  

## Exclusions
**3.1** - GovAlpha Facilitators may exclude any Recognized Delegate from engagement payouts at any time, for any reason.  
**3.2** - GovAlpha Facilitators must communicate a reason publicly if a given Recognized Delegate is being excluded from off-chain proposal bounty payouts.  
