# Token Streaming Module

```
Alias: Vest
Contract Name: DSSVest
Scope: System
```

## Description

The Token Streaming Module automates vesting of tokens being paid from the Maker Protocol to Core Units or individuals. It allows scheduling, cliff vesting, specification of vesting periods or third-party revocation. Once the vesting cliff has been reached, the reward cannot be revoked and users can independently redeem their tokens.

The Token Streaming Module can pay out tokens in Dai or in MKR. It is able to either mint new tokens, or pay out tokens that have been deposited within the Module by Maker Governance.

The following is an example of how this might work in practice:

Maker Governance has agreed to reward a contributor with 100 MKR with a cliff period of 6 months. Once 6 months have expired, the contributor will be able to redeem 100 MKR from the Token Streaming Module.

In an alternative scenario, the contributor leaves the Maker Protocol before 6 months have expired. Here, a representative of Maker Governance, usually a Core Unit Facilitator, would be able to halt the vesting process through third-party revocation, and the contributor will be unable to claim the MKR.

## Purpose

The Token Streaming Module provides multiple benefits both to the Maker Protocol and to Contributors. These include:

* Provision of a secure mechanism to reward contributors to the Maker Protocol
* Reduction of Governance Overhead regarding compensation for contributors
* Enabling management of contributor compensation by Core Unit Facilitators when contributors leave the Maker Protocol
* Provision of an ability to track vesting of Dai and MKR, increasing transparency
* Enabling independent user control over claiming of vested tokens, this may be important in regards to tax in certain jurisdictions

## Trade-offs
* What dangers does this module represent?
* What advantages does this module represent?

## Key Parameters
* What are the key parameters to this module, and how do they work?

## User Interaction
* How can users interact with this module?

## Considerations
* Is there anything little known about this module?
* How does this interact with other parts of the protocol?
* Are there any Emergency Shutdown considerations to take into account?
