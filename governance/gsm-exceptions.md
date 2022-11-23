# GSM Pause Delay Exceptions

The [GSM Pause Delay](../parameter-index/core/param-gsm-pause-delay.md) prevents changes from being made to the Maker Protocol without first waiting for a time delay. 

However, changes may be made to some functionality without waiting for this delay. 

This page lists the current exceptions and gives details of: 
* The contract that manages the functionality.
* The exceptional functionality.
* The reason for the exceptional functionality.

Contracts may be looked up using the [Chainlog](https://chainlog.makerdao.com/).

### Executive Drop Functionality
> Contract: `MCD_PAUSE`

The MCD_PAUSE contract manages the timelock functionality of the [GSM Pause Delay](../parameter-index/core/param-gsm-pause-delay.md), however it also contains an in-built exception to its own rule.

The executive drop functionality allows a successful governance proposal to cancel a previous governance proposal that has not yet passed the [GSM Pause Delay](../parameter-index/core/param-gsm-pause-delay.md) period and been executed. Note that the new executive proposal must be the `hat` proposal, meaning more MKR is voting for it than is voting for any other executive proposal. 

This functionality allows Maker governors to prevent a malicious attack on the protocol if they are able to exceed the attackers MKR weight before the [GSM Pause Delay](../parameter-index/core/param-gsm-pause-delay.md) expires.

### Oracle Freeze Functionality
> Contract: `OSM_MOM`

The OSM_MOM contract manages the freeze functionality for MakerDAO's oracles. 

The freeze functionality allows a successful governance proposal to immediately freeze the oracle price for any or all of the vault types in the Maker Protocol. Once frozen, the oracle price will remain at its current value. The oracle cannot be unfrozen without waiting for the [GSM Pause Delay](../parameter-index/core/param-gsm-pause-delay.md) as part of a regular governance proposal.

This functionality gives Maker Governance a chance to prevent a malicious oracle price from causing liquidations (or unbacked DAI minting) in the Maker Protocol. Due to the structure of Maker's oracles, the next oracle value is known one hour in advance of it becoming active in the Protocol. This is the window in which Maker Governance can act to prevent a malicious oracle price entering the protocol.

### Dynamic Debt Ceiling Functionality
> Contract: `MCD_IAM_AUTO_LINE`

The MCD_IAM_AUTO_LINE contract manages the debt ceiling parameters for many of MakerDAO's vault types according to preset rules.

Keepers can use the contract to attempt to maintain a [Target Available Debt](../module-index/module-dciam.md) in a given vault type. The contract modifies the debt ceiling up or down to maintain a level of available debt.

This functionality is exceptional so that the Maker protocol can react to changes in debt demand more quickly than waiting for the GSM delay.

### Liquidations Circuit Breaker
> Contract: `CLIPPER_MOM`

The CLIPPER_MOM contract manages the circuit breaker functionality for vault types using [Liquidations 2.0](https://docs.makerdao.com/smart-contract-modules/dog-and-clipper-detailed-documentation). 

The circuit breaker functionality allows a successful governance proposal to impose governance's choice of limitations on liquidations for any or all of the vault types in the Maker Protocol.
* Level 0 - Liquidations Enabled - The breaker is not tripped, new vaults can be liquidated and old liquidations can proceed.
* Level 1 - New Liquidations Disabled - No new liquidations can take place.
* Level 2 - New Liquidations and Resets Disabled - No new liquidations can take place. No existing auctions can be reset if they expire.
* Level 3 - All Liquidations Disabled - No new liquidations, no resets, no bidding in active auctions. 

This functionality is exceptional because liquidations at non-market prices have the potential to be irreversibly damaging to both users and the Maker Protocol. The circuit breaker allows Maker governance to attempt to limit the damage in the event of an issue affecting liquidations without waiting for the [GSM Pause Delay](../parameter-index/core/param-gsm-pause-delay.md).

### Direct Deposit Breaker
> Contract: `DIRECT_MOM`

The DIRECT_MOM contract manages the breaker functionality for [Direct Deposit Modules (D3Ms)](../module-index/module-dai-direct-deposit.md).

The breaker functionality allows a successful governance proposal to disable any or all of the active D3Ms. In practice, this will set the `bar` parameter to zero, which (contrary to intuition) disables the module by setting the allowed Debt Ceiling to zero. At this point, no further DAI can be minted through the Direct Deposit Module.

This functionality is exceptional to give Maker Governance a chance to limit the lost value if the target protocol or entity for a D3M becomes insolvent. Because targets are often publicly accessible protocols there is likely to be a race to extract as much value as possible in the event of a hack or insolvency event. Waiting for the [GSM Pause Delay](../parameter-index/core/param-gsm-pause-delay.md) to expire makes it likely that the Maker Protocol will lose significant value - likely close to the maximum debt ceiling on the D3M. 

### 


FLIPPER_MOM ?? Still used?

STARKNET_ESCROW_MOM ?? Does this apply to Arbitrum and Optimism too?

