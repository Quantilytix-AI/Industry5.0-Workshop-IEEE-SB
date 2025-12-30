# CryptaTrace-Industry 5.0

🚀 **Conceived, Engineered & Presented by Youssef Attia**  
🎓 **IEEE Student Branch Technical Workshop**  
📅 **Industry 5.0 Secure Data Workflows | 2025**

---

## Overview

**CryptaTrace-Industry 5.0** is a hands-on, industry-aligned demonstration of **secure document exchange** and **cryptographic traceability** within an **Industry 5.0 manufacturing environment**.

Developed and presented as part of an **IEEE Student Branch technical workshop**, this project introduces engineering students to **real-world encryption workflows** used in modern industrial systems, through a realistic scenario inspired by an **automotive antenna manufacturing process**.

The repository models secure communication between **Production** and **Quality Assurance (QA)** departments, where sensitive reports must remain **confidential, verifiable, and tamper-evident** throughout their lifecycle.

---
![Hybrid Crypto](https://img.shields.io/badge/Crypto-Hybrid%20AES%2BRSA%20DigitalSignature-8e44ad?style=for-the-badge)
![Base64](https://img.shields.io/badge/Encoding-Base64-e67e22?style=for-the-badge)
![QR Code](https://img.shields.io/badge/Hash-QR%20Code-f1c40f?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.10%2B-3776ab?style=for-the-badge&logo=python&logoColor=white)


## Industrial Scenario

In high-reliability manufacturing environments (e.g., RF and automotive antenna production - a scenario proposed by students), reports contain sensitive performance data that must be:

- **Confidential** during transmission  
- **Authenticated** at the receiving department  
- **Protected** against tampering  
- **Traceable** for audit and compliance purposes  

This project simulates that workflow using modern cryptographic primitives and widely adopted Python security libraries.

---

## Security Architecture

The implemented workflow follows industry best practices:

### 🔐 Cryptographic Design

- **Hybrid Encryption**
  - AES-GCM (Advanced Encryption Standard - Galois/Counter Mode) for data confidentiality and integrity  
  - RSA-OAEP (Rivest-Shamir-Adleman-Optimal Asymmetric Encryption Padding) for secure AES key exchange  
- **Digital Signatures**
  - RSA-PSS (RSA-Probabilistic Signature Scheme) for report authenticity and non-repudiation  
- **Deterministic Signing**
  - Canonical JSON serialization to prevent signature ambiguity  
- **Tamper Detection**
  - Signature verification and authenticated decryption  
- **Traceability**
  - SHA-256 hash embedded as a QR code inside the generated report  

---

## Workflow Summary

### Production Department

- Digitally signs the report using its private RSA key  
- Encrypts the signed payload using AES-GCM  
- Encrypts the AES key using QA’s RSA public key  

### Quality Assurance Department

- Decrypts the AES key using its private RSA key  
- Decrypts the payload  
- Verifies the Production signature  
- Logs verification status  
- Exports a tamper-evident PDF report with embedded QR hash  

---

## Key Components

### 1. `sample_report.enc`

- **Type:** Encrypted JSON payload  
- **Contents:**
  - `nonce`: Random nonce used in AES-GCM encryption.
  - `ciphertext`: AES-GCM encrypted signed report.
  - `encrypted_key`: AES key encrypted with QA’s public RSA key.

This file represents the **secure, tamper-evident report** that is exchanged between production and QA.

---

### 2. `keys/` Folder

This folder contains **RSA key pairs** for both the production and QA roles. Each role has a **private and public PEM file**:

| Role        | PEM Files                                   | Purpose                                           |
|------------|--------------------------------------------|--------------------------------------------------|
| Production | `private_key.pem`, `public_key.pem`        | Signs reports before encryption                 |
| QA         | `private_key.pem`, `public_key.pem`        | Decrypts AES key and verifies report integrity  |


---

### 3. `sample_report.json`

- **Type:** Signed JSON report (human-readable)  
- **Purpose:** Provides a **reference of the report before encryption**. It includes:
  - RF measurement data
  - Manufacturing context and traceability
  - QA verdict and release status
  - Digital signature ensuring integrity

This file is useful for **debugging, auditing, or verification** of the signing process.

---

## Hands-On Learning Objectives

This project was designed to give students practical exposure to:

- Applied cryptography using `cryptography.hazmat`  
- Hybrid encryption systems used in industry  
- Secure inter-department data exchange  
- Cryptographic integrity verification  
- Traceable and auditable document workflows  
- Industry 5.0 security principles beyond theory  

---
## ⚡ Usage / Run Instructions
1. Install dependencies:
```bash
pip install -r requirements.txt
```
## Launch Encryption
```bash
python encrypt_sign.py
```
## Launch Decryption
```bash
python decrypt_verify.py
```
