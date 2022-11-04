# Dai Savings Rate

>**Alias:** DSR  
>**Parameter Name:** `dsr`  
>**Containing Contract:** `MCD_POT`  
>**Scope:** System  
>**Technical Docs:** [Pot Detailed Documentation](https://docs.makerdao.com/smart-contract-modules/rates-module/pot-detailed-documentation)  

## Description
The Dai Savings Rate parameter allows Maker Governance to adjust the interest rate paid to DAI holders who have deposited DAI into the Dai Savings Rate contract (`MCD_POT`). All DAI Holders are permitted to deposit into the contract to receive the DSR.

The Dai Savings Rate is usually expressed as an APY percentage and will increase balances when set to any positive value.

For example, if the Dai Savings Rate is set to 1%, a user depositing 100 DAI will be able to withdraw 101 DAI after one year.

## Purpose

The Dai Savings Rate parameter enables Maker Governance to increase or decrease the incentive for DAI holders to deposit DAI within the Dai Savings Rate contract.

## Trade-offs

Increasing the Dai Savings Rate increases DAI demand at the cost of decreased DAI liquidity and increased expenses for the Maker Protocol.

Decreasing the Dai Savings Rate will decrease the expenses of the Maker Protocol but may simultaneously reduce DAI demand and cause users to move DAI out of the Dai Savings Rate contract, thus increasing market supply.

## Changes
Adjusting the Dai Savings Rate is a manual process that requires an executive vote. Changes to the Dai Savings Rate are subject to the [GSM Pause Delay](param-gsm-pause-delay.md).

In essence, a higher Dai Savings Rate results in upward pressure on Dai price, and a lower Dai Savings Rate will reduce this pressure.

**Why increase this parameter?**

The primary reason for increasing the Dai Savings Rate is to increase DAI demand. This increase in demand is achieved by encouraging DAI holders to deposit DAI to the Dai Savings Rate contract - thus removing it from the market, which should create upwards pressure on the dollar peg. Therefore, raising the Dai Savings Rate should be considered if DAI is trading below the dollar peg.

Increasing the Dai Savings Rate should make DAI a more attractive asset for holders than other stablecoin assets, potentially increasing DAI's market share in comparison to these assets. It may also incentivize additional integrations with DAI and the Maker Protocol in other dApps.

**Why decrease this parameter?**

The primary reason to decrease the Dai Savings Rate is to reduce DAI demand. Reducing the Dai Savings Rate should result in less DAI deposited in the Dai Savings Rate contract and cause that DAI to re-enter the market. In addition, it may be advisable to decrease the Dai Savings Rate if DAI trades above the dollar peg to reduce upwards price pressure.

Maker Governance may also wish to decrease the Dai Savings Rate when The Maker Protocol experiences a drop in revenue. If Maker Governance does not reduce the Dai Savings Rate when income falls, the Maker Protocol could encounter negative cash flows. Negative cash flow will reduce the System Surplus Buffer over time, and if the buffer is depleted, the Protocol will mint and sell MKR to cover the shortfall.

## Considerations
When DAI holders deposit DAI to the Dai Savings Rate contract, interest is paid from accrued stability fees. Therefore, increasing the Dai Savings Rate will cause the System Surplus Buffer to fill more slowly and reduce the amount of Dai available for Surplus Auctions. If the Dai Savings Rate is set too high, the Maker Protocol could have negative cash flow and eventually need to print MKR.

A negative Dai Savings Rate will not work as intended as balances within the Dai Savings Rate contract cannot decrease.

Any changes to the Dai Savings Rate may affect PSM usage behavior. For example, increased upward pressure on the dollar peg caused by the Dai Savings Rate may require increased PSM usage to balance.

In the event of an [Emergency Shutdown](https://docs.makerdao.com/smart-contract-modules/shutdown), the Dai Savings Rate will be set to 0% to prevent the total debt of the Maker Protocol from increasing.

>Page last reviewed: 2022-11-02  
>Next review due: 2023-11-02  

