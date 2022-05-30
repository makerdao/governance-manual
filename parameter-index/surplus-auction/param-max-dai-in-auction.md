
# Maximum DAI in auction   

>Alias:   
>Parameter Name: lid  
>Containing Contract: Flap  
>Scope: System  
>Technical Docs:   


## Description
During surplus auctions, excess DAI within the system is auctioned off in fixed lots for MKR. In this process, keepers bid on how much MKR they are willing to pay for a fixed Dai amount. MKR received this way is burned. 

To avoid flooding the system with too many simultaneous auctions, the maximum amount of DAI that can be auctioned at any given point of time is limited. The parameter that sets this limit is the `Max DAI in auction` or `lid` parameter.

For example, if the `Max DAI in auction` is set to 30,000, then there can be at most 30,000 DAI being auctioned for MKR at any point of time.


## Purpose
Changing the `Max DAI in auction` parameter allows Maker Governance to strike a reasonable tradeoff between efficient auctions and the rate at which protocol profits are directed towards burning MKR. 


## Trade-offs

A small `Max DAI in auction` parameter limits the number of simultaneous flap auctions to a small number. This decreases the probability of there being auctions with insufficient participants. When auctions have enough participants, there is a low probability of winning MKR bids being significantly below market price.


A large `Max DAI in auction` parameter allows for more parallel surplus auctions. This increases the potential rate at which protocol profits can be used to burn MKR. If the protocol profits are high on average, then more parallel auctions are also needed to occur to buyback and burn MKR at a fast enough rate. Finally, under certain specific scenarios where the protocol makes large profits and MKR price is simultaneously low (such as liquidations due to a market crash), a large `Max DAI in auction` parameter could result in more MKR being burned. 



## Changes
Adjusting the `Max DAI in auction` parameter is a manual process that requires an executive vote. Changes to the `Max DAI in auction` parameter are subject to the GSM Pause Delay.

**Why increase this parameter?**
This parameter should be increased to increase the number of potential parallel auctions. This could be when the average protocol profits are high enough that more parallel auctions are necessary.


**Why decrease this parameter?**
This parameter should be decreased to avoid too many simultaneous auctions resulting in uncompetitive MKR bids.



## Considerations
The `Max DAI in auction` parameter should be at least as high as the `lot` amount for a single auction. Otherwise, no auctions will take place.

Changing this parameter only has an effect if it increases/decreases from one integer multiple of the `lot` to another. For example, if the `lot` is 30,000 DAI, setting the `Max DAI in auction` to 45,000 DAI would have the same effect as setting it to 30,000 DAI.

