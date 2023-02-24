# Dai Direct Deposit

>**Alias:** D3M, DDM, Direct DAI Deposit  
>**Primary Contract Name:** `D3MHub`  
>**Secondary Contracts:** Numerous  
>**Etherscan Link:** [0x12F36cdEA3A28C35aC8C6Cc71D9265c17C74A27F](https://etherscan.io/address/0x12f36cdea3a28c35ac8c6cc71d9265c17c74a27f)  
>**Scope:** A contract (or set of contracts) per deposit target.  
>**Technical docs:** [MIP50](https://mips.makerdao.com/mips/details/MIP50)  

## Description

The DAI Direct Deposit Module (D3M) allows DAI to be minted and deposited in other crypto lending protocols on the Ethereum blockchain in exchange for a deposit/collateral token from that lending protocol.

In essence, this allows Maker to distribute newly minted DAI indirectly through other lending protocols while ensuring that DAI remains fully backed. 

For example, the Aave D3M deposits DAI into the Aave protocol in exchange for aDAI tokens that represent deposits in Aave. The aDAI tokens are then used as collateral against the minted DAI. Effectively, this means that collateral deposited by Aave users that borrow DAI is indirectly used to maintain DAI's backing in the Maker Protocol. 

## Purpose

The primary purpose of the D3M is to expand the reach of the DAI stablecoin by providing DAI directly to other lending protocols. In addition, it allows the Maker Protocol to earn a yield on the DAI deposited in these protocols, thus creating a source of income.

Further, it allows Maker the potential to undercut centralized stablecoins on these lending protocols. By providing DAI directly on other lending protocols, Maker could ensure that the borrow rate for DAI on those protocols is almost always below the borrow rate for centralized stablecoins. 

Finally, it is likely that the D3M module is triggered during volatile markets as borrowing rates on lending protocols also tend to fluctuate heavily during such periods. The module assures DAI users on the lending protocol that the lending/borrowing rates remain predictable making DAI a better choice than other stablecoins.

## Technical Information

### Contracts

The primary contract for the Dai Direct Deposit Module is called D3MHub. It is important to note that each deployment of the D3M will have a Plan and a Pool contract associated with it. There may also be Oracle contracts associated with a D3M.

#### D3MHub

The D3M is the primary manager contract responsible for collecting all information and determining which action to take (if any). Each D3M instance is registered on the Hub using relevant file(ilk, ...) admin functions.

#### D3MPool

D3MPool helps move DAI in and out of a protocol, based on what the Hub tells it to do. It also has some functions that tell the Hub how much DAI can be moved in or out at a time. One of these functions is called maxWithdraw(), which tells the Hub how much DAI is available to be moved out right away. Different systems have different ways of making DAI available to be moved out, like raising interest rates or selling off some assets.

#### D3MPlan

D3MPlan can be seen as the decision-making mechanism for D3M instances. It is responsible for analyzing various inputs, such as the target interest rate and the current supply and borrowing levels in the market, and using this information to determine a target debt level. This target debt level is then communicated to the Hub, which takes the necessary actions to achieve the desired level of debt as quickly as possible.

## Key Parameters

### Debt Ceiling (`line`)
The Debt Ceiling parameter for the DAI Direct Deposit Module is substantially identical to the [Debt Ceiling](../parameter-index/vault-risk/param-debt-ceiling.md) parameter for vault types. It controls the maximum amount of DAI that can be minted via the D3M. A D3M Debt Ceiling may also be controlled by the [Debt Ceiling Instant Access Module](../module-index/module-dciam.md).

### Target Borrow Rate (`bar`)
The Target Borrow Rate allows Maker Governance to set the 'ideal' rate for borrowing DAI on the target lending protocol. This is done by adding or removing an amount of DAI from the lending protocol such that the borrow rate on the target protocol becomes equal to the Target Borrow Rate (provided the debt ceiling constraint allows it.) 

If the borrowing interest rate on the target lending protocol is higher than the target borrow rate and the debt ceiling has not been hit, then the module mints and deposits additional DAI into the lending protocol in exchange for deposit tokens.

## Meta Parameters

Meta parameters are not directly present in a smart contract, but they are vital parameters that Maker Governance uses to determine general rules about how to set key parameters.

### Maximum Share

The maximum share meta-parameter is the maximum proportional share of deposit tokens that MakerDAO is willing to hold for a target lending protocol. The parameter is expressed in terms of a percentage and is used to calculate the debt ceiling parameter.

For instance, a maximum share of 100% indicates that MakerDAO is ready to be the only provider of DAI to the target lending protocol. On the other hand, a maximum share of 30% implies that MakerDAO is willing to provide 30% of the total DAI to the target lending protocol, with the remaining 70% being provided by other users or protocols.

### Spread

The spread meta-parameter is the difference between the borrow rate for DAI on the target lending protocol and the Maker Protocol stability fee on ETH-A. This is used to calculate the target borrow rate parameter. The spread parameter enables Maker governance to decide whether it should be cheaper or more expensive to borrow DAI on the target lending protocol compared to the Maker Protocol.

The ETH-A stability fee acts as a proxy for the cost to borrow DAI using the Maker Protocol. It has traditionally been the largest non-PSM vault type in Maker.

The spread is expressed as an annual percentage rate. A spread of 0% indicates that the cost to borrow DAI on the target lending protocol should equal the cost to borrow DAI in the ETH-A vault type over one year.

For example, a spread of -0.5% implies that the cost to borrow DAI on the target lending protocol should be 0.5% cheaper than on the Maker Protocol over one year. Conversely, a spread of 0.5% implies that the cost to borrow DAI on the target lending protocol should be 0.5% more expensive than on the Maker Protocol over one year.

It is crucial to note that the effective borrow rate for DAI on the target lending protocol may be affected by rewards offered by the lending protocol in question. Currently, these additional rewards are not considered while comparing borrow rates.

### Formulas

The Debt Ceiling can be calculated using the following formula:

``Debt Ceiling = Maximum Share * Total DAI Supply (Platform)``

## Considerations

Important things to consider regarding the D3M module:

- Lending protocols often offer farming rewards in the form of a native token, which can result in additional earnings for the D3M module. Governance must decide whether to keep these rewards in the native token or convert them to DAI and add them to the surplus buffer. By default, rewards stay in the native token.
- DAI supply on the lending protocol may not always match the parameters set. For instance, a significant decrease in the line parameter may take some time to have an effect because of liquidity issues in swapping the lending token for DAI. Similarly, the DAI supplied by the module may temporarily exceed the maximum share if other users on the lending protocol rapidly reduce their DAI supply.
- Anyone can call the D3M module, but MakerDAO's Tech-Ops Core Unit operates a bot that calls the module if the target borrow rate and actual rate on the lending protocol diverge beyond a threshold. The Tech-Ops Core Unit manages this threshold with guidance from the Protocol Engineering Core Unit. The threshold is chosen so that rates remain close to the target rate, but the number of calls to the module doesn't get too high, as each call incurs gas costs.
- Yield farming often leads to recursive lending on lending protocols, where users deposit DAI as collateral, borrow DAI from the protocol, and then deposit the borrowed DAI back into the protocol. This loop can be repeated multiple times and increase the total DAI supply figure. The maximum share calculation for the D3M debt ceiling only considers real DAI supply without recursive lending.

>Page last reviewed: 2023-02-24  
>Next review due: 2024-02-24
