
# Auction Duration (Flap)

```
Alias: 
Parameter Name: tau
Containing Contract: Flap
Scope: System
Technical Docs: https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flap-detailed-documentation 
```

## Description
During surplus auctions, excess DAI within the system is auctioned off in fixed lots for MKR. In this process, keepers bid on how much MKR they are willing to pay for a fixed Dai amount. MKR received this way is burned. 

Each auction has a lifetime determined by the `Auction Duration (Flap)` parameter or `tau`. The auction will end when the `Auction Duration (Flap)` has been reached OR `Bid Duration (Flap)` after the latest bid, whichever is earlier. 

For example, if `Auction Duration (Flap)` is set to 1 hour, all surplus auctions will end at most after 1 hour (but possibly earlier) and the highest MKR bid at this time will be successful.


## Purpose
The `Auction Duration (Flap)` parameter limits the maximum duration for auctions which is essential for keepers and also ensures a predictable time frame for MKR burning. 

Changing the `Auction Duration (Flap)` parameter allows Maker Governance to maximize the total MKR burned by ensuring sufficient time for keepers to make competitive bids and encouraging adequate keeper participation through fair auctions for keepers. 


## Trade-offs
The `Auction Duration (Flap)` makes a trade-off between ensuring enough time for keepers to organize funds and make competitive bids and encouraging keeper participation through fair auctions.

A larger `Auction Duration (Flap)` gives keepers more time to participate in auctions. A smaller `Auction Duration (Flap)` means that keepers are more likely to make profits through the auction process. Incentivizing keeper participation results in a higher number of bidders. This would result in more MKR being burned. 


If the `Auction Duration (Flap)` is too large, then auctions become almost always unprofitable for keepers. This is because as the price of MKR rises, new and higher bids will continue to come in until the price trend reverses and the price of MKR starts to fall. At this point, the current bid will become unprofitable but still win the auction when the `Bid Duration (Flap)` expires. Such a system would eventually discourage keeper participation. Moreover, a `Auction Duration (Flap)` that is too large could result in a situation where there are many auctions happening simultaneously. This would decrease the efficiency of a given auction and might result in lower amounts of MKR burned. 

If the `Auction Duration (Flap)` is too small, then keepers may not have sufficient time to organize their resources and place bids, resulting in insufficient competition and lower amounts MKR being burned.


## Changes
Adjusting the `Auction Duration (Flap)` parameter is a manual process that requires an executive vote. Changes to the `Auction Duration (Flap)` are subject to the GSM Pause Delay.

**Why increase this parameter?**
Maker Governance may wish to increase the `Auction Duration (Flap)` if too few keepers are participating in `Flap` auctions to encourage greater participation.

**Why decrease this parameter?**
Maker Governance may wish to decrease the `Auction Duration (Flap)` if the auctions are so long that keepers almost always make losses. Additionally, if there are too many overlapping auctions, it may be desirable to decrease this parameter.



## Considerations
`Auction Duration (Flap)` is always lower bounded by the `Bid Duration (Flap)` i.e. the time period before which a bid expires. If it is set lower than the `Bid Duration (Flap)`, it will render that parameter unnecessary since the auction will end before a bid expires. 

For example, if `Bid Duration (Flap)` is 1 hour and `Auction Duration (Flap)` is 30 minutes, then the auction will only last 30 minutes, making the `Bid Duration (Flap)` irrelevant.

