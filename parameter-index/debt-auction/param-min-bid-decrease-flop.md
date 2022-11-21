
# Min Bid Decrease (Flop)

>**Alias:** Minimum Bid Decrease  
>**Parameter Name:** `beg`  
>**Containing Contract:** `MCD_FLOP`  
>**Scope:** System  
>**Technical Docs:** [Flop Detailed Documentation](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flop-detailed-documentation)  

## Description

Debt auctions are used to recapitalize the system by minting and auctioning off MKR for a fixed amount of Dai. In this process, keepers bid a reducing amount of MKR they are willing to accept for the fixed amount of DAI they have to pay at auction settlement. 

During debt auctions, new MKR bids must be lower than the current MKR bid by at least an amount determined by the Debt Auction Min Bid Decrease (`beg`). The Debt Auction Min Bid Decrease is given in terms of a minimum percentage decrease on the current bid.

In practice the Debt Auction Min Bid Decrease represents both:
* The maximum profit that keepers can make when bidding in Debt Auctions. 
* The maximum slippage MakerDAO is willing to accept during auctions to ensure sufficient keeper participation. 

## Example

_Debt Auction Min Bid Decrease = 5%_ 

If the current bid is 10 MKR for 1000 Dai, the next bid must be at most 9.5 MKR for 1000 Dai, a 5% decrease.

## Purpose

The Debt Auction Bid Decrease parameter allows Maker Governance to ensure that keepers are sufficiently incentivized to bid in debt auctions.

## Trade-offs

A small Debt Auction Min Bid Decrease helps to reduce the amount of MKR minted in a debt auction as bids will be closer to the market value of MKR. However, if it is too low it can result in low keeper participation due to lack of perceived profit. If only a single keeper participates in an auction it can lead to significant losses for the Maker Protocol, and potentially Dai Holders.

A large Debt Auction Min Bid Decrease ensures high keeper participation as there is an opportunity for a larger profit. It also helps to balance other costs to the keeper when making a bid, such as the effect of the price volatility of MKR over the duration of the auction, and the cost of gas when making a bid.

## Changes

Adjusting the Debt Auction Min Bid Decrease parameter is a manual process that requires an executive vote. Changes to the Debt Auction Min Bid Decrease are subject to the [GSM Pause Delay](../core/param-gsm-pause-delay.md).

**Why increase this parameter?**
This parameter should be increased to increase keeper participation in Debt Auctions.

**Why decrease this parameter?**
This parameter should be decreased to increase auction efficiency, i.e., winning bid price vs. market price of MKR.

## Considerations

The gas cost to `kick` (trigger) a debt auction is non-trivial. If the Debt Auction Min Bid Decrease is too low, debt auctions may not be triggered by any keeper because they are required to accept a fixed cost for an uncertain return.

"Front-running" may be an issue in debt auctions.

>Page last reviewed: 2022-11-14  
>Next review due: 2023-11-14  



