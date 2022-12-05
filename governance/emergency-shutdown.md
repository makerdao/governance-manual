# Emergency Shutdown

## Overview

An important security feature of the Maker Protocol is the ability to perform an Emergency Shutdown of the protocol. This allows the system to shut down and makes underlying collateral available for redemption by DAI holders and Vault owners. 

## Activation

If MKR voters believe that the system is subject to a high-severity attack, or if an Emergency Shutdown is scheduled as part of a technical upgrade, they can activate an Emergency Shutdown by depositing MKR into the [Emergency Shutdown Module (ESM)](../module-index/module-emergency-shutdown.md). Emergency Shutdown is triggered when MKR deposited to the ESM exceeds the minimum threshold parameter. 

Emergency Shutdown may also be triggered through a regular Executive Vote, though the ESM would be a more direct method that does not have to wait for the [GSM Pause Delay](../parameter-index/core/param-gsm-pause-delay.md) imposed by the Governance Security Module.

## Sequence of events

1. Once Emergency Shutdown has been activated, the following items take effect immediately:
    * The ability to create vaults, generate DAI from existing vaults, or repay borrowed DAI to vaults is disabled. 
    * All debt and surplus auctions are disabled. 
    * The DAI Savings Rate and all stability fees are set to zero. 
    * All price oracles are frozen to their current reference prices. 
    * Vault owners may withdraw any excess collateral from their vaults. 
2. Once Emergency Shutdown has been activated, a cooldown period is needed to allow any ongoing collateral auctions to conclude. Once all collateral auctions finish, the system can calculate the collateral that can be assigned to remaining DAI in circulation.
3. Each DAI holder will then be able to redeem collateral through a series of individual transactions for each collateral type.

## Redeployment

Since the Maker Protocol is open source and decentralized, anyone can redeploy the system and decide with what configuration. Ideally, the parameters of redeployment should depend on the reason for the Emergency Shutdown, and should not be altered unilaterally and arbitrarily. It is likely that the Maker Community will decide on the whether redeployment is appropriate and if so, launch a redeployment themselves with the appropriate configuration.

## Considerations

DAI is no longer soft pegged to 1 USD after Emergency Shutdown, as it is now tied to the value of a fixed amunt of underlying collateral. Such a depegging can result in significant disruption across the wide DeFi ecosystem due to many other dapps that use DAI with the assumption that it is pegged to 1 USD.

DAI holders need to manually redeem their DAI for the underlying collateral. The process is not automatic. Similarly, vault owners must manually withdraw any excess collateral from their vaults.

MKR tokens are not expected to have value after the system is shut down. If the protocol is relaunched and the community decides to do so, existing MKR holders, including those who burned their MKR by depositing them into the ESM, may receive goverance tokens of the relaunched protocol.

Real-world Assets are represented by RWA tokens and DAI holders may redeem the tokens which represent a fractional share of their ownership of the corresponding asset.

## Detailed Documentation

Technical documentation about how Emergency Shutdown works can be found in the [Emergency Shutdown Module](https://docs.makerdao.com/smart-contract-modules/emergency-shutdown-module) section and [End - Detailed Documentation](https://docs.makerdao.com/smart-contract-modules/shutdown/end-detailed-documentation) section of [MakerDAO Technical Docs](https://docs.makerdao.com/).

>Page last reviewed: 2022-11-25  
>Next review due: 2023-11-25  
