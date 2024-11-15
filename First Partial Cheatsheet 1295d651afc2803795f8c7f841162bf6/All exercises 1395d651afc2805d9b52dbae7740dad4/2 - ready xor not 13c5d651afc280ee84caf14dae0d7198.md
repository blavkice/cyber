# 2 - ready xor not

look at the notes on XOR encoding

[https://www.notion.so/Encryption-with-XOR-Stream-Encryption-1225d651afc2801c8fffff5b1f617cdb?pvs=4](../../Crypto%2011c5d651afc280cab894c6437c2f77e9/Encryption%20with%20XOR%20Stream%20Encryption%201225d651afc2801c8fffff5b1f617cdb.md)

### $ciphertext=plaintext⊕key$

> if we have $plaintext$ and $ciphertext$ it becomes really easy to get the key:
> 
- XOR both sides with the $plaintext$
    
    $ciphertext⊕plaintext=(plaintext⊕key)⊕plaintext$
    
- XOR is commutative and associative, so the right-hand side simplifies to
    
    **$ciphertext⊕plaintext=key$**
    
    (because XORing the same value 2 times cancels out):
    
    $(plaintext⊕plaintext)=0$
    

### $plaintext=ciphertext⊕key$

---

```python
'''
original data: "El Psy Congroo"
encrypted data: "IFhiPhZNYi0KWiUcCls="
encrypted flag: "I3gDKVh1Lh4EVyMDBFo="
---> we can get the key by doing this: ciphertext ^ plaintext = key
'''
import base64
def base64_to_ascii(base_string):
    # decode
    ascii_bin = base64.b64decode(base_string)
    # convert to ascii str
    return ascii_bin.decode('utf-8', errors='ignore')

data = 'El Psy Congroo'
enc_data_b = 'IFhiPhZNYi0KWiUcCls='
enc_data = base64_to_ascii(enc_data_b)

def string_to_ordinals(input_string):
	return [ord(char) for char in input_string]

def ordinals_to_string(ordinals_list):
		return ''.join(chr(ordinal) for ordinal in ordinals_list)

def xor_strings(s1, s2):
    # convert strings to their ordinal representations
    or1 = string_to_ordinals(s1)
    or2 = string_to_ordinals(s2)
    # adjust strings length to make sure they are equal
    # by adding padding if needed
    max_len = max(len(or1), len(or2))
    or1 += [0] * (max_len - len(or1))
    or2 += [0] * (max_len - len(or2))
    # xor and return the result
    return [a ^ b for a,b in zip(or1, or2)]

ord_key = xor_strings(data, enc_data)
key = ordinals_to_string(ord_key)
# print(key)
enc_flag_b = 'I3gDKVh1Lh4EVyMDBFo='
enc_flag = base64_to_ascii(enc_flag_b)
# plaintext = ciphertext ^ key
# print(enc_flag)
ord_flag = xor_strings(key, enc_flag)
flag = ordinals_to_string(ord_flag)
print(flag)
```

→ FLAG=Alpacaman