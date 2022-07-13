
# Auction Duration (Flop)

>**Alias:** N/A  
>**Parameter Name:** `tau`  
>**Containing Contract:** `Flop`  
>**Scope:** System  
>**Technical Docs:** [link](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flop-detailed-documentation)  

## Description
The Auction Duration (Flop) parameter allows governance to control the maximum lifetime of a Debt Auction. A Debt Auction can end prior to this maximum duration if the Bid Duration timer expires without any additional bids.

Debt Auctions are used to recapitalize the Maker Protocol by minting and auctioning off MKR for a fixed amount of DAI. In this process, Keepers bid the amount of MKR they are willing to accept for a fixed amount of DAI that they provide. 

### Example

`Bid Duration (Flop)` = 300 seconds  
`Auction Duration (Flop)` = 24 hours  

1. A Debt Auction has been triggered and 3 hours pass with no bid.
2. Keeper A offers to take 20 MKR in exchange for 100 DAI at the 3-hour mark.
3. Keeper B has 300 seconds in which to offer a more attractive bid or else Keeper A will win the auction.
4. Keeper B offers to take 19 MKR in exchange for 100 DAI at 23 hours and 59 minutes into the auction.
5. Keeper A has 60 seconds in which to offer a more attractive bid or else Keeper B will win the auction.

## Purpose
The Auction Duration (Flop) parameter allows Maker Governance to adjust the maximum duration for debt auctions in order to ensure robust keeper participation. It also helps to ensure a predictable time frame for the protocol to recover from an undercollateralized state. 

## Trade-offs
The Auction Duration (Flap) makes a trade-off between ensuring enough time for keepers to deploy their capital while limiting their market risk. A larger Auction Duration (Flop) gives keepers more time to participate in auctions. A smaller Auction Duration (Flop) means that keepers are less likely to be affected by negative price movements of the MKR Token during the auction process. Maximizing the number of participating bidders results in more efficient auctions and less MKR being minted.

However, an Auction Duration (Flop) that is too large could result in a situation where there are many auctions happening simultaneously. If the Auction Duration (Flop) is too small, then keepers may not have sufficient time to organize their resources and place bids. Either of these situations could result in inefficient auctions that increase the amount of MKR that is minted.

The parameter will also have an effect on how long it takes to recapitalize the Maker Protocol in the event that the protocol ends up with bad debt, which may be important depending on the severity of the situation.

## Changes
Adjusting the Auction Duration (Flop) parameter is a manual process that requires an executive vote. Changes to the Auction Duration (Flop) are subject to the GSM Pause Delay.

**Why increase this parameter?**
Maker Governance may wish to increase the Auction Duration (Flop) if too few keepers are participating in debt auctions to encourage greater participation.

**Why decrease this parameter?**
Maker Governance may wish to decrease the Auction Duration (Flop) if the auctions are so long that keepers almost always make losses. If there are too many overlapping auctions, it may be desirable to decrease this parameter.

## Considerations
Auction Duration (Flop) is always lower bounded by the Bid Duration (Flop) i.e. the time period before which a bid expires. If it is set lower than the Bid Duration (Flop), it will render that parameter unnecessary since the auction will end before a bid expires. 

### Example
`Bid Duration (Flop)` = 1 hour  
`Auction Duration (Flop)` = 30 minutes

The auction will only last 30 minutes, making the Bid Duration (Flop) irrelevant.

The Auction Duration (Flap) parameter fulfills the same role as this parameter in Surplus Auctions.

$eof$