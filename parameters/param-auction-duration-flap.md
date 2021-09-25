
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


## Purpose
Changing the `Auction Duration (Flap)` parameter allows Maker Governance to maximize the total MKR burned by ensuring sufficient time for keepers to make competitive bids and encouraging adequate keeper participation through fair auctions for keepers. 


## Trade-offs
The `Auction Duration (Flap)` makes a tradeoff between ensuring enough time for keepers to organize funds and make competitive bids and encouraging keeper participation through fair auctions.

A larger `Auction Duration (Flap)` gives keepers more time to participate in auctions, hopefully encouraging a higher number of bidders. This would result in more MKR being burned.


If the `Auction Duration (Flap)` is too large, then auctions become almost always unprofitable for keepers. This is because as the price of MKR rises, new and higher bids will continue to come in until the price trend reverses and the price of MKR starts to fall. At this point, the current bid will become unprofitable but still win the auction when the `Bid Duration (Flap)` expires. Such a system would eventually discourage keeper participation.


## Changes
Adjusting the `Auction Duration (Flap)` parameter is a manual process that requires an executive vote. Changes to the `Auction Duration (Flap)` are subject to the GSM Pause Delay.

**Why increase this parameter?**
Maker Governance may wish to increase the `Auction Duration (Flap)` if too few keepers are participating in `flop` auctions to encourage greater participation.

**Why decrease this parameter?**
Maker Governance may wish to decrease the `Auction Duration (Flap)` if the auctions are so long that keepers almost always make losses.



## Considerations
`Auction Duration (Flop)` is always lower bounded by the `Bid Duration (Flop)` i.e. the time period before which a bid expires. If it is set lower than the `Bid Duration (Flop)`, it will render that parameter unnecessary since the auction will end before a bid expires. 

