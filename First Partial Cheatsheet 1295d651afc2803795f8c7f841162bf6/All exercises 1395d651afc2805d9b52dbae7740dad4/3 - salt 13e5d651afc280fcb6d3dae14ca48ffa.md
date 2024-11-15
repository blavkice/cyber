# 3 - salt

![image.png](3%20-%20salt%2013e5d651afc280fcb6d3dae14ca48ffa/image.png)

### Code Breakdown

1. **Load `flag.php`:**
    
    ```php
    require_once('flag.php');
    ```
    
    This line includes the `flag.php` file, which likely contains the `$flag` variable that holds the flag or answer for the challenge. Without the correct conditions, the flag will not be displayed.
    
2. **Retrieve the `pass` Parameter:**
    
    ```php
    if ($_ = @$_GET['pass']) { ... }
    ```
    
    Here, the code checks if there’s a `pass` parameter in the URL's query string (`$_GET['pass']`). If the `pass` parameter is set, it assigns its value to `$_` and proceeds with the code inside the `if` block. If `pass` is not provided, it falls back to displaying the code itself.
    
3. **Extract User Agent (UA):**
    
    ```php
    $ua = $_SERVER['HTTP_USER_AGENT'];
    ```
    
    This retrieves the `HTTP_USER_AGENT` header, which usually contains information about the client browser (e.g., "Mozilla/5.0...").
    
4. **First Condition - `md5($_) + $_[0] == md5($ua)`:**
    
    ```php
    if (md5($_) + $_[0] == md5($ua)) { ... }
    ```
    
    - `md5($_)`: Computes the MD5 hash of the `pass` parameter.
    - `$_[0]`: Retrieves the first character of the `pass` parameter.
    - `md5($ua)`: Computes the MD5 hash of the User-Agent string.
    
    The condition checks if the sum of `md5($_)` and the first character of `$_` (likely cast to an integer) is equal to `md5($ua)`. This condition is complex to meet because MD5 hashes are 32-character hexadecimal strings, so the arithmetic here might be a bit unconventional.
    
5. **Second Condition - `$_[0] == md5($_[0] . $flag)[0]`:**
    
    ```php
    if ($_[0] == md5($_[0] . $flag)[0]) { ... }
    ```
    
    - `$_[0]`: Retrieves the first character of the `pass` parameter.
    - `md5($_[0] . $flag)`: Computes the MD5 hash of the first character of `pass` concatenated with `$flag`.
    - `[0]`: Accesses the first character of this MD5 hash.
    
    The condition checks if the first character of the `pass` parameter matches the first character of the MD5 hash of `$_[0] . $flag`.
    
6. **Display the Flag:**
    
    ```php
    echo $flag;
    ```
    
    If both conditions are met, the code displays the flag, which is the solution to the CTF.
    
7. **Highlight Source Code if `pass` is Missing:**
    
    ```php
    else { highlight_file(__FILE__); }
    ```
    
    If the `pass` parameter is not provided, this displays the source code, enabling users to read it and figure out the logic for the challenge.
    

---

- let’s try to set `pass` to `0` and `user-agent` to `0` too

![image.png](3%20-%20salt%2013e5d651afc280fcb6d3dae14ca48ffa/image%201.png)

![image.png](3%20-%20salt%2013e5d651afc280fcb6d3dae14ca48ffa/image%202.png)

the first if is passed because

`(md5($_) + $_[0] == md5($ua)` → `md5(0) + 0 == md5(0)`