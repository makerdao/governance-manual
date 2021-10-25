
# Auction Duration (Flop)

```
Alias: 
Parameter Name: tau
Containing Contract: Flop
Scope: System
Technical Docs: https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flop-detailed-documentation 
```

## Description
Debt Auctions are used to recapitalize the system by minting and auctioning off MKR for a fixed amount of DAI. In this process, keepers bid on how little MKR they are willing to accept for the fixed Dai amount they have to pay at auction settlement. Each auction has a maximum lifetime from the moment it is kicked and that lifetime is determined by the `Auction Duration (Flop)` parameter or `tau`. The auction will end when the Auction Duration (`tau`) has been reached OR `Bid Duration (Flop)` after the latest bid, whichever is earlier. 

For example, if `Auction Duration (Flop)` is set to 1 hour, all surplus auctions will end at most after 1 hour (but possibly earlier) and the lowest MKR bid at this time will be successful.


## Purpose
The `Auction Duration (Flop)` parameter limits the maximum duration for auctions which is essential for keepers and ensures a predictable time frame for the protocol to recover from an undercollateralized state. 

Changing the `Auction Duration (Flop)` parameter allows Maker Governance to minimize the total MKR minted by ensuring sufficient time for keepers to bid as well, ensuring fair auctions for keepers and that the protocol recovers from an undercollateralized state quickly. 


## Trade-offs
The `Auction Duration (Flop)` makes a trade-off between ensuring enough time for keepers to organize funds and make competitive bids and encouraging keeper participation through fair auctions as well as minimizing the time for which the protocol holds bad debt.

A larger `Auction Duration (Flop)` gives keepers more time to participate in auctions. A smaller `Auction Duration (Flop)` means that keepers are more likely to make profits through the auction process. Incentivizing keeper participation results in a higher number of bidders. This would result in less MKR being minted. 


If the `Auction Duration (Flop)` is too large, then auctions become almost always unprofitable for keepers. This is because as the price of MKR falls, new and lower bids will continue to come in until the price trend reverses and the price of MKR starts to rise. At this point, the current bid will become unprofitable but still win the auction when the `Bid Duration (Flop)` expires. Such a system would eventually discourage keeper participation.

Additionally, if the `Auction Duration (Flop)` is too large, the protocol holds bad debt during this time which could mean that DAI is not fully backed by collateral.

If the `Auction Duration (Flop)` is too small, then keepers may not have sufficient time to organize their resources and place bids, resulting in insufficient competition and larger amounts MKR being minted.



## Changes
Adjusting the `Auction Duration (Flop)` parameter is a manual process that requires an executive vote. Changes to the `Auction Duration (Flop)` are subject to the GSM Pause Delay.

**Why increase this parameter?**
Maker Governance may wish to increase the `Auction Duration (Flop)` if too few keepers are participating in `Flop` auctions to encourage greater participation.

**Why decrease this parameter?**
Maker Governance may wish to decrease the `Auction Duration (Flop)` if the auctions are so long that keepers almost always make losses. If there are too many overlapping auctions, it may be desirable to decrease this parameter. Finally, the parameter must be below the time for which the protocol is willing to hold bad debt.



## Considerations
`Auction Duration (Flop)` is always lower bounded by the `Bid Duration (Flop)` i.e. the time period before which a bid expires. If it is set lower than the `Bid Duration (Flop)`, it will render that parameter unnecessary since the auction will end before a bid expires. 

For example, if `Bid Duration (Flop)` is 1 hour and `Auction Duration (Flop)` is 30 minutes, then the auction will only last 30 minutes, making the `Bid Duration (Flop)` irrelevant.

