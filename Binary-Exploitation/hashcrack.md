# Description
A company stored a secret message on a server which got breached due to the admin using weakly hashed passwords. Can you gain access to the secret stored within the server?
Access the server using nc verbal-sleep.picoctf.net 62644

# Hints
1. Understanding hashes is very crucial. Read more here. (https://primer.picoctf.org/#_hashing)
2. Can you identify the hash algorithm? Look carefully at the length and structure of each hash identified.
3. Tried using any hash cracking tools?

# Solution

When connected to `nc verbal-sleep.picoctf.net 62644`, three hashed data are shown on the screen
```
Welcome!! Looking For the Secret?

We have identified a hash: 482c811da5d5b4bc6d497ffa98491e38
Enter the password for identified hash:
```
I just used `https://crackstation.net/` to solve the hashes. 
