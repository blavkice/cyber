# 1 - julius

**exp: just convert base64 and use caesar cracker**

Julius,Q2Flc2FyCg==

World of Cryptography is like that Unsolved Rubik's Cube, given to a child that has no idea about it. A new combination at every turn.

Can you solve this one, with weird name?

ciphertext: fYZ7ipGIjFtsXpNLbHdPbXdaam1PS1c5lQ==

```python
import base64
def base64_to_ascii(base_string):
    # decode
    ascii_bin = base64.b64decode(base_string)
    # convert to ascii str
    return ascii_bin.decode('utf-8', errors='ignore')

t1 = "Q2Flc2FyCg=="
print(base64_to_ascii(t1))
# Caesar
ciphertext = "fYZ7ipGIjFtsXpNLbHdPbXdaam1PS1c5lQ=="
text = base64_to_ascii(ciphertext)
print(text)
# seems it can be caesar

def caesar_displayer(text, from_=-30, to_=30):
    for i in range(from_, to_):
        # take every char in text end shift it of i
        # to achieve this first convert char to unicode point
        # add i and then reconvert to char
        curr_step = ''.join([chr(ord(c) + i) for c in text])
        print(f"step={i}\t{curr_step}")
caesar_displayer(text)
# step -24 ->ecCTF3T_7U_BRU73?!
```