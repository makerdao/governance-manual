# Dai Direct Deposit

>**Alias:** D3M  
>**Contract Name:** `DssDirectDeposit`  
>**Scope:** One DssDirectDeposit contract per deposit target.  

## Description

The Dai Direct Deposit Module (D3M) allows DAI to be minted and deposited in other crypto lending protocols on the Ethereum blockchain in exchange for some sort of deposit/collateral token from that lending protocol.

In essence, this allows Maker to distribute newly minted DAI indirectly via other lending protocols while ensuring that DAI remains fully backed. 

For example, the Aave D3M deposits DAI into the Aave protocol in exchange for aDAI tokens that represent that deposit in Aave. The aDAI tokens are then used as collateral against the minted DAI. Effectively, this means that collateral deposited by Aave users that borrow DAI is indirectly used to maintain DAI's backing in the Maker Protocol. 

## Purpose

The primary purpose of the D3M is to expand the reach of the DAI stablecoin by providing DAI directly to other lending protocols. In addition to this, it allows the Maker Protocol to earn yield on the deposited DAI in these protocols, providing a source of income. 

Further, it allows Maker to undercut centralized stablecoins on these lending protocols. By providing DAI directly on other lending protocols, Maker can ensure that the borrow rate for DAI on those protocols is almost always below the borrow rate for centralized stablecoins.

## Key Parameters

### Debt Ceiling (line)  
The Debt Ceiling parameter for the Dai Direct Deposit Module is substanstially identical to the Debt Ceiling parameter for vault types. It controls the maximum amount of DAI that can be minted via the D3M. Note that the D3M Debt Ceiling may also be controlled by the Debt Ceiling Instant Access Module.

### Target Borrow Rate (bar)  
The Target Borrow Rate allows Maker Governance to set the 'ideal' rate for borrowing DAI on the target lending protocol for the D3M. This works through the following mechanism:

```
if(DAI_BORROW_RATE is greater than TARGET_BORROW_RATE and the DEBT_CEILING is not met) then...
... Mint and deposit additional DAI into the target lending protocol in exchange for deposit tokens

if(DAI_BORROW_RATE is less than TARGET_BORROW_RATE and the module holds a non-zero amount of deposit tokens) then...
... Return deposit tokens to the target lending protocol in exchange for DAI which is then burned.
```

The function to trigger this mechanism is permissionless, and is called by bots at regular intervals.

### Meta Parameters

Meta parameters are parameters that don't exist directly on the DssDirectDeposit smart contract, but are parameters that Maker Governance uses to determine general rules about how to set actual parameters.

#### Maximum Share

The maximum share meta-parameter refers to the maximum proportional share of deposit tokens that MakerDAO wishes to hold for a target lending protocol. The parameter is expressed in terms of a percentage.

A maximum share of 100% would indicate that MakerDAO is willing to be the sole provider of DAI to the target lending protocol.

A maximum share of 30% would indicate that MakerDAO is willing to provide 30% of the total DAI to the target lending protocol, with the other 70% being provided by other users or protocols.

#### Spread

The spread meta-parameter refers to the difference between the _effective_ borrow rate for DAI on the target lending protocol and the Maker Protocol stability fee on ETH-A. The goal of this parameter is for Maker governance to be able to decide whether it should be cheaper or more expensive to borrow DAI on the target lending protocol in comparison to the Maker Protocol. 

The ETH-A stability fee is used as a proxy for cost to borrow DAI using the Maker Protocol, given it has traditionally been the largest non-PSM vault type on the Maker Protocol.

The spread is described as a percentage rate. A spread of 0% would indicate the cost to borrow DAI on the target lending protocol should equal the cost to borrow DAI in the ETH-A vault type.

A spread of -0.5% indicates that the cost to borrow DAI on the target lending protocol should be 0.5% cheaper than on the Maker Protocol.

A spread of 0.5% indicates that the cost to borrow DAI on the target lending protocol should be 0.5% more expensive than on the Maker Protocol.

The _effective_ borrow rate for DAI on the target lending protocol is often affected by rewards offered by the lending protocol in question.

### Formulas

Bar = ETH-A Rate (Maker) + Borrow Rewards (Aave on DAI) + 2x Supply Rewards (Aave On ETH) + Spread




## Trade-offs

## Considerations