---
layout: post
title: Understanding Hashing and Its Application with Encryption
comments: true
author: Chen Hao
categories: [Skills]
tags: [SSL, TLS, Security, Encryption]
---



**SHA** (Secure Hash Algorithm) is a family of cryptographic hash functions designed to take an input (or "message") and produce a fixed-size string of bytes, typically a hash value (also called a digest), that uniquely represents the input data. SHA is used for various security applications, such as verifying data integrity, digital signatures, and password storage. 

### Key Characteristics of SHA:
- **Fixed-Length Output**: No matter how large or small the input data is, SHA will always produce a fixed-length hash value. For example, SHA-256 always produces a 256-bit (32-byte) hash.
- **Deterministic**: The same input will always produce the same output hash.
- **One-Way Function**: It is computationally infeasible to reverse the process (i.e., to recover the original data from the hash).
- **Collision-Resistant**: It is designed so that it is extremely unlikely to find two different inputs that produce the same hash value. This ensures the uniqueness of the hash for different inputs.

### What is SHA Used For?

1. **Data Integrity Verification**:
   - SHA is commonly used to verify the integrity of data transmitted over networks or stored in files. By generating a hash of the original data before transmission or storage and comparing it with the hash of the received or retrieved data, you can check if the data has been altered in any way.
   - **Example**: When downloading software, a website may provide the SHA hash of the file. You can calculate the hash of the downloaded file and compare it to ensure the file hasn't been tampered with during the download process.

2. **Digital Signatures**:
   - In public key cryptography, SHA is used to generate a hash of a message, and the hash is then signed by a private key to create a digital signature. The recipient can verify the signature by hashing the message again and checking the hash against the signature, which ensures both the integrity and authenticity of the message.
   - **Example**: When a sender sends an email, the content of the email might be hashed using SHA and then signed with their private key. The recipient can use the sender’s public key to verify the message's authenticity and integrity.

3. **Password Hashing**:
   - SHA is used to hash passwords before they are stored in databases. Instead of saving the actual password, a hash of the password is stored. When users attempt to log in, the system hashes the entered password and compares it to the stored hash.
   - **Example**: A user’s password is hashed (e.g., using SHA-256) and stored in the database. When the user attempts to log in, the system hashes the entered password and checks if it matches the stored hash. This prevents the system from storing plaintext passwords.

4. **Cryptographic Applications**:
   - SHA is used in many cryptographic protocols, such as SSL/TLS for secure communication, and digital certificates to create a hash of the data being signed, which is then encrypted with the private key.
   - **Example**: In blockchain systems like Bitcoin, SHA-256 is used in mining processes to create hash values that ensure the integrity and security of transaction data.

5. **File Integrity and Checksums**:
   - SHA is used to create checksums for files. By generating the SHA hash of a file, you can create a fingerprint that can be used to check if the file has been modified over time.
   - **Example**: A backup service might generate an SHA checksum of your files when they are backed up. Later, when restoring files, the checksum can be used to verify that the files have not been altered or corrupted.

6. **Blockchain and Cryptocurrency**:
   - In blockchain systems, SHA-256 (a specific SHA algorithm) is extensively used in creating and validating blocks of data, ensuring the immutability of the blockchain.
   - **Example**: Bitcoin uses SHA-256 in its proof-of-work algorithm to secure transactions and prevent tampering.

### Variants of SHA
SHA has several variants, which produce hash values of different lengths and are optimized for different use cases:
- **SHA-1**: Produces a 160-bit hash value (20 bytes). It is now considered weak and vulnerable to collision attacks and should not be used for security-sensitive applications.
- **SHA-256**: Part of the SHA-2 family, it produces a 256-bit hash value (32 bytes). It is commonly used in applications like SSL certificates, digital signatures, and blockchain.
- **SHA-512**: Also part of the SHA-2 family, it produces a 512-bit hash value (64 bytes). It is used in scenarios that require higher security.
- **SHA-3**: A newer family of algorithms, designed to offer an alternative to SHA-2, using a different underlying structure (Keccak). SHA-3 is used where extra security is required or to avoid vulnerabilities in SHA-2.

### Example of SHA in Action:
- **SHA-256 Example**:
  - Input: "Hello, world!"
  - SHA-256 Hash: `a591a6d40bf420404a011733cfb7b190d62c65bf0bcda1b070b0f3790e10d52d`

Even a tiny change in the input (e.g., changing "Hello, world!" to "Hello, world?") would result in a completely different hash.

### Example Application in Email Communication

SHA (Secure Hash Algorithm) is a cryptographic function that is widely used for ensuring data integrity, creating digital signatures, and securely storing passwords. Its one-way nature and resistance to collisions make it an essential tool in cryptography and data security. Although older variants like SHA-1 are no longer secure, newer versions such as SHA-256 and SHA-3 continue to play a crucial role in securing digital communications and data. Let's walk through a detailed example of how **SHA hashing** and **digital signatures** work together when a sender sends an email, using SHA and a private key for signing, and how the recipient uses the sender's public key to verify the authenticity and integrity of the email. 

### The Process

1. **Sender's Side (Email Signing)**:
   - **Step 1: Hashing the Email Content**  
     The sender takes the email content (message body, attachments, etc.) and applies a **SHA hashing function** (for example, SHA-256) to it. This will create a fixed-length hash (digest) that represents the content of the email.
   
     **Example**:  
     - **Email Content**: "Hello Bob, please find the attached report."
     - **SHA-256 Hash**: `a591a6d40bf420404a011733cfb7b190d62c65bf0bcda1b070b0f3790e10d52d` (a 64-character hexadecimal string)

   - **Step 2: Signing the Hash with the Sender's Private Key**  
     Next, the sender signs the hash of the email using their **private key**. This creates a **digital signature** that is unique to the email content and the sender.
     
     The private key used for signing is kept secret, and only the sender possesses it. The digital signature will be a unique encrypted string that can only be decrypted with the sender’s public key.
   
     **Digital Signature Example**:  
     After applying the private key, the sender’s signature might look like this (it’s just an example and would be much longer in practice):  
     `b3d22ffb8758e17fdf6c1b1a948682b01d8e1c...`

2. **Sender Sends the Email**:  
   The sender then sends the email to the recipient along with the **email content** and the **digital signature**.

   The email is sent like this:
   - **Email Content**: "Hello Bob, please find the attached report."
   - **Digital Signature**: `b3d22ffb8758e17fdf6c1b1a948682b01d8e1c...`

3. **Recipient's Side (Email Verification)**:
   - **Step 1: Recipient Receives the Email**  
     The recipient receives the email, which contains the original email content and the digital signature.

   - **Step 2: Hash the Received Email Content**  
     The recipient will then apply the same SHA hashing function (SHA-256, in this case) to the **received email content** (the message and attachments) to generate a hash of the email they’ve received.
   
     The recipient hashes the email content:  
     - **Email Content**: "Hello Bob, please find the attached report."
     - **SHA-256 Hash**: `a591a6d40bf420404a011733cfb7b190d62c65bf0bcda1b070b0f3790e10d52d`
     
     This is the **same hash** that the sender generated when they signed the email.

   - **Step 3: Decrypt the Digital Signature Using the Sender's Public Key**  
     Now, the recipient uses the **public key** of the sender (which is publicly available, e.g., on the sender's website or provided via a certificate) to **decrypt the digital signature**.  
     This decrypted signature is a hash that was generated by the sender when they signed the original message with their private key.

     Using the public key, the recipient is able to decrypt the signature to obtain the hash value that the sender created before signing it.
     
     **Decrypted Signature Hash**:  
     The decrypted signature yields the **hash**: `a591a6d40bf420404a011733cfb7b190d62c65bf0bcda1b070b0f3790e10d52d`.

   - **Step 4: Compare the Two Hashes**  
     Now, the recipient compares the two hash values:
     - The hash they generated by hashing the received email content.
     - The hash they decrypted from the digital signature.
   
     If both hashes match, it means the email has not been tampered with and the signature is valid. Therefore, the recipient can be sure that:
     - The email **hasn't been altered** since it was sent by the sender (data integrity).
     - The email **was indeed sent by the sender** who holds the private key corresponding to the public key (authenticity).

   If the hashes do not match, it indicates that the email has been altered or the signature is invalid, and the recipient can discard the email as potentially compromised or fake.

---


Note that in many encryption scenarios, the **public key** is used for encryption, and the **private key** is used for decryption. This is the classic approach in **asymmetric encryption**. However, in the example of digitally signing an email, the roles are reversed—but for good reason:


### **Encryption vs. Signing**

1. **Encryption**:
   - **Goal**: Keep data confidential.
   - The sender uses the recipient’s **public key** to encrypt a message.
   - The recipient uses their **private key** to decrypt the message.
   - Example use case: Sending sensitive information securely.

2. **Digital Signing**:
   - **Goal**: Ensure authenticity and integrity.
   - The sender uses their **private key** to generate a signature (sign the data).
   - The recipient uses the sender’s **public key** to verify the signature.
   - Example use case: Proving the sender’s identity and ensuring the message wasn’t tampered with.


### **Why the Roles are Reversed in Signing**
In the case of digital signatures, the intent is not to encrypt the message but to **prove the sender’s identity** and the **integrity of the message**. Here's why the roles are reversed:

1. **Private Key for Signing**:
   - Only the sender has access to their private key.
   - Signing with the private key ensures that only the sender could have created the signature.
   
2. **Public Key for Verification**:
   - The public key is widely available.
   - Anyone with the sender’s public key can verify that the message and signature were created by the sender.


### **How This Works in the Email Case**
1. **Hash the Email Content**:
   - The email content is hashed using a hashing algorithm like SHA-256, producing a fixed-length hash value.

2. **Sign the Hash**:
   - The sender encrypts the hash using their **private key**, creating the digital signature.

3. **Attach Signature**:
   - The signature is attached to the email and sent to the recipient.

4. **Verify the Signature**:
   - The recipient uses the sender’s **public key** to decrypt the signature.
   - The recipient computes the hash of the received email content and compares it to the decrypted signature.

5. **If They Match**:
   - The signature is valid, proving:
     - The email was sent by the sender (authenticity).
     - The content has not been tampered with (integrity).


### **Why This Makes Sense**
- Using the **private key** to sign ensures that only the sender can generate the signature, as the private key is secret.
- Verifying with the **public key** allows anyone to confirm authenticity without needing access to the private key.


### **Summary**
In digital signing:
- The private key ensures **authenticity** (only the sender can sign).
- The public key ensures **verification** (anyone can check the signature).

In encryption:
- The public key ensures **confidentiality** (only the intended recipient can decrypt with their private key). 

Let me know if you'd like further clarification!