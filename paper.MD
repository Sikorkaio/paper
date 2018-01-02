# Sikorka

Sikorka is an Ethereum based system that allows for deployment of decentralized blockchain contracts on locations in the real world. This is achieved by a combination of hardware beacons, a mobile application and ethereum smart contracts. In the end any user can deploy a contract on a specific real world location and accept transactions only from users who are physically present there.

## Components of the Network

Proving your location to the blockchain requires that you own a mobile phone equipped with bluetooth and GPS. It also requires that someone has installed a sikorka beacon in the area. Proving your location to a blockchain contract is called Proof Of Presence. Once those requirements are in place anyone can deploy a contract at a physical location and have others interact with it.

### Proof Of Presence

Proof of Presence, abbreviated as `PoP` is the process of proving to a smart contract that you are indeed on a particular location at a specific point in time. This is achieved by utilizing a hardware beacon that can assert to smart contracts that you are indeed in a particular physical location at a certain point in time.


### Mobile Application

The Sikorka mobile app runs an ethereum light client so that it can synchronize with the ethereum network without relying on any centralized services. It allows the user to create an identity and associate it with an Ethereum account. The identity is local only to the Application, but is used by the system in various ways. Users are incentivized to have only 1 identity because they get rewarded for proper behaviour via a reputation system.

The mobile app allows for:
 - Searching for nearby contracts
 - Interaction with nearby contracts
 - Deploying a contract
 - Installing a sikorka beacon

### End Users

An end user is anyone who has the mobile application installed in his phone.

### Builders

The term `builder` is used for the people who install beacons in real world locations. A builder can but does not necessarilly need to be the same person who will deploy a contract at a real world location. Multiple contracts can be deployed in a location around a beacon.

A builder's responsibility is to obtain a beacon and set it in place on a location where it would be difficult to remove. Behind a brick, inside a wall, on a whole in a tree and so forth. Additionally they should be checking on their beacons from time to time and if something is wrong or if the beacon is lost they should deregister it from the system.

The builders get rewarded for their effort. Check the incentives section for more information. [TODO: Link].

### Contract Owners

The `contract owner` is anyone who deploys a sikorka contract on a location. In order to deploy a contract in a location the owner must himself go through the Proof Of Presence process with a beacon. 

## Sikorka Smart Contracts

Following is a list of the smart contracts involved in the sikorka network.

### Registry

The sikorka registry allows you to query for contracts around a specific location. It contains a data structure mapping coordinates to contracts. It is also with this contract that newly deployed sikorka smart contracts get registered with when created.

### BasicInterface

All contracts must implement this interface to be considered sikorka contracts.

### Reputation

The reputation contract is the contracts that tracks the sikorka reputation token.

### BeaconRegistry

The sikorka beacon registry contract allows a builder to register a beacon in an exact location.

### BeaconDeed

The BeaconDeed contract is a very simple contract containing the deployment deposit for a beacon.

## Reputation

Sikorka Reputation is what helps the system grow, develop the network effect and for leaders to rise in the user communities. It also helps in weeding out malicious actors from the network. Reputation is essentially an ethereum token. You will need to use it in various parts of interacting with the network and doing so burns it. For more information take a look at the Incentives section.

You can earn it in the following ways.

### As a user

- When you interact with a contract and prove your presence via a beacon you earn `X` reputation.
- A contract owner can scan the user's phone and give him `10X` reputation only once every month. This is the most valuable form of reputation a user can earn because it's done by human verifiers.

### As a builder

- Whenever your beacon gets used for proving a user's presence you get `Y` reputation.

### As a contract owner

- Whenever users interact with your contract after having proved their presence you earn `Z` reputation.

### The development team

At least in the beginning the team can mint any amount of tokens for themselves and give it out to the first people who run the pilot program. Trust in the team is required here. Look at the Incentives section for more information. Once the network is up and running and pilot program proves succesful then this may be removed from the contract or kept only to provide reputation to people who buy beacons made by the team.


## Incentives

In this section we look at all the different actors that take the stage in the sikorka platform and analyze their incentives.

### Builders

- The builders should not lie about the location they deployed the beacon at.
- Builders should get rewarded for deploying and maintaining a beacon.
- Builders should not deploy beacons where other beacons are already deployed. A healthy network needs beacons
  spread over a large area.

In order to stop builders from lying about the location of their beacon, we give to users the ability to report malicious beacons. Reporting costs at least D amount of reputation. This amount of reputation is burned both for the user and for the deployer of the beacon. The deployer of the beacon also stands to lose his ETH deposit. As soon as his beacon's reputation reaches 0 then the deposited ETH is lost for him and is distributed to the reporter's depending on the reputation they burned in order to report it.

In the happy scenario the builders should be rewarded for their efforts. This is achieved by the Proof Of Presence modifier in the Sikorka BasicInterface that all sikorka contracts must implement. If a contract uses a beacon for proof of presence a tiny amount of ether is sent to the builder of the beacon.

TODO: Should that amount be editable by the beacon's builder? What should the amount be?

(If a beacon is already deployed in a location then the deployment should not be allowed. This could be enforced in the smart contract side .. with a bit of work. Perhaps. Needs more thinking)

### Contract Owners

- The contract owners need accurate location reporting for their users as they rely on that for the contract
to operate succesfully

The users who have also deployed contracts are the contract owners. They use the beacons deployed by the builders to provide proof of presence to their end users. They pay for this service by having an amount of ETH in the contract that is used as payment each time a beacon is used.

### End users

- End users should not lie about their location when reporting malicious beacons.
- End users should use the system truthfully and not try to spoof their address

The end users are those who interact with sikorka deployed contracts. They can't lie about their location since it's determined by the proximity to the beacon, if we assume that beacons are truthfull.

They can also make sure that the builders don't lie about the location of a beacon. If they are in the exact location of a beacon and can't interact with it then they can report the beacon as explained above.

Whenever users utilize the system truthfully then they are rewarded. That means that if a user interacts with a contract's function that requires proof of presence using a physical beacon then the user also gains E reputation.

### Sikorka Development Team

- The development team needs to foster the growth and adoption of the sikorka network.
- The development team needs to have enough funds for the day to day operations, research&development, hardware costs.

The development of sikorka also needs to be funded somehow and for this reason all sikorka enabled contracts pay a very small fee `F` into the development wallet for each time they utilize the sikorka network. This fee is changeable and can be changed by the development multisig. It is in the best interests of the sikorka development team to have a healthy network and for many people to create sikorka contracts. For that reason the fee should be reasonably low and also changeable depending on the price of ETH.

The development multisig also controls the sikorka ENS subregistrar. This is how the address of the sikorka registry, the sikorka reputation and all other contracts is determined and this is how upgrades to the contracts will happen.

The above 2 points require some trust in the development team. That is just how this system will work in the beginning. This can evolve though and users of the system with high enough reputation could be getting a vote in all network governance related matters.

