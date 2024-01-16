
# Security Audit Report for StorageVictim Contract using Slither:

## Uninitialized Pointer Vulnerability:

The `store` function in the contract currently contains an uninitialized pointer `Storage str` that points to the storage address 0 (owner). This presents a potential security risk, as malicious actors could exploit this pointer to manipulate data or gain unauthorized access.

### Recommended Solution:

To mitigate this issue, it is recommended to initialize the `Storage` struct directly within the `store` function and assign values to `storages[msg.sender]`. Here is the updated code:

solidity

`function store(uint256 _amount) public {
    storages[msg.sender] = Storage(msg.sender, _amount);
}` 

## Deprecated Constructor Usage:

The contract utilizes a constructor named `function StorageVictim()`, which follows a deprecated naming convention in Solidity 0.8.18. To enhance code clarity and ensure compatibility with the latest version of Solidity, it is advisable to use the `constructor` keyword.

### Recommended Solution:

Rename the constructor from `function StorageVictim()` to `constructor`:

solidity

`constructor() {
    owner = msg.sender;
}` 

## State Variables Visibility:

The `owner` variable, defined as an address, lacks a visibility specifier. In Solidity 0.8.18, explicitly declaring visibility for state variables is crucial to prevent unintended access or modification.

### Recommended Solution:

If the `owner` variable should only be accessed within the contract, declare it as `immutable`:

solidity

`address immutable owner;`
