
# new ceaser


## Encoding Process

1. **Key Generation:**
   - The key is a single character.
   - The key must be one of the first 16 characters of the alphabet (`a` to `p`).

2. **Encoding to Binary:**
   - The message is converted to binary.

3. **Hex Encoding and Splitting:**
   - Each binary character is then encoded into hexadecimal.
   - The hexadecimal value is split in the middle.

4. **Mapping to Alphabet Sequence:**
   - The two halves of the hexadecimal value are mapped to the alphabet sequence, where each character from 'a' to 'p' corresponds to the values 0 to 15.

5. **Shifting:**
   - The resulting mapped values are shifted using a rotation (similar to a Caesar cipher, i.e., rot n).

6. **Concatenation:**
   - The shifted values are concatenated.

