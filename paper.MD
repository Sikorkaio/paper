# Sikorka

Sikorka is an Ethereum based system that allows for deployment of decentralized blockchain contracts on locations in the real world.
This is achieved by a combination of hardware beacons, a mobile application and ethereum smart contracts. In the end any user can
deploy a contract on a specific real world location and accept transactions only from users who are physically present there.

## Components

Proving your location to the blockchain requires that you own a mobile phone equipped with bluetooth and optionally GPS. It also requires
that someone has installed a sikorka beacon in the area. Proving your location to a blockchain contract is called Proof Of Presence.
Once those requirements are in place anyone can deploy a contract at a physical location and have others interact with it.

### Proof Of Presence

Proof of Presence, abbreviated as `PoP` is the process of proving to a smart contract that you are indeed on a particular location at a
specific point in time. This is achieved in two different ways.

The main and most effective way is by making use of a hardware beacon which testifies that you are in that location on the given time.
The secondary method is to use the phone's GPS location along with a combination of challenge questions and answers, but that is definitely
not tamper-proof.

### Mobile Application

The Sikorka mobile app contains an ethereum light client so that it can synchronize with the ethereum network without any centralized
service. It allows the user to create an identity and associate it with an Ethereum account. The identity is local only to the Application,
but is used by the system in various way. Users are insentivized to have only 1 identity because they get rewarded for proper behaviour via
a reputation system.

The mobile app allows for:
 - Searching for nearby contracts
 - Interaction with nearby contracts
 - Deploying a contract
 - Installing a sikorka beacon

### End Users

An end user is anyone who has the mobile application installed in his phone.

### Builders

The term `builder` is used for the people who install beacons in real world locations. A builder can but does not necessarilly need to be the same
person who will deploy a contract at a real world location. Multiple contracts can be deployed in a location around a beacon.

A builder's responsibility is to obtain a beacon and set it in place on a location where it would be difficult to remove. Behind a brick, inside a wall,
on a whole in a tree and so forth. Additionally they should be checking on their beacons from time to time and if something is wrong or if the beacon is lost
they should deregister it from the system.

The builders get rewarded for their effort. Check the incentives section for more information. [TODO: Link].

### Contract Owners

The `contract owner` is anyone who deploys a sikorka contract on a location. In order to deploy a contract in a location the owner must himself go through
the Proof Of Presence process with a beacon. The owner has the option to use a more loose PoP method to deploy the contract as desribed here[TODO: Link] .
If the owner of the contract did not use a beacon to deploy it then the users will also be able to skip the beacon verification. That should only be done for
contracts that deal with insignificant amounts of money as it is **not safe**.

## Sikorka Smart Contracts

### Registry

The sikorka registry allows you to query for contracts around a specific location. It contains a data structure mapping coordinates to contracts.
It is also with this contract that newly deployed sikorka smart contracts get registered with when created.

### BasicInterface

All contracts must implement this interface to be considered sikorka contracts.

### BeaconRegistry

The sikorka beacon registry contract allows a builder to register a beacon in an exact location.

### BeaconDeed

The BeaconDeed contract is a very simple contract containing the deployment deposit for a beacon.

## Incentives

### Builders

The builders should not lie about the location they deployed the beacon at. To prevent that, each beacon deployment also requires a deposit of X amount
of ETH held in a Deed contract. If a builder's beacon location is challenged we are going through a dispute resolution mechanism which could cost the builder
his deposit.

At the same time, the builders should be rewarded for their efforts. This is achieved by the Proof Of Presence modifier in the Sikorka BasicInterface that all sikorka
contracts must implement. If a contract uses a beacon for proof of presence a tiny amount of ether is sent to the builder who deployed it.

### Contract Owners

The users who have also deployed contracts are the contract owners. They use the beacons deployed by the builders to provide proof of presence to their end users.
They pay for this service by having an amount of ETH in the contract that is used as payment each time a beacon is used.

### End users

The end users are those who interact with sikorka deployed contracts. They can't lie about their location since it's determined by the proximity to the beacon.

They can also make sure that the builders don't lie about the location of a beacon. If they are in the exact location of a beacon and can't interact with it then
they can start a dispute with the builder for that beacon.

## Reputation

Sikorka Reputation is what helps the system grow, develop the network effect and for leaders to rise in the user communities. It also
helps in the process of dispute resolution. The rules are the following:

- Each time you succesfully interact with a beacon and get proof of presence proved to a smart contract you get X reputation.
- Each time you deploy and register a beacon you get Y reputation.
- Each time you deploy a contract and register it at a specific location with a beacon you get Z reputation

## Dispute Resolution

A dispute can happen if a user challenges the location of a beacon registered by a builder. To do that the user deposits an amount of ETH equal to the deposit of the
beacon deed stating a challenge to the builder.

From that point on and for a number of blocks the challenging period begins. Any users who have previously used a sikorka contract in the greater vicinity are eligible
to vote on the dispute resolution. The votes of users are weighed by their reputation.

The deposit of the loser of the dispute gets distributed in the following way:
- 50% to the counterparty (challenger if the builder lost, and the builder if the challenger loses)
- The remaining 50% is divided equally between all the people who voted in favour of the winner of the dispute.

