# CTF Writeup - picoGym

## Challenge: GDB baby step 2

#### Category: Reverse Engineering

#### Writeup Author: iamgreedy

### Challenge Description
We need to find out the content of the eax register at the end of the main function for the given file `debugger0_b`.

### Disassembling main function:
```bash
(gdb) disas main
Dump of assembler code for function main:
   0x0000000000401106 <+0>:	    endbr64
   0x000000000040110a <+4>:	    push   %rbp
   0x000000000040110b <+5>:	    mov    %rsp,%rbp
   0x000000000040110e <+8>:	    mov    %edi,-0x14(%rbp)
   0x0000000000401111 <+11>:	mov    %rsi,-0x20(%rbp)
   0x0000000000401115 <+15>:	movl   $0x1e0da,-0x4(%rbp)
   0x000000000040111c <+22>:	movl   $0x25f,-0xc(%rbp)
   0x0000000000401123 <+29>:	movl   $0x0,-0x8(%rbp)
   0x000000000040112a <+36>:	jmp    0x401136 <main+48>
   0x000000000040112c <+38>:	mov    -0x8(%rbp),%eax
   0x000000000040112f <+41>:	add    %eax,-0x4(%rbp)
   0x0000000000401132 <+44>:	addl   $0x1,-0x8(%rbp)
   0x0000000000401136 <+48>:	mov    -0x8(%rbp),%eax
   0x0000000000401139 <+51>:	cmp    -0xc(%rbp),%eax
   0x000000000040113c <+54>:	jl     0x40112c <main+38>
   0x000000000040113e <+56>:	mov    -0x4(%rbp),%eax
   0x0000000000401141 <+59>:	pop    %rbp
   0x0000000000401142 <+60>:	ret
End of assembler dump.
```

## Solution
Set the break point at the end `0x0000000000401142` and then check then run the file and check the content of the eax register.

```bash
(gdb) break *0x0000000000401142
Breakpoint 1 at 0x401142
(gdb) run
Breakpoint 1, 0x0000000000401142 in main ()
(gdb) info registers eax
eax            0x4af4b             307019
```


### Extracted Flag

```
picoCTF{307019}
```




