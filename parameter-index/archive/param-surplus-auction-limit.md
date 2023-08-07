# Surplus Auction Limit   

>**Alias:** N/A  
>**Parameter Name:** `lid`  
>**Containing Contract:** `MCD_FLAP`  
>**Scope:** System  
>**Technical Docs:** [Flapper Detailed Documentation](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flap-detailed-documentation)  


## Description
During surplus auctions, excess DAI within the system is auctioned off in fixed lots for MKR. In this process, keepers bid on how much MKR they are willing to pay for a fixed amount of DAI. MKR received this way is burned. 

To avoid flooding the system with too many simultaneous auctions, the maximum amount of DAI that can be auctioned at any given point in time is limited. The parameter that sets this limit is the Surplus Auction Limit or `lid` parameter.

{% hint style="info" %} 

**Example**

_Surplus Auction Limit_ = 30,000 DAI  
_Surplus Auction Lot Size_ = 10,000 DAI

1. Three DAI Surplus Auctions (A, B and C) are triggered, accepting bids of MKR in exchange for 10,000 DAI.
2. The amount of DAI in Surplus Auction now equals the Surplus Auction Limit.
3. Keeper A attempts to start Surplus Auction D, but the transaction fails.
3. Surplus Auction A concludes, and the amount of DAI in Surplus Auction now equals 20,000 DAI.
4. Keeper A may now start Surplus Auction D.

{% endhint %}

## Purpose
Changing the Surplus Auction Limit allows Maker Governance to strike a reasonable tradeoff between efficient auctions and the rate at which protocol profits are directed towards burning MKR. 


## Trade-offs

A small Surplus Auction Limit restricts the number of simultaneous flap auctions to a small number. This decreases the probability of there being auctions with insufficient participants. When auctions have enough participants, there is a low probability of winning MKR bids being significantly below market price. 

However, if the Surplus Auction Limit is too low and the protocol is making a large amount of profit on average, this may result in excess DAI remaining in the surplus buffer instead of being used to burn MKR.


A large Surplus Auction Limit allows for more parallel surplus auctions. This increases the potential rate at which protocol profits can be used to burn MKR. If the protocol profits are high on average, then more parallel auctions are also needed to occur to buy back and burn MKR at a fast enough rate. Finally, under certain specific scenarios where the protocol makes large profits and MKR price is simultaneously low (such as liquidations due to a market crash), a large Surplus Auction Limit could result in more MKR being burned. 

On the other hand, if the Surplus Auction Limit is too large, it can lead to highly inefficient auctions due to too many auctions. In particular, past examples such as [Flappy Friday](https://forum.makerdao.com/t/flappy-friday-clip-and-flap-analysis/12790) have shown that too many simultaneous flap auctions can result in zero MKR bids winning the auction due to a lack of competition.



## Changes
Adjusting the Surplus Auction Limit is a manual process that requires an executive vote. Changes to the Surplus Auction Limit are subject to the [GSM Pause Delay](../core/param-gsm-pause-delay.md).

**Why increase this parameter?**
This parameter should be increased to increase the number of potential parallel auctions. This could be when the average protocol profits are high enough that more parallel auctions are necessary.


**Why decrease this parameter?**
This parameter should be decreased to avoid too many simultaneous auctions resulting in uncompetitive MKR bids.



## Considerations
The Surplus Auction Limit should be at least as high as the `lot` amount for a single auction. Otherwise, no auctions will take place.

If the amount of Dai on auction (`fill`) is less than the Surplus Auction Limit, then a new auction can be started even if that puts the total DAI on auction above the Surplus Auction Limit. At that point, no further auctions can be started. In other words, the maximum Dai on auction can be almost one `lot` higher than the Surplus Auction Limit.

>Page last reviewed: 2022-11-09  
>Next review due: 2023-11-09  

