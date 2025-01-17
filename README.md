# assignment3 Alisher Mukhamedov, Yerkanat Manasov

![Yoshi](https://github.com/user-attachments/assets/e5a8ee47-b247-4602-a5ae-0b9e38fd8505)




In this task, we created a custom ERC-20 token using Solidity and deployed it on a test blockchain. We followed these steps:

ERC-20 Token Creation:

Built an ERC-20 token contract named <University_name_your_Group_name> (e.g., UniversityGroupToken).
Set the initial supply to 2000 tokens.
The token was deployed to the contract creator's address.
Implemented Required Functions:

Transaction Logging: Added a function to log details of token transfers, including the sender, receiver, amount, and timestamp.
Timestamp Retrieval: Created a function to retrieve the timestamp of the most recent transaction in a human-readable format.
Sender & Receiver Address: Implemented functions to retrieve the sender's and receiver's addresses for any transaction.
Test and Deployment:

Tested the contract using Remix and Ganache locally.
Successfully deployed the contract on a public testnet (e.g., Goerli) using MetaMask to handle transactions.
Outcome
The ERC-20 token was successfully deployed with all required features and tested on a public testnet.
All the required functions to interact with the token and log transactions were implemented and verified.


![5211135961596033773](https://github.com/user-attachments/assets/d9b229d3-3165-4956-bf46-5efabd90f617)
![5211135961596033772](https://github.com/user-attachments/assets/351362ce-8130-4448-b691-b2351a60d790)
![5211135961596033771](https://github.com/user-attachments/assets/6fbe2892-fdf8-42f8-99ea-08d5919cecba)
![5211135961596033774](https://github.com/user-attachments/assets/f9a74247-3e9b-4e4d-9ceb-abf1263ab3f0)
![5211135961596033775](https://github.com/user-attachments/assets/f5b14548-0f77-43d2-a15d-fa277fb2e257)







// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import {ERC20} from "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import {ERC20Permit} from "@openzeppelin/contracts/token/ERC20/extensions/ERC20Permit.sol";


contract UniversityGroupToken is ERC20 {
    // Events for logging transactions
    event TransactionInfo(address indexed sender, address indexed receiver, uint256 value, uint256 timestamp);

    uint256 public latestTransactionTimestamp; // Last transaction timestamp

    // Constructor to initialize token
    constructor() ERC20("<University_name_your_Group_name>", "UGT") {
        _mint(msg.sender, 2000 * 10 ** decimals()); // Initial supply of 2000 tokens
    }

    // Function to log transaction information and update timestamp
    function logTransaction(address receiver, uint256 amount) public {
        _transfer(msg.sender, receiver, amount);
        latestTransactionTimestamp = block.timestamp;
        emit TransactionInfo(msg.sender, receiver, amount, block.timestamp);
    }

    // Function to retrieve the latest transaction timestamp
    function getLatestTransactionTimestamp() public view returns (uint256) {
        return latestTransactionTimestamp;
    }

    // Function to retrieve the address of the transaction sender
    function getTransactionSender() public view returns (address) {
        return msg.sender; // Use msg.sender instead of tx.origin
    }

    // Internal utility to convert uint256 to string
    function uint2str(uint256 _i) internal pure returns (string memory) {
        if (_i == 0) {
            return "0";
        }
        uint256 j = _i;
        uint256 len;
        while (j != 0) {
            len++;
            j /= 10;
        }
        bytes memory bstr = new bytes(len);
        uint256 k = len;
        while (_i != 0) {
            k = k - 1;
            uint8 temp = (48 + uint8(_i - (_i / 10) * 10));
            bytes1 b1 = bytes1(temp);
            bstr[k] = b1;
            _i /= 10;
        }
        return string(bstr);
    }
}
