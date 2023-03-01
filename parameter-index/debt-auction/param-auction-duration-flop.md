
# Debt Auction Duration

>**Alias:** N/A  
>**Parameter Name:** `tau`  
>**Containing Contract:** `MCD_FLOP`  
>**Scope:** System  
>**Technical Docs:** [Flop Detailed Documentation](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flop-detailed-documentation)  

## Description
The Debt Auction Duration parameter allows governance to control the maximum lifetime of a Debt Auction. A Debt Auction can end before this maximum duration is reached if the [Bid Duration](param-bid-duration-flop.md) timer expires without any additional bids.

Debt Auctions are used to recapitalize the Maker Protocol by minting and auctioning off MKR for a fixed amount of DAI. In this process, Keepers bid the amount of MKR they are willing to accept for a fixed amount of DAI that they provide. 

{% tabs %} 
{% tab title="Example" %}

`Debt Auction Bid Duration` = 300 seconds  
`Debt Auction Duration` = 24 hours  
  
<br>
**Scenario 1 - Limited by Bid Duration**
1. A Debt Auction has been triggered and 3 hours pass with no bid.
2. Keeper A offers to take 20 MKR in exchange for 100 DAI at the 3-hour mark.
3. Keeper B has 300 seconds in which to offer a more attractive bid or else Keeper A will win the auction.
  
<br>
**Scenario 2 - Limited by Auction Duration**
1. A Debt Auction has been triggered and 23 hours and 59 minutes pass with no bid.
2. Keeper A offers to take 20 MKR in exchange for 100 DAI at 23 hours and 59 minutes into the auction.
3. Keeper B has 60 seconds in which to offer a more attractive bid or else Keeper A will win the auction.

<br>
{% endtab %}
{% endtabs %} 

{% hint style="info" %} 

# Example

`Debt Auction Bid Duration` = 300 seconds  
`Debt Auction Duration` = 24 hours  
  

<br>
**Scenario 1 - Limited by Bid Duration**
1. A Debt Auction has been triggered and 3 hours pass with no bid.
2. Keeper A offers to take 20 MKR in exchange for 100 DAI at the 3-hour mark.
3. Keeper B has 300 seconds in which to offer a more attractive bid or else Keeper A will win the auction.
  

<br>
**Scenario 2 - Limited by Auction Duration**
1. A Debt Auction has been triggered and 23 hours and 59 minutes pass with no bid.
2. Keeper A offers to take 20 MKR in exchange for 100 DAI at 23 hours and 59 minutes into the auction.
3. Keeper B has 60 seconds in which to offer a more attractive bid or else Keeper A will win the auction.

{% endhint %}

## Purpose
The Debt Auction Duration parameter allows Maker Governance to adjust the maximum duration for debt auctions in order to ensure robust keeper participation. It also helps to ensure a predictable time frame for the protocol to recover from an undercollateralized state. 

## Trade-offs
The Debt Auction Duration makes a trade-off between ensuring enough time for keepers to deploy their capital while limiting their market risk. A larger Debt Auction Duration gives keepers more time to participate in auctions. A smaller Debt Auction Duration means that keepers are less likely to be affected by negative price movements of the MKR Token during the auction process. Maximizing the number of participating bidders helps ensure that auctions are efficient and less MKR is minted.

A Debt Auction Duration that is too large could result in a situation where there are many auctions happening simultaneously. If the Debt Auction Duration is too small, then keepers may not have sufficient time to organize their resources and place bids. Either of these situations could result in inefficient auctions that increase the amount of MKR that is minted.

The parameter will also have an effect on how long it takes to recapitalize the Maker Protocol in the event that the protocol ends up with bad debt, which may be important depending on the severity of the situation.

## Changes
Adjusting the Debt Auction Duration parameter is a manual process that requires an executive vote. Changes to the Debt Auction Duration are subject to the [GSM Pause Delay](../core/param-gsm-pause-delay.md).

**Why increase this parameter?**
Maker Governance may wish to increase the Debt Auction Duration if too few keepers are participating in debt auctions to encourage greater participation.

**Why decrease this parameter?**
Maker Governance may wish to decrease the Debt Auction Duration if the auctions are so long that keepers almost always make losses. If there are too many overlapping auctions, it may be desirable to decrease this parameter.

## Considerations
Debt Auction Duration is always lower bounded by the Debt Auction Bid Duration i.e. the time period before which a bid expires. If it is set lower than the Debt Auction Bid Duration, it will render that parameter unnecessary since the auction will end before a bid expires. 

For example, if Debt Auction Bid Duration is 1 hour and Debt Auction Duration is 30 minutes, then the auction will only last 30 minutes, making the Debt Auction Bid Duration irrelevant.

The [Surplus Auction Duration](../surplus-auction/param-auction-duration-flap.md) parameter fulfills the same role as this parameter in Surplus Auctions.

>Page last reviewed: 2022-12-05  
>Next review due: 2023-12-05  

