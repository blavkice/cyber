# backstreetboys

```python
enc_text = 'ltctfd{p-peye-mp-raee-ieu}'
key = 'tellmewhy'

def decryption(enc_text, key):
    clear_text = ''
    # i know that |clear_text| = |enc_text|
    # and that key_extended depends on len(plain_text) and not on plain_text itself
    key_extended = (key * (len(enc_text) // len(key))) + key[:len(enc_text) % len(key)]
    for i in range(len(enc_text)):
        c_plain = enc_text[i]
        c_key = key_extended[i]
        offset = 97
        if c_plain.isalpha():
            e_c = chr((ord(c_plain) - ord(c_key)) % 26 + offset)
            clear_text += e_c
        else: clear_text += c_plain
    return clear_text

print(decryption(enc_text, key))
```

```python
#!/usr/bin/env python3

# encryption method
def encryption(plain_text, key):
    encrypted_text = ""
    key_extended = (key * (len(plain_text) // len(key))) + key[:len(plain_text) % len(key)]

    for i in range(len(plain_text)):
        char_plain = plain_text[i]
        char_key = key_extended[i]

        offset = 97

        if char_plain.isalpha():
            # here is the most important part
            encrypted_char = chr((ord(char_plain) + ord(char_key) - 2 * offset) % 26 + offset)
            
            encrypted_text += encrypted_char
        else:
            encrypted_text += char_plain

    return encrypted_text

# key for the encryption
k = "tellmewhy"

# this is my message
flag = '??????????????????????????'
        
c = encryption(flag, k)
print("Encrypted text:", c)

# OUTPUT: ltctfd{p-peye-mp-raee-ieu}
```