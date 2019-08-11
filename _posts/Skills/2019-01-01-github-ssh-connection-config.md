---
layout: post
title: Setup SSH Connection to Github
comments: true
categories: [Skills]
tags: [terminal, bash, bash-it, macbook, shell, theme]
---


When you set up SSH, you'll generate an SSH key and add it to the `ssh-agent` and then add the key to your GitHub account. Adding the SSH key to the `ssh-agent` ensures that your SSH key has an extra layer of security through the use of a `passphrase`. 


### 1. Generating a new SSH key

```bash
cd /Users/haochen/.ssh
ssh-keygen -t rsa -b 4096 -C "haoeric@hotmail.com"
#- file in which to save the key (/Users/haochen/.ssh/id_rsa): hit enter
#- passphrase: xxxxxxxxxx
```

### 2. Adding your SSH key to the ssh-agent

Start the ssh-agent in the background.

```bash
eval "$(ssh-agent -s)"
```

Then modify your ~/.ssh/config file to automatically load keys into the ssh-agent and store passphrases in your keychain.

```bash
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```

Add your key to the ssh-agent

```bash
ssh-add -K ~/.ssh/id_rsa
```

## 3. Adding a new SSH key to your GitHub account

Copy the SSH public key to your clipboard with command `pbcopy < ~/.ssh/id_rsa.pub`, then go to **profile photo > Settings > SSH and GPG keys > New SSH key > Paste your key into the "Key" field**.

Then you are done, you can start working with your github repositories.

