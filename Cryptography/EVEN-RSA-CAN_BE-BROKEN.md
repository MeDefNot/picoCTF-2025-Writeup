
# Description
This service provides you an encrypted flag. Can you decrypt it with just N & e?
Connect to the program with netcat:
`$ nc verbal-sleep.picoctf.net 51510`
The program's source code can be downloaded here.

# Hints
1. How much do we trust randomness?
2. Notice anything interesting about N?
3. Try comparing N across multiple requests

# Solution
Connecting to `$ nc verbal-sleep.picoctf.net 51510`

<br>
![image](https://github.com/user-attachments/assets/c7d7af01-5f28-4e49-9d35-9aa6ed6b2653)


After reading how RSA works, you'll know N is the product of two prime numbers. We can see N ends with 2, meaning the two prime numbers are 2 amd N/2. Puttinng these in an RSA decryptor, we get our flag

Used `https://www.dcode.fr/rsa-cipher` 

![Untitled](https://github.com/user-attachments/assets/45cf116c-2e81-4bba-a268-e50584a84060)
