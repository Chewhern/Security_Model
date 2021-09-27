# What is MFA(Multi-Factor Authentication)?
**MFA** is an idea where a single authentication is not enough to stop
an attacker or a hacker to get into user's account.\

MFA commonly consists of 3 characteristics which are **Something we know(can
be password but doesn't need to be**,**Something we have(refers to email/phone
number)** , **Something we are(refers to biometrics such as our eyes, face, voice
,  fingerprint)**

Anyone who have a knowledge of passwords security and machine learning will
understand why biometrics are not as good as public key authentication or
password based authentication. However, it's up to people to decide whether it's
worthy to use.

### Common MFA (Something we have)
1. OTP
2. TOTP
3. FIDO

People may or may not know OTP or TOTP but they are everywhere in our life. When you
use an online banking service, you will usually receive a PIN or some message that
asks you to type into the bank website to further authenticate you. They commonly
send you the PIN via SMS/email.

FIDO is a relatively new MFA which we uses a login mechanism similar to SSH public key
authentication.

However, these common MFA does not really suit privacy based use cases as they require
the binding of email/phone number/IP addresses which defeats the purpose of privacy.

## Double public key authentication for privacy use cases (Something we know + have)
Let's have a look at how SSH public key authentication work. In public key authentication,
a user is required to generate pkcs's digital signature keypair. During sign up process (other
process that may be applicable), the public key from the keypair was send to the server.

Everytime a user wants to login, the server sends a random data that generated through cryptography
randomness with a minimum length of 128 bits. The user gets the random data and use their private
key from the keypair to sign the random data. The user then sends back the signed random data to
the server. The server uses the user's public key to verify the signed random data. If the verification
succeeded, it's best to assume user does not give their private key away or to public and user had login
into the system.

This is a general idea of how public key authentication works by using digital signatures.

Assuming a user has 2 device which is device A and B. The device can be any device which consists of desktop/laptop/mobile phone.
Device A and B must not be the same. Let's assume the user is Alice. Alice uses device A(laptop) to sign up by using public key
authentication. If 2FA was not required, Alice can just use a pretty secure "Something we know" to login without any pain.

If 2FA was required, Alice requires to use 2 devices. Device A which is her laptop is responsible to achieve "Something we know"
in MFA. Device B which she chooses to use her mobile phone is responsible to achieve "Something we have". The device and Alice's
user ID can be generated without requiring the user to submit any of their private credentials(email/phone number/device number/IP
address). These 2 devices Alice chooses are using public key authentication. This mechanism does not have a formal name hence I name
it as double public key authentication.

### Problems that caused by using double public key authentication (User side)
1. It's quite problematic for user as the convenient aspect had lost
2. It's impossible to know whether the user uses the same device for double public key authentication
3. It's an increased risk on user side as losing either of the devices will cause serious troubles to user
