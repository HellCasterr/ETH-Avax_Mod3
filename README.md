# ETH_AVAX
# TYPES OF FUNCTIONS

In this code we are writing a smart contract for Social Rewards points.
## Description

In this contract, we create our own token and use different functions such as mint fucntion which can be used by the owner only, burn and transfer function can be used by any of the user. The contract has been tested and deployed using Remix IDE. The functionalities of the contract has been explained in this Loom video.

## Getting Started

### Executing program

    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;
    
    contract SocialPointsSystem {

    address public owner;
    string public contractName = "Social Points System";

    mapping(address => uint256) public socialPoints;
    mapping(address => bool) public hasVipBadge;

    constructor() {
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Only the owner can perform this action");
        _;
    }

    function minting(address recipient, uint256 points) public onlyOwner {
        require(recipient != address(0), "Invalid recipient address");
        require(points > 0, "Points to mint must be greater than 0");

        socialPoints[recipient] += points;
    }

    function transfer(address to, uint256 points) public {
        require(to != address(0), "Cannot transfer to the zero address");
        require(points > 0, "Points to transfer must be greater than 0");
        require(socialPoints[msg.sender] >= points, "Insufficient points");

        socialPoints[msg.sender] -= points;
        socialPoints[to] += points;
    }

    function spending(uint256 points) public {
        require(points > 0, "Points to spend must be greater than 0");
        require(socialPoints[msg.sender] >= points, "Insufficient points");

        socialPoints[msg.sender] -= points;
        hasVipBadge[msg.sender] = true; // Unlock VIP Badge feature
    }
}



To compile the code, press CRTL+ SHIFT+P  then select Solidity compile contract and the program is compile sucessfully will be shown in console 
## Authors

Bhomik Jain


## License

This project is licensed under the MIT License - see the LICENSE.md file for details
