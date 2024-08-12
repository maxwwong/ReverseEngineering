# [Crackme0x01 (★☆☆☆☆)](https://crackmes.one/crackme/653d87f30f4238b24302b0d4)



| Language | Arch   | Platform | Time to Complete  | Tools Used |
| -------- | ------ | -------- | ----------------- | ---------- |
| C/C++    | x86-64 | Mac OS X | 2 minutes | Ghidra     |


### Description and Solution

The goal was to find the password and enter it in the terminal. The solution password was

> 45067

### Walkthrough

Finding the CMP instruction immediately revealed that the input was being compared with the hex number 0xb00b. When translated to decimal this gave the correct password.

### Takeaways and Learning

- Easy
