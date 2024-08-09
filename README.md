# SWISSTRONIK Technical Task 5

Steps to a deploy private NFT

1. Clone repository
```shell
https://github.com/fung93/swisstronik-private-nft-task-5.git
```
```shell
cd swisstronik-private-nft-task-5
```
2. Install Dependency
```shell
npm install
```
3. Set .env File
```shell
PRIVATE_KEY="your private key"
```
4. Update Smart Contract (Skipp if you won't modify Token name)
- Open contracts folder
- Open PERC20Sample.sol file
- Feel free to modify token name and token symbol
```shell
// SPDX-License-Identifier: MIT
// Compatible with OpenZeppelin Contracts ^5.0.0
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/token/ERC721/extensions/ERC721Burnable.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract PrivateNFT is ERC721, ERC721Burnable, Ownable {
    constructor(address initialOwner)
        ERC721("FUNG","FNG")
        Ownable(initialOwner)
    {}

    function safeMint(address to, uint256 tokenId) public onlyOwner {
        _safeMint(to, tokenId);
    }

    function balanceOf(address owner) public view override returns (uint256) {
        require(msg.sender == owner, "PrivateNFT: msg.sender != owner");
        return super.balanceOf(owner);
    }

    function ownerOf(uint256 tokenId) public view override returns (address) {
        address owner = super.ownerOf(tokenId);
        require(msg.sender == owner, "PrivateNFT: msg.sender != owner");
        return owner;
    }

    function tokenURI(uint256 tokenId) public view override returns (string memory) {
        address owner = super.ownerOf(tokenId);
        require(msg.sender == owner, "PrivateNFT: msg.sender != owner");
        return super.tokenURI(tokenId);
    }
}
```
5. Compile Smart Contract
```shell
npm run compile
```
6. Deploy Smart Contract
```shell
npm run deploy
```
7. Mint Token
```shell
npm run mint
```
8. Transfer Token
9. Final
   - Copy the address and paste the address to testnet dashboard
   - Copy the transaction link to testnet dashboard
   - Push this project to your github and paste the repository link to testnet dashboard
