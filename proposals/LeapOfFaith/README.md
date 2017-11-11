# Leap of Faith

## Preamble

    Title: Leap of Faith
    Author: Alessio Delmonti
    Type: ER20 Saving token 
    Status: Draft, v0.1
    Created: 11 November 2017

## Stack

    Frontend: React + Web3 --> Metamask/Mist
    Backend: Solidity Smart Contracts
    Architecture: dApp hosted on IPFS + Mobile Apps
    Mobile App: React Native + Web3
    Blockchain: Ethereum
    Token: FHT
    
### Goals

Providing the possibility to lock up ether for beneficiary which will unlock upon certain condition.

The service need to act as trusted party to IRL indentification of the benificiary.

### Description

As a blockchain/cryptocurrency enthusiast I'm confident the price of ETH will go up in 5 to 20 years time, therefore I want to lock up some ether as an investiment for myself, my son, my nephew, my wife, scientific research, etc.

**Use cases:**
- As a father I want to lock up 5 ether for my new born.
- As a father I want to make sure: my son won't be able to unlock the ether before he is 21
- As a father I want to make sure: if my son lost his private key he can still unlock the funds.
- As a father I want to make sure: if the return of investment is +100x this condions are executed:
    1. Only 10% of ether gets unlocked at 21
    2. A passive income contracts release 1/100th of ether every month (PassiveIncome.sol)

>TODO: List other usecases

**Flow**

1. I deposit N eth to `LeapOfFaith.sol`
2. FHT Tokens will be issued when ETH are received into the contract.
3. 1% Fee is collected
4. Eth gets locked up until `RELEASE_TIMESTAMP`

**Scenario A, conditions:**

    * Sufficient time has passed to unlock the eth (TIMESTAMP >= RELEASE_TIMESTAMP)
    * Beneficiary has his private key (NO_AUTH_REQUIRED)
    * Tokens are sent to the beneficiary or a RealingStrategy contract is invoked if any (PassiveIncome, Donate, Speculation)

**Scenario B, conditions:**

    * Sufficient time has NOT passed to unlock the eth (TIMESTAMP < RELEASE_TIMESTAMP | INSTANT_WITHDRAW)
    * Depositor has his private key (NO_AUTH_REQUIRED)
    * 3% fee is payed for Immediate ETH withdrawal.
    * Tokens are sent back to the owner (depositor)

>TODO: Describe IRL indentification process

**Common rules**

1. For all Withdrawals: FHT tokens will be destroyed after withdrawal.
2. Eth Tokens pending normal withdrawal will be locked until explicit request.
3. While tokens are locked, they cannot be transferred or sent.
4. While tokens are locked, you cannot add more ETH to the address where the tokens are locked. (Or can you?)
5. If the Fee Pot is not empty, you will automatically claim a reward from the Fee Pot

6. *Optional* When claiming the reward from the Fee Pot (Complete Withdrawal), the following formula is used:
   - reward = feePot * v / totalSupply
7. *Optional* Where v is the amount you had when the withdrawal was requested,
8. *Optional* totalSupply is the total amount of tokens in circulation at the time when Complete Withdrawal was called.
9. *Optional* After withdrawal to ETH, tokens are burned, thus deflating the token supply.

**Game theory**

If enough holders enter the contract, Price of ETH should go up, because ETH is removed from the market.

Better than normal holding, since holders can claim from the fee-pot, after holding for the minimum time, 
Should the ETH price spike to say $500 USD, immediate withdraw will still be possible.

FHT tokens may be trade-able on an exchange, and on face value 1 FHT = 1 ETH, should an exchange add them.

Who is the bigger hodler? Basically the bigger the holder, the bigger chunk the reward they get, and yes, the risk is there that there could suddenly be a larger hodler than you coming in! (The reward is based in the Total Supply, and it will be increased when new ether is locked in, but also decreased in your favour if weak-hands use the quick withdraw)

### Budget

* Dev Time: 300h
* GAS to deposit contract
* Website
* UI / UX


### Uncertainties

- FHT token may not be necessary
- It's tricky to design an IRL indentification service completely decentralised.
