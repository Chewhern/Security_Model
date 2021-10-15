## Continuation of MAC and Stream Cipher
Let's suppose the message we want to encrypt was "010203 sends $900
to 112233". The **"010203"** and **"112233"** are the sender's and
recipient's bank account number. The encrypted message was
"dc53e70b3d4eb1643b3c6f1fbb5a1b2c5bdd0c4905c429104ad8d9ba0b4aa837"
with the key of
"dc53e70b3d7e8054090c5c3fc83f754828fd287035f4096425f8e88b39789b04".

The middle man can try to change/tamper with the message so that
the output can be changed. In this example we can change the last
bit
"dc53e70b3d4eb1643b3c6f1fbb5a1b2c5bdd0c4905c429104ad8d9ba0b4aa836"
of the encrypted message. When decrypting the message, we should
see "010203 sends $900 to 112232".

Stream Cipher alone can't stop the message from being changed/
altered(through malicious unauthorized third party). Changing
bank account number, amount of sending/receiving is some of the
effects that caused by using stream cipher to encrypt/decrypt
messages.

This is why MAC was used in conjunction with stream cipher,
we take the encrypted message and use any of the available MAC
algorithm like HMAC-SHA1, HMAC-SHA256, HMAC-SHA512 to generate
a message authentication code with a secret key that used in
encrypting message through stream cipher.

https://www.freeformatter.com/hmac-generator.html

In modern industry, stream cipher will always append with MAC.
The MAC can either append in front of stream cipher encrypted text
or append behind of stream cipher encrypted text. If the key that
used to encrypt in stream cipher was not known, attacker can't
generate the same MAC. If any changes were made in either MAC
or stream cipher encrypted text, the recipient side will detect
the changes. Hence, they will abort decrypting the malicious changed
encrypted text.

I have made an example on appending MAC to stream cipher which was
shown below.\
MAC was appended in front of Stream Cipher encrypted text
```
3eb141fd952f1aca25d326d1f22399862596cc69766c1acc671cd8bd1e250a151c
596715b3cda7a421ff02a517eb494830ca5256b60043360156803e024e87a3
dc53e70b3d4eb1643b3c6f1fbb5a1b2c5bdd0c4905c429104ad8d9ba0b4aa837
```
