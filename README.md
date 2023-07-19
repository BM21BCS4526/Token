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
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MyToken is ERC20, Ownable {
    constructor() ERC20("MyToken", "MTK") {
        _mint(msg.sender, 1000000 * 10**decimals());
    }

    function mint(address account, uint256 amount) public onlyOwner {
        _mint(account, amount);
    }

    function transfer(address recipient, uint256 amount) public override returns (bool) {
        _transfer(_msgSender(), recipient, amount);
        return true;
    }

    function burn(uint256 amount) public {
        _burn(_msgSender(), amount);
    }

    function burnFrom(address account, uint256 amount) public {
        uint256 currentAllowance = allowance(account, _msgSender());
        require(currentAllowance >= amount, "ERC20: burn amount exceeds allowance");
        _approve(account, _msgSender(), currentAllowance - amount);
        _burn(account, amount);
    }
}
**Author**
Baby Monal
