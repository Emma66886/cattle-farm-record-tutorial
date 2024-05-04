## Tutorial: A Step-by-Step Guide to Building a Cattle Farm Record Smart Contract on CELO Alfajores

## Table of content
1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Explanation of data structures and variables](#explanation-of-data-structures-and-variables)
4. [Modifiers](#modifiers)
5. [Admin functions](#admin-functions)
6. [Employees functions](#employees-functions)
7. [The update functions](#the-update-functions)
8. [The Get functions](#the-get-functions)
9. [Complete Code](#complete-code)
10. [Setting up Remix for CELO Alfajores](#setting-up-remix-for-celo-alfajores)

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
 //Admin or owner functions
 //Change admin
    function transfer_admin(address _new_admin)public is_owner returns (bool){
        owner = _new_admin;
        return owner == _new_admin;
    }
```
The `transfer_admin` function takes the new admin wallet address as a parameter as `_new_adminn`, `is_owner` modifier is added to ensure only the owner of the contract can perform this action.

#### Add Employee function
```solidity
//Add an employee
    function add_employee(
        bool _can_create_record,
        string memory _name,
        string memory _id_number,
        string memory _other_employee_info,
        address _employee_address)public is_owner returns(employee memory){
        require(!employees[_employee_address].exists,"Employee already exist");
        employees[_employee_address] = employee({
        can_create_record:_can_create_record,
         name:_name,
         id_number:_id_number,
         other_employee_info:_other_employee_info,
         employee_address:_employee_address,
         exists:true
        });
        employees_addresses.push(_employee_address);
        return employees[_employee_address];
    }
```
This function allows the contract owner to add an employee to the system. The function takes in the employee's details such as `can_create_record` (a boolean indicating if the employee can create farm records), `name`, `id_number`, `other_employee_info`, and `employee_address`. It checks if the employee already exists and then adds the employee to the `employees mapping` and `employees_addresses array`.

#### Function to reset an employee's ability
```solidity
    // reset employee's ability to create farm record
    function revoke_employee_authority(bool _can_create_record,address _employee)public is_owner returns(bool) {
        require(employees[_employee].exists,"This employee does not exist");
        employees[_employee].can_create_record = _can_create_record;
        return employees[_employee].can_create_record == _can_create_record;
    }
```
This function takes `_can_create_record` which is a boolean value(true or false) and the wallet address of the employee as a parameter and sets the employee's state

### Employees functions
#### Function to Create cattle farm record
```solidity
    //Create a Cattle farm record
    function create_cattle_record(
        int tagid,
        int date_stocked,
        string memory breed,
        string memory stocked_from,
        string memory other_descriptions
    ) public is_employee_elegible returns(cattle memory){
        require(!cattle_data_storage[tagid].exists,"Cattle already exist");
        cattle_data_storage[tagid] = cattle({
            tagid:tagid,
            date_stocked:date_stocked,
            total_expenses:0,
            number_of_expenses:0,
            breed:breed,
            stocked_from:stocked_from,
            other_descriptions:other_descriptions,
            exists:true
        });
        cattle_ids.push(tagid);
    return cattle_data_storage[tagid];
    }
```
This function allows an eligible employee to create a cattle record. The function takes in the cattle's details such as `tagid`, `date_stocked`, `breed`, `stocked_from`, and `other_descriptions`. It checks if the cattle already exists and then creates a new cattle record in the `cattle_data_storage mapping` and adds the `tagid` to the `cattle_ids array`.


#### Function to create an expense
```solidity
    //create an expense
    function create_an_expense(int tagid,
        int amount,
        int date,
        string memory description_and_other_info)public is_employee_elegible returns(cattle_expenses memory){
        require(cattle_data_storage[tagid].exists,"Cattle does not exist or has not been recorded");
        cattle memory current_cattle = cattle_data_storage[tagid];
        cattle_expense_storage[tagid].push(cattle_expenses({
             amount:amount,
         date:date,
         description_and_other_info:description_and_other_info
        }));
        current_cattle.total_expenses += amount;
        current_cattle.number_of_expenses += 1;
        cattle_data_storage[tagid] = current_cattle;
        return cattle_expense_storage[tagid][uint(current_cattle.number_of_expenses)];
    }
```
This function allows an eligible employee to record an expense for a specific cattle. The function takes in the `tagid` of the cattle, `amount`, `date`, and `description_and_other_info` of the `expense`. It checks if the cattle exists and then adds the expense to the `cattle_expense_storage mapping`. It also updates the total expenses and number of expenses for the cattle.

### The update functions
```solidity
  //Update functions
        function update_cattle_record(
        int tagid,
        int date_stocked,
        string memory breed,
        string memory stocked_from,
        string memory other_descriptions
    ) public is_employee_elegible returns(cattle memory){
        require(cattle_data_storage[tagid].exists,"Cattle deos not exist");
        cattle_data_storage[tagid] = cattle({
            tagid:tagid,
            date_stocked:date_stocked,
            total_expenses:0,
            number_of_expenses:0,
            breed:breed,
            stocked_from:stocked_from,
            other_descriptions:other_descriptions,
            exists:true
        });
    return cattle_data_storage[tagid];
    }

    //Update a cattle expense
        function update_an_expense(int tagid,
        int amount,
        int date,
        uint index,
        string memory description_and_other_info)public is_employee_elegible returns(cattle_expenses memory){
        require(cattle_data_storage[tagid].exists,"Cattle does not exist or has not been recorded"); // Ensure cattle is created in the cattle data storage
        require(cattle_expense_storage[tagid].length > 0,"No expense record found for this cattle"); // Ensures tagid is valid
        require((cattle_expense_storage[tagid].length - 1) >= index,"Index out of range"); // Ensures the index 
        cattle memory current_cattle = cattle_data_storage[tagid];
        current_cattle.total_expenses -= cattle_expense_storage[tagid][index].amount;
        current_cattle.total_expenses += amount;
        cattle_expense_storage[tagid][index] = (cattle_expenses({
             amount:amount,
         date:date,
         description_and_other_info:description_and_other_info
        }));
        cattle_data_storage[tagid] = current_cattle;
        return cattle_expense_storage[tagid][index];
    }
```
These functions allow users to be able to update data for expenses on each cattle and also the data of each cattle.
The `update_cattle_record` performs the function to update the cattle record, It takes the same parameters as the `cattle struct`,it has `require` function that ensures the tag id of the cattle is available before it can be updated.

The `update_an_expense` acts to update expenses on each cattle.

### The Get functions
```solidity
//Get functions
    //get all the employees
    function get_all_employees()public view returns(employee[] memory){
        employee[] memory local_employee_data;
        for (uint i =0; i < employees_addresses.length; i++) 
        {
            local_employee_data[i] = (employees[employees_addresses[i]]);
        }
        return local_employee_data;
    }

    // Get total farm expenses on all cattle
    struct TotalfarmExpenses{
        int total_amount; // this represents the total amount of money in the expense
        cattle_expenses[] farm_expense; // this represent the array containing each expense
    } // This struct represents the data type to be returned back to the user upon request

    // Get all the farm expenses
    function get_total_farm_expenses()public view returns(TotalfarmExpenses memory){
        cattle_expenses[] memory local_cattle_expenses; // defining a local type of the cattle expenses array
        int total_amount = 0;
        uint counter =0; // total count of all the expenses
        for (uint i = 0; i < cattle_ids.length; i++) 
        {
            for (uint j = 0; j < cattle_expense_storage[int(i)].length; j++) 
            {
                local_cattle_expenses[counter] = cattle_expense_storage[int(i)][j]; // getting the each cattle expense and adding it to the local defined variable local_cattle_expenses
                total_amount += local_cattle_expenses[counter].amount; // calculating and adding the total amount spent in total
                counter++;
            }
        }
        return TotalfarmExpenses({
            total_amount:total_amount,
            farm_expense:local_cattle_expenses
        });
    }
```

The `get_all_employees` gets all the employees on the farm and returns their details to the caller. Note that this is a `view` function, the view here enables users to be able to get data from the blockchain.

The `get_total_farm_expenses` get all the expenses in total from the farm.

### Complete Code
This is the complete code for this cattle farm record contract.
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract CattleFarmRecord {
    address public owner; // The owner of the contract
    
    struct Employee {
        bool canCreateRecord;
        string name;
        string idNumber;
        string otherEmployeeInfo;
        bool exists;
    } // A struct defining data of an employee
    
    mapping (address => Employee) public employees; // The record of all the employees in memory
    
    struct CattleExpense {
        uint256 amount;
        uint256 date;
        string descriptionAndOtherInfo;
    }
    mapping (uint256 => CattleExpense[]) public cattleExpenseStorage; // This will map the tagid number of each cattle expense cost
    
    struct Cattle {
        uint256 tagId;
        uint256 dateStocked;
        uint256 totalExpenses;
        uint256 numberOfExpenses;
        string breed;
        string stockedFrom;
        string otherDescriptions;
        bool exists;
    }
    mapping (uint256 => Cattle) public cattleDataStorage; // This will map the tagid number of each cattle 
    
    uint256[] public cattleIds; //This is an array containing the ids of all cattles on the farm

    event EmployeeAdded(address indexed employeeAddress, string name);
    event EmployeeAccessRevoked(address indexed employeeAddress);
    event CattleRecordCreated(uint256 indexed tagId, string breed);
    event CattleExpenseCreated(uint256 indexed tagId, uint256 expenseId, uint256 amount);
    
    modifier onlyOwner {
        require(msg.sender == owner, "You are not the owner of this contract");
        _;
    }

    modifier onlyEligibleEmployee {
        require((employees[msg.sender].exists && employees[msg.sender].canCreateRecord) || msg.sender == owner, "You are not authorized to perform this action");
        _;
    }

    constructor() {
        owner = msg.sender; //Setting the deployer of the contract as the owner
    }

    function transferAdmin(address newAdmin) public onlyOwner returns (bool) {
        owner = newAdmin;
        return true;
    }

    function addEmployee(
        bool canCreateRecord,
        string memory name,
        string memory idNumber,
        string memory otherEmployeeInfo,
        address employeeAddress
    ) public onlyOwner {
        require(!employees[employeeAddress].exists, "Employee already exists");
        employees[employeeAddress] = Employee({
            canCreateRecord: canCreateRecord,
            name: name,
            idNumber: idNumber,
            otherEmployeeInfo: otherEmployeeInfo,
            exists: true
        });
        emit EmployeeAdded(employeeAddress, name);
    }

    function revokeEmployeeAccess(bool canCreateRecord, address employee) public onlyOwner {
        require(employees[employee].exists, "This employee does not exist");
        employees[employee].canCreateRecord = canCreateRecord;
        emit EmployeeAccessRevoked(employee);
    }

    function createCattleRecord(
        uint256 tagId,
        uint256 dateStocked,
        string memory breed,
        string memory stockedFrom,
        string memory otherDescriptions
    ) public onlyEligibleEmployee {
        require(!cattleDataStorage[tagId].exists, "Cattle already exists");
        cattleDataStorage[tagId] = Cattle({
            tagId: tagId,
            dateStocked: dateStocked,
            totalExpenses: 0,
            numberOfExpenses: 0,
            breed: breed,
            stockedFrom: stockedFrom,
            otherDescriptions: otherDescriptions,
            exists: true
        });
        cattleIds.push(tagId);
        emit CattleRecordCreated(tagId, breed);
    }

    function createCattleExpense(
        uint256 tagId,
        uint256 amount,
        uint256 date,
        string memory descriptionAndOtherInfo
    ) public onlyEligibleEmployee {
        require(cattleDataStorage[tagId].exists, "Cattle does not exist or has not been recorded");
        cattleDataStorage[tagId].totalExpenses += amount;
        cattleDataStorage[tagId].numberOfExpenses += 1;
        cattleExpenseStorage[tagId].push(CattleExpense({
            amount: amount,
            date: date,
            descriptionAndOtherInfo: descriptionAndOtherInfo
        }));
        emit CattleExpenseCreated(tagId, cattleDataStorage[tagId].numberOfExpenses, amount);
    }

    // Get all the employees
    function getAllEmployees() public view returns (Employee[] memory) {
        Employee[] memory localEmployeeData = new Employee[](employeesAddresses.length);
        for (uint i = 0; i < employeesAddresses.length; i++) {
            localEmployeeData[i] = employees[employeesAddresses[i]];
        }
        return localEmployeeData;
    }

    // Get total farm expenses on all cattles
    function getTotalFarmExpenses() public view returns (uint256 totalAmount, CattleExpense[] memory farmExpenses) {
        for (uint i = 0; i < cattleIds.length; i++) {
            for (uint j = 0; j < cattleExpenseStorage[cattleIds[i]].length; j++) {
                totalAmount += cattleExpenseStorage[cattleIds[i]][j].amount;
                farmExpenses.push(cattleExpenseStorage[cattleIds[i]][j]);
            }
        }
    }
}

```

## Setting up Remix for CELO Alfajores
  
  ### Open Remix IDE and paste code
  Go to your web browser and open [remix IDE](https://remix.ethereum.org).

  Click on `contracts` folder and create a new file named `farm_record.sol` then paste the full code in the file.

### Compile and deploy
On the left tab, click on `compile` icon at the top of the `farm_record.sol` file when opened in the editor.

Next, click on `compile farm_record.sol` to compile your contract.

Upon successful compilation of your contracts, you should see a green check mark at the top of your file.

Now, proceed to deploy your contract by clicking on `deploy and run transactions` icon on the left side bar.

Before you proceed, ensure you have connected Metamask or the provider you are using to CELO alfajores. You can follow this [guide](https://medium.com/defi-for-the-people/how-to-set-up-metamask-with-celo-912d698fcafe) to connect CELO to Metamask.

Next, select `injected provider ` under your environments to connect to Metamask and click on `deploy` button. 

Upon successful deployment of your contract, you should see the interface to interact with the contract.

Congratulations! You have successfully written a cattle farm record smart contract and deployed it to CELO on Remix.
