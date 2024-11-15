# conversions

> a lot more inside [irriversible_encryption](../All%20exercises%201395d651afc2805d9b52dbae7740dad4/irriversible_encryption%2013f5d651afc28080b3b4fa2bacfd325a.md)
> 

[https://www.notion.so/irriversible_encryption-13f5d651afc28080b3b4fa2bacfd325a?pvs=4](../All%20exercises%201395d651afc2805d9b52dbae7740dad4/irriversible_encryption%2013f5d651afc28080b3b4fa2bacfd325a.md)

## binary → str

```python
def binary_to_ascii(binary_string):
    # split the binary string into chunks of 8 bits
    n = 8
    binary_values = [binary_string[i:i+n] for i in range(0, len(binary_string), n)]
    # convert binary to ASCII
    ascii_characters = [chr(int(bv, 2)) for bv in binary_values]
    # join the characters into a single string
    ascii_string = ''.join(ascii_characters)
    return ascii_string
```

## base64 → ascii

```python
import base64
def base64_to_ascii(base_string):
    # decode
    ascii_bin = base64.b64decode(base_string)
    # convert to ascii str
    return ascii_bin.decode('ascii')
```

another version to be used if errors are displayed (converts to UTF8 not ascii)

```python
import base64
def base64_to_ascii(base_string):
    # decode
    ascii_bin = base64.b64decode(base_string)
    # convert to ascii str
    return ascii_bin.decode('utf-8', errors='ignore')
```

## morse → ascii

```python
# given a morse code text (spaced) converts it to ascii
def morse_to_text(morse_code):
    # define a morse code dictionary
    MORSE_CODE_DICT = {
    '.-': 'A', '-...': 'B', '-.-.': 'C', '-..': 'D', '.': 'E', '..-.': 'F',
    '--.': 'G', '....': 'H', '..': 'I', '.---': 'J', '-.-': 'K', '.-..': 'L',
    '--': 'M', '-.': 'N', '---': 'O', '.--.': 'P', '--.-': 'Q', '.-.': 'R',
    '...': 'S', '-': 'T', '..-': 'U', '...-': 'V', '.--': 'W', '-..-': 'X',
    '-.--': 'Y', '--..': 'Z', '-----': '0', '.----': '1', '..---': '2',
    '...--': '3', '....-': '4', '.....': '5', '-....': '6', '--...': '7',
    '---..': '8', '----.': '9', '.-.-.-': '.', '--..--': ',', '..--..': '?',
    '-.-.--': '!', '-....-': '-', '.-..-.': '"', '-.--.': '(', '-.--.-': ')',
    '.----.': "'"
    }
    # split the morse code by space for each character, and double space for each word
    words = morse_code.strip().split("  ")  # Words are separated by two spaces
    decoded_message = []

    # iterate through each word
    for word in words:
        decoded_word = []
        # split the word into morse characters
        for morse_char in word.split():
            # translate the morse character using the dictionary
            # empty string for unrecognized chars
            decoded_word.append(MORSE_CODE_DICT.get(morse_char, ''))  
        # join the decoded characters into a word
        decoded_message.append(''.join(decoded_word))
    # join the words into a final message
    return ' '.join(decoded_message)
```

## string → ordinal representation (list)

```python
def string_to_ordinals(input_string):
		return [ord(char) for char in input_string]
```

## ordinal representation (list) → string

```python
def ordinals_to_string(ordinals_list):
		return ''.join(chr(ordinal) for ordinal in ordinals_list)
```

## bytes → string

```python
def bytes_to_string(byte_data):
		return byte_data.decode('utf-8')
```

## hex (str) → decimal (list of decimals)

```python
def hex2dec(text):
    res = []
    for i in range(len(text)//2):
        # get the current pair of hex
        curr = text[i*2:(i+1)*2]
        # convert to int
        res.append(int(curr, 16))
    return res
```

## decimal (number) → hex (number)

```python
def decimal_to_hex(decimal_value):
	return hex(decimal_value)[2:]
```