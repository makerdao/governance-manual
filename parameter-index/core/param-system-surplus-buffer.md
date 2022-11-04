# Maximum System Surplus

>**Alias:** Surplus Auction Buffer  
>**Parameter Name:** `hump`  
>**Containing Contract:** `MCD_VOW`  
>**Scope:** System  
>**Technical Docs:** [Vow Detailed Documentation](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/vow-detailed-documentation)  

## Description

The  Maximum System Surplus parameter controls the maximum amount of DAI that can accrue to the protocol's balance from revenue before FLAP auctions are triggered. As revenue comes in, the total amount of DAI inside the System Surplus Buffer increases until it reaches:

 * Maximum System Surplus (`hump`) + Surplus Lot Size (`bump`)*  

At that point, a FLAP auction can be triggered and DAI is auctioned off for MKR. This purchased MKR is then burned.

The Maker Protocol only has one System Surplus Buffer and the stability fees from all vaults accrue to it. Other revenues may also be deposited into the buffer by governance or external actors.

The  Maximum System Surplus is expressed in absolute rather than relative terms, so 1,000,000 DAI rather than 1% of the Total DAI Debt.

## Purpose

In general, whenever the Maker Protocol accrues sufficient value in DAI, MKR is bought and burnt. Likewise, every time the system loses money (bad debt), it mints MKR, sells it, and buys DAI. The primary purpose of the System Surplus Buffer is to reduce the frequency that this occurs. This is beneficial to the protocol because each time an auction takes place (whether FLAP or FLOP), the auction is not perfectly efficient and the protocol loses some percentage of the auctioned value.

In addition, the buffer provides a reserve of DAI which may be used by governance to fund the operations of Core Units and Oracle feeds without requiring the minting of MKR.

## Trade-offs

Increasing the  Maximum System Surplus allows the Maker Protocol to accrue a larger reserve of DAI before burning MKR. This larger reserve provides greater security for the protocol in the event of bad debt.

However, while the buffer is not full FLAP auctions do not take place, and MKR is not burned. This means that Maker Governance is not being rewarded for its efforts during this time.

Additionally, DAI in the System Surplus Buffer is not circulating in the market. This means that holding large amounts of DAI in the System Surplus Buffer will increase upwards pressure on the DAI peg.

Maintaining too low of a  Maximum System Surplus on the other hand means that FLOP auctions are more likely to take place in the event of bad debt. This makes it more likely that the supply of MKR will increase and dilute the value of current MKR Holders.

## Changes

Adjusting the Maximum System Surplus parameter is a manual process that requires an executive vote. Changes to the Maximum System Surplus are subject to the [GSM Pause Delay](param-gsm-pause-delay.md).

**Why increase this parameter?**

The primary reason for increasing the Maximum System Surplus is if it is judged that more surplus is needed to minimize the risk of MKR minting in the case of a market event leading to bad debt. In general, the larger the total DAI debt, the larger the Maximum System Surplus should be to balance the risk from volatile collateral.

Another reason to increase the Maximum System Surplus is if for whatever reason it is beneficial to prevent the burning of MKR for a certain time.

**Why decrease this parameter?**

The primary reason for decreasing the Maximum System Surplus when the buffer is full would be to use the DAI currently in the buffer to buy and burn MKR. Alternatively, if the buffer was not full, Governance may choose to decrease the buffer to restart the continuous MKR burn arising from the buffer overflow.

Another reason to decrease the Maximum System Surplus might be if the risk from the collateral portfolio decreases, either due to reduced DAI debt across all vaults, or the portfolio of collateral backing DAI becoming more stable and less risky on average.

## Considerations

Care should be taken when decreasing the Maximum System Surplus parameter while the buffer is full. Decreasing the size of the buffer will trigger FLAP auctions for the amount of outstanding DAI that no longer fits within the new buffer. Large numbers of FLAP auctions at once have the potential to overwhelm auction keepers and result in the protocol buying MKR at a higher than market price.

DAI can be pulled out of the Maker Protocol by Maker Governance by using the `suck` method as part of an executive vote. DAI `suck`ed from the protocol in this way will be deducted from the System Surplus Buffer and will trigger MKR mints if more DAI is `suck`ed than exists in the System Surplus Buffer.

The System Surplus Buffer is not made up of ERC-20 DAI tokens. Rather, it is a number derived by subtracting the Maker Protocol's liabilities from its assets. At [Emergency Shutdown](https://docs.makerdao.com/smart-contract-modules/shutdown) the value represented by the system surplus goes to DAI holders in the form of a greater share of the collateral backing DAI.

>Page last reviewed: 2022-11-04  
>Next review due: 2023-11-04  

