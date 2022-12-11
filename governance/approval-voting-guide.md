# Approval Voting Guide for MakerDAO

Approval Voting is a form of voting used to identify a consensus option among a group of voters. Voters may already be familiar with Approval Voting from Signal Requests on the Maker Forum. Voters can select multiple options they agree with without needing to rank them, which enables polls to determine a consensus winner.

The DUX Core Unit has recently added functionality for Approval Voting to the [voting portal](https://vote.makerdao.com/), allowing the use of Approval Voting for on-chain voting at MakerDAO.

Our Approval Voting implementation is flexible; Maker Governance can use it to select single or multiple winners, depending on the polled question. It can also be configured to require the winner(s) to receive majority support, or to declare the option with the most support the winner(s), regardless of whether or not it received a majority.

When voting on an Approval Vote, voters should select **all** options with which they agree. There is no penalty for choosing multiple options. However, it is legitimate to only vote for one option if there is only one option that the voter wishes to support.

Voters cannot vote for "Abstain" and other options. If a voter wishes to Abstain, that should be the voter's only selection - the UI will enforce this.

We have the option to stop people from voting for the "Reject" option in combination with other poll options. However, the use case for this is limited, and if this restriction is in place, GovAlpha will indicate it in the poll text.

If you have questions about Approval Voting and its use at MakerDAO, please get in touch with GovAlpha.

For further information on Approval Voting, see the [Wikipedia article](https://en.wikipedia.org/wiki/Approval_voting).

>Page last reviewed: 2022-10-10  
>Next review due: 2023-10-10  

