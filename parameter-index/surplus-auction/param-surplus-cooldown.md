# Smart Burn Engine Cooldown

>**Alias:** N/A  
>**Parameter Name:** `hop`  
>**Containing contract:** `MCD_FLAP`  
>**Scope:** System  
>**Technical Docs:** N/A  

## Description
The Smart Burn Engine Cooldown or `hop` parameter controls the amount of time that must elapse between activations of the Smart Burn Engine. It is defined in seconds.

The Smart Burn Engine can be triggered when:  

_Time elapsed since last activation > Smart Burn Engine Cooldown_

{% hint style="info" %} 

**Example**

_Last Activation_ = -90 seconds   
_Smart Burn Engine Cooldown_ = 100 seconds  

1. Keeper A attempts to trigger the Smart Burn Engine, but the transaction fails.
2. A further 10 seconds pass.
3. Keeper A may now succesfully trigger the Smart Burn Engine

{% endhint %}

## Purpose

The Smart Burn Engine Cooldown parameter allows Maker Governance to tune the frequency of Smart Burn Engine actions in order to achieve better efficiency.

## Trade-offs

Increasing the Smart Burn Engine Cooldown will increase the frequency of Smart Burn Engine purchases. This can be useful in low liquidity situations when paired with a smaller lot size. If this is being done by the Keeper Network, this will lead to increased gas costs for Maker as they funding the gas for each transaction.

Reducing the Smart Burn Engine Cooldown will decrease the frequency of Smart Burn Engine purchases. This can allow for lower gas expenditure but will usually need higher lot sizes, leading to higher gas expenses.

## Changes
Adjusting the Smart Burn Engine Cooldown parameter is a manual process that requires an executive vote. Changes to the Smart Burn Engine Slipppage Tolerance are subject to the [GSM Pause Delay](../core/param-gsm-pause-delay.md).

In general the goal when tweaking this parameter is partner changes to the Smart Burn Engine Lot Size to balance the frequency and size of Smart Burn Engine purchases to hit the target purchase rate defined in the [Stability Scope](https://mips.makerdao.com/mips/details/MIP104#9-surplus-buffer-and-smart-burn-engine).

**Why increase this parameter?**

The main reason for Maker Governance to increase the Smart Burn Engine Cooldown is to balance increases in the Smart Burn Engine Lot Size, leading to bigger purchases happening less frequently.

**Why decrease this parameter?**

The main reason for Maker Governance to decrease the Smart Burn Engine Cooldown is to balance reductions in the Smart Burn Engine Lot Size, leading to smaller purchases happening more frequently.
 
 ## Considerations
 
As triggering the Smart Burn Engine is permissionless, incorrectly setting the Smart Burn Engine Cooldown may lead to more or less Dai being spent to purchase MKR, depending on whether the Smart Burn Engine Cooldown was set too high or too low.

>Page last reviewed: 2023-08-07  
>Next review due: 2024-08-07