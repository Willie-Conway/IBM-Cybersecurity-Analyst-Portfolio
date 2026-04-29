![alt text](<../Screenshots/Cryptool.png>)

# Lab: End-to-End Encryption/Decryption (RSA Algorithm)

**Estimated duration:** 30 minutes

---

## Introduction

This lab will guide you through the installation and initial use of a cryptographic tool called **CrypTool**. It focuses on encryption, decryption, and key generation using the **RSA algorithm**.

RSA (Rivest-Shamir-Adleman) is one of the first public-key cryptosystems and is widely used for secure data transmission.

---

## Learning Objectives

After completing this lab, you will be able to:

| # | Objective                                        |
| - | ------------------------------------------------ |
| 1 | Install CrypTool 2.1 on your system              |
| 2 | Generate RSA key pairs (public and private keys) |
| 3 | Encrypt a message using an RSA public key        |
| 4 | Decrypt a message using an RSA private key       |

---

## What is RSA?

RSA is an **asymmetric encryption algorithm** that uses two different keys:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         RSA ENCRYPTION PROCESS                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   SENDER                                              RECIPIENT              │
│                                                                              │
│   ┌─────────────┐                                   ┌─────────────┐         │
│   │  "HELLO"    │                                   │  "HELLO"    │         │
│   │  Plaintext  │                                   │  Plaintext  │         │
│   └──────┬──────┘                                   └──────▲──────┘         │
│          │                                                 │                │
│          │  Encrypt with                                   │  Decrypt with  │
│          │  RECIPIENT'S                                    │  RECIPIENT'S   │
│          │  PUBLIC KEY                                     │  PRIVATE KEY   │
│          ▼                                                 │                │
│   ┌─────────────┐         ┌─────────────┐         ┌─────────────┐           │
│   │  7F4E8C...  │────────►│  7F4E8C...  │────────►│  7F4E8C...  │           │
│   │  Ciphertext │ Network │  Ciphertext │         │  Ciphertext │           │
│   └─────────────┘         └─────────────┘         └─────────────┘           │
│                                                                              │
│   PUBLIC KEY  = Can be shared openly                                         │
│   PRIVATE KEY = Must be kept secret                                          │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### RSA Key Concepts

| Concept                  | Description                                    |
| :----------------------- | :--------------------------------------------- |
| **Public Key**     | Used for encryption; can be shared with anyone |
| **Private Key**    | Used for decryption; must remain secret        |
| **Key Size**       | Typically 2048 or 4096 bits                    |
| **Security Basis** | Difficulty of factoring large prime numbers    |

---

## Part 1: Installing CrypTool 2.1

### Step 1: Download CrypTool 2.1

CrypTool 2.1 is the current version available as a desktop application.

1. Open your web browser
2. Go to the official CrypTool website:

```
https://www.cryptool.org/en/
```

> **Note:** To open the links, right-click (or long-press) on the link and select **"Open in new tab."** Avoid clicking the link directly, as this might block it.

![CrypTool website]

![alt text](../Screenshots/CrypTool_Website_RSA.png)

### Step 2: Navigate to Download Page

1. Click on **Download** in the top menu
2. Select **CrypTool 2 (CT2)** from the dropdown

### Step 3: Download CrypTool 2.1 (Stable Build)

Go to the CrypTool 2 Download Page:

```
https://www.cryptool.org/en/ct2/
```

1. Find the latest **Stable Build** (e.g., Build 9778.2 or newer)
2. Select the version compatible with your operating system:
   - **Windows**: .exe installer
   - **macOS**: .dmg file
   - **Linux**: .tar.gz or AppImage

![Download CrypTool 2 RSA]

![alt text](../Screenshots/Download_CrypTool2_RSA.png)

### Step 4: Install CrypTool 2.1 on Windows

1. **Run the installer** by double-clicking the downloaded `.exe` file
2. If prompted by User Account Control (UAC), click **Yes**
3. **Follow the prompts** and accept the default installation options:

| Installation Step     | Action                                      |
| :-------------------- | :------------------------------------------ |
| License Agreement     | Click "I Agree"                             |
| Choose Components     | Leave defaults (select all)                 |
| Installation Location | Use default:`C:\Program Files\CrypTool 2` |
| Start Menu Folder     | Use default                                 |
| Additional Tasks      | Create desktop shortcut (recommended)       |

4. Click **Install**
5. Click **Finish** to complete installation

### Step 5: Launch CrypTool 2.1

After installation, launch CrypTool 2.1 using one of these methods:

| Method                     | Instructions                            |
| :------------------------- | :-------------------------------------- |
| **Desktop shortcut** | Double-click the CrypTool 2 icon        |
| **Start Menu**       | Click Start → CrypTool 2 → CrypTool 2 |
| **Search**           | Type "CrypTool" in Windows search       |

![CrypTool launch RSA]

![alt text](../Screenshots/CrypTool_Launch_RSA.png)

---

## Part 2: Using RSA Algorithm for Encryption/Decryption

### Step 1: Open CrypTool 2.1

Launch the application. The main window will appear:

![CrypTool main window RSA]

![alt text](../Screenshots/CrypTool_Main_RSA.png)

### Step 2: Create a New Template

1. Click on **New** in the top menu bar
2. Alternatively, press `Ctrl + N` on your keyboard

![New template RSA]

![alt text](../Screenshots/CrypTool_New_RSA.png)

### Step 3: Select Encryption/Decryption

1. In the template wizard, select **Encryption/Decryption** from the list of options
2. Click **Next**

![Select Encryption/Decryption]

![alt text](../Screenshots/Select_Encryption_Decryption.png)

### Step 4: Choose RSA Algorithm

From the list of encryption algorithms, select:

```
RSA (Rivest-Shamir-Adleman)
```

Click **Next**

![Choose RSA]

![alt text](../Screenshots/Choose_RSA.png)

---

## Part 3: Generating RSA Keys

### Step 1: Configure Key Generation

You will now generate an RSA key pair. Configure the following parameters:

| Parameter                 | Recommendation  | Description              |
| :------------------------ | :-------------- | :----------------------- |
| **Key Length**      | 2048 bits       | 2048 is current standard |
| **Key Format**      | PEM / Plain     | Standard format for keys |
| **Public Exponent** | 65537 (default) | Standard RSA exponent    |

### Step 2: Generate Key Pair

1. Click **Generate Keys** or **Generate New Key Pair**
2. Wait for key generation to complete (may take a few seconds)

![Generate RSA keys]

![alt text](../Screenshots/Generate_RSA_Keys.png)

### Step 3: View the Key Pair

After generation, CrypTool will display:

**Public Key:**

```
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAv2qX5jUZxYvW3qNnP7pQ
R8sT9uVxWzY1aBcDeFgHiJkLmNoPqRsTuVwXyZ1aBcDeFgHiJkLmNoPqRsTuVwXy
... (more lines) ...
-----END PUBLIC KEY-----
```

**Private Key:**

```
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAv2qX5jUZxYvW3qNnP7pQR8sT9uVxWzY1aBcDeFgHiJkLmNoP
qRsTuVwXyZ1aBcDeFgHiJkLmNoPqRsTuVwXyZ1aBcDeFgHiJkLmNoPqRsTuVwXy
... (more lines) ...
-----END RSA PRIVATE KEY-----
```

![View RSA keys]

![alt text](../Screenshots/View_RSA_Keys.png)

### Step 4: Save the Keys

1. Click **Save Public Key** to save to a file (e.g., `public_key.pem`)
2. Click **Save Private Key** to save to a file (e.g., `private_key.pem`)
3. Choose a secure location for your keys

> **Important:** The private key should be kept secret and stored securely. Never share your private key with anyone.

---

## Part 4: Encrypting a Message with RSA

### Step 1: Enter the Message to Encrypt

In the CrypTool workspace, type or paste the message you want to encrypt:

```
Hello SecureBank! This is a confidential message.
```

Or use a shorter message (RSA has size limitations):

```
Secret: Q4 Revenue $10M
```

![Enter plaintext]

![alt text](../Screenshots/Enter_Plaintext_RSA.png)

### Step 2: Select the Public Key for Encryption

1. Ensure you are using the **public key** for encryption
2. The public key should be loaded in the encryption component
3. Verify the key is correct before encrypting

### Step 3: Perform Encryption

1. Click **Encrypt** or **Run** button
2. Observe the encryption process

![RSA encryption]

![alt text](../Screenshots/RSA_Encryption.png)

### Step 4: View the Ciphertext

After encryption, CrypTool will display the **ciphertext** (encrypted message):

```
Ciphertext (hex):
4A 7F 3C 2E 9D 1B 8F 5A 2C 6E 7D 8F 9A 2B 3C 4D
5E 6F 7A 8B 9C 0D 1E 2F 3A 4B 5C 6D 7E 8F 9A 0B
1C 2D 3E 4F 5A 6B 7C 8D 9E 0F 1A 2B 3C 4D 5E 6F
... (more bytes) ...
```

The ciphertext will appear as **gibberish** (binary data) because it is encrypted.

![View ciphertext]

![alt text](../Screenshots/View_Ciphertext_RSA.png)

---

## Part 5: Decrypting a Message with RSA

### Step 1: Load the Ciphertext

If you are decrypting a message you just encrypted, the ciphertext is already in the workspace. Otherwise:

1. Click **Load** or paste the ciphertext
2. Ensure the ciphertext is in the correct format

### Step 2: Select the Private Key for Decryption

1. Ensure you are using the **private key** for decryption
2. The private key must match the public key used for encryption
3. Load your private key file (e.g., `private_key.pem`)

### Step 3: Perform Decryption

1. Click **Decrypt** or **Run** button
2. Observe the decryption process

![RSA decryption]

![alt text](../Screenshots/RSA_Decryption.png)

### Step 4: View the Decrypted Message

After decryption, CrypTool will display the **original plaintext**:

```
Hello SecureBank! This is a confidential message.
```

![View decrypted message]

![alt text](../Screenshots/View_Decrypted_RSA.png)

### Step 5: Verify Correctness

Check that the decrypted message matches the original plaintext exactly:

| Original                                          | Decrypted                                         | Match? |
| :------------------------------------------------ | :------------------------------------------------ | :----- |
| Hello SecureBank! This is a confidential message. | Hello SecureBank! This is a confidential message. | ✓ Yes |

---

## Part 6: Understanding RSA Encryption

### Step 1: Explore RSA Parameters

CrypTool shows the mathematical components of RSA:

| Parameter                      | Description                    | Example Value       |
| :----------------------------- | :----------------------------- | :------------------ |
| **n (modulus)**          | Product of two primes (p × q) | `0x00c4...`       |
| **e (public exponent)**  | Typically 65537                | `0x10001`         |
| **d (private exponent)** | Modular inverse of e           | `0x3b0...`        |
| **p (prime factor)**     | First large prime              | (hidden by default) |
| **q (prime factor)**     | Second large prime             | (hidden by default) |

![RSA parameters]

![alt text](../Screenshots/RSA_Parameters.png)

### Step 2: Message Size Limitations

RSA can only encrypt messages smaller than the key size:

| Key Size | Max Message Size (bytes) | Max Message Size (characters) |
| :------- | :----------------------- | :---------------------------- |
| 1024-bit | 117 bytes                | ~117 characters               |
| 2048-bit | 245 bytes                | ~245 characters               |
| 4096-bit | 501 bytes                | ~501 characters               |

> **Note:** For longer messages, use hybrid encryption (RSA to encrypt a symmetric key, then symmetric encryption for the message).

### Step 3: Try Different Key Sizes

Experiment with different RSA key sizes:

| Key Size  | Security Level         | Generation Time |
| :-------- | :--------------------- | :-------------- |
| 512 bits  | Broken (do not use)    | Instant         |
| 1024 bits | Weak (deprecated)      | 1-2 seconds     |
| 2048 bits | Standard (recommended) | 2-5 seconds     |
| 4096 bits | High security          | 10-30 seconds   |

---

## Part 7: Digital Signatures with RSA (Optional)

RSA can also be used for **digital signatures** (the opposite of encryption):

### Step 1: Sign a Message

1. Using your **private key**, you can "sign" a message
2. The signature proves you are the sender

### Step 2: Verify a Signature

1. Using your **public key**, anyone can verify the signature
2. Confirms the message hasn't been tampered with

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    RSA DIGITAL SIGNATURE PROCESS                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   SENDER                                              RECIPIENT              │
│                                                                              │
│   ┌─────────────┐                                   ┌─────────────┐         │
│   │  Message    │                                   │  Message    │         │
│   └──────┬──────┘                                   └──────┬──────┘         │
│          │                                                 │                │
│          │  Hash + Sign with                              │  Verify with   │
│          │  PRIVATE KEY                                    │  PUBLIC KEY    │
│          ▼                                                 ▼                │
│   ┌─────────────┐                                   ┌─────────────┐         │
│   │  Signature  │────────► Encrypted───────────────►│  Verified   │         │
│   │             │         (Hash of message)         │  ✓ or ✗     │         │
│   └─────────────┘                                   └─────────────┘         │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Lab Completion Checklist

| Task                                        | Completed |
| :------------------------------------------ | :-------- |
| **Part 1: Installation**              | ☐        |
| Downloaded CrypTool 2.1                     | ☐        |
| Installed CrypTool 2.1                      | ☐        |
| Launched CrypTool 2.1                       | ☐        |
| **Part 2: RSA Setup**                 | ☐        |
| Created new Encryption/Decryption template  | ☐        |
| Selected RSA algorithm                      | ☐        |
| **Part 3: Generate Keys**             | ☐        |
| Generated RSA key pair (2048-bit)           | ☐        |
| Viewed public and private keys              | ☐        |
| Saved keys to files                         | ☐        |
| **Part 4: Encrypt Message**           | ☐        |
| Entered plaintext message                   | ☐        |
| Encrypted with public key                   | ☐        |
| Viewed ciphertext                           | ☐        |
| **Part 5: Decrypt Message**           | ☐        |
| Decrypted with private key                  | ☐        |
| Verified decrypted message matches original | ☐        |
| **Part 6: Understanding RSA**         | ☐        |
| Explored RSA parameters (n, e, d)           | ☐        |
| Understood size limitations                 | ☐        |

---

## Screenshot Checklist

| Screenshot     | File Name                     | Description                 |
| :------------- | :---------------------------- | :-------------------------- |
| Generate Keys  | `RSA_Generate_Keys.png`     | RSA key generation screen   |
| Public Key     | `RSA_Public_Key.png`        | Display of public key       |
| Private Key    | `RSA_Private_Key.png`       | Display of private key      |
| Plaintext      | `RSA_Plaintext.png`         | Message before encryption   |
| Encryption     | `RSA_Encryption_Result.png` | Ciphertext after encryption |
| Decryption     | `RSA_Decryption_Result.png` | Decrypted message           |
| RSA Parameters | `RSA_Parameters.png`        | Mathematical components     |

---

## Troubleshooting Tips

| Issue                                   | Solution                                                                 |
| :-------------------------------------- | :----------------------------------------------------------------------- |
| **CrypTool won't install**        | Run installer as Administrator; disable antivirus temporarily            |
| **Key generation takes too long** | Use 2048-bit keys (not 4096) for faster generation                       |
| **Encryption fails**              | Message may be too long; use shorter message or hybrid encryption        |
| **Decryption fails**              | Ensure you are using the correct private key that matches the public key |
| **Cannot find keys after saving** | Check the save location; search for `.pem` files                       |
| **Wrong key type error**          | Use public key for encryption, private key for decryption                |

---

## RSA vs Other Algorithms

| Feature                  | RSA                      | AES                  | ECC                 |
| :----------------------- | :----------------------- | :------------------- | :------------------ |
| **Type**           | Asymmetric               | Symmetric            | Asymmetric          |
| **Key Size**       | 2048-4096 bits           | 128-256 bits         | 256-512 bits        |
| **Speed**          | Slow                     | Fast                 | Medium              |
| **Best Use**       | Key exchange, signatures | Bulk data encryption | Mobile devices, IoT |
| **Security Level** | High (2048+)             | Very High            | High                |

---

## Test Your Knowledge

**Q1:** What does RSA stand for?

```
Your answer:
_________________________________________________________________________
```

**Q2:** Which key should be used for encryption (public or private)?

```
Your answer:
_________________________________________________________________________
```

**Q3:** Which key should be used for decryption (public or private)?

```
Your answer:
_________________________________________________________________________
```

**Q4:** Why is RSA not used to encrypt large files directly?

```
Your answer:
_________________________________________________________________________
_________________________________________________________________________
```

**Q5:** What is the current recommended minimum RSA key size?

```
Your answer:
_________________________________________________________________________
```

### Answer Key

| Q# | Answer                                                                 |
| -- | ---------------------------------------------------------------------- |
| 1  | Rivest-Shamir-Adleman (the three inventors)                            |
| 2  | Public Key                                                             |
| 3  | Private Key                                                            |
| 4  | RSA is slow and has size limitations (max ~245 bytes for 2048-bit key) |
| 5  | 2048 bits                                                              |

---

## Key Takeaways

| Concept                     | Description                                                          |
| :-------------------------- | :------------------------------------------------------------------- |
| **RSA**               | Asymmetric encryption algorithm using public/private key pairs       |
| **Public Key**        | Shared openly; used for encryption and signature verification        |
| **Private Key**       | Kept secret; used for decryption and signing                         |
| **Key Generation**    | Based on multiplication of two large prime numbers                   |
| **Size Limitations**  | RSA can only encrypt small messages (under key size)                 |
| **2048-bit**          | Current minimum recommended key size                                 |
| **Hybrid Encryption** | Use RSA to encrypt symmetric key, then symmetric encryption for data |

---

## Summary

In this lab, you have:

| Activity                                            | Completed |
| :-------------------------------------------------- | :-------- |
| Installed CrypTool 2.1                              | ☐        |
| Generated an RSA key pair (public and private keys) | ☐        |
| Encrypted a message using the RSA public key        | ☐        |
| Decrypted the ciphertext using the RSA private key  | ☐        |
| Verified the decrypted message matches the original | ☐        |
| Explored RSA parameters and size limitations        | ☐        |

---

## Additional Resources

| Resource                                                 | URL                                                               |
| :------------------------------------------------------- | :---------------------------------------------------------------- |
| **CrypTool Official Website**                      | https://www.cryptool.org                                          |
| **RSA Algorithm Explained**                        | https://www.cs.cornell.edu/courses/cs4820/2018fa/lectures/rsa.pdf |
| **NIST Digital Signature Standard (includes RSA)** | https://csrc.nist.gov/publications/detail/fips/186/5/final        |
| **OpenSSL RSA Documentation**                      | https://www.openssl.org/docs/man3.0/man1/openssl-rsa.html         |

---

## Congratulations!

You have successfully completed the **End-to-End Encryption/Decryption (RSA Algorithm)** lab. You now know how to:

- Install and use CrypTool 2.1
- Generate RSA public/private key pairs
- Encrypt messages using an RSA public key
- Decrypt messages using an RSA private key
- Understand the mathematical components of RSA (n, e, d)
- Recognize the size limitations of RSA encryption

These skills are essential for:

- Implementing secure communications
- Understanding public key infrastructure (PKI)
- Designing secure systems that use encryption
- Preparing for security certifications (CISSP, Security+, etc.)

---

**Next Steps:** Explore other CrypTool features:

- Digital signatures with RSA
- Hybrid encryption (RSA + AES)
- Different key sizes and their performance
- Other encryption algorithms (AES, ECC)
