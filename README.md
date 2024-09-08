# smart-contracts-audit-checklist

### **General Security**
- [ ] **Audit**: Has the contract been reviewed by a third-party security audit?
- [ ] **Review external contracts**: Does the contract interact securely with other external contracts?
- [ ] **Check admin permissions**: Are administrative functions restricted to authorized users only?
- [ ] **Secure contract upgrade process**: Is there a secure method for upgrading or migrating the contract?

### **Input Validation**
- [ ] **Validate user inputs**: Are all inputs from users properly validated to prevent issues like **injection** or **overflows**?
- [ ] **Reentrancy**: Is the contract vulnerable to **reentrancy attacks**? Ensure functions update their internal state before making external calls.

### **Access Control**
- [ ] **Check access restrictions**: Are only authorized users able to access critical functions or sensitive data?
- [ ] **Correct function visibility**: Are functions marked with the correct visibility (`private`, `internal`, `public`)?
- [ ] **Admin function protection**: Are critical administrative functions like `mint`, `burn`, and `pause` properly secured?

### **Integer Overflows/Underflows**
- [ ] **Validate arithmetic calculations**: Are all arithmetic operations protected from **overflows** and **underflows**? Is `SafeMath` or equivalent being used?

### **Timestamp Dependency**
- [ ] **Check usage of `block.timestamp`**: Does the contract rely on `block.timestamp` in a way that could be manipulated by miners?

### **External Call Failures**
- [ ] **Validate external calls**: Does the contract properly check the return values of external calls to ensure execution halts on failure?
- [ ] **Call and Delegatecall**: Are functions using `call()` or `delegatecall()` implemented securely to avoid malicious code execution?

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

### **Oracle Manipulation**
- [ ] **Secure oracle usage**: If the contract relies on external oracles, are they protected against manipulation?

### **OWASP-related Vulnerabilities for Smart Contracts**
- [ ] **Proper data validation**: Are inputs and outputs validated properly to prevent data integrity issues?
- [ ] **Correct cryptography implementation**: Are cryptographic methods and hashing applied according to best practices?
- [ ] **Access control and authentication**: Are there any vulnerabilities allowing unauthorized users to access restricted functions?
- [ ] **Injection mitigation**: Ensure the contract is not vulnerable to data or command injection.

### **Tools to Automate Smart Contract Testing**
- [ ] **MythX**: Automatically analyze contracts for common vulnerabilities.
- [ ] **Slither**: Detect logic vulnerabilities, reentrancy issues, and gas optimizations.
- [ ] **Manticore**: Symbolic execution and fuzzing tool for smart contracts.
- [ ] **Oyente**: Static analyzer to find issues like reentrancy, uncontrolled loops, and others.
