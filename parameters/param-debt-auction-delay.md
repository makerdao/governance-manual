# Debt Auction Delay

```
Alias: Debt Auction Delay
Parameter Name: wait
Containing Contract: Vow
Scope: System
Technical Docs: https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/vow-detailed-documentation
```

## Description

The Debt Auction Delay, or `wait` parameter, defines how much time must pass after a Vault has been liquidated before any corresponding debt is marked as bad debt.

If a corresponding Collateral Auction does not clear the debt and any associated penalty fees within the Debt Auction Delay, the remaining debt will be considered bad debt. Initially, the Surplus Buffer will cover the bad debt, but if the system accrues enough bad debt to exhaust the Surplus Buffer, the system will trigger a Debt Auction where MKR is minted and sold to cover the balance.

For example, if the Debt Auction Delay is set to two hours, once a Vault is liquidated, Keepers have two hours to bid and cover the debt before the Vault’s debt is considered bad debt.

## Purpose

The Debt Auction Delay exists to provide time for Keepers to bid on liquidated Vaults via Collateral Auctions. If the Debt Auction Delay is set to zero, all liquidations will proceed instantly to Debt Auctions, which would mint unnecessary amounts of MKR.

The Debt Auction Delay is one of several parameters Maker Governance can utilize to adjust how auctions function in response to protocol risk and market conditions. For example, there may be circumstances where it is desirable to either increase or decrease the speed at which debt is transferred to Debt Auctions, and the Debt Auction Delay facilitates this.

## Trade-offs

It is essential to recognize the interaction between Collateral and Debt Auctions in the context of the Debt Auction Delay.

If the Debt Auction Delay is set too low, the system may prematurely commence a Debt Auction before the corresponding Collateral Auction has been completed. For example, this can occur if the Debt Auction Delay is set to a lower value than the Max Auction Duration of Collateral Auctions. In this situation, it is conceivable that Keepers might cover outstanding debt within the remaining time, and the Debt Auction is therefore unnecessary. This scenario could lead to excess MKR being minted or the Surplus Buffer being drained.

If the Debt Auction Delay is set too high, then it will prevent Debt Auctions from occurring. This will lead to undercollateralized DAI and downwards pressure on the Peg.

## Changes

Adjusting the Debt Auction Delay is a manual process that requires an executive vote. Changes to the Debt Auction Delay are subject to the GSM Pause Delay.

**Why increase this parameter?**

Debt Auction Delay should be increased if the Max Auction Duration of Collateral auctions is increased to prevent unnecessary Debt Auctions.

**Why decrease this parameter?**

The Debt Auction Delay might be decreased if it is taking too long for Debt Auctions to commence, leaving the system undercollateralized for longer than acceptable.

## Considerations

Given that Debt auctions can occur before the corresponding Collateral Auction has been completed, it is wise to ensure that `Debt Auction Delay > Max Auction Duration` to allow Collateral auctions time to complete.

In Emergency Shutdown, all Debt Auctions are cancelled, and the Debt Auction Delay is therefore nullified.
