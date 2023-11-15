# Stonk Market Exploitation


## Overview

- **Points:** N/A
- **Category:** Binary Exploitation

## Approach

### buy_stonks Function

In the `buy_stonks` function, we found a problem in the `printf()` function. Understanding the key syntax of `printf()` is crucial here. When given two arguments, the first sets the data type for the second (e.g., %s for strings, %d for decimals).
However, with only one argument, it either prints the argument or defines the format. In this context, using %s or %x is important. When we provide the data format, `printf()` tries to find the second argument.
If it fails, it starts printing data from the stack, which is a potential security issue.

As a test, by adding %x after choosing "Buy some stonks," we exposed a hex value leaked from memory, confirming the existence of a format string vulnerability.

### Further Exploration

To dig deeper, we added more %x's to extract more data from memory. Converting the hex data to a string using CyberChef showed a somewhat messed-up flag format. The distortion might be due to endianness, affecting how data is stored in memory.
Assuming little-endian encoding, even when converting the data to big-endian, we still didn't get the right flag.

Thinking about one byte affecting the next, removing hex values from the beginning slowly revealed the formatted flag:

**Flag:** `picoCTF{I_l05t_4ll_my_m0n3y_c7cb6cae}`
