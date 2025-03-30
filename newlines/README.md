# CTF Writeup - Chronos CTF (IIT Mandi)

## Challenge: Newlines

### Category: Forensics

### Writeup Author: iamgreedy

### Challenge Description
> Description: Some secrets hide in plain sight, while others lurk between the lines. Can you find what’s hidden in this seemingly ordinary text file?

### Given File
- `newlines.zip`

### Solution
Extracting `newlines.zip` revealed **70 text files** (`0.txt` to `69.txt`), each containing varying newlines. The newline count in each file corresponded to ASCII values. The following script extracted the hidden message:

```python
import os

def count_lines_to_ascii():
    line_counts = []
    for i in range(70):
        filename = f"{i}.txt"
        if os.path.exists(filename):
            with open(filename, "r", encoding="utf-8") as f:
                line_count = max(0, sum(1 for _ in f) - 1)
                line_counts.append(line_count)
        else:
            line_counts.append(0)
    
    ascii_string = ''.join(chr(count) for count in line_counts)
    print(ascii_string)

if __name__ == "__main__":
    count_lines_to_ascii()
```

### Extracted Flag
```
saic{s0_m4ny_n3wl1n35_b7w_7h15_15_4_v3ry_l0ng_fl4g_y0u_wr073_5cr1p7!!}
```

