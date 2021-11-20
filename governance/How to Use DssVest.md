# DssVest Documentation

## Overview

DssVest is a tool developed for streaming payments over time. The contracts were developed to support DAI, MKR, or any pre-sent ERC-20 token stream. This setup allows for things like budgets, MKR vesting, and other forms of compensation to be locked into the Maker Protocol.

With DssVest, token balences are accrued every block. The recipiant address may call a function of the contract to recieve the current balence at any time after the Cliff Date has passed. DssVest was intended to make the budgeting lighter on the technical load and Governance burden.

This documentation will highlight the smart contract implementation, as well as the callable functions stream recipients will need to know.

### Contract Addresses

The two main contracts for DssVest are for DAI Streams and MKR Streams. DAI streams are `sucked` from the Surplus Buffer, whereas MKR streams are `mint` new MKR tokens once called.

The DAI Stream contract is:
[0x2Cc583c0AaCDaC9e23CB601fDA8F1A0c56Cdcb71](https://etherscan.io/address/0x2Cc583c0AaCDaC9e23CB601fDA8F1A0c56Cdcb71)

The MKR Stream contract is:
[0x0fC8D4f2151453ca0cA56f07359049c8f07997Bd](https://etherscan.io/address/0x0fC8D4f2151453ca0cA56f07359049c8f07997Bd)

Any new ERC-20 streams will create a new contract address to use for that stream. These streams apply to any ERC-20 tokens and thus can be set up for DAI or MKR as well. This implementation requires the tokens to exist in the contract when called to be successful.

### Callable Functions

There are 11 callable functions in this contract implementation. They are listed out below in order of appearance:

1. `create`
2. `deny`
3. `file`
4. `move` - This function is used to move stream addresses, and can only be called by the steam recipient. The two inputs required for this function:
	- `_id` (uint256)
	- `_dst` (address)
5. `rely`
6. `restrict` - This function can be called to restrict who may transfer a DssVest balance. It is callable by the stream recipient address and if called will make it so only the recipient address may initiate transfers. There is one input for this function:
	- `_id` (uint256)
7. `unrestrict` - This function may be called by the recipient address. If called, this function enables any address to call `vest` and transfer the funds to the recipient address. There is one input for this function:
	- `_id` (uint256)
8. `vest` - This function is responsible for sending the entire token balance to the recipient address. By default, this can be called by any address, but often `restrict` to enable only the recipient address to call the function. There is one input for this function:
	- `_id` (uint256)
9. `vest` - This function is responsible for sending part of a token balance to the recipient address. Any attempt to claim more than the available balance will result in a failed transaction. This function has two inputs:
	- `_id` (uint256)
	- `_maxAmt` (uint256)
10. `yank` - This function is used to remove a stream and is restricted to the Pause Proxy by default. Any token balance already streamed will be available to the recipient. There is one input to this function:
	- `_id` (uint256)
11. `yank` -  This function is used to remove a stream at a specific time and is restricted to the Pause Proxy by default. Any token balance already streamed will be available to the recipient. There are two inputs to this function:
	- `_id` (uint256)
	- `_end` (uint256)
	
### Contract Inputs

- `_id` - ID number of the stream (given upon the stream's creation). Must be entered in uint256 format (ie *number*, for example, see the first column of DAI/MKR streams table).
- `_dst` - Destination address where the stream is being moved. Must be entered in address format (ie *address*, for example the Pause Proxy would be entered as *0xBE8E3e3618f7474F8cB1d074A26afFef007E98FB*)
- `_maxAmt` - The number of tokens to be transferred. This amount must be entered in the uint256 format and the input is the amount times 10^18 (ie *number*, for example, to receive 10,000 tokens *10000000000000000000000* would be entered)
- `_end` - Epoch number of the date that the stream is to be removed. Must be entered in the uint256 format (ie *number*, for example, to remove a stream on Jan. 1, 2022, at 00:00:00 UTC *1640995200* would be entered.) For help converting Human Times to UNIX epochs, visit [Epoch Converter](https://www.epochconverter.com/).


## Current Streams

### DAI Streams

| ID Number | Recipient         | Total Reward  | Start Date    | Cliff Date    | End Date      |
|-----------|-------------------|---------------|---------------|---------------|---------------|
| 1         | COM-001 MULTISIG  | 122,700.00    | 2021-08-31    | 2021-08-31    | 2021-12-31    |
| 2         | DAIF-001 WALLET   | 492,971.00    | 2021-09-30    | 2021-09-30    | 2022-08-31    |
| 3         | GOV-001 MULTISIG  | 123,333.00    | 2021-08-31    | 2021-08-31    | 2021-09-30    |
| 4         | GRO-001 MULTISIG  | 300,050.00    | 2021-08-31    | 2021-08-31    | 2021-10-31    |
| 5         | MKT-001 MULTISIG  | 103,134.00    | 2021-08-31    | 2021-08-31    | 2021-10-31    |
| 6         | ORA-001 MULTISIG  | 4,196,771.00  | 2021-08-31    | 2021-08-31    | 2022-06-30    |
| 7         | PE-001 MULTISIG   | 4,080,000.00  | 2021-08-31    | 2021-08-31    | 2022-04-30    |
| 8         | RISK-001 MULTISIG | 2,184,000.00  | 2021-08-31    | 2021-08-31    | 2022-08-31    |
| 9         | RWF-001 MULTISIG  | 620,000.00    | 2021-08-31    | 2021-08-31    | 2021-12-31    |
|   10      | GOV-001 MULTISIG  |   538,400.00  |   2021-09-30  |   2021-09-30  |   2022-03-30  |
|   11      |   SNE-001 WALLET  |   135,375.00  |   2021-09-30  |   2021-09-30  |   2021-12-30  |
|   12      |   SH-001 WALLET   |   58,000.00   |   2021-09-30  |   2021-09-30  |   2021-12-30  |

### MKR Streams

| ID Number | Recipient        | Total Reward | Start Date | Cliff Date | End Date   |
|-----------|------------------|--------------|------------|------------|------------|
| 1         | GRO-001 MULTISIG | 803.18       | 2021-06-30 | 2022-06-30 | 2022-06-30 |
| 2         | ORA-001 MULTISIG | 1051.25      | 2021-06-30 | 2022-06-30 | 2022-06-30 |
| 3         | 0xfDB9...78EdD   | 995          | 2021-04-30 | 2022-04-30 | 2025-04-29 |
| 4         | 0xBe4D...239C8   | 995          | 2021-04-30 | 2022-04-30 | 2025-04-29 |
| 5         | 0x58EA...fd7fc   | 995          | 2021-04-30 | 2022-04-30 | 2025-04-29 |
| 6         | 0xBAB4...0EcD5   | 995          | 2021-04-30 | 2022-04-30 | 2025-04-29 |
| 7         | 0xB5c8...B18dD   | 995          | 2021-04-30 | 2022-04-30 | 2025-04-29 |
| 8         | 0x780f...81b5b   | 995          | 2021-04-30 | 2022-04-30 | 2025-04-29 |
| 9         | 0x3436...D3284   | 995          | 2021-04-30 | 2022-04-30 | 2025-04-29 |
| 10        | 0x46E5...ec979   | 995          | 2021-04-30 | 2022-04-30 | 2025-04-29 |
| 11        | 0x18Ca...cb9FB   | 995          | 2021-04-30 | 2022-04-30 | 2025-04-29 |
| 12        | 0x301d...d9B25   | 995          | 2021-04-30 | 2022-04-30 | 2025-04-29 |
| 13        | 0xBFC4...D5d43   | 995          | 2021-04-30 | 2022-04-30 | 2025-04-29 |
| 14        | 0xcD16...fcF4a   | 995          | 2021-09-12 | 2022-09-12 | 2025-09-11 |
| 15        | 0x3189...30602   | 995          | 2021-06-20 | 2022-06-20 | 2025-06-19 |
| 16        | 0x29b3...442B6   | 995          | 2021-09-19 | 2022-09-19 | 2025-09-18 |

### Other Token Streams


