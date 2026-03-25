# Fundraiser
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Fundraiser {
    address public owner;
    uint256 public goal;
    uint256 public totalRaised;

    constructor(uint256 _goal) {
        owner = msg.sender;
        goal = _goal;
    }

    function donate() public payable {
        totalRaised += msg.value;
    }

    function withdraw() public {
        require(msg.sender == owner, "Only owner");
        require(totalRaised >= goal, "Goal not reached");
        payable(owner).transfer(address(this).balance);
    }
}
