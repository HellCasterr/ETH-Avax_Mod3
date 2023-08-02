# ETH_AVAX
# TYPES OF FUNCTIONS

In this code we are writing a smart contract for Class Representive Voting.
## Description

In this contract, we create our own token and use different functions such as mint fucntion which can be used by the owner only, burn and transfer function can be used by any of the user. The contract has been tested and deployed using Remix IDE. The functionalities of the contract has been explained in this Loom video.

## Getting Started

### Executing program

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract ClassRepresentativeVoting {
    address public owner;
    uint256 public totalCandidates;
    uint256 public totalVoters;
    bool public votingEnded;

    struct Candidate {
        string name;
        uint256 voteCount;
    }

    mapping(uint256 => Candidate) public candidates;
    mapping(address => bool) public voters;

    event Voted(address indexed voter, uint256 indexed candidateIndex);

    modifier onlyOwner() {
        require(msg.sender == owner, "Only the contract owner can perform this action");
        _;
    }

    modifier notEnded() {
        require(!votingEnded, "Voting has ended");
        _;
    }

    constructor(string[] memory _candidateNames) {
        owner = msg.sender;
        totalCandidates = _candidateNames.length;

        for (uint256 i = 0; i < totalCandidates; i++) {
            candidates[i] = Candidate(_candidateNames[i], 0);
        }
    }

    function vote(uint256 _candidateIndex) external notEnded {
        require(_candidateIndex < totalCandidates, "Invalid candidate index");
        require(!voters[msg.sender], "You have already voted");

        candidates[_candidateIndex].voteCount++;
        voters[msg.sender] = true;
        totalVoters++;

        emit Voted(msg.sender, _candidateIndex);
    }

    function endVoting() external onlyOwner notEnded {
        votingEnded = true;
    }

    function getCandidateVoteCount(uint256 _candidateIndex) external view returns (uint256) {
        require(_candidateIndex < totalCandidates, "Invalid candidate index");
        return candidates[_candidateIndex].voteCount;
    }
}


To compile the code, press CRTL+ SHIFT+P  then select Solidity compile contract and the program is compile sucessfully will be shown in console 
## Authors

Bhomik Jain


## License

This project is licensed under the MIT License - see the LICENSE.md file for details
