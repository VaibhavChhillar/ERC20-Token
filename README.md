# Types of Functions - ETH + AVAX
A smart contract to create your own ERC20 token and deploy it using HardHat or Remix

## DESCRIPTION
Written in Solidity, a programming language used to create smart contracts on the Ethereum blockchain, this program is a straightforward contract. The following are the functions of the contract:
1. the contract owner can mint tokens to a provided address and 
2. They can burn tokens.
3. They can transfer tokens.

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., HelloWorld.sol). Copy and paste the code from contract.sol file into your file:

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to latest solidity version (or another compatible version), and then click on the "Compile" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the your contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with it by calling the requireInstance, assertInstance and revertInstance function.
# SOURCE CODE

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract Token is ERC20, Ownable(msg.sender) {
    constructor() ERC20("Degen", "DGN") {}

    // Store item structure
    struct StoreItem {
        string itemName;
        uint256 price;
    }

    // Store items list
    StoreItem[] public storeItems;

    // Add store items (onlyOwner)
    function addStoreItem(string memory itemName, uint256 price) external onlyOwner {
        storeItems.push(StoreItem(itemName, price));
    }

    // Mint new tokens and distribute them to players as rewards. Only the owner can do this.
    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }

    // Transfer tokens from the sender's account to another account.
    function transferTokens(address to, uint256 amount) external {
        require(balanceOf(msg.sender) >= amount, "Don't have enough Degen Tokens");
        _transfer(msg.sender, to, amount);
    }

    // Anyone can burn their own tokens that are no longer needed.
    function burn(uint256 amount) public virtual {
        _burn(msg.sender, amount);
    }
}

contract StoreInitializer {
    // Deploy the DegenToken contract and add examples to storeItems
    constructor() {
        Token token = new Token();

        // Add examples to storeItems
        token.addStoreItem("Epic Sword of Valor", 100);
        token.addStoreItem("Mystic Potion of Power", 50);
        token.addStoreItem("Legendary Shield of Fortitude", 200);
    }
}

## Authors
vaibhav chhillar 
vaicozcchillar@gmail.com

## License

This project is licensed under the MIT License - see the LICENSE.md file for details
