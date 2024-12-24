# zk-lokomotive: Zero-Knowledge Based Multichain File Transfer System

<a href="https://www.drips.network/app/projects/github/zk-Lokomotive/zk-lokomotive-core" target="_blank"><img src="https://www.drips.network/api/embed/project/https%3A%2F%2Fgithub.com%2Fzk-Lokomotive%2Fzk-lokomotive-core/support.png?background=blue&style=drips&text=project&stat=none" alt="Support zk-lokomotive-core on drips.network" height="32"></a>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./zkl-light.svg">
  <img alt="ZKL logo" src="./zkl.svg">
</picture>
<br/><br/>

## Introduction

[GitHub Repository](https://github.com/zk-Lokomotive/zkl-docs)

zk-lokomotive is an advanced, zero-knowledge proof-based file transfer system designed to operate seamlessly across multiple blockchain networks, including EVM-compatible chains, Solana, and Sui. By leveraging state-of-the-art zero-knowledge cryptography, Arweave for decentralized storage, and Wormhole for cross-chain interoperability, zk-lokomotive provides an unparalleled solution for secure, private, and efficient file transfers in a trustless environment.

## Demos

- **Avalanche-Sui Demo:** [Watch on YouTube](https://www.youtube.com/watch?v=WpamMm3GP8U)
- **Solana-Solana Demo:** [Watch on YouTube](https://www.youtube.com/watch?v=zspxfSJNXbs&feature=youtu.be)

## Presentation

[Download Presentation](https://drive.google.com/file/d/1-7DNFiOYlN1-er6wnDAVkYeQX_won9aD/view?usp=sharing)

---

## System Architecture

### Overview

Our architecture consists of three layers, with the platform in the middle and users at the edges.

![zk-Lokomotive Module Legend](https://github.com/zk-Lokomotive/zkl-docs/blob/main/diagrams/zkl%20module%20legend%20light.png)

We offer enterprise-level solutions where the platform is fully on-chain for unmatched privacy potential. With the use of a decentralized Cross-Chain Identity Registry (CCIR), we provide identity proving and account management on the blockchain, eliminating any centralized layers where data can be tampered with.

**Enterprise Deployment Module Legend**

![zk-Lokomotive Enterprise Module Legend](https://github.com/zk-Lokomotive/zkl-docs/blob/main/diagrams/zkl%20enterprise%20module%20legend%20light.png)

### Elements

Our infrastructure consists of three main modules, with the JavaScript/Svelte web application comprising four submodules.

#### Modules

1. **JavaScript/Svelte Web Application (Client)**

   The client is the user-facing module of zk-lokomotive, allowing users to send and receive files by linking their wallet accounts.

   **Submodules:**

   - **aus**

     Provides functionality for communicating with distributed file chains and decentralized networks like IPFS. Currently, we utilize Arweave.

   - **roadhog**

     Interfaces with various blockchain networks used in our platform to perform specific objectives by calling or querying smart contracts, Solana programs, etc.

   - **crypto**

     Performs cryptographic operations. We support the Elliptic Curve Integrated Encryption Scheme (ECIES) through the `ecies/rs-wasm` package, which consumes the Rust crate `eciesrs`.

   - **kds**

     Generates pseudo-random mnemonics using BIP-39 that are then derived into elliptic curve key pairs.

2. **Platform-Level Components**

   - **Cross-Chain Identity Registry (CCIR)**

     The CCIR serves as a decentralized identity and public key management system. It links wallet addresses to their elliptic public keys. On the CCIR, wallet users can only add or modify information about themselves after proving ownership of the private key to that wallet account. Everyone is allowed to query from a public EC key to the wallet address or vice versa.

     - [GitHub Repository](https://github.com/zk-Lokomotive/zkl-ccir)

   - **Arweave**

     We use Arweave for decentralized and persistent file storage, providing a decentralized file storage solution.

   - **Inbox**

     Inboxes are on-chain and network-specific implementations. The client calls these using the `roadhog` submodule when querying for incoming files or sending a file.

     The inbox can be logically defined as:

     ```plaintext
     type message = { q_e: string; e_plink: string; uPK: string; }
     let inbox : message StringMap.t ref = ref StringMap.empty
     ```

---

## Key Components

### 1. Key Derivation Service (KDS)

The KDS is a crucial component that provides:

- A deterministic Curve25519 key pair generator derived from BIP-39 mnemonics.
- A pseudo-random BIP-39 mnemonic generator utilizing the `web-bip-39` package.

This service ensures consistent and secure key generation across different platforms and devices.

- [NPM Package](https://www.npmjs.com/package/@zklx/kds)

### 2. Cross-Chain Identity Registry (CCIR)

The CCIR serves as a decentralized identity and public key management system. It allows:

- Lookup of identities across different blockchain networks.
- Retrieval of corresponding public keys for secure communications.

- [GitHub Repository](https://github.com/zk-Lokomotive/zkl-ccir)

### 3. Encrypted File Storage (EFS)

The EFS is a distributed storage solution that:

- Allows recipients to retrieve encrypted payloads uploaded for them.
- Utilizes Arweave for decentralized and persistent file storage.
- Ensures data privacy through encryption before storage.

### 4. Client

The client component is responsible for:

- Generating encrypted payloads for recipients.
- Retrieving recipient public keys via the CCIR.
- Initiating the file transfer process.

### 5. Crypto

Provides cryptographic functions for encryption and decryption of both binary data and strings using public and private keys. It utilizes `ecies-wasm` for the underlying cryptographic operations.

- [NPM Package](https://www.npmjs.com/package/@zklx/crypto)

### 6. Wormhole Messaging Module SDK

The zk-lokomotive Ethereum-Solana Wormhole Messaging module facilitates secure and efficient cross-chain communication between Ethereum and Solana blockchains. This implementation leverages modern ES6+ standards to provide a robust, maintainable, and highly interoperable solution for cross-chain messaging needs. By utilizing the Wormhole protocol as its foundation, this module ensures reliable message delivery while maintaining the security guarantees essential for cross-chain operations.

- [GitHub Repository](https://github.com/zk-Lokomotive/zkl-eswm-ES6)

**Why ES6?**

Our decision to implement this module using ES6+ standards stems from several key considerations:

- **Modern Development Practices:** ES6 introduces significant improvements in code organization through modules.
- **Enhanced Type Safety:** Integration with TypeScript.
- **Better Asynchronous Handling:** Promises and async/await patterns are crucial in blockchain development.
- **Code Reliability and Maintainability:** Essential for cross-chain operations.
- **Expressive and Concise Code:** Without sacrificing readability or performance.

---

## Cryptographic Activities

### System Elements

The system elements are described and discussed in the zk-lokomotive System Architecture document.

#### 1. Key Derivation Service (KDS)

Provides:

- A deterministic secp256k1 key pair generator from BIP-39 mnemonics.
- A pseudo-random BIP-39 mnemonic generator through the `web-bip-39` package.

#### 2. Cross-Chain Identity Registry (CCIR)

Allows:

- Lookup of identities and their corresponding public keys across different blockchain networks.

#### 3. Encrypted File Storage (EFS)

A distributed storage solution that allows recipients to retrieve payloads that were uploaded for them.

#### 4. Client

The sender generates the encrypted payload to be sent to the receiver, whose public key is retrieved via the CCIR.

### Workflows

#### Definitions

- **Q<sub>r</sub>:** Recipient’s public key on curve secp256k1.
- **G:** The generator point on curve secp256k1.
- **Z:** A symmetric key derived for the file to be sent, the shared secret.
- **F<sub>c</sub>:** The file contents, in plaintext.
- **F<sub>m</sub>:** File's metadata (name, etc.).
- **F:** The intermediate file format, ready to be encrypted.
- **F<sub>c</sub>:** The file contents, in ciphertext.
- **IV:** The initialization vector required for AES-GCM-256.
- **P:** The payload, what is sent to the recipient.

The intermediate file format **F** is as follows:

| Bytes           | Content                             | Length in Bytes               |
|-----------------|-------------------------------------|-------------------------------|
| [0]..4          | Length of **F<sub>m</sub>**         | 4 bytes                       |
| [4]..1024       | **F<sub>m</sub>**                   | 1020 bytes (255 * 4 bytes)    |
| [1024]...       | **F<sub>c</sub>**                   | Variable                      |

#### Workflow: Sending a File

1. Retrieve **Q<sub>r</sub>** from the CCIR.
2. Generate an ephemeral key pair, **Q<sub>e</sub>** and **d<sub>e</sub>**.
3. Compute the shared secret **Z** = **d<sub>e</sub>** × **Q<sub>r</sub>**.
4. Encrypt the intermediate file **F** using AES-GCM-256 with encryption key **Z** and a randomly generated initialization vector, **IV**.
5. Create the payload **P** by concatenating **Q<sub>e</sub>**, **IV**, **MAC**, and **F<sub>e</sub>**.
6. Upload the payload **P** to the Encrypted File Storage (EFS).

> **Note:** The MAC in the payload **P** at step 5 is a result of using AES-GCM-256, which is selected in the ECIES implementation in the Rust crate we consume through the `ecies/rs-wasm` package.

---

## Diagrams

[View Diagrams](https://github.com/zk-Lokomotive/zkl-docs/tree/main/diagrams)

## PDFs

[View PDFs](https://github.com/zk-Lokomotive/zkl-docs/tree/main/pdfs)

---

## Cross-Chain Functionality

zk-lokomotive leverages Wormhole for seamless cross-chain file transfers. Here's an overview of the process:

1. **File Tokenization:** The encrypted file is tokenized on the source chain.
2. **Wormhole Bridge:** The tokenized file is transferred through Wormhole's bridge.
3. **Cross-Chain Verification:** Zero-Knowledge proofs are verified on the destination chain.
4. **File Retrieval:** The recipient retrieves and decrypts the file using their private key.

Our project operates across different blockchains such as Ethereum, Solana, and Sui, leveraging Wormhole for cross-chain functionality.

---

## User Story

As a user of the zk-lokomotive platform, I want to securely transfer tokens and send messages between Ethereum and Solana blockchains using Wormhole's cross-chain interoperability protocol.

![GXRni3rW0AAVI5S](https://github.com/user-attachments/assets/dd81307e-8bd6-41e5-82c2-c699cc8a6064)

### Acceptance Criteria

1. **Ethereum to Solana Transfer:**

   - I can connect my Ethereum wallet (e.g., MetaMask) to the zk-lokomotive dApp.
   - I can select an ERC20 token and specify an amount to transfer.
   - I can enter a Solana recipient address.
   - I can include an optional message with my transfer.
   - The dApp initiates a Wormhole core bridge contract call on Ethereum.
   - A Verifiable Action Approval (VAA) is generated by the Guardian network.
   - The transfer is completed on Solana, with the recipient receiving equivalent SPL tokens.

2. **Solana to Ethereum Transfer:**

   - I can connect my Solana wallet (e.g., Phantom) to the zk-lokomotive dApp.
   - I can select an SPL token and specify an amount to transfer.
   - I can enter an Ethereum recipient address.
   - I can include an optional message with my transfer.
   - The dApp initiates a Wormhole core bridge program call on Solana.
   - A VAA is generated by the Guardian network.
   - The transfer is completed on Ethereum, with the recipient receiving equivalent ERC20 tokens.

3. **Message Passing:**

   - I can send arbitrary messages between Ethereum and Solana without token transfers.
   - Messages are securely transmitted and verified using Wormhole's VAA mechanism.

4. **Transaction Monitoring:**

   - I can view the status of my cross-chain transactions in real-time.
   - The dApp shows me when the VAA is generated and when it's redeemed on the target chain.

5. **Security Features:**

   - All transactions require my explicit approval through wallet signatures.
   - The dApp uses Wormhole's consistency levels to ensure finality before completing transfers.
   - I receive clear warnings about the irreversibility of cross-chain transactions.

6. **Error Handling:**

   - If a transaction fails at any stage, I receive a clear error message explaining the issue.
   - The dApp provides guidance on how to resolve common errors (e.g., insufficient gas, network congestion).

## Audit & Security 

Our team working with **Ironnode Security**: [https://www.ironnode.io/]

Certainly! Here’s the text formatted in Markdown for a GitHub repository:

---

## Unique Value Proposition

### 1) Comparison with Similar Projects

In the global managed file transfer market, major players such as **BitTorrent**, **WeTransfer**, and **Dropbox** provide solutions for large-scale data transfer and storage. However, **zk-lokomotive** offers unique features that distinguish it from these established platforms:

#### Cross-Chain Interoperability
Unlike traditional file transfer solutions, zk-lokomotive is designed to operate across multiple blockchain networks, including **EVM-compatible chains**, **Solana**, and **Sui**. Powered by **Wormhole**, this cross-chain capability enables seamless data exchange across different blockchain ecosystems—a feature not available in conventional centralized solutions or single-chain decentralized applications.

#### Enhanced Privacy with Zero-Knowledge Proofs (ZKPs)
zk-lokomotive incorporates **zero-knowledge cryptography** that allows users to validate transactions or data without exposing any underlying information. This capability ensures data confidentiality, a critical advantage over platforms like WeTransfer or Dropbox, where privacy is often limited by centralized control.

#### Decentralized Identity Management
Through the **Cross-Chain Identity Registry (CCIR)**, zk-lokomotive provides decentralized identity and public key management. This enables users to securely link wallet addresses to their public keys across chains, removing the reliance on centralized identity providers and enhancing security for compliant and secure transfers.

#### Encrypted Storage Solution with Arweave
While other platforms such as Dropbox provide cloud storage, zk-lokomotive leverages **Arweave** for decentralized, immutable storage. Files are encrypted before storage, ensuring long-term data security and permanence—features not typically found in traditional cloud storage solutions.

#### Focused on Secure, High-Value Transfers
The managed file transfer market continues to grow, driven by the demand for secure and compliant solutions. zk-lokomotive addresses this need directly by prioritizing privacy, security, and interoperability, differentiating itself from both direct and indirect competitors in the data transfer space.

---

## 2) Benefits to the Wormhole Ecosystem and Connected Chains/Apps

Deploying zk-lokomotive offers significant benefits to the Wormhole ecosystem and its connected chains and applications:

### Benefits to the Wormhole Ecosystem

- **Enhanced Ecosystem Utility and User Growth**
  - **Broader Use Cases for Wormhole Protocol**: By supporting cross-chain file transfers with enhanced security and privacy, zk-lokomotive extends the utility of Wormhole beyond token transfers, adding a valuable application layer for privacy-focused users and industries.
  - **Attracting Privacy-Conscious Users**: zk-lokomotive appeals to security-conscious users and developers, introducing a new segment of users to the Wormhole ecosystem.

- **Promoting Advanced Security Standards**
  - **Integrating Zero-Knowledge Proofs**: zk-lokomotive’s use of zero-knowledge proofs in cross-chain file transfers demonstrates the feasibility of advanced cryptographic techniques, potentially encouraging other projects in the ecosystem to adopt similar standards.

- **Reinforcing Wormhole as a Cross-Chain Leader**
  - **Showcasing Versatility**: zk-lokomotive exemplifies Wormhole’s capability to facilitate complex, cross-chain applications, reinforcing Wormhole’s position as the leading protocol for cross-chain interoperability.

### Benefits to Connected Chains and Applications

- **Improved Privacy and Security for Connected Apps**
  - **Data Protection and Compliance**: Applications on connected chains can leverage zk-lokomotive’s encrypted file storage and transfer capabilities, offering users high standards of data security and regulatory compliance.

- **Unified Decentralized Identity Management**
  - **Seamless Cross-Chain Identity Solution**: The CCIR allows users to manage decentralized identities across multiple chains, simplifying user experience and reducing the need for multiple accounts—especially useful for applications requiring secure identity verification.

- **New Opportunities for Decentralized Applications**
  - **Cross-Chain File Sharing and Messaging**: Connected applications can integrate zk-lokomotive’s functionalities, such as secure file sharing, encrypted communication, and document exchange, enabling new use cases in areas like healthcare, legal, and finance.

### Ecosystem Growth and Collaborative Potential

- **Community Engagement and Innovation**
  - **Encouraging Hackathons and Grants**: zk-lokomotive’s success in hackathons and grants showcases its potential to drive community engagement and foster innovation within the Wormhole ecosystem.

- **Setting a Benchmark for Security and Privacy**
  - **Industry Leadership**: zk-lokomotive’s focus on cross-chain interoperability, privacy, and compliance sets new standards, potentially inspiring other projects to prioritize security and privacy.

### Summary

zk-lokomotive enhances the Wormhole ecosystem by introducing a secure, privacy-focused, cross-chain file transfer solution that sets it apart from traditional data transfer platforms. It strengthens Wormhole’s utility by adding privacy-centric use cases, attracting privacy-conscious users, and showcasing Wormhole’s versatility as a cross-chain solution provider. By offering decentralized identity management, encrypted storage, and cross-chain interoperability, zk-lokomotive not only fills a gap in the managed file transfer market but also brings a unique value proposition to the Wormhole ecosystem, benefiting both Modules and Submodules and its connected chains.

## Additional Resources

•⁠  ⁠GitHub Repository for Documentation: [zkl-docs](https://github.com/zk-Lokomotive/zkl-docs)
•⁠  ⁠Diagrams: [View Diagrams](https://github.com/zk-Lokomotive/zkl-docs/tree/main/diagrams)
•⁠  ⁠PDFs: [View PDFs](https://github.com/zk-Lokomotive/zkl-docs/tree/main/pdfs)

•⁠  ⁠Basic Diagram: [https://private-user-images.githubusercontent.com/158029357/361072139-a987b7fc-fc0d-43c5-abbe-200604d9a407.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzA1ODgxNjQsIm5iZiI6MTczMDU4Nzg2NCwicGF0aCI6Ii8xNTgwMjkzNTcvMzYxMDcyMTM5LWE5ODdiN2ZjLWZjMGQtNDNjNS1hYmJlLTIwMDYwNGQ5YTQwNy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMTAyJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTEwMlQyMjUxMDRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1mN2VjOGUyMjJjMGM1NmNmNDg2Y2ZlNjIzYmMxN2Q4NWY0NjNmMTUwN2JjZjdkYzE3YzdiMGM5MWNlN2QyNjZkJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.jRavoeXTSrwMxzj73BbwhqHIDg7_I_Uaz4XSe6NGBl4]

## Deployment Plans 

```
We aim to launch zk-lokomotive on the mainnet in the first quarter of 2025 across Solana, Ethereum, Sui, and Aptos networks. To
prepare for this deployment, we first conducted a thorough analysis of each blockchain’s technical specifications to ensure
compatibility. This involved examining each network’s consensus mechanisms, smart contract structures, and the requirements for
cross-chain (interoperability) integration, particularly through protocols like Wormhole. Our goal is to ensure zk-lokomotive operates
securely and efficiently on each network.
Before the mainnet launch, we subjected all our smart contracts to rigorous security audits and carried out extensive testing on
testnets to gather feedback from the community. These testnet deployments allowed us to assess the platform’s functionality,
performance, and user experience, gathering valuable insights for optimization and addressing potential issues. Through this iterative
process, we strengthened zk-lokomotive, making it more robust and user-friendly.
Now, we’re ready to bring zk-lokomotive to the mainnet, and we plan to deploy it in stages. We’ll begin with networks that have higher
user engagement and transaction volumes, allowing us to scale gradually and make real-time adjustments as user demand grows. By
deploying zk-lokomotive in a phased manner, we can monitor performance and scalability more effectively and respond swiftly if
needed. With the mainnet launch scheduled for early 2025, our primary goal is to establish zk-lokomotive as a secure and reliable
solution across all supported chains. Additionally, we’ve released our SDK packages to make our technical infrastructure accessible to
users and developers alike. For example, developers can access our Key Derivation Service (KDS) SDK at
npmjs.com/package/@zklx/kds and the Cross-Chain Identity Registry (CCIR) on GitHub at github.com/zk-Lokomotive/zkl-ccir, enabling
seamless integration with zk-lokomotive.
To attract users, we are adopting a community-driven approach. We’ve prepared educational content, guides, webinars, and onboarding
materials to help users understand zk-lokomotive’s security and privacy benefits. To encourage early adoption, we offer incentive
programs, including referral bonuses, airdrops, and loyalty rewards. Our referral program, in particular, aims to foster organic growth by
leveraging network effects within the community, helping us expand our user base through word-of-mouth.
Strategic partnerships will also play a key role in our growth. By collaborating with other blockchain projects and dApps that require
secure file transfer, we aim to position zk-lokomotive as a valuable tool within their ecosystems. For developers, we’ve established a
comprehensive support program, hosting hackathons, providing grants, and offering detailed documentation to encourage the
development of new solutions built on zk-lokomotive. Through these efforts, we aim to strengthen our ecosystem with the contributions
of a dedicated developer community.
Our go-to-market strategy focuses on clearly differentiating zk-lokomotive from competitors. The platform’s unique features—such as
cross-chain compatibility, high security via zero-knowledge proofs (ZKPs), and permanent, decentralized storage with Arweave—are
central to our value proposition. By conducting pilot programs with early users, we’ll be able to showcase real-world use cases, build
success stories, and establish zk-lokomotive as a trusted solution for secure file transfer.
In terms of regulatory compliance and security standards, we are highly attentive to maintaining high levels of security and adherence
to regulations. Positioning zk-lokomotive as a high-security, compliance-ready solution is crucial, especially for enterprise users who
need reliable and regulatory-compliant options. To that end, we’ve built a strong infrastructure to earn and maintain user trust.
Finally, we prioritize a feedback-driven development process. We continually update and enhance zk-lokomotive based on user needs,
aiming to make it a user-friendly and trustworthy platform. By doing so, we aspire to become a leader in secure file transfer across the
Solana, Ethereum, Sui, and Aptos ecosystems, fulfilling the demand for secure, private, cross-chain data transfers.
```

### Contributors
![Alt](https://repobeats.axiom.co/api/embed/8af38ce4e9ef72168a09aef4baed9f2aebe8c9be.svg "Repobeats analytics image")

#### Team
![GakzeyUWAAATGOI](https://github.com/user-attachments/assets/8303a43b-e9a2-4886-975e-5ab8fae47f8f)

**1- Baturalp Güvenç (Blockchain Developer) - Computer Engineer**

- **Linkedin:** https://www.linkedin.com/in/baturalpguvenc/
- **Github:** https://github.com/virjilakrum
- **X:** https://x.com/baturalpguvnc
- **Mail:** baturalp@zk-lokomotive.xyz
- **Medium:** https://medium.com/@baturalpguvenc
- **Telegram:** guattaridante

**2- Ferit Yiğit Balaban (System Architecture Specialist) - Computer Engineer**

- **Website:** https://fybx.dev/
- **Linkedin** https://www.linkedin.com/in/fybx/
- **Github:** https://github.com/fybx
- **X:** https://x.com/fybalaban
- **Mail:** fybalaban@fybx.dev
- **Telegram:** fybalaban

**3- Salih Eryılmaz (Product Manager) - Management Information Systems** 

- **Linkedin:** https://www.linkedin.com/in/salih-eryilmaz/
- **Mail:** salih.eryilmaz@outlook.com
- **Telegram:** slheryilmaz


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

## Acknowledgements

**Encode Project ID:** `f8zlq506ekpdpdnjxf8zlysubo9pi2a0`
- [Wormhole](https://wormhole.com/) for cross-chain interoperability
- [Arweave](https://www.arweave.org/) for decentralized storage
- [Solana](https://solana.com/) for high-performance blockchain infrastructure
- [Ethereum](https://ethereum.org/) for smart contract capabilities

---

### Awards and Recognitions of zk-lokomotive

* Movement Labs Battle of Olympus Hackathon (Finalist🏆) | Oct 2024
* Encode Wormhole Global Hackathon Best Integration on an Existing Project (Winner🥉) | Oct 2024
* Wormhole xGrant (Project Grant) | Jun 2024
* Superteam Solana Grant (Project Grant) Jun 2024
* Sui Overflow Local Track (Winner🥇) | May 2024
* EDCON Japan (Finalist🏆) | May 2024
* Solana Global Renaissance Hackathon Multichain Track (Winner🥇) | April 2024
* Solana Demoday (Winner🥈) | March 2024
* Solana Mini Hackathon (Winner🥇) | March 2024

---

![Thank You](https://github.com/zk-Lokomotive/zk-lokomotive/assets/158029357/af24913b-b649-4bf5-90e1-fdd99e68ca51)

For more information, please visit our [official website](https://zk-lokomotive.xyz)
