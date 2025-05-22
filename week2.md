## Chapter: Security and Trusted Hardware Applications

### 1. Symmetric and Public-key Cryptography: Primitives and Security Goals

- **Symmetric cryptography** utilizes pre-shared secret keys between users to secure communication channels by ensuring **confidentiality and integrity**.

- Key primitives include:
  - **Encryption modes** like AES-CBC, AES-CTR, and RC4 to provide confidentiality.
  
  - **Message Authentication Codes (MACs)** such as HMAC and CMAC ensure integrity.

- In contrast, **Public-key Cryptography** operates with asymmetric key pairs, enabling secure communication even when users do not share keys beforehand.

- Core components:
  - Encryption algorithms like **RSA-OAEP** protect confidentiality and integrity.
  
  - **Digital signatures**, notably the **Schnorr signature scheme**, enforce integrity and non-repudiation.
  
  - **Key exchange protocols** such as **Diffie-Hellman** facilitate secure symmetric key sharing.

- The concept of Man-in-the-Middle attacks illustrates the risks when an adversary intercepts or compromises communication parties, highlighting the necessity of robust cryptographic protocols and **Public-key Infrastructure (PKI)** with trusted root **Certificate Authorities (CAs)** to establish trust hierarchies.

### 2. Trusted Computing Base (TCB): Assumptions and Components

- Every security system relies on a **Trusted Computing Base (TCB)** - a minimal set of components assumed to function reliably and securely.

- TCB may include cryptographic coprocessors, tamper-resistant hardware, and standardized APIs, acknowledging that **trust is assumed, not unwarranted**.

- Recognizing and minimizing the TCB is crucial for reducing potential attack surfaces.

### 3. Smart Cards and Java Cards: Portable Security Anchors

- **Smart cards** are portable, tamper-resistant devices embedding microcontrollers that securely process and store information without relying on external vulnerable resources.

- They serve as **security anchors**, enabling **two-factor authentication** and **portable key and certificate management**, enhancing password-based systems and enabling PKI operations.

- The **Java Card** platform, a stripped-down Java environment, provides features such as hardware independence, cost-efficiency, and security through isolated execution of applets.

### Applets:
- Follow a predefined API, enabling multiple applets to coexist securely via enforced isolation.

- Communicate with host systems through **APDUs (Application Protocol Data Units)**, a half-duplex, fine-grained communication protocol.

- Despite ease of entry due to Java familiarity, mastering Java Card development requires deep attention due to low-level communications and subtle vulnerabilities.

## 4. Trusted Platform Module (TPM): Hardware-based Trust Anchors

- The **Trusted Platform Module (TPM)** is a microchip dedicated to performing cryptographic operations independent of the operating system.

- A critical application is **integrity measurement and secure boot**, where the TPM serves as the **Root of Trust for Measurement (RTM)** by storing known-good hashes (e.g., SHA-256) of essential system code to verify boot integrity.

- TPM components and software stacks support development, but trusted setup commonly relies on hardware providers.

- Application development entails managing multiple TPM versions and understanding the unique, hardware-enforced trust models.

## 5. Hardware Security Modules (HSM): Secure Key Custodians

- HSMs are tamper-resistant, high-performance devices optimized for cryptographic operations, ensuring keys are not extractable.

### Types include:
- **Network HSMs:** Shared over LAN, higher cost, accessible by multiple servers.

- **Internal HSMs:** PCI-installed, non-shareable but cheaper.

- **Offline HSMs:** USB-connected, less vulnerable, commonly used in Root Certificate Authorities.

- **Cloud HSMs:** Provide password-based authentication, emulate network HSM functionalities.

- Certified under standards such as **FIPS 140-2**, HSMs scale security by maintaining keys internally and enabling secure key management services.

- Application design must carefully incorporate HSM APIs to mitigate vulnerabilities, leveraging hardware strengths.

## 6. Intel Software Guard Extensions (SGX): Enclaved Execution for Confidentiality

- **Intel SGX** provides isolated execution environments (enclaves) within processors, ensuring code and data confidentiality and integrity against malware and privileged software threats.

### Core features:
- Enclaves guarantee that sensitive operations, such as storing secret TLS keys or processing confidential cloud jobs, remain inaccessible even to administrative personnel.

- Supports attestation, allowing local or remote parties to verify enclave identity and code integrity.

- Client-side uses include protecting malware signatures and preventing runtime tampering.

- SGX architecture is pervasive in Intel machines since Skylake and includes tools and simulators for application development (primarily in C/C++).

- However, SGX faces challenges from **side-channel attacks** (e.g., cache timing, branch prediction), which threaten security by leaking sensitive information.

- Related technology, **Intel Trusted Domain Extensions (TDX)**, extends trusted hardware capabilities to virtual machines, though currently less widespread.

## 7. ARM TrustZone: Secure World Isolation on Embedded Systems

- **ARM TrustZone** offers hardware-enforced isolation by dividing the platform into **Normal** and **Secure Worlds**, enforcing root of trust on embedded devices like smartphones and IoT.

- Only signed, trusted applications execute in the secure world, denying malware access to sensitive data.

- Development requires certified applets and setup setups like OP-TEE OS in emulators such as QEMU.

- Unlike SGX, TrustZone lacks built-in remote attestation, but is widely deployed in embedded and mobile domains.

## 8. Side-Channel Attacks and Fault Injection: Vulnerabilities in Hardware Security

- Hardware security is only as strong as its weakest link, with adversaries exploiting unintended information leakage through **side-channel attacks**.

### Several attack types highlighted:
- **Timing attacks:** Exploit correlation between execution time and secret data (PIN verification timing analysis).

- **Fault injection attacks:** Use physical manipulations like clock glitches, temperature shifts, or UV exposure to provoke faults breaking security checks or limits.

- **Power analysis attacks:** Measure power consumption to deduce operational patterns, revealing algorithmic structure and data relationships.

- **Speculative execution attacks:** Exploit CPU optimization mechanisms to access unauthorized memory regions, undermining access control.

These attacks highlight the critical need for system designers to preempt adversarial tactics by incorporating constant-time operations and hardened implementations.

## Key Takeaways

- Symmetric and asymmetric cryptography provide foundational primitives securing confidentiality, integrity, and authenticity.

- Trusted hardware includes layers - from smart cards and TPMs to complex enclaves like SGX and TrustZone - each with defined trust assumptions.

- Secure hardware implementations improve performance and assurance but require diligent development to prevent vulnerabilities.

- Sophisticated side-channels and fault attacks remain potent threats, necessitating a proactive defense posture.

- Understanding the trade-offs and interplay among these technologies is essential for building resilient security architectures.
