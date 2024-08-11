# [easy\_one (★☆☆☆☆)](https://crackmes.one/crackme/5d443bb533c5d444ad3018b3)



| Language | Arch   | Platform | Time to Complete  | Tools Used |
| -------- | ------ | -------- | ----------------- | ---------- |
| C/C++    | x86-64 | Mac OS X | 1 hour 10 minutes | Ghidra     |


### Description and Solution

The goal was to find the password and enter it in the terminal. The solution password was any length 10 string that starts and end with the same character. A sample solution is

> x12345678x

### Walkthrough

Ghidra easily decompiled the file into the following mostly manageable code:

```c

undefined4 entry(void)

{
  size_t sVar1;
  char local_118 [9];
  char local_10f;
  long local_10;
  
  local_10 = *(long *)PTR____stack_chk_guard_100001000;
  _printf("Enter the password...\n");
  _fgets(local_118,0x100,*(FILE **)PTR____stdinp_100001008);
  sVar1 = _strcspn(local_118,"\n");
  local_118[sVar1] = '\0';
  sVar1 = _strlen(local_118);
  if ((int)sVar1 == 10) {
    if (local_118[0] == local_10f) {
      _printf("Correct!\nthe password is: %s\n",local_118);
    }
    else {
      _wrong_password();
    }
  }
  else {
    _wrong_password();
  }
  if (*(long *)PTR____stack_chk_guard_100001000 == local_10) {
    return 0;
  }
                    /* WARNING: Subroutine does not return */
  ___stack_chk_fail();
}


```



Immediately, the plain text strings made it easy to follow the execution of the code. It is also obvious that there are two conditions that must be met in order to find the correct password. 



The first condition is trivial. It is evident from the decompiled code that the password is 10 characters. However, the second condition is not immediately obvious.



Because this is my first attempt at reverse engineering, a lot of time was spent exploring options within Ghidra and understanding how it worked. Further time was spent understanding the assembly code, as I am only familiar with RISC-V. 



My initial reaction was to understand the value of local\_10f so I could ensure the comparison. I spent a lot of time trying to follow the value throughout the assembly. However, eventually I made the realization that 

```c
if (local_118[0] == local_10f)
```

had a respective CMP instruction that I could analyze.

From this, I understood how the first character is stored in the register, and used that information to determine that local\_10f was the last character. All together, that yielded the solution that any string of length 10 with matching first and lasts characters was a valid password.

<img width="194" alt="Screenshot 2024-08-11 at 23 22 01" src="https://github.com/user-attachments/assets/11a69124-7e81-46c5-ac6c-5394b8fdabcc">

### Takeaways and Learning

- Don’t be afraid to explore and spend time understanding your tools

- When you can find patterns that will help your understanding, use them

- CMP and Branching Instructions
