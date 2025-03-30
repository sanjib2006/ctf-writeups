# CTF Writeup - Chronos CTF (IIT Mandi)

## Challenge: Catch Me If You Can

### Category: Reversing

### Writeup Author: iamgreedy

### Challenge Description
> This EXE lets you copy something… but before you can paste it, poof—it’s gone! Can you outsmart it?

### Given File
- `clip.exe`

### Solution
The given exe has a copy button and a timer of 0.01 secs, as soon as you copy the flag, the clipboard is cleared in 0.01 secs.
So if your clipboard history is turned on then it is easily available or you can track the the clipboard changes and print it using the following script. 
Run this script and then click on the copy button.

```python
import pyperclip
import time

def check_clipboard():
    original_clipboard = pyperclip.paste()
    
    while True:
        time.sleep(0.01)  
        current_clipboard = pyperclip.paste()

        if current_clipboard != original_clipboard:
            print(f"Clipboard changed: {current_clipboard}")
            break  

check_clipboard()
```

### Extracted Flag
```
saic{y0u_f!n@lly_c0p!3d_!t,right?}
```

