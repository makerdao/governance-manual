# Hashing Proposals 

In the Governance Process, all copy for Polls and Executive Proposals are hashed to verify their validity. This gives MKR Voters the ability to confirm the contents they see displayed on the [Voting Portal](https://vote.makerdao.com/) are the same contained in the onchain code.

## Why hashing? 

Hash functions are one of the core cryptographic tools that make our work on the blockchain possible. Hashes are particularly useful for verification as the same data will always produce the same hash, but the resuting hash cannot be used to reverse engineer the orginal data.

Worth noting this one-way relationship between the data and the hash is only protected when the data is unique. Hash databanks for common phrases are used in password attacks, but given that even the slightest change to the input data results in a wildly different hash the technology allows users to verify that data they are viewing is exactly the same as advertised. 

## How are proposals hashed?

Maker uses the Keccak256 hash function to generate hashes for the Executive and Poll copy. This is the hashing function that the Ethereum blockchain uses internally, but since we are just displaying the hash onchain any function could have been chosen.

The process for Polls and Executives varries slightly, but both depend on the [MakerDAO Community Repo](https://github.com/makerdao/community). The contents from a specific commit make up the hash, and as long as the correct commit is used to compare to the hash onchain the same result will be returned.

### Executive Process

Executive Proposals are slightly more difficult to verify as the hashed version will not be the most recent commit by nature of the work flow. 

This is becasue the spell address is added to the copy of every Executive Proposal in the GitHub Repo, but this can only be done once the hash of the copy has been generated and added to the code.

As a result, the hash the appears in the code of an executive proposal is generated from the last GitHub commit before the Spell Address is added into the copy. 

### Polling Process

## How can the hashes be verrified?

### Verifying Executive Hashes

### Verifying Polling Hashes
