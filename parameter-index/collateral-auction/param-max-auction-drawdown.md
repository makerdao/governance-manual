# Max Auction Drawdown

>**Alias:**  Max Auction Drawdown
>**Parameter Name:** `cusp`  
>**Containing Contract:** `MCD_CLIP_$ILK`  
>**Scope:** Vault Type (Ilk)  
>**Technical Docs:** [Liquidations 2.0](https://docs.makerdao.com/smart-contract-modules/dog-and-clipper-detailed-documentation)  

## Description

The Max Auction Drawdown is the maximum percentage drop in collateral price during a collateral auction before the auction is reset. 'Collateral price' in this context refers to the collateral _auction price_ rather than the collateral _market price._ Collateral auctions use a falling price auction, where the price starts high and decreases according to the [Auction Price Function](param-auction-price-function.md) until it has dropped by the Max Auction Drawdown percentage parameter.

If a collateral auction starts at a collateral price of $100, and the Max Auction Drawdown is set to 70%, the auction will be reset if the auction collateral price reaches $30.

The Max Auction Drawdown parameter overlaps with the [Max Auction Duration](param-max-auction-duration.md) parameter in that an auction will need to be reset once either maximum is exceeded.

## Purpose

This parameter primarily exists to prevent collateral auctions from continuing past the point of sanity and auctioning off collateral at far below market price in the event of an unforeseen issue that prevents bids. It is redundant with the Max Auction Duration parameter and allows Maker Governance to decide whether to set the lowest price directly or implicitly via the Auction Price Function and Max Auction Duration parameters.

## Trade-offs

Setting this parameter too low may result in collateral auctions selling collateral for below market price in the event of unforeseen disruptions that prevent bids.

On the other hand, setting this parameter too high may delay successful auction resolution due to the auction being reset too frequently. Frequent resets also result in the protocol paying out additional kick incentives (both [proportional](param-proportional-kick-incentive.md) and [flat](param-flat-kick-incentive.md)).

## Changes

Adjusting a Max Auction Drawdown parameter for a specific vault type is a manual process that requires an executive vote. Changes to Max Auction Drawdown parameters are subject to the [GSM Pause Delay](../core/param-gsm-pause-delay.md).

## Considerations

Max Auction Drawdown is based on the starting auction price (`top`), which is equal to the OSM price multiplied by the [Auction Price Multiplier (`buf`)](../param-auction-price-multiplier.md).

Auction resets can only take place when either the Max Auction Drawdown parameter or the Max Auction Duration parameter are exceeded.

>Page last reviewed: 2022-11-07  
>Next review due: 2023-11-07  

