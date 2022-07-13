# Debt Auction Bid Size

>**Alias:  
>**Parameter Name: `sump`  
>**Containing Contract: Vow  
>**Scope: System  
>**Technical Docs: https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/vow-detailed-documentation

## Description
Debt Auctions are used to recapitalize the system by minting and auctioning off MKR for a fixed amount of DAI. In this process, keepers bid on how little MKR they are willing to accept for the fixed Dai amount they have to pay at auction settlement. During debt auctions, the fixed amount of Dai to be covered by any debt auction is determined by the `Debt Auction Bid Size` parameter.


## Purpose
Changing the `Debt Auction Bid Size` parameter allows Maker Governance to minimize the total MKR minted while ensuring that the protocol does not remain in an undercollateralized state for too long. 


## Trade-offs
A small `Debt Auction Bid Size` would result in an auction being triggered more quickly when the protocol is undercollateralized. If the protocol is quickly recollateralized, this improves user confidence in Dai. A small `Debt Auction Bid Size` also means that gas costs for the auction would decrease the profit that keepers receive. In the event of a large system debt, this could also result in many parallel auctions, and keepers may not be able to participate in all of them. Both of these could result in uncompetitive auctions with more MKR minted than necessary.
	
A large `Debt Auction Bid Size` keeps the protocol undercollateralized for longer. In the extreme case where this parameter is too large, debt auctions would never occur. Keepers may find it harder to organize sufficient capital to participate in the debt auction if this parameter is too large. This lack of competition could result in more MKR minted. However, when this parameter is large, the gas costs paid by the keepers to participate in the auction would be small relative to their profit. In the case of large system debt, there would also be fewer auctions running in parallel and, therefore, a higher participation rate among keepers. Both of these would result in more competitive bids and decrease the amount of MKR minted. 


## Changes
Adjusting the `Debt Auction Bid Size` parameter is a manual process that requires an executive vote. Changes to the `Debt Auction Bid Size` are subject to the GSM Pause Delay.

**Why increase this parameter?**
Maker Governance may wish to increase the `Debt Auction Bid Size` if gas costs for keepers are too high or if the number of debt auctions that may occur in parallel is too large.

**Why decrease this parameter?**
Maker Governance may wish to decrease the `Debt Auction Bid Size` if there is insufficient keeper participation or to keep the protocol undercollateralized for a shorter duration.

$eof$