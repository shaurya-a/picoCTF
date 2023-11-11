# **Tunn3l V1s10n**
_File Recovery and Image Reconstruction_

- The file initially lacked an extension, but its magic header strongly hinted at a BMP image format (magic header: 424D). After renaming it to "tunel_vision.bmp" and trying to open it, the attempt failed, indicating potential corruption.

- A closer look at the binary data on the first line revealed two deliberately incorrect 4-byte values (BAD00000 followed by BAD00000), a clear clue that the header needed repair.

- Consulting BMP documentation, the first 4-byte value represents an offset to the pixel array, while the second represents the BMP DIB Header Size, typically a constant value of 40 (0x28). By manually adjusting the pixel data offset to point to 0x36 and setting the BMP header size to 0x28, the image finally opened correctly. Further inspection using exiftool uncovered that the image size was 2893400 bytes, while the displayed resolution was only 1134x307, indicating that only a fraction of the image was visible.

- Calculated original height in pixels turned out to be 850px after adjusting the height in a hex editor, revealing the complete image.

**Flag:** `picoCTF{qu1t3_a_v13w_2020}`

---

# **Trivial Flag Transfer Protocol**
_Steganography and Extraction_

From the extracted files:
- picture1.bmp
- picture2.bmp
- picture3.bmp
- program.deb
- instructions.txt
- plan

Inside "picture3.bmp," the flag is covertly hidden using steganography techniques. "program.deb" is a Debian package containing steghide. Both "instructions.txt" and "plan" hold ROT13-encoded text, guiding the process to extract the flag from the image.

Use steghide with the password "DUEDILIGENCE" to extract the flag, which will be saved in "flag.txt".
**Flag:** `picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}`

---

# **MacroHard WeakEdge**
_File Decoding and Exploration_

After unzipping all the files, only one file made sense. It contained alphanumeric characters, seemingly encoded. Testing various common encoding types revealed it was base64 encoded. Decoding it revealed the answer.
**Flag:** <font color="purple">`picoCTF{D1d_u_kn0w_ppts_r_z1p5}`</font>
