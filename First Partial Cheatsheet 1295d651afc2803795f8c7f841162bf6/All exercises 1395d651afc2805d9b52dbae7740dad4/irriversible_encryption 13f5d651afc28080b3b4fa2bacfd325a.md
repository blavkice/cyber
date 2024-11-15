# irriversible_encryption

first only useful functions…

```python
import base64
import binascii
import string

ALPHABET = list(string.printable)  # len = 100
LEN = len(ALPHABET)

# decode base64
def base64decode(encoded_message):
    b64_bytes = encoded_message.encode('ascii')
    message_bytes = base64.b64decode(b64_bytes)
    message = message_bytes.decode('ascii')
    return message

# decode base32
def base32decode(encoded_message):
    b32_bytes = encoded_message.encode('ascii')
    message_bytes = base64.b32decode(b32_bytes)
    message = message_bytes.decode('ascii')
    return message

# decode XOR (known key)
def XORdecode(encoded_message, KEY="c4mPar1"):
    rep = len(encoded_message) // len(KEY) + 1
    key = (KEY * rep)[:len(encoded_message)]  # adjust the key length
    original = ''.join([chr(ord(a) ^ ord(b)) for a, b in zip(encoded_message, key)])
    return original

# decode rot
def ROTdecode(encoded_message, pos):
    rot_dec = ''
    for c in encoded_message:
        i = ALPHABET.index(c)
        rot_dec += ALPHABET[(i - pos) % LEN]
    return rot_dec

# hex -> ascii
def hex_to_ascii(encoded_message):
    decoded = binascii.unhexlify(encoded_message).decode()
    return decoded

# all useful "inverse" functions should be there
```

---

```python
import base64
import binascii
import string

ALPHABET = list(string.printable)  # len = 100
LEN = len(ALPHABET)

# decode base64
def base64decode(encoded_message):
    b64_bytes = encoded_message.encode('ascii')
    message_bytes = base64.b64decode(b64_bytes)
    message = message_bytes.decode('ascii')
    return message

# decode base32
def base32decode(encoded_message):
    b32_bytes = encoded_message.encode('ascii')
    message_bytes = base64.b32decode(b32_bytes)
    message = message_bytes.decode('ascii')
    return message

# decode XOR (known key)
def XORdecode(encoded_message, KEY="c4mPar1"):
    rep = len(encoded_message) // len(KEY) + 1
    key = (KEY * rep)[:len(encoded_message)]  # adjust the key length
    original = ''.join([chr(ord(a) ^ ord(b)) for a, b in zip(encoded_message, key)])
    return original

# decode rot
def ROTdecode(encoded_message, pos):
    rot_dec = ''
    for c in encoded_message:
        i = ALPHABET.index(c)
        rot_dec += ALPHABET[(i - pos) % LEN]
    return rot_dec

# hex -> ascii
def hex_to_ascii(encoded_message):
    decoded = binascii.unhexlify(encoded_message).decode()
    return decoded

# all useful "inverse" functions should be there

with open('encrypted_flag.txt', 'r') as file:
    secret = file.read()
    xor_enc = hex_to_ascii(secret)
    encrypted = XORdecode(xor_enc)
    for _ in range(15):
        b32_enc = ROTdecode(encrypted,3)
        rot13_enc = base32decode(b32_enc)
        b64_enc = ROTdecode(rot13_enc,13)
        encrypted = base64decode(b64_enc)
    # encrypted is now decrypted
    print(encrypted)
```

→ Encode as if there's no tomorrow: spritz{But_wa1t_R3vers1ble_OP3rations_are_B4D}