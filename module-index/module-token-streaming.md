# Token Streaming Modules

>**Alias:** Vesting Module, Vest  
>**Contract Names:** DSSVestMintable, DssVestSuckable, DssVestTransferrable  
>**Scope:** Three separate contracts that cover: minted MKR (DSSVestMintable), minted DAI (DssVestSuckable), and any ERC20 (DssVestTransferrable).  

## Description

The Token Streaming Modules allow the streaming of tokens from the Maker Protocol to Core Units or individuals. Between them they support:
* Scheduling - Set start and end dates for the stream.
* Cliff Vesting - Set a date before which funds cannot be claimed.
* Third-party revocation - Designate a third party who has the permission to cancel the stream of funds.
* Minted MKR - One version of the contract (DSSVestMintable) supports streaming purpose-minted MKR tokens.
* Minted DAI - One version of the contract (DssVestSuckable) supports streaming purpose-minted DAI tokens.
* Any ERC20 - One version of the contract (DssVestTransferrable) supports streaming any ERC20 (though the source address must have the requiste tokens.)

In practice, the recipients of the streamed funds can call a function on the relevant smart contract and recieve some or all of the funds that have vested at the point the function is called.

## Examples

Maker Governance has agreed to reward a contributor with 100 MKR with a cliff period of 6 months. Once 6 months have expired, the contributor will be able to redeem 100 MKR from DSSVestMintable.

In an alternative scenario, the contributor leaves the Maker Protocol before 6 months have expired. Here, a representative of Maker Governance, usually a Core Unit Facilitator, would be able to halt the vesting process through third-party revocation, and the contributor will be unable to claim the MKR.

## Purpose

The Token Streaming Modules provide several advantages to governance:
* Provision of a secure mechanism to reward contributors to the Maker Protocol over time.
* Reduction of Governance Overhead regarding compensation for contributors.
* On-chain visibility of governance's budget commitments of DAI and MKR, increasing transparency.
* Enabling user control over the claiming of vested tokens.
* It allows governance to credibly commit to the intention to fund DAI or MKR at a future date by moving the required action to *preventing* a distribution, rather than *approving* a distrbiution. 

## Trade-offs

DssVest should be compared to manual transfers of the DAI and MKR tokens. 

DssVest allows MKR holders to vote on issues of token distribution less often, which streamlines governance, however it also requires more attention to continued operations from MKR holders, as tokens will continue to stream until fully allocated or stopped by a further governance action.

## Key Parameters

Parameters for DssVest are unique as they are set upon deployment of a new stream. The primary parameters are:

- address
- start date
- end date
- "cliff" date (ie tokens will not be available to the end address until this date)

## User Interaction

DssVest allows recipients to claim streamed tokens at their discretion. For a full review on how to use DssVest please see [$insert-link-here]().

## Considerations

Once a vesting stream has reached its end-date, the streamed tokens cannot be revoked and users can independently redeem their tokens. The exception to this is if governance revokes permissions over the entire contract, revoking all streams and access to unclaimed funds by the former recipients.

If a stream is revoked at a future date, it will continue streaming up until that date.

When using the DAI Vesting contract, funds remain in the surplus buffer until a transfer is triggered by the recipient. This means any unused funds can be used to protect the protocol, however, also the contract carries the danger of MKR minting if a recipient collects funds from DssVestSuckable when the surplus buffer is depleted. 
