# Cryptography Keys Decentralization

Cryptography Keys Decentralization is a technique used in Google Drive.\
It's uncertain how one can implement it properly but here's the rough
concept.

## Password/Passphrase login
Imagine that you have a password that's 100 characters long or passphrase
that's 100 words long. Under normal circumstance, one user is responsible
for holding the password or passphrase.

Let's say in a small company, there's an IT department that has about
10 staffs. Each staff will be holding 10 characters or 10 words of the
password/phrase. This was one of the form of cryptography keys
decentralization. 

## Symmetric key encryption
Imagine that you have a document/data/file that you would like to encrypt
using any of the industry standard symmetric key encryption algorithm.
Under normal circumstance, you are responsible for encrypting/decrypting
the data/document/file.

Let's say in a small company, there's an IT department that has about
10 staffs. Each staff will be encryping the document/data/file using their
own symmetric encryption keys. This was one of the form of cryptography
keys decentralization.

## Public key encryption
Imagine that you have a document/data/file that you would like to encrypt
using any of the industry standard public key encryption algorithm.
Under normal circumstance, you are responsible for encrypting/decrypting
the data/document/file.

Let's say in a small company, there's an IT department that has about
10 staffs. Each staff will be encryping the document/data/file using their
own private key. This was one of the form of cryptography
keys decentralization.

**Note: People can use RSA to achieve PKE or sealed diffie hellman that
exists in libsodium to achieve PKE**

## Public key digital signature
PKCS DSA was commonly used in preventing data/document/file from being
able to change/forge/tamper. It was also used in SSH login.

Imagine that you want to sign data/document/file or login through SSH,
this was done by only you.

Let's say in a small company, there's an IT department that has about
10 staffs. Each staff will be signing the document/data/file or login
into SSH in order. This was one of the form of cryptography
keys decentralization.

### Pros
1. A client side malicious insider hacker can't betray the company/group
because the hacker needs to get all possible cryptography keys that
hacker might or might not have access to the machine that holds these
cryptography keys.

2. Any attempt to hack on service provider side is futile. 

### Cons
1. It will become harder to manage on client side as scale goes up.

2. Client needs to solve internal trusts problem shown on the
examples above.

3. Client won't be able to find any software/solutions that provides
such feature. The main reason was due to the extreme complexity and
ever changing demand on client side.

4. Client won't be able to login/decrypt if any of the client's
internal staffs lost their keys(can be passwords/phrase of PKCS
private key). 

### Side Note
This does not apply only to client whose identity was a company/corporate,
normal user can also use such technique if there's such use case.
