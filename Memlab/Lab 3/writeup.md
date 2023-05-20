# Mem Lab-03 Writeup

## Challenge discription 
A malicious script encrypted a very secret piece of information I had on my system. Can you recover the information for me please?

Note-1: This challenge is composed of only 1 flag. The flag split into 2 parts.

Note-2: You'll need the first half of the flag to get the second.

You will need this additional tool to solve the challenge,

```bash 
$ sudo apt install steghide
```


The flag format for this lab is: inctf{s0me_l33t_Str1ng}

## Flag 01

<hr>

from the discription we can see that a malicious script has been run 
so my first hinch was to do a filescan and check for a .py extension files 
```batch 
vol.py --plugins=plugin/ -f MemoryDump_Lab3.raw --profile Win7SP1x86_23418 filescan | grep .py
```
and on going through the list the file ```evilscript.py```
caught my eye quickly dumped the file renamed it and checked the code. The important file is ```vip.txt``` and simple base64,xoring was done on the contents. 

dumped the file vip.txt wrote a script to decode the contents wrote a scritp to decode the content 

```py
import base64
a='jm`wex3m0\k7oe'
base64.b64decode(a)
b = ''.join(chr(ord(i)^3) for i in a)
print(b)
```

got first part of the flag ```inctf{0n3_h4lf```

## Flag -01 part 2

in the description steghide was mention which is a big clue as steghide is used to embed and extract secret messages in images. It supports all the general formats of images like .png, .jpg etc.

 we can guess that the second part of the flag is in a png or jpg file on using the command 

```bash statement
 vol.py --plugins=plugin/ -f MemoryDump_Lab3.raw --profile Win7SP1x86_23418 filescan | grep jpeg
  ```

got jpeg file ```suspision1.jpeg``` now no using steghide extracted the second part of the flag 
```bash statement 
steghide --extract -sf sus.jpeg -p inctf{0n3_h4lf
```
second part of the flag ```_1s_n0t_3n0ugh}```

final flag 
``` inctf{0n3_h4lf_1s_n0t_3n0ugh}```
