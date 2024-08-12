# [Crackme0x03 (★★☆☆☆)](https://crackmes.one/crackme/653d88460f4238b24302b0e4)



| Language | Arch   | Platform | Time to Complete  | Tools Used |
| -------- | ------ | -------- | ----------------- | ---------- |
| C/C++    | x86-64 | Mac OS X | 10 minutes | Ghidra     |


### Description and Solution

The goal was to find the password and enter it in the terminal. The solution was any sequence of numbers that adds up to 15. For example

> 12345

### Walkthrough

Here is the initially decompiled code.

```c
undefined8 entry(void)

{
  undefined local_78 [104];
  long local_10;
  
  local_10 = *(long *)PTR____stack_chk_guard_100004000;
  _printf("Crackme Level 0x03 (created by Nox)\n");
  _printf("\nEnter the passcode: ");
  _scanf("%99s",local_78);
  FUN_100003e00(local_78);
  if (*(long *)PTR____stack_chk_guard_100004000 == local_10) {
    return 0;
  }
                    /* WARNING: Subroutine does not return */
  ___stack_chk_fail();
}
```

Immediately, it is clear that we are storing the input in local_78 and running the function FUN_100003e00 with it as a parameter. For now, I ignore the code following the 
function because it seems like it is the failure branch.


FUN_100003e00 decompiled shows this

```c
void FUN_100003e00(char *input)

{
  size_t sVar1;
  int local_20;
  int local_1c;
  int local_18;
  char local_11;
  char *local_10;
  
  local_1c = 0;
  local_20 = 0;
  local_10 = input;
  sVar1 = _strlen(input);
  for (; local_1c < (int)sVar1; local_1c = local_1c + 1) {
    local_11 = local_10[local_1c];
    _sscanf(&local_11,"%d",&local_18);
    local_20 = local_18 + local_20;
  }
  if (local_20 == 0xf) {
    FUN_100003ea0();
                    /* WARNING: Subroutine does not return */
    _exit(0);
  }
  _puts("Invalid passcode.\n");
  return;
}
```

From here, I immediately follow FUN_100003ea0 and find that it prints that I've found a correct password. So, I know that local_20 must be equal to 0xf or 15. I 
tracked the code execution in my notes app, following what each line was doing. After some quick analysis, I found that the loop was summing each character of the input and 
storing it in local_20. This yields the solution that the password must be a sequence of numbers summing to 15.


### Takeaways and Learning

- sscanf function
- Track psuedocode in notes for easier analysis
- Understand function calls and pathways before analyzing
