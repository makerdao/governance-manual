# Surplus Auction Minimum Bid Increase

>**Alias:** N/A  
>**Parameter Name:** `beg`  
>**Containing Contract:** `MCD_FLAP`  
>**Scope:** System  
>**Technical Docs:** [Flapper Detailed Documentation](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flap-detailed-documentation)  


## Description
During surplus auctions, excess DAI within the system is auctioned off in fixed lots for MKR. In this process, keepers bid increasing amounts of MKR for a fixed amount of DAI. MKR received this way is burned by the Maker Protocol. 

New MKR bids must be higher than the current MKR bid by at least an amount determined by the Surplus Auction Minimum Bid Increase or `beg`.  The Surplus Auction Minimum Bid Increase is given in terms of a minimum percentage increase on the current bid.

In practice the Surplus Auction Minimum Bid Increase represents both:
* The maximum profit that keepers can make when bidding in Surplus Auctions. 
* The maximum slippage MakerDAO is willing to accept during auctions to ensure sufficient keeper participation. 

{% hint style="info" %} 

**Example**

_Surplus Auction Minimum Bid Increase_ = 5%  
_Surplus Auction Lot Size_ = 1,000 DAI

1. A DAI Surplus Auction is triggered, accepting bids of MKR in exchange for 1,000 DAI.
2. Keeper A bids to pay 10 MKR in exchange for 1,000 DAI.
3. Keeper B must bid at least 10.5 MKR in exchange for the 1,000 DAI, a 5% increase.

{% endhint %}

## Purpose
The Surplus Auction Minimum Bid Increase parameter allows Maker Governance to ensure that keepers are sufficiently incentivized to bid in surplus auctions.

## Trade-offs
A small Surplus Auction Minimum Bid Increase helps to increase the amount of MKR burned as bids will be closer to the market value of MKR. However, if it is too small, it can result in low keeper participation due to lack of perceived profit. If only a single keeper participates in an auction it can lead to significant losses for the Maker Protocol.

A large Surplus Auction Minimum Bid Increase ensures high keeper participation as there is an opportunity for a larger profit. It also helps to balance other costs to the keeper when making a bid, such as the effect of the price volatility of MKR over the duration of the auction, and the cost of gas when making a bid.

## Changes
Adjusting the Surplus Auction Minimum Bid Increase parameter is a manual process that requires an executive vote. Changes to the Surplus Auction Minimum Bid Increase are subject to the [GSM Pause Delay](../core/param-gsm-pause-delay.md).

**Why increase this parameter?**

This parameter should be increased to increase keeper participation in surplus auctions.

**Why decrease this parameter?**

This parameter should be decreased to increase auction efficiency i.e. winning bid price vs. market price of MKR.

## Considerations
The gas cost to `kick` (trigger) a surplus auction is non-trivial. If the Surplus Auction Minimum Bid Increase is too small, surplus auctions may not be triggered by any keeper because they are required to accept a fixed cost for an uncertain return.

>Page last reviewed: 2022-11-09  
>Next review due: 2023-11-09  

