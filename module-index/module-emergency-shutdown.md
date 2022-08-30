# Emergency Shutdown

>**Alias:** ESM  
>**Contract Name:** `esm.sol`  
>**Scope:** system  
>**Technical Docs:** [link](https://docs.makerdao.com/smart-contract-modules/shutdown/emergency-shutdown-module)

## Description

The Emergency Shutdown Module allows users to deposit MKR into the module to perform an emergency shutdown of the Maker Protocol.

When MKR holders have deposited enough MKR to the Emergency Shutdown Module, if the Emergency Shutdown Module has the appropriate authorization over the `End` contract, the emergency shutdown process can be triggered permissionlessly by calling the `fire` function.

MKR deposited to the module is not retrievable and should be considered burned.

## Purpose

The Emergency Shutdown Module allows MKR holders to trigger the emergency shutdown process, allowing the Maker Protocol to wind down, with DAI holders able to redeem DAI for underlying collateral. It is intentionally designed to allow a minority of MKR token holders to intervene against the wishes of a (potentially malicious) majority.

The Emergency Shutdown Module was designed with certain scenarios in mind, such as to prevent a malicious governance attack or to mitigate critical bugs.

## Key Parameter

### Minimum Threshold (`min`)

The minimum threshold parameter controls how much MKR must be deposited to the Emergency Shutdown Module before emergency shutdown may be triggered.

### Example

Suppose Governance has set the minimum threshold of MKR required to trigger emergency shutdown as 100,000 MKR. In that case, emergency shutdown cannot be initiated until at least 100,000 MKR has been deposited to the Emergency Shutdown Module. 

## Trade-offs

Suppose the minimum threshold parameter is set to too low a value. In that case, the Maker Protocol is potentially vulnerable to emergency shutdown being performed by an actor, or group of actors, in possession of enough MKR to perform an emergency shutdown. This vulnerability is particularly relevant when a large amount of MKR is available to borrow from DeFi protocols. Theoretically, a user could borrow enough MKR to trigger emergency shutdown and open shorts on MKR; in this scenario, the attacker would expect that the price of MKR would fall following emergency shutdown, allowing the attacker to close their loans for a profit without endangering their collateral too much.

Suppose the minimum threshold parameter is set too high. In that case, it becomes increasingly economically challenging to perform an emergency shutdown and may leave the protocol unable to respond to critical bugs or governance attacks. This difficulty is because MKR deposited to the Emergency Shutdown Module is not retrievable and should be considered burned by depositors. 

## Considerations

Triggering the Emergency Shutdown Module is not subject to the GSM Pause Delay.

Maker Governance can effectively turn off the Emergency Shutdown Module by removing its authorization to trigger an emergency shutdown. This can also be achieved by raising the minimum threshold to a value greater than the amount of MKR in circulation.

Delegate contracts are unable to interact with the Emergency Shutdown Module. Therefore, there is no risk of a delegate depositing their delegated MKR into the Emergency Shutdown Module.

If the protocol is restarted, Governance might choose to mint MKR to reward MKR holders depositing MKR into the Emergency Shutdown Module to encourage good-faith actors to act in a manner beneficial to the protocol. However, this is not guaranteed and requires a degree of trust in Governance of the restarted protocol.


>Page last reviewed: 31/08/2022
>Next review due: 31/08/2023

