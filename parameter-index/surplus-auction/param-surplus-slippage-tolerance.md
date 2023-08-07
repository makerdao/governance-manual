# Smart Burn Engine Slippage Tolerance

>**Alias:** N/A  
>**Parameter Name:** `want`  
>**Containing contract:** `MCD_FLAP`  
>**Scope:** System  
>**Technical Docs:** N/A  

## Description
The Smart Burn Engine Slipppage Tolerance or `want` parameter controls the amount of deviation between the oracle price of MKR and the price obtained by the Smart Burn Engine. It is one of the parameters that defined whether or not the Smart Burn Engine can be triggered.

The Smart Burn Engine can be triggered when:  

_Surplus DAI > [Maximum System Surplus](../core/param-system-surplus-buffer.md) (`hump`) + Smart Burn Engine Slipppage Tolerance (`want`)_

{% hint style="info" %} 

**Example**

_Maximum System Surplus_ = 50 million DAI   
_Smart Burn Engine Lot Size_ = 10,000 DAI  
_Smart Burn Engine Slippage Tolerance_ = 2%

1. The current System Surplus reaches 50 million DAI.
2. Keeper A attempts to trigger the Smart Burn Engine, but the transaction fails.
3. The current System Surplus reaches 50,010,000 DAI.
4. Keeper A successfully triggers the Smart Burn Engine and exchanges 10,000 DAI for MKR as long as the price of MKR is at minimum within 2% of the oracle price.

{% endhint %}

## Purpose

The Smart Burn Engine Slipppage Tolerance parameter allows Maker Governance to tune the frequency and accessibility of Smart Burn Engine actions in order to achieve better efficiency.

## Trade-offs

Increasing the Smart Burn Engine Slipppage Tolerance will allow greater slippage when the Smart Burn Engine is activated - this increases the probability of trades executing, but also increases the risk the purchases being frontrun and/or sandwiched and could potentially lead to a poor deal for the Protocol.

Reducing the Smart Burn Engine Slipppage Tolerance will reduce the allowed slippage. This means that the price of purchases will be closer to the oracle price, but it may also result in purchases not happening if the Uniswap price deviates from the oracle price too much. If the `want` is very small, it would be possible to prevent the Smart Burn Engine from making purchases by deliberately moving the price of the pool out of the range of the Smart Burn Engine Slippage Tolerance.

## Changes
Adjusting the Smart Burn Engine Slipppage Tolerance parameter is a manual process that requires an executive vote. Changes to the Smart Burn Engine Slipppage Tolerance are subject to the [GSM Pause Delay](../core/param-gsm-pause-delay.md).

In general the goal when tweaking this parameter is to trade-off of making sure that there is a steady stream of purchases of MKR against the risks of sandwich attacks against the Smart Burn Engine resulting in less efficient purchases.

**Why increase this parameter?**

The main reason for Maker Governance to increase the Smart Burn Engine Slipppage Tolerance is if it is too restrictive and preventing purchases from happening.

**Why decrease this parameter?**

The main reason for Maker Governance to decrease the Smart Burn Engine Slipppage Tolerance is if there is an excessive amount of sandwiching happening. If the parameter is set too high, MEV bots and other participants will be able to abuse the Smart Burn Engine to make risk-free profit at the detriment of the Maker Protocol.
 
 ## Considerations
 
As triggering the Smart Burn Engine is permissionless, incorrectly setting the Smart Burn Engine Slipppage Tolerance may expose the Protocol to sandwich attacks.

The Smart Burn Engine Slippage Tolerance only applies when the price of MKR in the Uniswap pool is *worse* than the oracle price. It will not prevent purchases when the pool price is > `want`% *better* than the oracle price.

>Page last reviewed: 2023-08-01  
>Next review due: 2024-08-01  

