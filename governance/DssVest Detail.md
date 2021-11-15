# Token Streaming Module

```
Alias: Vest
Contract Name: DSSVest
Scope: System
```

## Description

The Token Streaming Module automates vesting of tokens being paid from the Maker Protocol to Core Units or individuals. It allows scheduling, cliff vesting, specification of vesting periods, or third-party revocation. Once the vesting cliff has been reached, the reward cannot be revoked and users can independently redeem their tokens.

The Token Streaming Module can primarily payout tokens in Dai or in MKR. It can either mint new tokens or payout tokens that have been deposited within the Module by Maker Governance.

The following is an example of how this might work in practice:

Maker Governance has agreed to reward a contributor with 100 MKR with a cliff period of 6 months. Once 6 months have expired, the contributor will be able to redeem 100 MKR from the Token Streaming Module.

In an alternative scenario, the contributor leaves the Maker Protocol before 6 months have expired. Here, a representative of Maker Governance, usually a Core Unit Facilitator, would be able to halt the vesting process through third-party revocation, and the contributor will be unable to claim the MKR.

## Purpose

The Token Streaming Module provides multiple benefits both to the Maker Protocol and to Contributors. These include:

* Provision of a secure mechanism to reward contributors to the Maker Protocol
* Reduction of Governance Overhead regarding compensation for contributors
* Enabling management of contributor compensation by Core Unit Facilitators when contributors leave the Maker Protocol
* Provision of an ability to track vesting of Dai and MKR, increasing transparency
* Enabling independent user control over-claiming of vested tokens, this may be important in regards to tax in certain jurisdictions

## Trade-offs

DssVest is ultimately a different way of distributing tokens. As such, it should be compared to manual transfers of tokens. In general, DssVest allows for distributions over some time, with Governance retaining the ability to halt streaming at any point in time. 

Thus, there are some trade-offs with MKR Voter control over token distributions. DssVest allows MKR holders to vote on issues of token distribution less often, which might be an advantage for the convenience, however also requires more attention to continued operations from MKR holders, as tokens will continue to stream until fully allocated or stopped by a further governance action.

Additionally, DssVest shifts the gas costs from the protocol (or more accurately the team doing the spell-crafting) to address receiving the tokens. While gas efficient, these transactions can cost upwards of a couple of hundred DAI in times of heavy network congestion. 

## Key Parameters

Parameters for DssVest are unique as they are set upon deployment of a new stream. The primary parameters are:

- address
- start date
- end date
- "cliff" date (ie tokens will not be available to the end address until this date)

## User Interaction

DssVest allows recipients to claim streamed tokens at their discretion. For a full review on how to use DssVest please see [$insert-link-here]().

## Considerations

In addition to the considerations described as well, the DssVest Contract can be used to set up a stream of any ERC-20 token. This not only allows for novel tokens to be distributed through the contract but also has unique implications for groups receiving DAI or MKR funding. Upon receiving the tokens, groups can make use of the ability to stream tokens to do things like payout salaries or set up individual vesting from a group allocation.

Also of note is when using the DAI Vesting contract, funds remain in the surplus buffer until called by the recipient. This means any unused funds can be used to protect the protocol, however, also the contract carries the danger of MKR minting if a recipient calls their funds in when the surplus buffer is depleted. 
