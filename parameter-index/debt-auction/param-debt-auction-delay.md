# Debt Auction Delay

>**Alias:** Flop Delay  
>**Parameter Name:** wait  
>**Containing Contract:** Vow  
>**Scope:** System  
>**Technical Docs:** [link](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/vow-detailed-documentation)  

## Description

The Debt Auction Delay, or `wait` parameter, defines how much time must pass after a Vault has been liquidated before any corresponding debt is marked as bad debt.

If a corresponding Collateral Auction does not clear the debt and any associated penalty fees within the Debt Auction Delay, the remaining debt will be considered bad debt. This can happen either if the Collateral Auction does not raise enough Dai to cover the total debt despite all collateral being sold, or if the auction does not finish within the Debt Auction Delay. 

Initially, the Surplus Buffer will cover the bad debt, but if the system accrues enough bad debt to exhaust the Surplus Buffer, the system will trigger a Debt Auction where MKR is minted and sold to cover the balance.

### Example
`Debt Auction Delay` = 2 hours

Once a Vault is liquidated, if the Vault's debt has not been covered within two hours it will be considered bad debt, if the Surplus Buffer cannot cover the debt, a debt auction will begin.

## Purpose

The Debt Auction Delay exists to provide time for Keepers to bid on liquidated Vaults via Collateral Auctions. If the Debt Auction Delay is set to zero, all liquidations will proceed instantly to Debt Auctions, as well as triggering a Collateral Auction, which would mint, and subsequently burn, unnecessary amounts of MKR.

## Trade-offs

If the Debt Auction Delay is set too low, the system may prematurely commence a Debt Auction before the corresponding Collateral Auction has been completed. For example, this can occur if the Debt Auction Delay is set to a lower value than the Max Auction Duration of Collateral Auctions. In this situation, it is conceivable that Keepers might cover outstanding debt within the remaining time, and the Debt Auction is therefore unnecessary. This scenario could lead to excess MKR being minted or the Surplus Buffer being drained.

If the Debt Auction Delay is set too high, then it will prevent Debt Auctions from occurring. This will prevent undercollateralized Dai being removed from the system. By allowing Dai to remain undercollateralized, confidence in Dai could be undermined.

## Changes

Adjusting the Debt Auction Delay is a manual process that requires an executive vote. Changes to the Debt Auction Delay are subject to the GSM Pause Delay.

**Why increase this parameter?**

Debt Auction Delay should be increased if the Max Auction Duration of Collateral auctions is increased to prevent unnecessary Debt Auctions. It might also be increased if a large number of Debt Auctions are expected to take place, to ensure Keepers have enough Dai capital to bid on the MKR being auctioned.

**Why decrease this parameter?**

The Debt Auction Delay might be decreased if it is taking too long for Debt Auctions to commence, leaving the system undercollateralized for longer than acceptable. This could impact Dai users and undermine confidence in Dai.

## Considerations

Given that Debt Auctions can occur before the corresponding Collateral Auction has been completed, it is wise to ensure that `Debt Auction Delay > Max Auction Duration` to allow Collateral auctions time to complete.

In theory, Maker Governance can arbitrarily extend the Debt Auction Delay, thus preventing Debt Auctions from occurring indefinitely.

In Emergency Shutdown, all Debt Auctions are cancelled, and the Debt Auction Delay is therefore nullified.

>Page last reviewed: -
>Next review due: -

