# RWA Agreement

>**Alias:** Asset Document Hash   
>**Parameter Name:** `doc`  
>**Containing Contract:** `RwaLiquidationOracle`  
>**Scope:** MIP21/Ilk (RWA)  
>**Technical Docs:** [MIP21](https://mips.makerdao.com/mips/details/MIP21)  

## Description

Real-World Asset (RWA) Vaults are dependent on a contractual arrangement, the RWA Agreement. The RWA Agreement parameter allows the Maker Protocol to record an [IPFS](https://ipfs.tech) hash that links to the actual contract documentation. Each deal will have individual contract documentation, and the documentation format may change from deal to deal.

## Purpose
By recording the contents of the RWA Agreement to the blockchain, a clear and transparent record of legal agreements made by the RWA Core Unit is available. This transparency benefits governance and will be useful in the event of any disputes with borrowers.

This parameter is only used in RWA vaults using the MIP21-defined vault structure.

## Changes
Changing the RWA Agreement parameter can be done through a manual process that requires an Executive Vote. Changes to the RWA Agreement parameter are subject to the GSM Pause Delay.

Maker Governance should make changes to the parameter to reflect changes in the underlying contractual documentation.

Maker Governance should not change the parameter unless there has been a change in the underlying contractual documentation.

## Considerations
As MakerDAO is not a legal entity, the actual use of the contractual documentation may be limited.

>Page last reviewed: 2022-11-08  
>Next review due: 2023-11-08  

