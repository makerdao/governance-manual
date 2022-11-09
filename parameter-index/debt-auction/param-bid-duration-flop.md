# Bid Duration (Flop)

>**Alias:** N/A  
>**Parameter Name:** `ttl`  
>**Containing Contract:** `MCD.FLOP`  
>**Scope:** System  
>**Technical Docs:** [Flop Detailed Documentation](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flop-detailed-documentation)  

## Description

The Debt Auction (Flop) Bid Duration parameter (`ttl`) allows governance to control how soon after a successful bid a Debt Auction will end. Further bids reset this timer, extending the auction. A debt auction can extend up to a maximum time which is set by the Flop Duration parameter, at which point the auction will end regardless of the Bid Duration timer.

Debt Auctions are used to recapitalize the system by minting and auctioning off MKR for a fixed amount of Dai. In this process, Keepers bid on how little MKR they are willing to accept for a fixed amount of Dai that they provide. 

### Example

```text
Flop Bid Duration = 300 seconds  
Flop Auction Duration = 24 hours  
```

1. A Debt Auction has been triggered and 3 hours pass with no bid.
2. Keeper A offers to take 20 MKR in exchange for 100 DAI at the 3-hour mark.
3. Keeper B has 300 seconds in which to offer a more attractive bid or else Keeper A will win the auction.
4. Keeper B offers to take 19 MKR in exchange for 100 DAI at 23 hours and 59 minutes into the auction.
5. Keeper A has 60 seconds in which to offer a more attractive bid or else Keeper B will win the auction.

## Purpose

Adjusting the Flop Bid Duration parameter allows Maker Governance to minimize the total MKR minted by ensuring sufficient competition among Keepers.

## Trade-offs

When bidding, Keepers take a risk that the MKR-DAI price will change negatively (for them) during the auction's duration; if this happens, they can lose money.

A Flop Bid Duration that is small means that Keepers take less risk that the market will move while the auction is in progress. Since the risk is lower, keepers can submit more aggressive bids which can result in less MKR being minted. However, if the Flop Bid Duration is too small, there may not be enough time for keepers to organize funds and participate in such auctions. In the extreme, an auction with only one bidder will result in arbitrarily high MKR bids and a loss of value for the Maker Protocol.

A small Flop Bid Duration also increases the risk of a more severe loss of value in the case of blockchain congestion: Rising gas prices may lock out keepers either due to technical issues or due to the additional fixed cost of gas. 

A larger Flop Bid Duration gives keepers more time to participate in auctions, hopefully encouraging a higher number of bidders. If the Flop Bid Duration is too large, there may be bids for very high amounts of MKR to safeguard against price volatility during the Flop Bid Duration period. Realistically priced bids would only appear when the auction end (determined by Auction Duration) is closer than the Flop Bid Duration period. In situations where the price of MKR is dropping, this would lead to more MKR being minted than with a smaller Flop Bid Duration.

## Changes

Adjusting the Flop Bid Duration parameter is a manual process that requires an executive vote. Changes to the Flop Bid Duration are subject to the [GSM Pause Delay](../core/param-gsm-pause-delay.md).

**Why increase this parameter?**

Maker Governance may wish to increase the Flop Bid Duration if too few keepers are participating in debt auctions to encourage greater participation or if they are concerned about blockchain congestion.

**Why decrease this parameter?**

Maker Governance may wish to decrease the Flop Bid Duration if keepers are submitting high bids due to volatility in the price of MKR during the Flop Bid Duration period.

## Considerations

Flop Bid Duration is always upper-bounded by the total auction duration. If it is set higher than the total auction duration, then it will have no effect. 

### Example

```text
Flop Bid Duration = 1 hour  
Flop Auction Duration = 30 minutes
```

The auction will only last 30 minutes, making the Flop Bid Duration irrelevant.

The Flap Bid Duration parameter fulfills the same role as this parameter in Surplus Auctions.

_Historic Note: A similar auction system was initially used for collateral auctions as well; it was replaced by a dutch auction system._

>Page last reviewed: 2022-09-11  
>Next review due: 2023-09-11  


