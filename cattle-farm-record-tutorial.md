## Tutorial: A Step-by-Step Guide to Building a Cattle Farm Record Smart Contract on CELO Alfajores

### Introduction
This article will guide you through the development of a smart contract for managing cattle farm records. Utilizing Solidity, the leading language for smart contracts, and the intuitive Remix IDE, we'll delve into the creation and deployment of a blockchain-driven social media platform.

The CattleFarmRecord contract is a Solidity smart contract that allows for the management of cattle farm records. It provides functionality for adding employees, creating cattle records, recording expenses, and retrieving farm data. This contract is designed to be owned by a single address, which has administrative privileges to manage the contract and authorize employees to perform certain actions.

### Prerequisites

Before proceeding, ensure you have the following:

- Basic understanding of Solidity programming language
- Celo testnet faucet [faucet](https://faucet.celo.org/alfajores)
- Access to Remix IDE [Remix](https://remix.ethereum.org).

 ### Explanation of data structures and variables
 ```solidity
// SPDX-License-Identifier: MIT
pragma solidity >0.8.0;

contract CattleFarmRecord {
    address public owner; // The owner of the contract
    struct employee{
        bool can_create_record;
        string name;
        string id_number;
        string other_employee_info;
        address employee_address;
        bool exists;
    } // A struct defining data of an employee
    mapping (address => employee) public employees; // The record of all the employees in memory
    address[] public employees_addresses; // The addresses of all the employees on the farm

    struct cattle_expenses {
        int amount;
        int date;
        string description_and_other_info;
    }
    mapping (int => cattle_expenses[]) cattle_expense_storage; // This will map the tagid number of each cattle expense cost
    struct cattle{
        int tagid;
        int date_stocked;
        int total_expenses;
        int number_of_expenses;
        string breed;
        string stocked_from;
        string other_descriptions;
        bool exists;
    }
    mapping (int => cattle) cattle_data_storage; // This will map the tagid number of each cattle 
    int[] cattle_ids; //This is an array containg the ids of all cattles on the farm
     constructor(){
        owner = msg.sender; //Setting the deployer of the contract as the owner
    }
  ```
The `owner` variable represents the address that owns the contract. Only the owner has the authority to perform administrative functions such as transferring ownership and adding employees.

The `employee struct` defines the data of an employee. It includes fields such as `can_create_record` (a boolean indicating if the employee can create farm records), `name`, `id_number`, `other_employee_info`, `employee_address`, and `exists` (a boolean indicating if the employee exists in the system).

The `employees mapping` stores the records of all the employees in memory. It maps an employee's address to their corresponding `employee struct`

The `cattle_expenses struct` represents the expenses incurred for a specific cattle. It includes fields such as `amount` (the expense amount), `date` (the date of the expense), and `description_and_other_info` (additional information about the expense).

The `cattle struct` represents the data of a cattle. It includes fields such as `tagid` (a unique identifier for the cattle), `date_stocked` (the date the cattle was stocked), `total_expenses` (the total expenses incurred for the cattle), `number_of_expenses` (the number of expenses recorded for the cattle), `breed`, `stocked_from`, `other_descriptions`, and `exists` (a boolean indicating if the cattle exists in the system).

The `cattle_data_storage` mapping stores the cattle data. It maps a cattle's `tagid` to its corresponding cattle struct.

The `cattle_ids` array contains the IDs of all the cattle on the farm. It is used to iterate over all the cattle records.

### Modifiers

```solidity
//Modifiers
    //Check if owner is the executional of this contract
    modifier is_owner{
        require(msg.sender == owner,"You are not the owner of this contract");
        _;
    }

    //Check if the caller of a function is an employee
    modifier is_employee_elegible{
        require((employees[msg.sender].exists && employees[msg.sender].can_create_record) || msg.sender == owner,"You are not authorized to perform this action");
        _;
    }
```
Modifiers ensure the reusability of authentications in multiple functions in the code.

The `is_owner` modifier checks if the sender of the transaction is the owner or an admin of the contract.

The `is_employee_elegible` modifier checks if the sender of the transaction is an employee or an admin of the smart contract.

### Admin functions
#### Transfer admin or contract ownership
```solidity
 //Change admin
    function transfer_admin(address _new_admin)public is_owner returns (bool){
        owner = _new_admin;
        return owner == _new_admin;
    }
```
