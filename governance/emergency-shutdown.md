# Emergency Shutdown

## Overview

An important security feature of the Maker Protocol is the ability to perform an Emergency Shutdown of the protocol. This allows the system to shut down gracefully and makes underlying collateral available for redemption by DAI holders and vault owners in a fair manner. The main goals of Emergency Shutdown are to ensure that 
1. Vault owners with excess collateral in their vaults are able to fully withdraw that excess collateral. 
2. DAI holders are then entitled to a pro-rata share of remaining collateral assets. Depending on what the protocol's total assets are worth, each unit of DAI may be worth less than $1. 
3. Race conditions are avoided so that no matter when DAI holders and Vault owners choose to redeem their collateral, the collateral they are entitled to remains unchanged.

{% hint style="warning" %}

While all reasonable effort has been made to ensure the accuracy and currency of this page, the authors are not smart contract developers, and changes to the Emergency Shutdown procedure may be made by Maker Governance at any time (subject to the GSM Pause Delay).

{% endhint %}

## Activation

Emergency Shutdown is a last-resort measure that shuts down the protocol. Example situations where it can be used is to defend the protocol against a high-severity attack or if MKR holders believe the protocol cannot be made solvent through debt auctions.

The process of Emergency Shutdown starts with MKR holders depositing MKR into the [Emergency Shutdown Module (ESM)](../module-index/module-emergency-shutdown.md). Emergency Shutdown is triggered when MKR deposited to the ESM exceeds the minimum threshold parameter. 

The protocol may also be shut down through a regular Executive Vote. Unlike triggering the ESM, this type of shutdown would be subject to the [GSM Pause Delay](../parameter-index/core/param-gsm-pause-delay.md) imposed by the Governance Security Module and is more likely to be used in the case of major technical upgrades.

## Sequence of events

1. Once Emergency Shutdown has been activated, the following items take effect immediately:
    * The ability to create vaults, generate DAI from existing vaults, or repay borrowed DAI to vaults is disabled. 
    * All debt and surplus auctions can be permisionlessly disabled. 
    * The DAI Savings Rate and all stability fees are set to zero. 
    * All price oracles are frozen to their current reference prices. 
    * Vault owners may still withdraw any excess collateral from their vaults but cannot repay DAI debt to retrieve the remaining collateral. 
2. Once Emergency Shutdown has been activated, a cooldown period is needed to allow any ongoing collateral auctions to conclude. Once all collateral auctions finish, the system can calculate the collateral that can be assigned to the remaining DAI in circulation.
3. Each unit of DAI is entitled to withdraw a pro-rata share of collateral from each collateral type. Users may either continue to hold their DAI or transfer it to other wallets until it is used to redeem the underlying basket of collateral. 

## Redeployment

Since the Maker Protocol is open source and decentralized, anyone can redeploy the system. Ideally, the parameters of redeployment should depend on the reason for the Emergency Shutdown, and should not be altered unilaterally and arbitrarily. 

It is likely that the Maker Community will decide on whether redeployment is appropriate and if so, MKR holders will vote on a redeployment with the appropriate configuration.

## Considerations

DAI is no longer soft pegged to 1 USD after Emergency Shutdown, as it is now tied to the value of a fixed amount of underlying collateral. Such a depegging could result in significant disruption across the wide DeFi ecosystem due to many other dapps that use DAI with the assumption that it is pegged to 1 USD.

DAI holders need to manually redeem their DAI for the underlying collateral. The process is not automatic. It is likely that there will be secondary markets where DAI can be traded for specific assets rather than the underlying basket of collateral.  

Vault owners must manually withdraw any excess collateral from their vaults.

MKR tokens may or may not have value after the system is shut down. If the protocol is relaunched and the community decides to do so, existing MKR holders, including those who burned their MKR by depositing them into the ESM, may receive governance tokens of the relaunched protocol. The relaunched protocol may even continue to use existing MKR tokens.

Real-world Assets are represented by RWA tokens and DAI holders may redeem DAI for the RWA tokens. The RWA tokens represent a fractional share of the corresponding real-world asset.

## Detailed Documentation

Additional technical documentation about how Emergency Shutdown works can be found in the following links.
* [Emergency Shutdown Module documentation](https://docs.makerdao.com/smart-contract-modules/emergency-shutdown-module)
* [End - Detailed Documentation](https://docs.makerdao.com/smart-contract-modules/shutdown/end-detailed-documentation)
* [MakerDAO Technical Docs](https://docs.makerdao.com/).

>Page last reviewed: 2022-12-11  
>Next review due: 2023-12-11  
