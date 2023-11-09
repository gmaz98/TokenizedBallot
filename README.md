# Tokenized Voting DApp

## Overview

This decentralized application (DApp) allows users to participate in a tokenized voting system. The DApp consists of two smart contracts: **MyToken** and **TokenizedBallot**. The MyToken contract is an ERC-20 token with voting capabilities, and the TokenizedBallot contract facilitates token-based voting on proposals.

## Smart Contracts

### 1. MyToken

- An ERC-20 token with added features from OpenZeppelin libraries.
- Implements roles for the admin and minter roles.
- Allows minting of tokens by the designated minter.

### 2. TokenizedBallot

- Manages a voting system with token-based participation.
- Users can vote on proposals using voting tokens from the MyToken contract.
- The voting power is determined by the token holdings at a specific block.
- Proposals are created with associated names, and users can vote on them.

## Usage

### 1. Deploy Contracts

- Deploy the MyToken contract to create a new ERC-20 token.
- Deploy the TokenizedBallot contract, specifying the proposal names, the MyToken contract address, and the duration in blocks.

### 2. Mint Tokens

- As the admin (chairperson), mint tokens using the `mint` function in the MyToken contract.
- Grant voting rights using the `giveRightToVote` function.

### 3. Vote on Proposals

- Users can vote on proposals using the `vote` function in the TokenizedBallot contract.
- The voting power is determined by the token holdings at a specific block.
- Users cannot vote more than their available voting power.

### 4. Determine Winners

- Use the `winningProposal` and `winnerName` functions in the TokenizedBallot contract to determine the winning proposal.

### 5. List Proposals

- Retrieve the list of proposals using the `listProposal` function.

## Security Considerations

- Ensure that the admin (chairperson) is a trusted address.
- Users should be aware of the duration of the voting period and the block at which voting power is calculated.

## Example Deployment and Usage

```solidity
// Deploy MyToken contract
MyToken myToken = new MyToken();
// Mint tokens and grant voting rights
myToken.mint(address1, 100);
myToken.giveRightToVote(address1);

// Deploy TokenizedBallot contract
TokenizedBallot ballot = new TokenizedBallot(["Proposal A", "Proposal B"], myToken, 100);

// Users vote on proposals
ballot.vote(0, 50, {from: address1});
ballot.vote(1, 30, {from: address2});

// Determine winners
bytes32 winningProposal = ballot.winnerName();
