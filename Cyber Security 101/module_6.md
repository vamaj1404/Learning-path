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
