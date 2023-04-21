# BasicToken

BasicToken is an ERC20 token implementation that uses OpenZeppelin contracts. This token supports the following features:

- ERC20 standard functionalities
- Burnable tokens
- Pausable token

## Smart Contract

The smart contract code can be found in the `BasicToken.sol` file:

\```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";
import "@openzeppelin/contracts/security/Pausable.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract BasicToken is ERC20, ERC20Burnable, Pausable, Ownable {
    constructor(uint256 initialSupply) ERC20("Basic Token", "BT") {
        _mint(msg.sender, initialSupply);
    }

    function pause() public onlyOwner {
        _pause();
    }

    function unpause() public onlyOwner {
        _unpause();
    }

    function _beforeTokenTransfer(address from, address to, uint256 amount)
        internal
        whenNotPaused
        override
    {
        super._beforeTokenTransfer(from, to, amount);
    }
}
\```

To deploy this contract, you will need to compile and deploy it using a development environment like Truffle, Hardhat or Remix IDE.