# **tunn3l v1s10n**

## Overview

- **Points:** 40
- **Category:** Forensics

## Description

Locate the flag within this file

## Approach

Given the absence of a file extension, the file type is uncertain. Using a hex editor like HxD, the initial two characters "BM" suggest a BMP file

Changing the extension to ".bmp" and attempting to open it with ImageMagick did not do much. While there may be a way to adjust the file header for proper opening, the image was displayed

No flag was visible. A notable observation was the BMP file's disproportionately large size of about 2MB for such a small image. Further insights into the BMP header's components were gathered from different sources.

In a BMP file, the height is found at  0016h. Modifying offset 0017h from 0x01 to 0x03, the file was reopened and the flag was visible

## Flag

picoCTF{qu1t3_a_v13w_2020}
---

# **Trivial Flag Transfer Protocol**

## Overview

Points: 90
Category: Forensics

## Description

Discover the secret behind the movement of the flag

## Hints

1. Explore alternative methods for data concealment.

## Approach

In analyzing the packet capture through Wireshark, a variety of files emerge.

To unveil the files:

`File > Export Objects > TFTP`

Save all files, including instructions.txt, plan, program.deb, picture1.bmp, picture2.bmp, and picture3.bmp

### instructions.txt

Content of instructions.txt:

```text
GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA
```

Decrypted using ROT13:

```text
TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER.FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPLAN
```

Adding spaces for clarity:

> TFTP DOESN'T ENCRYPT OUR TRAFFIC SO WE MUST DISGUISE OUR FLAG TRANSFER. FIGURE OUT A WAY TO HIDE THE FLAG, AND I WILL CHECK BACK FOR THE PLAN.

### plan

Raw contents of plan:

```text
VHFRQGURCEBTENZNAQUVQVGJVGU-QHRQVYVTRAPR.PURPXBHGGURCUBGBF
```

Decrypted using ROT13:

```text
IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE.CHECKOUTTHEPHOTOS
```

Adding spaces:

> I USED THE PROGRAM AND HID IT WITH-DUE DILIGENCE. CHECK OUT THE PHOTOS.

### program.deb

Reading program.deb with 7-zip reveals files hinting at the use of steghide


The actual content of the pictures is irrelevant. The file size of picture2.bmp was weird

### steghide and solving

Consulting the steghide README's "Quick-Start" section, the command `steghide info picture3.bmp` is run, prompting for a passcode. Recalling the plan

```text
IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE.CHECKOUTTHEPHOTOS
```

> AND HID IT WITH-DUE DILIGENCE

Considering "DUEDILIGENCE" as the password, steghide reveals a hidden flag.txt within picture3. Using `steghide extract -sf picture3.bmp` and "DUEDILIGENCE" as the password, the flag is successfully extracted.

## Flag

picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}

---

# MacroHard WeakEdge - Forensics Challenge

## Overview

- **Points:** 60
- **Category:** Forensics

## Description

This challenge provides a PowerPoint file named Forensics is fun.pptm and hints that a hidden flag is waiting to be discovered within the file.

## Approach

To tackle this challenge, we use a tool called `binwalk` to examine the contents of the PowerPoint file. Using the command `binwalk -e "Forensics is fun.pptm"` helps us uncover potential hidden files, resulting in the creation of a folder named `_Forensics is fun.pptm.extracted`.

Next, we explore this extracted folder, paying particular attention to a file named `0.zip`. In an effort to simplify our search, we extract the contents of `0.zip` and navigate through them using the terminal.

Despite trying various commands like `grep` and `find` to locate the flag, we come up empty-handed. However, a breakthrough occurs when we use the command `find -D tree | grep hidden`, revealing a file path: `./ppt/slideMasters/hidden`.

The contents of this file, viewed with `cat ./ppt/slideMasters/hidden`, present an encoded string: "ZmxhZzogcGljb0NURntEMWRfdV9rbjB3X3BwdHNfcl96MXA1fQ". Suspecting base64 encoding, we remove spaces from the string, resulting in "ZmxhZzogcGljb0NURntEMWRfdV9rbjB3X3BwdHNfcl96MXA1fQ".

Decoding this string using an online base64 decoder yields the flag: `picoCTF{D1d_u_kn0w_ppts_r_z1p5}`.

## Flag

`picoCTF{D1d_u_kn0w_ppts_r_z1p5}`

