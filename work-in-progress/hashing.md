# Hashing Proposals 

In the Governance Process, all copy for Polls and Executive Proposals is hashed to verify their validity. This gives MKR Voters the ability to confirm that the contents displayed on the [Voting Portal](https://vote.makerdao.com/) are the same contained in the onchain code. With Governance proposals requiring a high degree of coordination, taking the hash of a proposal is one way to verify its validity. 

## Why hashing? 

Hash functions are one of the core cryptographic tools that make work on the blockchain possible. Hashes are particularly useful for verification as the same data will always produce the same hash, but the resulting hash cannot be used to reverse engineer the original data.

However, this one-way relationship between the data and the hash is only protected when the data is unique. Hash databanks for common phrases are used in password attacks, but given that even the slightest change to the input data results in a wildly different hash, the technology allows users to verify that the data they are viewing is exactly the same as advertised. 

Another common use of hash functions is to verify downloaded files. A user can get the expected hash of a file from a trusted source and run a hash algorithm on the file to ensure it has not been tampered with before opening. Likewise, any onchain proposal can have its hash verified before MKR holders submit their vote.

## How are proposals hashed?

MakerDAO uses the Keccak256 hash function to generate hashes for the Executive Proposals. This is the hashing function that the Ethereum blockchain uses internally, but since we are just displaying the hash onchain any function could have been chosen.

For polls, MakerDAO utilizes IPFS Hash. As long as the end-user knows what hashing algorithm has been used, they can independently verify the contents. 

The process for Polls and Executives varies slightly, but both depend on the [MakerDAO Community Repo](https://github.com/makerdao/community). The contents from a specific commit make up the hash, and as long as the correct commit is used to compare to the hash onchain the same result will be returned.

### Executive Process

Executive Proposals are slightly more difficult to verify as the hashed version will not be the most recent commit by nature of the workflow. 

This is because the spell address is added to the copy of every Executive Proposal in the GitHub Repo, but this can only be done once the hash of the copy has been generated and added to the code.

As a result, the hash the appears in the code of an executive proposal is generated from the last GitHub commit before the Spell Address is added into the copy.

This is the hash that will appear in the code of any Governance-sanctioned Executive Proposal. Since any changes, no matter how slight, will completely change the resulting hash function, coordination takes place between Governance and Spell-crafters so the onchain proposal contains the hash of the executive copy that is displayed on the voting portal.

### Polling Process

Hashing for onchain-polls is a simpler process. When a poll is created through the voting portal, it is submitted onchain and hashed automatically through the [front end code](https://github.com/makerdao/governance-portal-v2/blob/bf8c8008e21e76e6c48ad052477aeda142b985f6/pages/polling/create.tsx). This code sends the information to the Log of the poll creation, and can be viewed on Etherscan.

![image](https://user-images.githubusercontent.com/75535017/141056352-823c1e49-ad3e-4c8e-a2c5-de7c08f99798.png)
*A poll example showing the data transmitted onchain.*


## How can the hashes be verified?

For an in-depth view on how to verrify Executive Proposals, please see [$insert-page-link-here]().

For onchain polls, users have a variety of options. IPFS uses [multihash](https://github.com/multiformats/multihash), so users could add any of the linked repositories to their local environment and run the hash algorithm. This output would be compared to the Log of the transaction for the specific poll. 
