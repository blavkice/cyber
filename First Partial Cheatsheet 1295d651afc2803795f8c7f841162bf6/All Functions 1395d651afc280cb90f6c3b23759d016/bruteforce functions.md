# bruteforce functions

## *caesar* cracker \ displayer

```python

def caesar_displayer(text, from_=-30, to_=30):
    for i in range(from_, to_):
        # take every char in text end shift it of i
        # to achieve this first convert char to unicode point
        # add i and then reconvert to char
        curr_step = ''.join([chr(ord(c) + i) for c in text])
        print(f"step={i}\t{curr_step}")
```
