
# Auction Duration (Flap)

>**Alias:** N/A  
>**Parameter Name:** `tau`  
>**Containing Contract:** `MCD_FLAP`  
>**Scope:** System  
>**Technical Docs:** [Flap Detailed Documentation](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flap-detailed-documentation)  

## Description

The Surplus Auction Duration parameter allows governance to control the maximum lifetime of a Surplus Auction. A surplus auction can end before this maximum duration is reached if the Bid Duration timer expires without any additional bids.

Surplus auctions are used to auction off excess DAI in fixed lots for a variable bid of MKR, which is then burned. In this process, keepers bid the amount of MKR they are willing to pay for a fixed amount of DAI. 

### Example

_Surplus Bid Duration = 300 seconds_  
_Surplus Auction Duration = 24 hours_  

1. A surplus auction has been triggered and 3 hours pass with no bid.
2. Keeper A offers to give 10 MKR in exchange for 100 DAI at the 3-hour mark.
3. Keeper B has 300 seconds in which to offer a more attractive bid or else Keeper A will win the auction.
4. Keeper B offers to give 11 MKR in exchange for 100 DAI at 23 hours and 59 minutes into the auction.
5. Keeper A has 60 seconds to offer a more attractive bid or else Keeper B will win the auction.

## Purpose

The Surplus Auction Duration parameter allows Maker Governance to adjust the maximum duration for surplus auctions in order to ensure robust keeper participation.

## Trade-offs

The Surplus Auction Duration makes a trade-off between ensuring enough time for keepers to deploy their capital while limiting their market risk. A larger Surplus Auction Duration gives keepers more time to participate in auctions. A smaller Surplus Auction Duration means that keepers are less likely to be affected by negative price movements of the MKR token during the auction process. Maximizing the number of participating bidders results in more efficient auctions and more MKR being burned. 

However, too large a Surplus Auction Duration could result in a situation where there are many auctions happening simultaneously. On the other hand, if the Surplus Auction Duration is too small, then keepers may not have sufficient time to organize their resources and place bids. Either of these situations could result in inefficient auctions that reduce the amount of MKR burned.

## Changes

Adjusting the Surplus Auction Duration parameter is a manual process that requires an executive vote. Changes to the Surplus Auction Duration are subject to the [GSM Pause Delay](../core/param-gsm-pause-delay.md).

**Why increase this parameter?**
Maker Governance may wish to increase the Surplus Auction Duration to encourage greater participation if too few keepers are participating in surplus auctions.

**Why decrease this parameter?**
Maker Governance may wish to decrease the Surplus Auction Duration if the auctions are so long that keepers almost always make losses. Additionally, if there are too many overlapping auctions, it may be desirable to decrease this parameter.

## Considerations

Surplus Auction Duration is always lower-bounded by the [Surplus Auction Bid Duration](param-bid-duration-flap.md), i.e., the time period that must pass before the latest successful bid wins the auction. If it is set lower than the Surplus Auction Bid Duration, it will render that parameter unnecessary since the auction will end before a bid expires. 

For example, if Surplus Auction Bid Duration is 1 hour and Surplus Auction Duration is 30 minutes, then the auction will only last 30 minutes, making the Surplus Auction Bid Duration irrelevant.

>Page last reviewed: 2022-11-18  
>Next review due: 2022-11-18  


