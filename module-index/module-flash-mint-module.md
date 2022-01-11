# Flash Mint Module

```
Alias: Flash
Contract Name: DSSFlash
Scope: System
Techincal Docs: https://docs.makerdao.com/smart-contract-modules/flash-mint-module
```

## Description

The Flash Mint Module allows anyone to permisionlessly mint Dai as long as it is paid back in the same transaction. This is commonly known as a Flash Loan.

Users can combine Flash Loans with other smart contract functions to perform powerful multi-step transactions across multiple decentralized exchanges (DEX). This process can be used to exploit arbitrage opportunities when Dai deviates from the Peg, among other uses.

### Example

To demonstrate how this works in practice, we will imagine Dai trades at 1.02 DAI/USDC at DEX-1 and 0.98 DAI/USDC at DEX-2. Using the Flash Mint Module, a user could arbitrage this price difference as follows:

* Mint 1000 DAI using the Flash Mint Module
* Exchange 1000 DAI for 1020 USDC at DEX-1
* Exchange 1020 USDC for 1040 DAI at DEX-2
* Pay 1000 DAI back to the Flash Mint Module and has made a profit of 40 DAI

The above example ignores gas fees for simplicity. In reality, flash loan arbitrage must account for gas fees in order to be profitable.

## Purpose

The Flash Mint Module adds Dai Flash Loans to the Maker Protocol, under the control of Maker Governance. There are several advantages to this which are listed below.

## Benefits

There are several benefits offered to the Maker Protocol and broader Dai ecosystem by the Flash Mint Module:

* Improved Flash Loan liquidity - other providers of Flash Loans are reliant on market supply of DAI in order to provide Flash Loan capability. Because the Maker Protocol is able to mint DAI, Flash Loans can theoretically be of infinite size. Because DAI is burned at the end of the transaction this will not effect collatearlization of DAI.
* Market efficiency of DAI is improved by Flash Loan arbitrage - a secondary effect of this could be increased liquidity in DAI markets and Peg stability as deviations from the Peg will be more susceptible to arbitrage.
* The ability to borrow large sums increases the utility of Flash Loans to identify exploits in DeFi protocols - by exposing exploits and attack vectors, the DeFi ecosystem can be made more robust.
* The Flash Mint Module encourages further integration between the Maker Protocol and other Decentralized Apps - DEX aggregators can use it to ensure their users get the best prices available, or Vault automation systems can utilize Flash Loans to leverage and deleverage Vaults.
* Income for The Maker Protocol - The Maker Protocol can charge Minting Fees on Flash Loans that use the Flash Mint Module. Minting Fees have the potential to be an alternative source of revenue for the Maker Protocol. Typically, fees charged on Flash Loans are in the order of 0-0.1%.
* The Flash Mint Module is permissionless, meaning anyone can use it. Similarly, it makes access to arbitrage opportunities to be easier as it is no longer capital dependant.

## Drawbacks

Flash Loans are potent tools, but they also carry some risk. For example, they can be used as an attack vector against DeFi protocols. In addition, it is theoretically possible to mint extremely high amounts of Dai if unrestricted, potentially destabilizing some DeFi protocols.

## Key Parameters

There are two key parameters in the Flash Mint Module that are controlled by Maker Governance. Changes to these parameters are a manual process that require an executive vote. Changes to these parameters are subject to the GSM Pause Delay.

### Debt Ceiling (`line`)

The Debt Ceiling refers to the maximum amount of Flash Loaned Dai that a user can mint in a single transaction.

The higher this value, the greater the potential for profit from arbitrage opportunities and the potential for exploits to cause losses for DeFi protocols.

If the Debt Ceiling is too low, the potential applications of the Flash Mint Module will be lower in number, as potential profit will be lower. As a result, users may look to alternative sources of Flash Loans if they provide more attractive Debt Ceilings.

### Minting Fee (`toll`)

The Minting Fee is an optional fee that the Maker Protocol can charge to users of Flash Loans. Users must repay the Minting Fee simultaneously as they repay the principle of the Flash Loan. For example, a Flash Loan of 1000 DAI with a Minting Fee of 0.1% will require 1001 DAI to be paid back at the end of the transaction.

Minting Fees can be a source of revenue for the Maker Protocol but will decrease the profits of Flash Loan users.

If alternative sources of Dai Flash Loans charge lower or no fees, users may choose to use them rather than the Flash Mint Module.

## User Interaction

The Flash Mint Module conforms to ERC1356. Therefore, users can use the reference borrower implementation from the ERC1356 spec. It requires the user to have the technical ability to work with solidity, or access to a UI that is able to execute the desired transaction.

## Considerations

Fees accrued through the Flash Mint Module are transferred to the Surplus Buffer upon completion of the transaction.
