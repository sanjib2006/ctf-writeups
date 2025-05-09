# CTF Writeup - Chronos CTF (IIT Mandi)

## Challenge: Xpecto Decryptum

### Category: Reversing

### Writeup Author: iamgreedy

### Challenge Description

> Someone thought it’d be funny to wrap a secret inside layers of Python magic. With just the right touch you might just unwrap this digital present and find the treasure inside. But be careful—messing with the wrong parts might leave you scratching your head instead! 🔐🐍

### Given Code:
```python
import base64
from cryptography.fernet import Fernet

payload = b'gAAAAABn2vH52liBfuFfazSkLcAVO5N3AaoIJslqczD_GbOi7Ygbq2eKZWF2YYqFSUv34O-eQeH_2DvL-cJZceUmk1Tlp_fOEhXn30uG4tjmgZm0Dfc2LhSDJtFrdYSriHuKOIfpjrs0V6xyo8_Vg2HsUePmXDXFF_mzicZqDX5wLw0NHBFn3fqjsdbavOnqZw0YIhPbEbyaupbzOULllF9VUGvn53D3RFlyHD8M3jY8xAPkj0YY6D2WmmKtDu16XKK4asdLEsYo-7uSGFG-UO6fxdf1ncWXD8pM0EAOYj1Y6tlSH3t9qXE='
key_str = 'supersecretkeyforthexpecto2025XD'
key_base64 = base64.b64encode(key_str.encode())
f = Fernet(key_base64)
plain = f.decrypt(payload)
exec(plain.decode())
```

## Issue
- Fernet requires a 32-byte key before Base64 encoding.
- The given `key_str` is 30 bytes long.
- Base64 encoding it directly doesn't work.

## Solution
- The original script attempts to use a key that is too short for Fernet encryption, leading to a decryption failure. To fix this:
- We ensure the key is exactly 32 bytes long by padding it if necessary.
- The adjusted key is then encoded correctly before being used for decryption.
- After fixing the key issue, the script successfully decrypts the payload, which contains a Python script.
- The exec() function executes the decrypted script, revealing the flag.

### Fixed Code:
```python
import base64
from cryptography.fernet import Fernet

payload = b'gAAAAABn2vH52liBfuFfazSkLcAVO5N3AaoIJslqczD_GbOi7Ygbq2eKZWF2YYqFSUv34O-eQeH_2DvL-cJZceUmk1Tlp_fOEhXn30uG4tjmgZm0Dfc2LhSDJtFrdYSriHuKOIfpjrs0V6xyo8_Vg2HsUePmXDXFF_mzicZqDX5wLw0NHBFn3fqjsdbavOnqZw0YIhPbEbyaupbzOULllF9VUGvn53D3RFlyHD8M3jY8xAPkj0YY6D2WmmKtDu16XKK4asdLEsYo-7uSGFG-UO6fxdf1ncWXD8pM0EAOYj1Y6tlSH3t9qXE='

key_str = 'supersecretkeyforthexpecto2025XD'
key_32_bytes = key_str.ljust(32)[:32].encode()
key_base64 = base64.urlsafe_b64encode(key_32_bytes)

f = Fernet(key_base64)
decrypted_data = f.decrypt(payload)
print(decrypted_data.decode())
```

### Extracted Flag

```
saic{pr1n7ing_ju57_unp4ck3d_my_s3cr3t}
```




