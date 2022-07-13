# Price Function

>**Alias:** Price Curve  
>**Parameter Name:** `calc`  
>**Containing Contract:** `Clipper`  
>**Scope:** Vault Type (Ilk)  
>**Technical Docs:**  

## Description

The Auction Price Function is the mathematical function that determines how the collateral price changes over time during a collateral auction. Collateral auctions use a falling price auction, where the price starts high and decreases according to the function defined in this parameter.

Auction Price Functions are implemented as smart contracts exposing specific interface functions. An Auction Price Function contract may have additional parameters that allow Maker Governance to adjust certain aspects of the function.

Each vault type may have its own Auction Price Function, though in practice they may share the same Auction Price Function contract.

## Purpose

This parameter exists to control the shape of the price curve used when auctioning collateral from liquidated vaults.

## Price Curves

### Exponential Stair Step

#### cut  
Controls the 'depth' of each step in the function. A smaller cut means a smoother line, a large one means more pronounced steps.

This is a multiplicative factor. For example, 0.99 equates to a 1% price drop.

#### step  
Controls the length of time between price drops. A smaller step means a smoother line, a large one means more pronounced steps. This is defined in seconds.

![Exponential Stair Step Auction](https://github.com/makerdao/governance-manual/blob/main/parameter-index/collateral-auction/images/cut-and-step.png?raw=true)

### Linear Decrease

In an auction utilizing a Linear Decrease Auction Price Function the auction will start at a price defined by the Auction Price Multiplier. The price will decrease linearly over time until it reaches 0. The time that it takes for an auction to reach 0 is controlled by the tau function.

#### tau
A value in seconds which controls how long it takes for the price of a Linear Decrease auction to reach 0. This controls the rate of fall in the price of the collateral being auctioned. A higher tau will result in slower reduction in the price of collaterals, whereas a lower tau will cause faster falls in price.

The Linear Decrease function is also bounded by the Maximum Auction Duration parameter. This can be used to set a lower bound on the price accepted by the Maker Protocol. Once this value has been reached, the price will stop falling, Keepers can re-start the auction from the initial price at this point.

## Trade-offs

Having control over the parameters of the Auction Price Function allows Governance to fine-tune the performance of auctions to best fit changing market conditions. A non-optimal setting could result in auctions resolving less quickly or in collateral being auctioned off at a lower price.

An auction price falling too quickly may lead to a situation where keepers are not able to bid before the auction ends.

An auction price falling too slowly may increase the auction slippage, and could potentially cause bad debt.

## Changes

Adjusting an Auction Price Function parameter is a manual process that requires an executive vote. Changes to an Auction Price Function are subject to the GSM Pause Delay.

>Page last reviewed: -
>Next review due: -

