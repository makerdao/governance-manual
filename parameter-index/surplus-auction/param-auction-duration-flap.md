
# Auction Duration (Flap)

>**Alias:** N/A  
>**Parameter Name:** `tau`  
>**Containing Contract:** `Flap`  
>**Scope:** System  
>**Technical Docs:** [link](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flap-detailed-documentation)  

## Description
The Auction Duration (Flap) parameter allows governance to control the maximum lifetime of a Surplus Auction. A Surplus Auction can end prior to this maximum duration if the Bid Duration timer expires without any additional bids.

Surplus Auctions are used to auction off excess DAI in fixed lots for a variable bid of MKR, which is then burned. In this process, keepers bid the amount of MKR they are willing to pay for a fixed DAI amount. 

### Example

`Bid Duration (Flap)` = 300 seconds  
`Auction Duration (Flap)` = 24 hours  

1. A Surplus Auction has been triggered and 3 hours pass with no bid.
2. Keeper A offers to give 10 MKR in exchange for 100 DAI at the 3-hour mark.
3. Keeper B has 300 seconds in which to offer a more attractive bid or else Keeper A will win the auction.
4. Keeper B offers to give 11 MKR in exchange for 100 DAI at 23 hours and 59 minutes into the auction.
5. Keeper A has 60 seconds in which to offer a more attractive bid or else Keeper B will win the auction.

## Purpose
The Auction Duration (Flap) parameter allows Maker Governance to adjust the maximum duration for surplus auctions in order to ensure robust keeper participation.

## Trade-offs
The Auction Duration (Flap) makes a trade-off between ensuring enough time for keepers to deploy their capital while limiting their market risk. A larger Auction Duration (Flap) gives keepers more time to participate in auctions. A smaller Auction Duration (Flap) means that keepers are less likely to be affected by negative price movements of the MKR Token during the auction process. Maximizing the number of participating bidders results in more efficient auctions and more MKR being burned. 

However, an Auction Duration (Flap) that is too large could result in a situation where there are many auctions happening simultaneously. If the Auction Duration (Flap) is too small, then keepers may not have sufficient time to organize their resources and place bids. Either of these situations could result in inefficient auctions that reduce the amount of MKR that can be burned.

## Changes
Adjusting the Auction Duration (Flap) parameter is a manual process that requires an executive vote. Changes to the Auction Duration (Flap) are subject to the GSM Pause Delay.

**Why increase this parameter?**
Maker Governance may wish to increase the Auction Duration (Flap) if too few keepers are participating in surplus auctions to encourage greater participation.

**Why decrease this parameter?**
Maker Governance may wish to decrease the Auction Duration (Flap) if the auctions are so long that keepers almost always make losses. Additionally, if there are too many overlapping auctions, it may be desirable to decrease this parameter.

## Considerations
Auction Duration (Flap) is always lower bounded by the Bid Duration (Flap) i.e. the time period before which a bid expires. If it is set lower than the Bid Duration (Flap), it will render that parameter unnecessary since the auction will end before a bid expires. 

For example, if Bid Duration (Flap) is 1 hour and Auction Duration (Flap) is 30 minutes, then the auction will only last 30 minutes, making the Bid Duration (Flap) irrelevant.

$eof1$
$eof2$
$eof3$
$eof4$