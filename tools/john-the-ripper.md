# John the Ripper - Password Cracker

John the Ripper is an Open Source password security auditing and password recovery tool available for many operating systems.

## John the Ripper

John the Ripper (JtR) is a password-cracking tool. It is helpful for penetration testers and password crackers. It was first released in 1996. It was designed to test password strength, recover passwords, brute-force encrypted (hashed) passwords, and crack passwords via dictionary attacks.

> Official Website: [https://www.openwall.com/john/](https://www.openwall.com/john/)
> 

> Open Source GitHub Repo: https://github.com/openwall/john
> 

## Crack Mode

1. **Single Crack Mode:** This mode is best used for easy password cracking. It works very fast. It is used to crack passwords that can be easily guessed. 
2. **********Wordlist Mode:********** A list of possible passwords is created in Dictionary Mode. The password will be cracked only if it is in that list. Usually, the rockyou.txt wordlist is the most popular password list. For any password list, we can use https://github.com/danielmiessler/SecLists or generate a password list using [Cupp - Generate Wordlist](https://www.notion.so/Cupp-Generate-Wordlist-383a29276d5746479738a3fc349c40c3?pvs=21).
3. **********************************Incremental Mode:********************************** Incremental Mode is JtR's powerful bruteforce mode used to crack many strong passwords. This mode is rarely used.

## Download

Installation Command: `sudo apt install john`

## Basic Syntax

Get Help: `john -h`

Single Mode: `john --single --format=raw-md5 pass.txt`

Wordlist Mode: `john --wordlist=rockyou.txt --format=raw-md5 pass.txt`

Increment Mode: `john -i:digits pass.txt`

## Normal Crack

For normal crack, we will use wordlist or dictionary mode. 

> **Syntax:** `john --wordlist=rockyou.txt --format=raw-md5 pass.txt`
> 

Here, `john` indicates the tool name. `--wordlist=` indicates the wordlist that contains many passwords. We can use rockyou.txt by default. 

> In Kali Linux, the rockyou.txt file path: /usr/share/wordlists/rockyou.txt
> 

We can also generate a custom wordlist if we have information about victims using [Cupp - Generate Wordlist](https://www.notion.so/Cupp-Generate-Wordlist-383a29276d5746479738a3fc349c40c3?pvs=21).

`--format=` indicates the password encryption format. JtR will automatically identify and crack if we don't use it. But it can’t always recognize it, which takes time. So, we will first identify the hash using the hash analyzer. To see the list of all formats supported in JtR, we can use the `john --list=formats` command.

`pass.txt` indicates the password file where the hash is saved. If there are many hashs, we can keep each hash in a single line.

A hash, once cracked, cannot be cracked a second time. They have to be viewed from the saved list.

To show the cracked password, we can use the `john --format=raw-md5 pass.txt --show` command.

With the above command, we can see only the crack pass of a hash file. But if we want to see the saved crack pass of all hash files, we will use `cat /home/kali/.john/john.pot` command.

If you don’t execute it successfully, find the `john.pot` file using the `whereis john.pot` command.

## Compress File Password Crack

We often forget or need to crack our ZIP or RAR file password. Using John, we can also crack the pass of these files. But it cannot be cracked directly. We'll use another tool to convert it into an understandable hash to JtR.

For ZIP files, we use `zip2john`

For RAR files, we use `rar2john`

For 7Z files, we use `7z2john`

> **Syntex:** `zip2john file.zip > hash.txt`
> 

After converting it into the hash, we crack it in the normal process.

There are more sub-tools of JtR to convert files to John. 

## More Crack

### ssh2john

Access via SSH requires a password. At the maximum time, these passwords need to be decrypted from the RSA private key. ssh2john is used to convert from RSA Private Key to Hash, which is understandable for JtR.

> **Syntex:** `ssh2john id_rsa > hash.txt`
> 

Now, we can easily crack it using the John tool.

### pem2john

The PEM file is used for Public Key, Private Key, or Certificate. 

> **Syntex:** `pem2john private.pem > hash.txt`
> 

**All sub-tools are found here:** [https://www.kali.org/tools/john/](https://www.kali.org/tools/john/)
