---
layout: post
title: Secure Remote Server Access use SSH Key Authentication
comments: true
author: Chen Hao
categories: [Skills]
tags: [SSH, Cybersecurity, linux]
---

Secure Shell (SSH) is a powerful tool for remote server access, but it can be daunting for beginners. This guide demystifies SSH, walking you through key concepts, setup processes, and best practices. Whether you're a budding developer or a curious tech enthusiast, you'll learn how to securely connect to remote servers like a pro.

## Understanding SSH Key Authentication

SSH key authentication is a secure method for accessing remote servers without using passwords. Here's what you need to know:

- **Key Pair**: SSH uses a public-private key pair for authentication.
- **Security**: It's more secure than password-based authentication.
- **Convenience**: Once set up, it allows for password-less logins.

### Setting Up SSH Keys in Your Local Machine

Follow these steps to set up SSH key authentication:

1. Generate the key pair on your local machine:
   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
2. Copy the public key to the server:
   ```bash
   ssh-copy-id username@remote_host
   ```
3. Ensure proper permissions:
   ```bash
   chmod 600 ~/.ssh/id_ed25519
   chmod 644 ~/.ssh/id_ed25519.pub
   ```

### Ed25519 vs RSA: Choosing Your Key Type

When generating SSH keys, you'll encounter different algorithms. Here's a comparison of Ed25519 and RSA:

| Feature | Ed25519 | RSA |
|---------|---------|-----|
| Security | Higher for equivalent key sizes | Good, but requires larger keys |
| Key Size | Smaller (256 bits) | Larger (2048 or 4096 bits) |
| Performance | Faster | Slower |
| Compatibility | Newer systems | Widely supported |

Ed25519 is recommended for new deployments due to its superior security and performance.

## Configuring SSH on the Server

1. Create the .ssh directory if it doesn't exist:
   ```bash
   mkdir -p ~/.ssh && chmod 700 ~/.ssh
   ```

2. Create or edit the authorized_keys file:
   ```bash
   nano ~/.ssh/authorized_keys
   ```
   Paste the public key you copied from your local machine into this file.

3. Set the correct permissions:
   ```bash
   chmod 600 ~/.ssh/authorized_keys
   ```

4. Modify the SSH configuration to enable key-based authentication:
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```
   Ensure these lines are set:
   ```
   PubkeyAuthentication yes
   PasswordAuthentication no
   ```

5. Restart the SSH service:
   ```bash
   sudo systemctl restart sshd
   ```


## Conect to Server using SSH Key Authentication

Test the connection:

```bash
ssh -i /path/to/your/private_key username@remote_host
```


### Troubleshooting Common SSH Issues

If you encounter issues, try these solutions:

1. **Permission denied (publickey)**: Check key permissions and authorized_keys file.
2. **Too open permissions**: Use `chmod 600` for private keys and `chmod 644` for public keys.
3. **Invalid format**: Ensure you're using the private key, not the public key (.pub file).


