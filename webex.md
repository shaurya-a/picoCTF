

## CaaS

- **Category:** Web Exploitation
- **Author:** BROWNIEINMOTION
- **Points:** 150

**Description:**
"Now presenting cowsay as a service."
We are given a link to the website and source code. Inspecting the source code, I see that it uses the binary `/usr/games/cowsay`, which prints whatever is supplied after `/cowsay` in the URL. Input has no filter or inspection, which gives us the opportunity for Code Injection.

I used `;` for separating two commands. `url/cowsay/whatever; ls` for listing the current directory. `url/cowsay/whatever; cat%20flag.txt` for reading the flag.

**Flag:** 
`picoCTF{moooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo0o}`

---

## Forbidden Paths

- **Category:** Web Exploitation
- **Author:** LT 'SYREAL' JONES

**Description:**
"Can you get the flag?"
Here's the website. We know that the website files live in `/usr/share/nginx/html/` and the flag is at `/flag.txt`, but the website is filtering absolute file paths. Can you get past the filter to read the flag?

This website has the useful feature of reading any file given its path. With file paths, a preceding `./` means the current directory, and `../` means the enclosing directory. Since we know that we are in `/usr/share/nginx/html/` and want to access `/flag.txt`, we can just use the path `../../../../flag.txt` to read the flag.

**Flag:**
`picoCTF{7h3_p47h_70_5ucc355_26b22ab3}`

---

## Local Authority

- **Category:** Web Exploitation
- **Author:** LT 'SYREAL' JONES

**Description:**
"Can you get the flag?"
Go to this website and see what you can discover.

Inspect element. Looking under Inspector (Elements in Chrome) and debugger (Sources), we don’t find anything useful. Let’s try dummy variables. I use `admin`, `admin` as the username and password respectively.

Now, it redirects to the `login.php` page. On searching through the inspector tab, we find the `checkPassword()` function, which invokes my interest. On searching through the debugger panel, I find `secure.js` which contained:

_From the above figure, it is apparent that the username is “admin” as we had guessed and the password is: `strongPassword098765`._

**Flag:** 
`picoCTF{j5_15_7r4n5p4r3n7_<unique_code>}`

