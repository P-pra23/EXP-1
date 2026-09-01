### Experiment 1: Decentralized Certificate Verification
## Aim:
  To develop a smart contract for issuing and verifying academic certificates on Ethereum, preventing forgery and ensuring authenticity.
## Algorithm:
1. Deploy a smart contract where universities can issue certificates.
2. Store a hash of certificate data on-chain.
3. Provide a verification function that checks certificate authenticity.
4. Users can verify the certificate by comparing the stored hash.
## Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;
contract CertificateVerification {
address public university;
mapping(bytes32 => bool) public certificates; // Store hashed certificates
event CertificateIssued(bytes32 indexed certHash);
constructor() {
university = msg.sender; // University deploys the contract
}
function issueCertificate(string memory studentName, string memory degree, uint256 year) public {
require(msg.sender == university, "Only university can issue certificates");
bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, year));
certificates[certHash] = true;
emit CertificateIssued(certHash);
}
function verifyCertificate(string memory studentName, string memory degree, uint256 year) public view returns (bool) {
bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, year));
return certificates[certHash];
}
}
```
# Expected Output:
```
● When the university issues a certificate, it gets stored as a hash.
● A student or employer can verify the certificate by entering the details.
● If valid, it returns true; otherwise, false.
High-Level Overview:
● Used to prevent fake certificates.
● Enables quick verification by employers or other institutions.
● Shows how blockchain can be used in education and credential verification.
```
<img width="877" height="731" alt="Screenshot 2026-08-03 113017" src="https://github.com/user-attachments/assets/d8d1d4db-b4fc-4acb-acbd-67af61ef142f" />


<img width="421" height="828" alt="Screenshot 2026-08-03 113040" src="https://github.com/user-attachments/assets/cb8abb3c-7720-4dac-a8d6-4cf5a177699a" />


<img width="412" height="732" alt="Screenshot 2026-08-03 113051" src="https://github.com/user-attachments/assets/7a236b08-a81b-471a-b07e-5247aec86240" />


# Result:
The decentralized certificate verification system was successfully implemented using an Ethereum smart contract. The certificate data hash was stored on the blockchain, and the verification function successfully compared the given certificate hash with the stored hash.

Thus, the authenticity of academic certificates was verified securely using blockchain, preventing unauthorized modification and forgery.
