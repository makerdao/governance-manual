# Dai Direct Deposit

>**Alias:** D3M, DDM, Direct DAI Deposit  
>**Contract Name:** `DssDirectDeposit`  
>**Scope:** One DssDirectDeposit contract per deposit target.  
>**Technical docs:** TBD  

## Description

The DAI Direct Deposit Module (D3M) allows DAI to be minted and deposited in other crypto lending protocols on the Ethereum blockchain in exchange for a deposit/collateral token from that lending protocol.

In essence, this allows Maker to distribute newly minted DAI indirectly via other lending protocols while ensuring that DAI remains fully backed. 

For example, the Aave D3M deposits DAI into the Aave protocol in exchange for aDAI tokens that represent deposits in Aave. The aDAI tokens are then used as collateral against the minted DAI. Effectively, this means that collateral deposited by Aave users that borrow DAI is indirectly used to maintain DAI's backing in the Maker Protocol. 

## Purpose

The primary purpose of the D3M is to expand the reach of the DAI stablecoin by providing DAI directly to other lending protocols. In addition to this, it allows the Maker Protocol to earn a yield on the deposited DAI in these protocols, providing a source of income. 

Further, it allows Maker to undercut centralized stablecoins on these lending protocols. By providing DAI directly on other lending protocols, Maker can ensure that the borrow rate for DAI on those protocols is almost always below the borrow rate for centralized stablecoins. 

Finally, it is likely that the D3M module is triggered during volatile markets as borrowing rates on lending protocols also tend to fluctuate heavily during such periods. The module assures DAI users on the lending protocol that the lending/borrowing rates remain predictable making DAI a better choice than other stablecoins.

## Key Parameters

### Debt Ceiling (line) 
The Debt Ceiling parameter for the DAI Direct Deposit Module is substantially identical to the Debt Ceiling parameter for vault types. It controls the maximum amount of DAI that can be minted via the D3M. A D3M Debt Ceiling may also be controlled by the [Debt Ceiling Instant Access Module](../module-index/module-dciam.md).

### Target Borrow Rate (bar) 
The Target Borrow Rate allows Maker Governance to set the 'ideal' rate for borrowing DAI on the target lending protocol. This is done by adding or removing an amount of DAI from the lending protocol such that the borrow rate on the target protocol becomes equal to the Target Borrow Rate (provided the debt ceiling constraint allows it.) 

If the borrowing interest rate on the target lending protocol is higher than the target borrow rate and the debt ceiling has not been hit, then the module mints and deposits additional DAI into the lending protocol in exchange for deposit tokens.

Conversely, if the borrowing interest rate on the target lending protocol is lower than the Target Borrow Rate and the module holds a nonzero amount of deposit tokens, then the contract returns deposit tokens to the lending protocol in exchange for DAI which is then burned. 

The function to trigger this mechanism is permissionless and is called by bots run by MakerDAO at regular intervals.

It is possible to deactivate the Aave D3M by setting the Target Borrow Rate to 0. Note that while setting the Target Borrow Rate to 0 might intuitively suggest that the Aave D3M will utilize its full debt ceiling, it is a pre-programmed state in the D3M code that will de-activate the D3M entirely. The Target Borrow Rate may be set to 0 using a `DIRECT_MOM`, this will bypass the [GSM Pause Delay](../parameter-index/core/param-gsm-pause-delay.md) and allow this change to take effect on the execution of an Executive Vote.

## Meta Parameters

Meta parameters are parameters that don't exist directly on a smart contract (in this case the DssDirectDeposit contract) but are parameters that Maker Governance uses to determine general rules about how to set actual parameters.

### Maximum Share

The maximum share meta-parameter refers to the maximum proportional share of deposit tokens that MakerDAO wishes to hold for a target lending protocol. The parameter is expressed in terms of a percentage and is used to compute the debt ceiling parameter.

A maximum share of 100% would indicate that MakerDAO is willing to be the sole provider of DAI to the target lending protocol.

A maximum share of 30% would indicate that MakerDAO is willing to provide 30% of the total DAI to the target lending protocol, with the other 70% being provided by other users or protocols. 

### Spread

The spread meta-parameter refers to the difference between the _effective_ borrow rate for DAI on the target lending protocol and the Maker Protocol stability fee on ETH-A. This is used to compute the target borrow rate parameter. The goal of this parameter is for Maker governance to be able to decide whether it should be cheaper or more expensive to borrow DAI on the target lending protocol in comparison to the Maker Protocol. 

The ETH-A stability fee is used as a proxy for the cost to borrow DAI using the Maker Protocol, given it has traditionally been the largest non-PSM vault type in Maker.

The spread is described as an annual percentage rate. A spread of 0% would indicate the cost to borrow DAI on the target lending protocol should equal the cost to borrow DAI in the ETH-A vault type over one year.

A spread of -0.5% indicates that the cost to borrow DAI on the target lending protocol should be 0.5% cheaper than on the Maker Protocol over one year.

A spread of 0.5% indicates that the cost to borrow DAI on the target lending protocol should be 0.5% more expensive than on the Maker Protocol over one year.

The _effective_ borrow rate for DAI on the target lending protocol is often affected by rewards offered by the lending protocol in question. For example, users are awarded borrow rewards (for borrowing DAI) and supply rewards (for supplying collateral) on many lending protocols. 

### Formulas

The target borrow rate is set as follows:

``Target Borrow Rate = ETH-A Rate (Maker) + DAI Borrow Rewards (Target Protocol) + 2 x ETH Supply Rewards (Target Protocol) + Spread`` 

The supply rewards are doubled based on the assumption that DAI borrowers keep a 200% collateralization ratio on the target protocol.

The debt ceiling is set as follows:

``Debt Ceiling = Maximum Share * Total DAI Supply (Platform)`` 

## Trade-offs

A more positive spread value and consequently a higher bar would result in less borrowing on the lending protocol via the D3M and hence reduced revenue for Maker from the D3M. However, this would result in potentially increased use of Maker's own vaults and hence higher revenues from those vaults. A more negative spread value results in higher revenues from the D3M module and potentially lower revenues from vaults. 

A higher D3M debt ceiling results in higher potential revenues from the D3M module and the ability to cater to spikes in demand for DAI but also results in higher credit risk for Maker, should the target lending protocol suffer any losses. Conversely, a lower D3M debt ceiling decreases credit risk for Maker but also lowers potential revenues from the D3M module and reduces the ability to cater to spikes in demand for DAI.

## Considerations

Due to lending protocols offering farming rewards in terms of a native token (e.g. stkAAVE on Aave), the D3M module results in additional earnings denominated in that native token. It is up to governance to decide whether to hold the farming rewards income in the native token or to convert it into DAI and add it to the surplus buffer. By default, rewards remain in the native token.

DAI supply on the lending protocol may not always reflect the parameters set. For example, a large decrease in the line parameter may require time to take effect due to liquidity issues in swapping the lending token for DAI. Similarly, the DAI supplied by the module may temporarily exceed the maximum share if the supply of DAI by other users on the lending protocol decreases rapidly.

While the D3M module can be called by anyone, MakerDAO's Tech-Ops Core Unit runs a bot that calls the module if the target borrow rate and actual rate on the lending protocol diverge by some threshold. This threshold is managed by the Tech-Ops Core unit with advice from the Protocol Engineering Core Unit. The threshold is chosen such that the rates remain close to the target rate but the number of calls to the module is not too high, since each call incurs gas costs.

Recursive lending is common on lending protocols due to yield farming. This is where a user deposits DAI as collateral, borrows DAI from the protocol, and deposits the borrowed DAI back into the protocol. This recursive loop can be repeated several times and inflates the total DAI supply figure. The maximum share calculation for the D3M debt ceiling only takes into account real DAI supply without recursive lending. 






