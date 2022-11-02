# Global Debt Ceiling

>**Alias:** Global Debt Ceiling  
>**Parameter Name:** `Line`  
>**Containing contract:** `MCD_VAT`  
>**Scope:** System  
>**Technical Docs:** [Vat Detailed Documentation](https://docs.makerdao.com/smart-contract-modules/core-module/vat-detailed-documentation)  

## Description

The Global Debt Ceiling, or `Line`, parameter allows Maker Governance to set a maximum total amount of DAI that can be minted by users of the Maker Protocol. If a user tries to mint DAI and the amount of new DAI minted would put the total amount of DAI minted above the Global Debt Ceiling, the transaction will fail and no DAI will be minted.

Additionally, vault types have a [Debt Ceiling](..\vault-risk\param-debt-ceiling.md) parameter that is not covered in this entry. For a user to mint DAI from their vault, there must be space available in both the vault type's Debt Ceiling and the Global Debt Ceiling.

## Purpose

The purpose of the Global Debt Ceiling is to act as an upper bound on the amount of DAI in circulation. If a failure elsewhere in the Maker Protocol results in unbacked DAI being minted, the Global Debt Ceiling will cap the loss in value. 

## Trade-offs

If the Global Debt Ceiling is set too low, it will prevent DAI from being minted. This is both a bad experience for vault users, and may also cause the DAI peg to break upward if DAI demand increases, but DAI supply cannot increase.

If the Global Debt Ceiling is set too high then the Maker Protocol will have increased losses in the event of a bug or exploit that mints unbacked DAI.

## Changes

Adjusting the Global Debt Ceiling parameter can be done through a manual process that requires an executive vote. Changes to the Global Debt Ceiling are subject to the [GSM Pause Delay](param-gsm-pause-delay.md).

Generally speaking, the Global Debt Ceiling does not need to be manually managed by Maker Governance. The Protocol Engineering Core Unit includes changes to the parameter in executive proposals such that it approximately equals the sum of the debt ceilings of each vault type.

The Global Debt Ceiling is also automatically adjusted to account for debt ceiling changes that occur via the [Debt Ceiling Instant Access Module](..\..\module-index\module-dciam.md). The Debt Ceiling Instant Access Module allows the Debt Ceiling of a given Vault type to be adjusted instantly according to certain hard-coded rules and parameters. When this occurs, the Global Debt Ceiling will change by the same amount.

## Considerations

The Global Debt Ceiling will not prevent DAI from accruing in the system surplus buffer from stability fees. Therefore, the overall DAI supply can still increase despite the Global Debt Ceiling being reached.

Maker Governance should exercise caution when reducing the debt ceiling of collateral types; this may lead to an unintended situation where the Global Debt Ceiling is below the overall DAI supply, thus preventing further DAI from being minted.

If Emergency Shutdown is triggered, DAI cannot be minted regardless of the Global Debt Ceiling.

>Page last reviewed: 2022-11-02  
>Next review due: 2023-11-02  

