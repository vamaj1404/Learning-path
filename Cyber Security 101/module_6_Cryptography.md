# Cryptography

## Public Key Cryptography Basics
ssh-keygen is the program usually used to generate key pairs:  
- DSA (Digital Signature Algorithm)  
- ECDSA (Elliptic Curve Digital Signature Algorithm)   
- ECDSA-SK (ECDSA with Security Key)   
- Ed25519 is a public-key signature system using EdDSA (Edwards-curve Digital Signature Algorithm)  
- Ed25519-SK (Ed25519 with Security Key)

example command: ssh-keygen -t ed25519  

Using tools like John the Ripper, you can attack an encrypted SSH key to attempt to find the passphrase, highlighting the importance of using a complex passphrase
During CTFs, penetration testing, and red teaming exercises, SSH keys are an excellent way to “upgrade” a reverse shell.  
Leaving an SSH key in the authorized_keys file on a machine can be a useful backdoor,  
You can get one from the various certificate authorities for an annual fee. Furthermore, you can get your own certificates for domains you own using Let's Encrypt (opens in new tab) for free. If you run a website, it’s worth setting up and switching to HTTPS, as any modern website would do.  
 ## 3- Hashing Basics
 ### Secure Password Storage

Passwords should never be stored in plaintext or with reversible encryption. Instead, use a slow, secure hashing algorithm such as **Argon2, bcrypt, scrypt, or PBKDF2**.

Each password must include a unique random **salt** before hashing. Salts prevent identical passwords from producing identical hashes and protect against rainbow-table attacks.

Store only the resulting hash and salt in the database.

### Hash Identification

Password hashes should be identified using their **prefix, length, format, and source**. Tools like `hashid` help, but context is often more reliable.

```bash
hashid '<HASH>'
```

#### Linux

Linux password hashes are stored in `/etc/shadow`:

```bash
sudo grep '^username:' /etc/shadow
```

Common prefixes:

| Prefix | Algorithm     |
| ------ | ------------- |
| `$y$`  | yescrypt      |
| `$2b$` | bcrypt        |
| `$6$`  | SHA-512 Crypt |
| `$1$`  | MD5 Crypt     |

Typical format:

```text
$algorithm$options$salt$hash
```

#### Windows

Windows commonly uses **NT hashes**, stored in the SAM database. NT hashes have no clear prefix, so context is important.

#### Authorized Testing

```bash
hashcat -m <MODE> hashes.txt wordlist.txt
hashcat -m <MODE> hashes.txt --show
```

### Cracking Password Hashes

Password hashes cannot be decrypted. They must be cracked by hashing possible passwords, applying the salt when required, and comparing the result with the target hash.

Common tools:

* **Hashcat** — optimized for GPU-based cracking
* **John the Ripper** — uses CPU by default
* **rockyou.txt** — common password wordlist

#### Hashcat Syntax

```bash
hashcat -m <hash_type> -a <attack_mode> hashfile wordlist
```

Example for bcrypt:

```bash
hashcat -m 3200 -a 0 hash.txt /usr/share/wordlists/rockyou.txt
```

Key options:

```text
-m 3200   Hash type: bcrypt
-a 0      Straight dictionary attack
```

GPU cracking is usually faster, so Hashcat performs best on the host system rather than inside a virtual machine. John the Ripper works well in VMs but may also run faster on the host.


