# [Crackme0x02 (★☆☆☆☆)](https://crackmes.one/crackme/653d880f0f4238b24302b0dc)



| Language | Arch   | Platform | Time to Complete  | Tools Used |
| -------- | ------ | -------- | ----------------- | ---------- |
| C/C++    | x86-64 | Mac OS X | 2 minutes | Ghidra     |


### Description and Solution

The goal was to find the password and enter it in the terminal. The solution password was

> 14478

### Walkthrough

```c
undefined8 entry(void)

{
  undefined4 local_10;
  undefined4 local_c;
  
  local_c = 0;
  _printf("Crackme Level 0x02 (created by Nox)\n");
  _printf("\nEnter the passphrase: ");
  _scanf("%99d",&local_10);
  _check(local_10,0x388e);
  return 1;
}

```

The text outputs this time have been obfuscated. However, ignoring that, you can still see that the input is compared against a hex number, so converting that to decimal yields the correct answer.

### Takeaways and Learning

- Easy
