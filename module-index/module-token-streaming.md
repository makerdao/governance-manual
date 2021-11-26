# Token Streaming

>**Alias:** Vesting Module, Vest  
>**Contract Names:** DSSVestMintable, DssVestSuckable, DssVestTransferrable  
>**Scope:** Three separate contracts that cover: minted MKR (DSSVestMintable), minted DAI (DssVestSuckable), and any ERC20 (DssVestTransferrable).  

## Description

The Token Streaming Modules allow the streaming of tokens from the Maker Protocol to Core Units or individuals. Between them they support:
* Scheduling - Set start and end dates for the stream.
* Cliff Vesting - Set a date before which funds cannot be claimed.
* Third-party revocation - Designate a third party who has permission to cancel the stream of funds.
* Minted MKR - One version of the contract (DSSVestMintable) supports streaming purpose-minted MKR tokens.
* Minted DAI - One version of the contract (DssVestSuckable) supports streaming purpose-minted DAI tokens.
* Any ERC20 - One version of the contract (DssVestTransferrable) supports streaming any ERC20 (though the source address must have the requisite tokens.)

The recipients of the streamed funds can call a function on the relevant smart contract and receive some or all of the funds that have been vested at the point the function is called.

## Examples

### Core Unit Budgets
1. Maker Governance has agreed on a 3 month budget for the GovAlpha Core Unit which totals 120,000 DAI. 
2. As part of an executive vote, governance confirms the setup of a DAI token stream using DssVestSuckable with the above parameters.
3. After 24 hours, GovAlpha will be able to claim `120,000 / 90 = ~1,333` DAI from the vesting contract.
4. After 45 days, GovAlpha will be able to claim an additional ~58,666 DAI from the vesting contract.
5. After 90 days, GovAlpha will be able to claim the rest of the DAI (~60,000) from the vesting contract.

### MKR Vesting

1. Maker Governance has agreed to reward a contributor with 200 MKR with a length of 12 months and a cliff period of 6 months. 
2. As part of an executive vote, governance confirms the setup of an MKR token stream using DssVestMintable with the above parameters.
3. Prior to 6 months passing, the contributor will not be able to redeem any MKR from the vesting contract.
4. Once 6 months have expired, the contributor will be able to redeem 100 MKR from the vesting contract.
5. After an additional month has passed, the contributor will be able to claim ~16.67 MKR from the vesting contract.
6. After 12 months have passed, the contributor will be able to claim the remainder of the MKR.

## Purpose

The Token Streaming Modules provide several advantages to governance:
* Provision of a secure mechanism to reward contributors to the Maker Protocol over time.
* Doesn't allow the recipient to access all the tokens up-front, reducing the risk of losing funds due to poor performance or malicious behavior.
* Reduction of Governance overhead regarding compensation for contributors.
* On-chain visibility of governance's budget commitments of DAI and MKR, increasing transparency.
* Enabling user control over the claiming of vested tokens.
* It allows governance to credibly commit to the intention to fund DAI or MKR at a future date by moving the required action to *preventing* a distribution, rather than *approving* a distribution. 

## Trade-offs

DssVest should be compared to manual transfers of the DAI and MKR tokens. 

DssVest allows MKR holders to vote on issues of token distribution less often, which streamlines governance, however, it also requires more attention to continued operations from MKR holders, as tokens will continue to stream until fully allocated or stopped by a further governance action.

## Key Parameters

Parameters for DssVest are upon the deployment of a new stream. The primary parameters are:
- Target Address - The recipient of the tokens.
- Start Date - The date to begin streaming tokens.
- End date - The date to end the token stream.
- Amount - The number of tokens to stream to the recipient.
- Cliff Date - The date after which tokens become accessible to the recipient.

## User Interaction

DssVest allows recipients to claim streamed tokens at their discretion. This involves:

1. Locating the relevant token contract. MakerDAO contracts are listed [here](https://chainlog.makerdao.com/). They are listed as:  
MCD_VEST_DAI - To get DAI minted from the Maker Protocol.  
MCD_VEST_MKR - To get MKR minted from the Maker Protocol.  
MCD_VEST_MKR_TREASURY - - To get MKR transferred from the Maker Protocol treasury.  

2. Call the `vest` function, passing the appropriate stream ID as a parameter. Stream IDs can be found on several prominent MakerDAO status front-ends.

3. Optionally pass a second parameter indicating the number of tokens to receive from the stream. The absence of this parameter will result in all eligible tokens being transferred to the recipient.

## Considerations

Once a vesting stream has reached its end date, the streamed tokens cannot be revoked and users can independently redeem their tokens. The exception to this is if governance revokes permissions over the entire contract, revoking all streams and access to unclaimed funds by the former recipients.

If a stream is revoked at a future date, it will continue streaming up until that date.

When using the DAI Vesting contract, funds remain in the surplus buffer until a transfer is triggered by the recipient. This means any unused funds can be used to protect the protocol, however, also the contract carries the danger of MKR minting if a recipient collects funds from DssVestSuckable while the system surplus buffer does not contain sufficient funds. 
