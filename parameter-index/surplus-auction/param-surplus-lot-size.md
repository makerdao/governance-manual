# Smart Burn Engine Lot Size

>**Alias:** N/A  
>**Parameter Name:** `bump`  
>**Containing contract:** `MCD_VOW`  
>**Scope:** System  
>**Technical Docs:** [Vow Detailed Documentation](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/vow-detailed-documentation)  

## Description
The Smart Burn Engine Lot Size or `bump` parameter controls the amount of DAI that is exchanged for MKR each time the Smart Burn Engine is triggered.

The Smart Burn Engine can be triggered when:  

_Surplus DAI > [Maximum System Surplus](../core/param-system-surplus-buffer) (`hump`) + Smart Burn Engine Lot Size (`bump`)_

{% hint style="info" %} 

**Example**

_Maximum System Surplus_ = 50 million DAI   
_Smart Burn Engine Lot Size_ = 10,000 DAI  

1. The current System Surplus reaches 50 million DAI.
2. Keeper A attempts to trigger the Smart Burn Engine, but the transaction fails.
3. The current System Surplus reaches 50,010,000 DAI.
4. Keeper A successfully triggers the Smart Burn Engine and exchanges 10,000 DAI for MKR.

{% endhint %}

## Purpose

The Smart Burn Engine Lot Size parameter allows Maker Governance to tune the frequency and accessibility of Smart Burn Engine actions in order to achieve better efficiency.

## Trade-offs

Increasing the Smart Burn Engine Lot Size will result in fewer auctions - leading to less overall gas expenditure. However, a larger Smart Burn Engine Lot Size may mean there is insufficient liquidity for the Smart Burn Engine to complete its planned actions.

Reducing the Smart Burn Engine Lot Size will result in a greater number of auctions. These events will occur more frequently. However, a higher number of events leads to a higher fixed cost as the protocol funds the Keeper Network that will reliably call these events.

## Changes
Adjusting the Smart Burn Engine Lot Size parameter is a manual process that requires an executive vote. Changes to the Smart Burn Engine Lot Size are subject to the [GSM Pause Delay](../core/param-gsm-pause-delay.md).

In general the goal when tweaking this parameter is to trade-off costs of running keepers against the liquidity available in the pool and the risk of sandwich attacks.

**Why increase this parameter?**

The main reason for Maker Governance to increase the Smart Burn Engine Lot Size is to reduce the overall number of actions. Fewer auctions reduces the gas cost for keepers as there are fewer transactions taking place. Since Maker funds the Keeper Network, this saves the protocol money in the long-term as there is less gas to subsidise.

**Why decrease this parameter?**

The main reason for Maker Governance to decrease the Smart Burn Engine Lot Size is if there is to reduce the required liquidity for each action. If the parameter is set too high, the slippage will be too high and the auction will not proceed.
 
 ## Considerations
 
The Smart Burn Engine Lot Size must be greater than 0 DAI.

As triggering the Smart Burn Engine is permissionless, incorrectly setting the Smart Burn Engine Lot Size may expose the Protocol to sandwich attacks.

>Page last reviewed: 2023-08-01  
>Next review due: 2024-08-01  

