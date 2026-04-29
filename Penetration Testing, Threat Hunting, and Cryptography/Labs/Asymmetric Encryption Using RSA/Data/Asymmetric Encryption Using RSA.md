![alt text](<../Screenshots/PhpMyAdmin_logo (1).png>)

# Lab: Asymmetric Encryption Using RSA

**Estimated time needed:** 30 minutes

---

## Overview

In this lab, you will learn how to encrypt and decrypt files using **RSA encryption** with OpenSSL. RSA (Rivest-Shamir-Adleman) is an asymmetric encryption algorithm that uses a pair of keys: a **public key** for encryption and a **private key** for decryption.

This lab will involve generating RSA keys, encrypting a file using the public key, and decrypting it using the private key.

---

## Learning Objectives

After completing this lab, you will be able to:

| # | Objective                                                   |
| - | ----------------------------------------------------------- |
| 1 | Create RSA key pairs for asymmetric encryption              |
| 2 | Encrypt files using RSA public keys                         |
| 3 | Decrypt files using RSA private keys                        |
| 4 | Understand the relationship between public and private keys |

---

## Prerequisites (Optional)

| Requirement                  | Description                                     |
| :--------------------------- | :---------------------------------------------- |
| **Linux command line** | Familiarity with using the Linux command prompt |
| **OpenSSL**            | Preinstalled in the lab environment             |
| **Terminal access**    | For executing commands                          |

---

## What is Asymmetric Encryption?

Asymmetric encryption uses **two different keys** for encryption and decryption:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    ASYMMETRIC ENCRYPTION (RSA)                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│                              ┌─────────────────┐                            │
│                              │  PUBLIC KEY     │                            │
│                              │  (shared openly)│                            │
│                              └────────┬────────┘                            │
│                                       │                                      │
│   ┌─────────────┐                    │                    ┌─────────────┐   │
│   │ Plaintext   │                    │                    │ Ciphertext  │   │
│   │ "Secret     │ ──── Encrypt ──────┼───────────────────► │ 7F4E8C...   │   │
│   │  Message"   │                    │                    │             │   │
│   └─────────────┘                    │                    └──────┬──────┘   │
│                                      │                             │         │
│                                      │                             │         │
│                             ┌────────┴────────┐                   │         │
│                             │  PRIVATE KEY    │◄──────────────────┘         │
│                             │  (kept secret)  │     Decrypt                  │
│                             └─────────────────┘                             │
│                                      │                                       │
│                                      ▼                                       │
│                              ┌─────────────┐                                │
│                              │ Plaintext   │                                │
│                              │ "Secret     │                                │
│                              │  Message"   │                                │
│                              └─────────────┘                                │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### RSA vs Symmetric Encryption

| Feature                    | RSA (Asymmetric)                 | AES (Symmetric)                   |
| :------------------------- | :------------------------------- | :-------------------------------- |
| **Keys**             | Two keys (public + private)      | Single key                        |
| **Key Distribution** | Public key can be shared openly  | Must securely share key           |
| **Speed**            | Slow                             | Fast                              |
| **Key Size**         | 2048-4096 bits                   | 128-256 bits                      |
| **Best Use**         | Key exchange, digital signatures | Bulk data encryption              |
| **Security**         | Based on factoring large numbers | Based on substitution/permutation |

---

## Initializing the Lab Environment

### Step 1: Open a New Terminal

**Method 1 - Using the Terminal menu:**

1. Click **Terminal** in the top menu
2. Select **New Terminal** from the drop-down menu

**Method 2 - Using the Getting Started section:**

1. Locate the Getting Started section
2. Click the link to open a new terminal

![Open new terminal]

![alt text](../Screenshots/Open_New_Terminal.png)

### Step 2: Verify Terminal is Ready

After clicking **New Terminal**, a terminal window will open. You will enter all commands in this terminal.

![Terminal ready]

![alt text](../Screenshots/Terminal_Ready_RSA.png)

### Step 3: Verify OpenSSL Installation

Check that OpenSSL is installed and available:

```bash
openssl version
```

**Expected output:**

```
OpenSSL 3.0.2 15 Mar 2022 (Library: OpenSSL 3.0.2 15 Mar 2022)
```

![OpenSSL version]

![alt text](../Screenshots/OpenSSL_Version_RSA.png)

---

## Step 1: Generate RSA Private Key

The first step is to generate an RSA **private key**. This key must be kept secret and never shared.

### Command

```bash
openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
```

### Command Breakdown

| Parameter                         | Description                               |
| :-------------------------------- | :---------------------------------------- |
| `openssl genpkey`               | OpenSSL command to generate a private key |
| `-algorithm RSA`                | Use RSA algorithm                         |
| `-out private_key.pem`          | Save key to file `private_key.pem`      |
| `-pkeyopt rsa_keygen_bits:2048` | Generate a 2048-bit RSA key               |

### Alternative Command (Using `genrsa`)

```bash
openssl genrsa -out private_key.pem 2048
```

This older command does the same thing but with slightly different syntax.

### Expected Output

```
.+.....+...+......+..+...+
```

The output shows random noise as OpenSSL gathers entropy to generate a cryptographically secure key.

![Generate private key]

![alt text](../Screenshots/Generate_Private_Key.png)

### Verify Private Key

```bash
ls -la private_key.pem
```

**Expected output:**

```
-rw-r--r-- 1 user user 1679 Apr 28 10:00 private_key.pem
```

### View Private Key Contents

```bash
cat private_key.pem
```

**Expected output (example):**

```
-----BEGIN PRIVATE KEY-----
MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQCyvVVlV9va9KZl
zFYX+oXJhQYiMqyKq2nqXe7pQJ... (more lines) ...
-----END PRIVATE KEY-----
```

![View private key]

![alt text](../Screenshots/View_Private_Key.png)

**What the PEM format means:**

| Format                          | Description                                |
| :------------------------------ | :----------------------------------------- |
| `-----BEGIN PRIVATE KEY-----` | Standard PEM header for PKCS#8 private key |
| Base64 encoded data             | The actual key data                        |
| `-----END PRIVATE KEY-----`   | Standard PEM footer                        |

---

## Step 2: Generate RSA Public Key

Extract the **public key** from the private key. The public key can be shared openly with anyone who needs to encrypt data for you.

### Command

```bash
openssl rsa -pubout -in private_key.pem -out public_key.pem
```

### Command Breakdown

| Parameter               | Description                        |
| :---------------------- | :--------------------------------- |
| `openssl rsa`         | OpenSSL RSA key processing command |
| `-pubout`             | Output the public key              |
| `-in private_key.pem` | Read private key from this file    |
| `-out public_key.pem` | Save public key to this file       |

### Expected Output

```
writing RSA key
```

![Generate public key]

![alt text](../Screenshots/Generate_Public_Key.png)

### Verify Public Key

```bash
ls -la public_key.pem
```

**Expected output:**

```
-rw-r--r-- 1 user user 451 Apr 28 10:00 public_key.pem
```

### View Public Key Contents

```bash
cat public_key.pem
```

**Expected output (example):**

```
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyr1VZVfb2vSmZcxWF/qF
yYUQlBZB... (more lines) ...
-----END PUBLIC KEY-----
```

![View public key]

![alt text](../Screenshots/View_Public_Key.png)

### Understanding Key Differences

| Key Type              | File Size | Header                          | Purpose                           |
| :-------------------- | :-------- | :------------------------------ | :-------------------------------- |
| **Private Key** | ~1.6 KB   | `-----BEGIN PRIVATE KEY-----` | Keep SECRET; used for decryption  |
| **Public Key**  | ~450 B    | `-----BEGIN PUBLIC KEY-----`  | Share openly; used for encryption |

---

## Step 3: Create a File to Encrypt

Create a sample file containing sensitive information that needs to be encrypted.

### Command

```bash
echo "Confidential: SecureBank financial data for Q4 2024" > confidential.txt
```

### Verify File Contents

```bash
cat confidential.txt
```

**Expected output:**

```
Confidential: SecureBank financial data for Q4 2024
```

![Create confidential file]

![alt text](../Screenshots/Create_Confidential_File.png)

### Alternative: Create Multi-line File

```bash
cat > important_data.txt << EOF
Customer Name: John Doe
Account Number: 1234-5678-9012-3456
Transaction Amount: $10,000
Date: 2024-04-28
EOF
```

---

## Step 4: Encrypt the File Using RSA Public Key

Encrypt the confidential file using the **public key**. Anyone with the public key can encrypt, but only the private key holder can decrypt.

### Important Limitation

RSA encryption has a size limitation. With a 2048-bit key, you can only encrypt data up to **190 bytes** (less than 200 characters). For larger files, we use a hybrid approach (encrypt a symmetric key with RSA, then encrypt data with AES).

### Command

```bash
openssl rsautl -encrypt -inkey public_key.pem -pubin -in confidential.txt -out confidential.enc
```

### Command Breakdown

| Parameter                 | Description                          |
| :------------------------ | :----------------------------------- |
| `openssl rsautl`        | OpenSSL RSA utility (for small data) |
| `-encrypt`              | Encryption mode                      |
| `-inkey public_key.pem` | Use this key file                    |
| `-pubin`                | Input key is a public key            |
| `-in confidential.txt`  | Input file (plaintext)               |
| `-out confidential.enc` | Output file (encrypted)              |

### Alternative for Newer OpenSSL Versions

```bash
openssl pkeyutl -encrypt -pubin -inkey public_key.pem -in confidential.txt -out confidential.enc
```

### Expected Output (No output if successful)

![Encrypt file]

![alt text](../Screenshots/Encrypt_File_RSA.png)

### Verify Encrypted File

```bash
ls -la confidential*
```

**Expected output:**

```
-rw-r--r-- 1 user user  56 Apr 28 10:00 confidential.txt
-rw-r--r-- 1 user user 256 Apr 28 10:00 confidential.enc
```

Notice the encrypted file is **larger** (256 bytes) than the original (56 bytes) due to RSA padding.

### View Encrypted Content (Binary)

```bash
cat confidential.enc
```

The encrypted file will appear as **gibberish** (binary data):

```
�z�M���%t�Y�������΃n�o[�̮�6�=�s�|�O���i��f�w�p
```

![View encrypted file]

![alt text](../Screenshots/View_Encrypted_File.png)

### View in Hex Format (Optional)

```bash
xxd confidential.enc | head -5
```

---

## Step 5: Decrypt the Encrypted File Using RSA Private Key

Decrypt the file using the **private key**. Only the holder of the private key can decrypt the data.

### Command

```bash
openssl rsautl -decrypt -inkey private_key.pem -in confidential.enc -out confidential.decrypted
```

### Command Breakdown

| Parameter                       | Description                       |
| :------------------------------ | :-------------------------------- |
| `openssl rsautl`              | OpenSSL RSA utility               |
| `-decrypt`                    | Decryption mode                   |
| `-inkey private_key.pem`      | Use private key for decryption    |
| `-in confidential.enc`        | Input file (encrypted)            |
| `-out confidential.decrypted` | Output file (decrypted plaintext) |

### Alternative for Newer OpenSSL Versions

```bash
openssl pkeyutl -decrypt -inkey private_key.pem -in confidential.enc -out confidential.decrypted
```

### Expected Output (No output if successful)

![Decrypt file]

![alt text](../Screenshots/Decrypt_File_RSA.png)

### Verify Decrypted Content

```bash
cat confidential.decrypted
```

**Expected output:**

```
Confidential: SecureBank financial data for Q4 2024
```

![View decrypted file]

![alt text](../Screenshots/View_Decrypted_File.png)

### Verify Original and Decrypted Match

```bash
diff confidential.txt confidential.decrypted
```

No output means the files are identical.

---

## Step 6: Hybrid Encryption for Larger Files

Since RSA has size limitations, real-world implementations use **hybrid encryption**:

1. Generate a random symmetric key (e.g., AES-256)
2. Encrypt the large file with the symmetric key (fast)
3. Encrypt the symmetric key with RSA public key (secure)
4. Send both encrypted key and encrypted file

### Command for Hybrid Encryption

```bash
# Step 1: Generate random symmetric key
openssl rand -base64 32 > symmetric.key

# Step 2: Encrypt large file with AES (using symmetric key)
openssl enc -aes-256-cbc -salt -in large_file.txt -out large_file.enc -pass file:symmetric.key

# Step 3: Encrypt symmetric key with RSA public key
openssl rsautl -encrypt -pubin -inkey public_key.pem -in symmetric.key -out symmetric.key.enc

# Step 4: Decrypt symmetric key with RSA private key
openssl rsautl -decrypt -inkey private_key.pem -in symmetric.key.enc -out symmetric.key.dec

# Step 5: Decrypt large file with recovered symmetric key
openssl enc -d -aes-256-cbc -in large_file.enc -out large_file.dec -pass file:symmetric.key.dec
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    HYBRID ENCRYPTION WORKFLOW                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   SENDER                                          RECIPIENT                  │
│                                                                              │
│   ┌─────────────┐                               ┌─────────────┐             │
│   │ Large File  │                               │ Large File  │             │
│   │   (1+ MB)   │                               │ (Decrypted) │             │
│   └──────┬──────┘                               └──────▲──────┘             │
│          │                                             │                     │
│          │ AES Encrypt                                 │ AES Decrypt         │
│          ▼                                             │                     │
│   ┌─────────────┐      ┌─────────────┐        ┌─────────────┐               │
│   │ Symmetric   │      │ Encrypted   │        │ Symmetric   │               │
│   │ Key (AES)   │─────►│ Symmetric   │───────►│ Key (AES)   │               │
│   └──────┬──────┘ RSA  │ Key         │   RSA  └─────────────┘               │
│          │ Encrypt     └─────────────┘  Decrypt                              │
│          │                                                                   │
│          └──────────────────────────────────────────────────────────────┘   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Step 7: Clean Up (Optional)

### Remove Sensitive Files

When you're finished, securely delete sensitive files:

```bash
# Securely delete plaintext files (if no longer needed)
shred -u confidential.txt
shred -u confidential.decrypted

# Remove encrypted files (if desired)
rm -f confidential.enc

# Remove keys (if no longer needed - be careful!)
# shred -u private_key.pem
# shred -u public_key.pem
```

### List Remaining Files

```bash
ls -la
```

---

## Complete Command Summary

| Step | Command                                                                                             | Purpose                  |
| :--- | :-------------------------------------------------------------------------------------------------- | :----------------------- |
| 1    | `openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048`               | Generate private key     |
| 2    | `openssl rsa -pubout -in private_key.pem -out public_key.pem`                                     | Generate public key      |
| 3    | `echo "message" > confidential.txt`                                                               | Create test file         |
| 4    | `openssl rsautl -encrypt -pubin -inkey public_key.pem -in confidential.txt -out confidential.enc` | Encrypt with public key  |
| 5    | `openssl rsautl -decrypt -inkey private_key.pem -in confidential.enc -out confidential.decrypted` | Decrypt with private key |
| 6    | `cat confidential.decrypted`                                                                      | Verify decryption        |

---

## Troubleshooting Guide

| Issue                           | Possible Cause              | Solution                              |
| :------------------------------ | :-------------------------- | :------------------------------------ |
| `openssl: command not found`  | OpenSSL not installed       | Run `sudo apt install openssl`      |
| `Error reading input file`    | File doesn't exist          | Check filename with `ls -la`        |
| `data too large for key size` | File larger than ~190 bytes | Use hybrid encryption approach        |
| `unable to load Private Key`  | Wrong file format           | Ensure key starts with `-----BEGIN` |
| `Expecting: PUBLIC KEY`       | Wrong key type              | Use `-pubin` with public key        |
| `bad decrypt`                 | Wrong key used              | Must use matching key pair            |

---

## Security Best Practices

| Best Practice                    | Description                                                     |
| :------------------------------- | :-------------------------------------------------------------- |
| **Key size**               | Use at least 2048-bit RSA (3072 or 4096 for higher security)    |
| **Private key protection** | Never share private key; use strong permissions (`chmod 600`) |
| **Key backup**             | Securely backup private keys in offline/encrypted storage       |
| **Key rotation**           | Generate new key pairs periodically                             |
| **Use hybrid encryption**  | For large files, use RSA to encrypt a symmetric key             |
| **Secure deletion**        | Use `shred` to securely delete plaintext files                |

---

## RSA Key Sizes and Security Levels

| Key Size            | Security Level               | Use Case                      |
| :------------------ | :--------------------------- | :---------------------------- |
| **1024 bits** | Weak (deprecated)            | Not recommended               |
| **2048 bits** | Standard (128-bit security)  | General purpose (recommended) |
| **3072 bits** | High (128-bit security)      | Long-term protection          |
| **4096 bits** | Very High (156-bit security) | Highly sensitive data         |

---

## Lab Completion Checklist

| Step                     | Task                                        | Completed |
| :----------------------- | :------------------------------------------ | :-------- |
| **Initialization** | Opened new terminal                         | ☐        |
| **Step 1**         | Generated RSA private key (2048-bit)        | ☐        |
| **Step 2**         | Extracted RSA public key                    | ☐        |
| **Step 3**         | Created confidential.txt test file          | ☐        |
| **Step 4**         | Encrypted file using public key             | ☐        |
| **Step 5**         | Decrypted file using private key            | ☐        |
| **Step 6**         | Verified decrypted content matches original | ☐        |
| **Cleanup**        | (Optional) Securely deleted sensitive files | ☐        |

---

## Screenshot Checklist

| Screenshot           | File Name               | Description                               |
| :------------------- | :---------------------- | :---------------------------------------- |
| Generate Private Key | `RSA_Private_Key.png` | Private key generation command and output |
| Generate Public Key  | `RSA_Public_Key.png`  | Public key extraction command             |
| Key Files            | `RSA_Key_Files.png`   | `ls -la` showing both key files         |
| Encrypt File         | `RSA_Encrypt.png`     | Encryption command and verification       |
| Decrypt File         | `RSA_Decrypt.png`     | Decryption command and output             |
| Verification         | `RSA_Verify.png`      | `cat` showing decrypted content         |

---

## Key Takeaways

| Concept                         | Description                                                        |
| :------------------------------ | :----------------------------------------------------------------- |
| **Asymmetric Encryption** | Uses two keys: public (encrypt) and private (decrypt)              |
| **RSA**                   | Most common asymmetric algorithm; based on factoring large numbers |
| **Public Key**            | Can be shared openly; used for encryption                          |
| **Private Key**           | Must be kept secret; used for decryption                           |
| **Key Size**              | 2048-bit is minimum recommended for RSA                            |
| **RSA Limitations**       | Cannot encrypt data larger than key size (~190 bytes for 2048-bit) |
| **Hybrid Encryption**     | RSA encrypts symmetric key; symmetric key encrypts data            |

---

## Test Your Knowledge

**Q1:** What is the main difference between RSA and AES encryption?

```
Your answer:
_________________________________________________________________________
_________________________________________________________________________
```

**Q2:** Why can't we encrypt a 1 MB file directly with RSA 2048-bit?

```
Your answer:
_________________________________________________________________________
_________________________________________________________________________
```

**Q3:** Which key should you share with others to allow them to encrypt messages for you?

```
Your answer:
_________________________________________________________________________
```

**Q4:** What happens if you lose your private key?

```
Your answer:
_________________________________________________________________________
_________________________________________________________________________
```

---

## Additional Resources

| Resource                               | URL                                                               |
| :------------------------------------- | :---------------------------------------------------------------- |
| **OpenSSL Documentation**        | https://www.openssl.org/docs/                                     |
| **RSA Algorithm Explained**      | https://www.cs.cornell.edu/courses/cs4820/2018fa/lectures/rsa.pdf |
| **NIST Cryptographic Standards** | https://csrc.nist.gov/projects/cryptographic-standards            |
| **OpenSSL Cookbook**             | https://www.feistyduck.com/library/openssl-cookbook/              |

---

## Summary

In this lab, you have:

| Activity                                            | Completed |
| :-------------------------------------------------- | :-------- |
| Generated an RSA 2048-bit private key               | ☐        |
| Extracted the corresponding public key              | ☐        |
| Created a test file with confidential data          | ☐        |
| Encrypted the file using the public key             | ☐        |
| Decrypted the file using the private key            | ☐        |
| Verified the decrypted content matched the original | ☐        |
| Learned about hybrid encryption for larger files    | ☐        |

---

## Congratulations!

You have successfully completed the **Asymmetric Encryption Using RSA** lab. You now know how to:

- Generate RSA public/private key pairs using OpenSSL
- Encrypt files using RSA public keys
- Decrypt files using RSA private keys
- Understand the limitations of direct RSA encryption
- Apply hybrid encryption for larger files

These skills are essential for:

- Securing sensitive data in transit (TLS/SSL)
- Implementing digital signatures
- Designing secure communication protocols
- Managing encryption keys in enterprise environments

---

**Next Steps:** Practice generating larger keys (4096-bit) and implement hybrid encryption for a multi-line file.
