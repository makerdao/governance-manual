
# Delegate Information and Resources


## Voting and the Governance System

Information about the major parameters that exist within the Maker Protocol can be found as part of the Maker Operational Manaual Parameter Index.

The [Executive Transation](../governance/executive-transaction-verification.md) page shows you how to check that your voting transactions match the Voting Portal UI.

The [Executive Audit](../governance/executive-audit.md) page describes a non-exhaustive set of items that are important to check when looking at executive spell code. 

Technical documentation for the Maker Protocol executive governance system is located [here](https://docs.makerdao.com/smart-contract-modules/governance-module/chief-detailed-documentation). Important concepts for delegates to understand about the Maker Protocol governance system include: 
* [Spells](https://docs.makerdao.com/smart-contract-modules/governance-module/spell-detailed-documentation#3.-key-mechanisms-and-concepts) and their [failure modes](https://docs.makerdao.com/smart-contract-modules/governance-module/spell-detailed-documentation#5.-failure-modes-bounds-on-operating-conditions-and-external-risk-factors).
* [Slates](https://docs.makerdao.com/smart-contract-modules/governance-module/chief-detailed-documentation#glossary-chief)
* The ['hat'](https://docs.makerdao.com/smart-contract-modules/governance-module/chief-detailed-documentation#4.-gotchas-potential-source-of-user-error)
* [Approval Voting](https://docs.makerdao.com/smart-contract-modules/governance-module/chief-detailed-documentation#approval-voting)
* [Key Failure Modes](https://docs.makerdao.com/smart-contract-modules/governance-module/chief-detailed-documentation#5.-failure-modes-bounds-on-operating-conditions-and-external-risk-factors)
* The [Pause](https://docs.makerdao.com/smart-contract-modules/governance-module/pause-detailed-documentation) contract
* The [Governance Pause Delay](../parameter-index/core/param-gsm-pause-delay.md)

Concretely, it is important that delegates act to ensure that amount of MKR on the `hat` remains as high as possible for as long as possible when voting for new executive spells. This can be achieved by voting for both the current and next executive using the official voting portal.

## Emergency Response

A list of all the exceptions to the Governance Security Module is available [here](../governance/gsm-exceptions.md). 

Any action that is not a part of the exception list will be delayed by the Governance Pause Delay before taking effect. This is in addition to any delay caused by failure for the emergency proposal to become the `hat`. For this reason, it is important that delegates vote as quickly as possible in an emergency.


