## Continuation of MAC and Stream Cipher
Let's suppose the message we want to encrypt was "010203 sends $900
to 112233". The **"010203"** and **"112233"** are the sender's and
recipient's bank account number. The encrypted message was\
"111000100010001010001100101011101000010010010100000000000000000000100\
0100011100000010110001110101000111000001000101100001011110010101000000\
0000000001100000111001001110010101010101111001011111000100100100001101\
000100"\
with the key of\
"010000010010000001110110011001010111001001111001001000000111001101110\
1000111001001101111011011100110011100100000011000010110111001100100001\
0000001110010011000010110111001100100011011110110110100100000011100000\
1110111".

The middle man can try to change/tamper with the message so that
the output can be changed. In this example we can change the last
bit from the encrypted text above to\
"1110001000100010100011001010111010000100100101000000000000000000001000\
10001110000001011000111010100011100000100010110000101111001010100000000\
00000001100000111001001110010101010101111001011111000100100100001101000\
101"\
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
22a2a593d8885bc6a2f3f9b639ca96b81957e110303130323033207365
6e6473202439303020746f20313132323333
```
or in computer formatted text/binary it's
```
00100010101000101010010110010011110110001000100001011011110001101
01000101111001111111001101101100011100111001010100101101011100000
01100101010111111000010001000000110000001100010011000000110010001
10000001100110010000001110011011001010110111001100100011100110010
00000010010000111001001100000011000000100000011101000110111100100
000001100010011000100110010001100100011001100110011
```
