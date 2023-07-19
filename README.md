**Token Creation**
This Solidity program is for creating tokens on a hardhat network and connecting remix with our contract so to mint the tokens. 

**Description**
In this smart contract program, we are creating a custom token using ERC20.In order to create an ERC20 token,  the following information is needed:

The Token’s Name
The Token’s Symbol
The Token’s Decimal Places
The Total Number of Tokens in Circulation

**Getting Started
Executing program**
To run this program, you can use Remix, an online Solidity IDE. 
//SPDX-License-Identifier: UNLICENSED

pragma solidity ^0.8.9;

import "hardhat/console.sol";



contract Token {
    
    string public name = "My Hardhat Token";
    string public symbol = "MHT";
    uint256 public totalSupply = 1000000;
    address public owner;
    mapping(address => uint256) balances;

    event Transfer(address indexed _from, address indexed _to, uint256 _value);

    constructor() {
        
        balances[msg.sender] = totalSupply;
        owner = msg.sender;
    }
    function transfer(address to, uint256 amount) external {
       
        require(balances[msg.sender] >= amount, "Not enough tokens");

        console.log(
            "Transferring from %s to %s %s tokens",
            msg.sender,
            to,
            amount
        );
        balances[msg.sender] -= amount;
        balances[to] += amount;

        emit Transfer(msg.sender, to, amount);
    }

    function balanceOf(address account) external view returns (uint256) {
        return balances[account];
    }
}
**Author**
Baby Monal
