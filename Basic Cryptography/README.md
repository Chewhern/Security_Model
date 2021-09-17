## Continuation of Symmetric Encryption Key Sizes

A lot of people may not understand what is 128 bits,192 bits and 256 bits key size.

### 128 bits key size
In 128 bits key size, the initial value was 0 and the last (long) value was
``` 
1797693134862315907729305190789024733617976978942306572734300811577326758
0550096313270847732240753602112011387987139335765878976881441662249284743
0639474124377767893424865485276302219601246094119453082952085005768838150
68234246288147391311054082723716335051068458629823994
7245938479716304835356329624224137215.
```

The key can be any value starting from 0 to that huge number shown above.\
Assuming the key was randomly generated, it has the value of\
72081832065758414117397666685607916814

There're approximate an average of
340282366920938463463374607431768211456 combinations to go through.

What an attacker has to do was to start from initial value 0 and keep on
incrementing by 1 till they reach the randomly generated value. This is a
task that needs life time of a universe to go through. In computer terms,
this is call brute forcing.

The same can be said to 192 bits and 256 bits.

### 192 bits key size
In 192 bits the last (long) value was
```
24103124269210325885801166060283141129120932479456889513596750390652573
91591803200669085024107346049663448766280888004787862416978794958324969
61298789077465145521333938162522477078207791768149967684554313738782005
75973458579045991094613871220995079649978156413423006776294733552816174
28411794163967785870370368969109221591943054232011562758450080579587850
90099371489228347664663118151506380487337518226050624699283789870597101
2525843324401232986857004760339316735
```

The average combinations to go through was
```
6277101735386680763835789423207666416102355444464034512896
```

### 256 bits key size
In 256 bits the last (long) value was
```
32317006071311007300714876688669951960444102669715484032130345427524655
13886789089319720141152291346368871796092189801949411955915049092109508
81523864482831206308773673009960917501977503896521067960576383840675682
76792218642619756161838094338476170470581645852036305042887575891541065
80860755239912393038552191433338966834242068497478656456949485617603532
63220580778056593310261927084603141502585928641771167259436037184618573
57598351152301645904403697613233287231227125684710820209725157101726931
32346967854258065669793504599726835299863821552516638943733554360213543
3229604645318478604952148193555853611059596230655
```

The average combinations to go through was
```
11579208923731619542357098500868790785326998466564056403945
7584007913129639936
```

### Quantum Computer
When big scale of QC arrived, all the average combinations(128 bits,
192 bits, 256 bits) was reduced by 50%. If that's the case, 256 bits
of key sizes should be able to withstand the attacks of QC.

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

## Continuation of PKCS
PKCS in general is a cryptography system that consists of public and
private key. However.., I believe many people may not understand it.

Let's use RSA as an example(Mathematics). There're several parameters
of RSA. Here's the list of paramaters:

1. P (Random Big Prime Number)
2. Q (Random Big Prime Number)
3. Modulus (P x Q)
4. N (P-1) x (Q-1)
5. Exponent
6. D

**Note: Prime number refers to it has only 2 factors which is 1 and itself,
2 is a prime number, 3 is a prime number, 5 is a prime number, 7 is a prime number,
11 is a prime number.**

Exponent and D must fulfill an equation in which Exponent x D divide by N
then get its remainder. The remainder must equal to 1. 

In general, we will first find an exponent in which it has a **GCD** of 1
with N (There're many ways to find exponent and D value which satisfies the
equation. However, let's do it my way). In industry, the exponent was always
a fixed small number(A prime number value of 65537). Once we have found the
value of exponent, we can find the value of D through ModularInverse(Do your
own research). 

Here's a sample run.
1. P=197
2. Q=199
3. Modulus = 39203
4. N = 38808
5. Exponent = 5
6. D = 23285


The variables that made up RSA public key was (Modulus,Exponent). The variables
that made up RSA private key was (Modulus, D). Due to the fact that Modulus
is present in both public and private key of RSA. The value of Modulus(if website
certificate uses RSA, you can see a long list of numbers) was automatically consider
as public value.

The encryption formula of RSA was:\
Encrypted Message = Message ^ Exponent % Modulus\
**Note: "^" is a mathematical symbol that refers to power/exponentiation\
"%" is a programming/coding symbol that refers to divide 2 values and get its
remainder**

The decryption formula of RSA was:\
Decrypted Message = Encrypted_Message ^ D % Modulus

Let's say, I give you only public key of RSA which is Modulus(39203) and Exponent(5).
I ask you what is my P,Q,N and D..? You have no idea.. What values do I pick and use.
It's very easy to calculate Modulus,N,Exponent and D if I give it any P or Q value. It's
not an easy task to try and get P and Q through Modulus. P and Q is randomly chosen big
prime numbers.

In modern industry, Exponent was always 65537(a prime number with special characteristics).
Hence, the attack can only be perform on Modulus. 

The process of finding possible P and Q value used in creating Modulus value was call
solving the discrete logarithm problem.

This small example describes why it's useless to obtain only PKCS's public key. The process
of finding private key through public key is not doable.

However.. If big quantuam computer arrives, getting private key through public key can be done
very easily. In RSA, this was affected heavily by an algorithm call **"Shor's algorithm"**, which
is impossible to do with current computer but it's very easy to do with big quantum computer.

Similar attacks can also be apply to Elliptic Curves, Diffie Hellman Key Exchange. This's the
reason why researchers(cryptography) all over the world is trying to find QC resistant PKCS.

## Continuation of PKCS public key encryption

Let's use RSA as an example. Assuming the message we want to encrypt in its number format was "84"
(T), we use the above sample exponent and modulus.

We can use the encryption formula to encrypt the "84". We will then get the encrypted data which was
"23285".

We can use the decryption formula to decrypt the "23285". We will then get the decrypted data which
was "84"(T).

Due to the fact that RSA has big decryption key, the bigger the decryption key gets, the slower
the process of decryption. 

In RSA, we can't encrypt message that's bigger than the modulus. If the message value was bigger
than the modulus value. We need to split the data into smaller chunks and decrypts it. Unlike
symmetric encryption algorithm like AES(Block Cipher), ChaCha20(Stream Cipher), Salsa20(Stream
Cipher), the splitting process is not automatic, developer/user will need to split the data
by implementing logic.. Often the case.., not only this is problematic, it will also allow more
attacks to perform on RSA. 

## Continuation of PKCS digital signature

Let's use RSA as an example. Assuming the message we want to encrypt in its number format was "84"
(T), we use the above sample exponent,modulus and D.

We can use the decryption formula to encrypt the "84". We will then get the encrypted data which was
"37499".

We can then use the encryption formula to decrypt the "37499". We will then get the decrypted data
which was "84". 

When we use RSA decryption formula to encrypt data. This was call signing like in real life's signature.
When we use RSA encryption formula to decrypt data. This was call signature verification.

Similar concept was used in DSA(Digital Signature Algorithm), ECDSA(Elliptic Curve Digital Signature
Algorithm) and ED25519 or ED448 (State of the art Elliptic Curve Digital Signature Algorithm).
