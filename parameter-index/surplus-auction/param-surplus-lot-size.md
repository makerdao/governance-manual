# Surplus Auction Lot Size

>**Alias:** N/A  
>**Parameter Name:** `bump`  
>**Containing contract:** `MCD_VOW`  
>**Scope:** System  
>**Technical Docs:** [Vow Detailed Documentation](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/vow-detailed-documentation)  

## Description
The Surplus Auction Lot Size or `bump` parameter controls the amount of DAI that is auctioned off in each surplus auction.

Surplus auctions can be triggered when:  

_Surplus DAI > [Maximum System Surplus](../core/param-system-surplus-buffer) (`hump`) + Surplus Auction Lot Size (`bump`)_

### Example

_Maximum System Surplus = 50 million DAI_  
_Surplus Auction Lot Size = 10,000 DAI_  

The system surplus must exceed 50,010,000 DAI before a surplus auction can be triggered. When the surplus auction occurs, 10,000 DAI will be auctioned to keepers in exchange for MKR.

## Purpose

The Surplus Auction Lot Size parameter allows Maker Governance to tune the frequency and accessibility of surplus auctions in order to achieve better auction efficiency.

## Trade-offs

Increasing the Surplus Auction Lot Size will result in fewer auctions - meaning more competition between keepers in each auction and increased gas efficiency. However, a larger Surplus Auction Lot Size may make the capital requirement prohibitive for some keepers, reducing the number of individuals that are able to bid.

Reducing the Surplus Auction Lot Size will result in a greater number of auctions. These auctions will require lower amounts of MKR to participate, allowing more keepers to take part. However, a higher number of auctions leads to a higher fixed cost to bid relative to the potential profit, which may decrease participation. If auctions are not competitive, then the price obtained for the auctioned DAI may be below-market rates.

## Changes
Adjusting the Surplus Auction Lot Size parameter is a manual process that requires an executive vote. Changes to the Surplus Auction Lot Size are subject to the [GSM Pause Delay](../core/param-gsm-pause-delay.md).

In general the goal when tweaking this parameter is to increase keeper participation in surplus auctions.

**Why increase this parameter?**

The main reason for Maker Governance to increase the Surplus Auction Lot Size is to reduce the overall number of surplus auctions. Fewer auctions reduces the gas cost for keepers relative to their potential profit, making participation more attractive to keepers.

**Why decrease this parameter?**

The main reason for Maker Governance to decrease the Surplus Auction Lot Size is to reduce the capital requirement for auction participation, potentially increasing the number of keepers able to participate.
 
 ## Considerations
 
The Surplus Auction Lot Size must be greater than 0 DAI.

The gas cost to `kick` (trigger) a surplus auction is non-trivial. If the Surplus Auction Lot Size is too small, surplus auctions may not be triggered by any keeper because they are required to accept a fixed cost for an uncertain return.

>Page last reviewed: 2022-11-09  
>Next review due: 2023-11-09  

