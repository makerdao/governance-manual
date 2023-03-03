# Bid Duration (Flap)

>**Alias:** N/A  
>**Parameter Name:** `ttl`  
>**Containing Contract:** `MCD_FLAP`  
>**Scope:** System  
>**Technical Docs:** [Flap Detailed Documentation](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flap-detailed-documentation)  

## Description

The Surplus Auction Bid Duration parameter allows governance to control how soon after a successful bid a Surplus Auction will end. Further bids reset this timer, extending the auction. A surplus auction can extend up to a maximum time which is set by the [Surplus Auction Duration](param-auction-duration-flap.md) parameter at which point the auction will end regardless of the Bid Duration timer.

Surplus auctions are used to auction off excess DAI in fixed lots for a variable bid of MKR, which is then burned. In this process, keepers bid on how much MKR they are willing to pay for a fixed amount of DAI. 

{% hint style="info" %} 

**Example**

_Surplus Bid Duration_ = 300 seconds  
_Surplus Auction Duration_ = 24 hours

1. A surplus auction is triggered and 3 hours pass with no bid.
2. Keeper A offers to give 10 MKR in exchange for 100 DAI at the 3-hour mark.
3. Keeper B has 300 seconds in which to offer a more attractive bid or else Keeper A will win the auction.
4. Keeper B offers to give 11 MKR in exchange for 100 DAI at 23 hours and 59 minutes into the auction.
5. Keeper A has 60 seconds to offer a more attractive bid or else Keeper B will win the auction.

{% endhint %}

## Purpose

Adjusting the Surplus Auction Bid Duration parameter allows Maker Governance to maximize the total MKR burned by ensuring sufficient competition among keepers.

## Trade-offs

When bidding, keepers take a risk that the MKR-DAI price will change negatively (for them) during the auction's duration. If this happens, they can lose money.

A small Surplus Auction Bid Duration lessens the risk that the market will move while the auction is in progress. Since the risk is lower, keepers can submit more aggressive bids which can result in more MKR being burned. However, if the Surplus Auction Bid Duration is too small, there may not be enough time for keepers to organize funds and participate in such auctions. In the extreme case, an auction with only one bidder will result in arbitrarily low MKR bids and a loss of value for the Maker Protocol.

A small Surplus Auction Bid Duration also increases the risk of a more severe loss of value in the case of blockchain congestion. Rising gas prices may lock out keepers either due to technical issues or due to the additional fixed cost of gas. 

A larger Surplus Auction Bid Duration gives keepers more time to participate in auctions, hopefully encouraging a higher number of bidders. However, if the Surplus Auction Bid Duration is too large, there may be bids for minimal amounts of MKR to safeguard against price volatility during the Surplus Auction Bid Duration period. Realistically priced bids would only appear when the auction end (determined by the [Surplus Auction Duration](param-auction-duration-flap.md)) is closer than the Surplus Auction Bid Duration period. In situations where the price of MKR is dropping, this would lead to less MKR being burned than with a smaller Surplus Auction Bid Duration.

## Changes

Adjusting the Surplus Auction Bid Duration parameter is a manual process that requires an executive vote. Changes to the Surplus Auction Bid Duration are subject to the [GSM Pause Delay](../core/param-gsm-pause-delay.md).

**Why increase this parameter?**
Maker Governance may wish to increase the Surplus Auction Bid Duration to encourage greater participation if they are concerned about blockchain congestion or if too few keepers are participating in surplus auctions.

**Why decrease this parameter?**
Maker Governance may wish to decrease the Surplus Auction Bid Duration if keepers are submitting low bids due to volatility in the price of MKR during the Surplus Bid Duration period.

## Considerations

Surplus Auction Bid Duration is always upper-bounded by the [Surplus Auction Duration](param-auction-duration-flap.md). If it is set higher than the total auction duration, it will have no effect. 

The [Debt Auction Bid Duration](../debt-auction/param-auction-duration-flop.md) parameter fulfills the same role as this parameter in Debt Auctions.


>Page last reviewed: 2022-11-18  
>Next review due: 2023-11-18  
