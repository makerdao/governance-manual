---
title: Module - Peg Stability Module
keywords: 'peg stability module, psm, dsspsm, stability'
---

# Module PSM

```text
Alias: PSM
Contract Name: DssPsm
Scope: Each PSM interacts with a single underlying vault type.
```

## Description

A Peg Stability Module allows users to swap a given collateral type directly for DAI at a fixed rate, rather than borrowing DAI. The PSM contract was designed with stablecoin collateral in mind, allowing users to swap other stablecoins for DAI at a fixed rate to aid with keeping DAI pegged to 1 dollar.

A PSM operates similarly to a regular vault type with a zero stability fee and a liquidation ratio of 100% that can only be accessed through a user-facing smart contract containing the relevant swap functions. Unlike the case with regular vaults, users of PSM don't retain ownership of the asset and borrow DAI, instead they swap the asset directly for DAI.

As an example, given the existence of a USDC-backed PSM, a user would be able to swap 100 USDC for 100 DAI \(minus fees\) using the USDC-backed PSM without taking on any debt or needing to manage a Maker vault.

## Purpose

The PSM contract was primarily created to help keep the DAI peg close to $1 during times where DAI demand outstrips DAI supply.

Initially, low liquidation ratio stablecoin vaults were used for this purpose, but this solution proved difficult for Governance to administer due to the risk of stability fees pushing vaults below the 100% collateralization ratio.

The PSM contract allows Governance to collect fees on stablecoins at the point of swap, rather than over time.

## Trade-offs

A PSM creates the same danger as low liquidation ratio stablecoin vault types: the Maker Protocol will take on a large amount of stablecoin collateral at times where DAI demand outstrips DAI supply. This is usually cited to be a risk due to the centralization of other stablecoins and the possibility of regulatory action targeting Maker specifically. The risk of regulatory action may be slightly greater with a PSM than the alternative because the stablecoin collateral created through a PSM is effectively owned by the Maker Protocol, rather than being owned by a user using it as collateral for a loan of DAI.

Additionally, the Maker Protocol bears the risk of the underlying collateral stablecoin losing its peg \(though this is no different from regular vault-types with stablecoin collateral.\)

On the other hand, a PSM offers several advantages:

* Increased DAI stability due to the instant arbitrage opportunity when the DAI price diverges from the price of the collateral type underlying the PSM.
* Fees are taken upfront on each swap to and from DAI. Because a PSM has no slippage, it's able to attract respectable trading volume.
* There is no requirement to micromanage parameters \(via governance actions\) to ensure continued functioning, in contrast to low liquidation ratio stablecoin vaults.

## Key Parameters

Under the hood, a PSM is just a wrapper contract around a privileged vault type in the Maker Protocol. All the parameters that apply to vault types also apply to a PSM. However, a stablecoin PSM should always have a Stability Fee of 0% and a Liquidation Ratio of 100%.

**Debt Ceiling \(line\)**

The Debt Ceiling refers to the maximum amount of debt the PSM can accrue.

Note that although users do not have a debt when using the PSM to trade between DAI and the collateral asset, the Maker Protocol _does_ accrue a DAI debt which is backed by the asset users trade into the PSM in exchange for DAI.

**Fee In \(tin\)**

The percentage fee applied when trading the collateral asset into the PSM in exchange for DAI.

**Fee Out \(tout\)**

The percentage fee applied when trading DAI into the PSM in exchange for the collateral asset.

## User Interaction

Users can directly call the swap functions on a PSM contract, but it is hoped that PSM's will be integrated into DEX aggregators such that trades will take place when a PSM can offer the best market price.

## Considerations

It's important to note that the amount of trades a PSM can offer is limited by its debt ceiling and the currently deposited amount of collateral tokens. A PSM cannot offer DAI in trade if its debt ceiling has been reached. Likewise, a PSM cannot offer the collateral asset in trade if no collateral tokens exist inside the PSM.

A PSM is a regular vault type with the exception that it can only be accessed by a specific wrapper contract. The wrapper contract defines trading functions to users and levies the trading fees set by Governance.

A PSM is only really possible with an asset that is pegged to the same asset as DAI. Offering 1-to-1 swaps requires a liquidation ratio of 100%. If a PSM with a non-stable asset is attempted, it would run the risk of becoming undercollateralized as soon as the market price of the collateral asset decreased.

