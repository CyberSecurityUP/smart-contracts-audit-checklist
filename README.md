# smart-contracts-audit-checklist

example1

### **General Security**
- [ ] **Audit**: Has the contract been reviewed by a third-party security audit?
- [ ] **Review external contracts**: Does the contract interact securely with other external contracts?
- [ ] **Check admin permissions**: Are administrative functions restricted to authorized users only?
- [ ] **Secure contract upgrade process**: Is there a secure method for upgrading or migrating the contract?

### **Input Validation**
- [ ] **Validate user inputs**: Are all inputs from users properly validated to prevent issues like **injection** or **overflows**?
- [ ] **Reentrancy**: Is the contract vulnerable to **reentrancy attacks**? Ensure functions update their internal state before making external calls.
- [ ] **Test for Reentrancy**: Use automated tools like Slither to test for reentrancy vulnerabilities. Ensure functions update internal state before making external calls.
- [ ] **Validate All Inputs**: Ensure all user inputs, including transaction amounts, addresses, and IDs, are validated to avoid common issues like overflow, underflow, or invalid entries.
- [ ] **Test Invalid or Out-of-Order Transactions**: Test the contract’s ability to handle invalid transaction sequences, especially grouped transactions.

### **Access Control**
- [ ] **Check access restrictions**: Are only authorized users able to access critical functions or sensitive data?
- [ ] **Correct function visibility**: Are functions marked with the correct visibility (`private`, `internal`, `public`)?
- [ ] **Admin function protection**: Are critical administrative functions like `mint`, `burn`, and `pause` properly secured?
- [ ] **Check Ownership and Admin Privileges**: Ensure that only authorized addresses can perform critical operations like minting, burning, staking, and withdrawal.
- [ ] **Multisig Program**: Implement multisig mechanisms for key administrative operations to prevent malicious actions by a single admin.
- [ ] **Role-based Function Access**: Test if the contract properly limits access to certain functions based on roles, like signatory and validator.

### **Integer Overflows/Underflows**
- [ ] **Validate arithmetic calculations**: Are all arithmetic operations protected from **overflows** and **underflows**? Is `SafeMath` or equivalent being used?

### **Timestamp Dependency**
- [ ] **Check usage of `block.timestamp`**: Does the contract rely on `block.timestamp` in a way that could be manipulated by miners?

### **Time-Based Attacks**
- [ ] **Timestamp Dependence**: Check for reliance on `block.timestamp` and ensure it cannot be manipulated by miners to gain unfair advantages.
- [ ] **Pool Start and End Date Validation**: Confirm that pool start dates are properly validated to prevent issues where a pool starts in the past.

### **Arithmetic Safety**
- [ ] **Integer Overflow and Underflow**: Verify that arithmetic operations in the contract are protected using libraries like `SafeMath` or similar mechanisms. Check for missing underflow protection as identified in Yieldly audits.

### **Governance**
- [ ] **DAO and Governance Attacks**: Test for possible governance manipulation where attackers could execute critical actions like upgrading contracts, minting new tokens, or changing protocol rules.
- [ ] **Threshold Validation for Voting**: Verify that threshold limits are properly defined and applied in voting mechanisms for signatory and validator roles.

### **External Call Failures**
- [ ] **Validate external calls**: Does the contract properly check the return values of external calls to ensure execution halts on failure?
- [ ] **Call and Delegatecall**: Are functions using `call()` or `delegatecall()` implemented securely to avoid malicious code execution?
- [ ] **Unchecked External Calls**: Ensure that external calls are properly validated and that the contract does not proceed after failed external calls.
- [ ] **Proxy Contract Validation**: Verify that the contract utilizes proxy contracts securely. Ensure that transactions routed through the proxy cannot be bypassed.

### **Gas Manipulation**
- [ ] **Gas limits**: Are contract functions designed to stay within gas limits? Are long-running loops avoided to prevent gas exhaustion?
- [ ] **Efficient gas usage**: Ensure that gas is not wasted unnecessarily, particularly in critical functions.

### **Token Management**
- [ ] **ERC20/721 compliance**: Are the token contracts (ERC20, ERC721) following the proper standards?
- [ ] **Transfer permissions**: Can transfer functions be manipulated? Does the contract handle permissions and limits correctly?

### **Insecure Randomness**
- [ ] **Randomness generation**: If the contract generates random numbers, are they generated securely to avoid manipulation?

### **Denial of Service (DoS)**
- [ ] **Test DoS resistance**: Can the contract be locked or rendered unusable by malicious transactions that consume excessive gas or halt critical functions?
- [ ] **Loops in functions**: Ensure that functions looping over arrays or lists do not allow attackers to exhaust gas limits.

### **State Management**
- [ ] **Storage and data access**: Ensure the contract is storing and accessing data efficiently.
- [ ] **State updates**: Does the contract correctly update its state after each transaction?

### **Front-running Attacks**
- [ ] **Prevent front-running**: Can important transactions be manipulated or reordered by front-running attacks?

### **Phishing Attacks**
- [ ] **Protect against phishing**: Test how the contract handles interactions with user interfaces that may deceive users.

### **Randomness Vulnerabilities**
- [ ] **Test randomness sources**: Are random numbers generated using secure and unpredictable sources to prevent manipulation?

### **Emergency Functions**
- [ ] **Implement Emergency Withdraw**: Confirm that users have access to emergency withdrawal functions to recover funds if a contract enters an unexpected state. Ensure admin privileges on emergency actions are not overly restrictive.

### **Staking, Pools, and Rewards**
- [ ] **Reward Calculation Verification**: Test if staking rewards and pool ratios are calculated correctly after staking and withdrawing actions. Ensure that updates to rewards are triggered as expected.
- [ ] **Dynamic Testing for Pool Operations**: Perform dynamic tests to ensure that pool ratios and user claimable amounts are updated correctly.

### **Oracle Manipulation**
- [ ] **Secure oracle usage**: If the contract relies on external oracles, are they protected against manipulation?
- [ ] **Secure Randomness**: Ensure that random number generation is not predictable or manipulable, especially in lottery or staking functionalities.
- [ ] **Oracle Manipulation**: Test contracts for potential oracle manipulation that could lead to pricing or staking rewards being incorrectly calculated.

### **OWASP-related Vulnerabilities for Smart Contracts**
- [ ] **Proper data validation**: Are inputs and outputs validated properly to prevent data integrity issues?
- [ ] **Correct cryptography implementation**: Are cryptographic methods and hashing applied according to best practices?
- [ ] **Access control and authentication**: Are there any vulnerabilities allowing unauthorized users to access restricted functions?
- [ ] **Injection mitigation**: Ensure the contract is not vulnerable to data or command injection.

### **Manual Testing Considerations**
- [ ] **Admin Bypass Testing**: Attempt to bypass admin privileges or role restrictions by manipulating function parameters or transaction sequences.
- [ ] **Test Role-based Enhancements**: Verify that role-based enhancements are structured properly, ensuring that only authorized users can perform specific actions.

### **Tools to Automate Smart Contract Testing**
- [ ] **MythX**: Automatically analyze contracts for common vulnerabilities.
- [ ] **Slither**: Detect logic vulnerabilities, reentrancy issues, and gas optimizations.
- [ ] **Manticore**: Symbolic execution and fuzzing tool for smart contracts.
- [ ] **Oyente**: Static analyzer to find issues like reentrancy, uncontrolled loops, and others.

### **Smart Contract Best Practices**
- [ ] **Adhere to Versioning**: Ensure the contract explicitly defines the Solidity or Algorand version (`pragma version`) being used to avoid unintended behavior during compilatio.
- [ ] **Boundaries for Function Parameters**: Check that input values for functions have well-defined boundaries, such as ensuring array sizes or transaction amounts are reasonable.
