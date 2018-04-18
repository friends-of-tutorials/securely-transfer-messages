# A tutorial to securely transfer messages

This is a tutorial to securely transfer messages from system A to system B with various coding languages and keep the rules of information security.

## 0. Contents

* [1. Rules of information security](#user-content-1-rules-of-information-security)
  * [1.1 confidentiality](#user-content-11-confidentiality)
  * [1.2 integrity](#user-content-12-integrity)
  * [1.3 availability](#user-content-13-availability)
  * [1.4 authenticity](#user-content-14-authenticity)
* [2. Preliminary considerations](#user-content-2-preliminary-considerations)
  * [2.1 Unciphered message transfer](#user-content-21-unciphered-message-transfer)
    * [2.1.1 Unciphered transfer](#user-content-211-unciphered-transfer)
  * [2.2 Ciphered message transfer](#user-content-22-ciphered-message-transfer)
    * [2.2.1 Symmetric cryptography](#user-content-221-symmetric-cryptography)
    * [2.2.2 Asymmetric cryptography](#user-content-222-asymmetric-cryptography)
    * [2.2.3 Hybrid cryptography](#user-content-223-hybrid-cryptography)
* [3. Implementations](#user-content-4-implementations)
  * [3.1 Bash](#user-content-31-bash)
    * [3.1.1 Preparations (public and private key)](#user-content-311-preparations-public-and-private-key)
    * [3.1.2 Encryption (System A)](#user-content-312-encryption-system-a)
    * [3.1.3 Decryption (System B)](#user-content-313-decryption-system-b)
  * [3.2 Javascript](#user-content-32-javascript)
    * [3.2.1 Preparations (public and private key)](#user-content-321-preparations-public-and-private-key)
    * [3.2.2 Encryption (System A)](#user-content-322-encryption-system-a)
    * [3.2.3 Decryption (System B)](#user-content-323-decryption-system-b)
  * [3.3 PHP](#user-content-33-php)
    * [3.3.1 Preparations (public and private key)](#user-content-331-preparations-public-and-private-key)
    * [3.3.2 Encryption (System A)](#user-content-332-encryption-system-a)
    * [3.3.3 Decryption (System B)](#user-content-333-decryption-system-b)
  
  
## 1. Rules of information security

### 1.1 Confidentiality

Data may only be read or modified by authorized users, both when accessing stored data and during data transmission.

* [Confidentiality on wikipedia.org](https://en.wikipedia.org/wiki/Information_security#Confidentiality)

### 1.2 Integrity

Data may not be changed unnoticed. All changes must be traceable.

* [Integrity on wikipedia.org](https://en.wikipedia.org/wiki/Information_security#Integrity)

### 1.3 Availability

Prevention of system failures: Access to data must be guaranteed within an agreed timeframe.

* [Availability on wikipedia.org](https://en.wikipedia.org/wiki/Information_security#Availability)

### 1.4 Authenticity

Authenticity refers to the characteristics of the authenticity, verifiability and trustworthiness of an object.

* [Authenticity on wikipedia.org](https://en.wikipedia.org/wiki/Message_authentication)

## 2. Preliminary considerations

### 2.1 Unciphered message transfer

#### 2.1.1 Unciphered transfer

[![No cryptography](/images/no_cryptography.png)](/images/no_cryptography.png)

##### 2.1.1.1 Advantages

* The transfer is easy to implement (just send the "readable message")

##### 2.1.1.2 Disadvantage

* The message is catchable and modifiable. This transfer breaks some rules of information security:
  * confidentiality
  * integrity
  * authenticity

### 2.2 Ciphered message transfer

#### 2.2.1 Symmetric cryptography

[![No cryptography](/images/symmetric_cryptography.png)](/images/symmetric_cryptography.png)

##### 2.2.1.1 Advantages

* simple key management, it only needs one secret key for ciphering and deciphering
* a symmetrical cryptosystem is faster than an asymmetrical one
* suitable for encrypting large amounts of data
* only a system which possesses the secret key are able to decrypt a message
* the encryption itself is fully compatible with the confidentiality provisions of information security

##### 2.2.1.2 Disadvantage

* symmetrical cryptosystems have a problem with key transportation
* the key must be transmitted via a secure route
* if someone gains access to the secret key, he or she can decrypt the sent message

##### 2.2.1.3 Implementations

* [DES (Data Encryption Standard)](https://en.wikipedia.org/wiki/Data_Encryption_Standard)
* [Triple-DES (also TDES, 3DES or DESede)](https://en.wikipedia.org/wiki/Triple_DES)
* [AES (Advanced Encryption Standard)](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)
* [IDEA (International Data Encryption Algorithm)](https://en.wikipedia.org/wiki/International_Data_Encryption_Algorithm)
* [Twofish](https://en.wikipedia.org/wiki/Twofish)
* [Serpent](https://en.wikipedia.org/wiki/Serpent_(cipher))
* [Blowfish](https://en.wikipedia.org/wiki/Blowfish_(cipher))
* [Кузнечик](https://en.wikipedia.org/wiki/Kuznyechik) (Kuznyechik)
* [CAST-128](https://en.wikipedia.org/wiki/CAST-128), [CAST-256](https://en.wikipedia.org/wiki/CAST-256)
* [RC2](https://en.wikipedia.org/wiki/RC2), [RC4](https://en.wikipedia.org/wiki/RC4), [RC5](https://en.wikipedia.org/wiki/RC5), [RC6](https://en.wikipedia.org/wiki/RC6)
* etc.

#### 2.2.2 Asymmetrical cryptography

[![No cryptography](/images/asymmetric_cryptography.png)](/images/asymmetric_cryptography.png)


##### 2.2.2.1 Advantages

* high security
* it solves the key exchange problem entirely (different keys when encrypting and decrypting)
* the knowledge of the public key of the recipient is enough to encrypt
* less complexity in keeping the keys secret
* [digital signatures](https://en.wikipedia.org/wiki/Digital_signature) - possibility of authentication (authenticity)

##### 2.2.2.2 Disadvantage

* asymmetrical cryptography works slow (up to 10.000 times slower than symmetrical methods)
* not suitable for encrypting large amounts of data (the maximum message length is determined by the size of key length)

##### 2.2.2.3 Implementations

* [RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem))
* [Merkle-Hellman](https://en.wikipedia.org/wiki/Merkle%E2%80%93Hellman_knapsack_cryptosystem)
*	[McEliece](https://en.wikipedia.org/wiki/McEliece_cryptosystem)
*	[Rabin](https://en.wikipedia.org/wiki/Rabin_cryptosystem)
*	Chor-Rivest
*	[Elgamal](https://en.wikipedia.org/wiki/ElGamal_encryption)
* [Elliptic-curve cryptography](https://en.wikipedia.org/wiki/Elliptic-curve_cryptography)
* [DSA](https://en.wikipedia.org/wiki/Digital_Signature_Algorithm)
* [LUC Cryptography](https://www.cryptopp.com/wiki/LUC_Cryptography)

#### 2.2.3 Hybrid cryptography

**Version 1 - The receiving system generates the symmetric key**

[![No cryptography](/images/hybrid_cryptography.png)](/images/hybrid_cryptography.png)

**Version 2 - The transmitting system generates the symmetric key**

[![No cryptography](/images/hybrid_cryptography_2.png)](/images/hybrid_cryptography_2.png)

##### 2.2.3.1 Advantages

* it combines the advantages of symmetric and asymmetric encryption
  * fast
  * no key exchange problem
  * suitable for encrypting large amounts of data

##### 2.2.3.2 Disadvantage

* more complex implementation on both the encryption system (system A) and the decryption system (system B)
* both systems need to comprehend the used encryption methods

##### 2.2.3.3 Implementations

* symmetric implementations
  * see symmetric cryptography
* asymmetric implementations
  * see asymmetric cryptography
* [key exchange](https://en.wikipedia.org/wiki/Key_exchange) implementations
  * Basics
    * [Encrypted key exchange](https://en.wikipedia.org/wiki/Encrypted_key_exchange) (EKE)
    * [Password-authenticated key agreement](https://en.wikipedia.org/wiki/Password-authenticated_key_agreement) (PAKE)
    * [Simple Password Exponential Key Exchange](https://en.wikipedia.org/wiki/SPEKE) (SPEKE)
  * [Diffie–Hellman key exchange](https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange) (DH)
  * [Elliptic-curve Diffie–Hellman](https://en.wikipedia.org/wiki/Elliptic-curve_Diffie%E2%80%93Hellman) (ECDH)
  * [Password Authenticated Key Exchange by Juggling](https://en.wikipedia.org/wiki/Password_Authenticated_Key_Exchange_by_Juggling) (J-PAKE)
  * [Secure Remote Password protocol](https://en.wikipedia.org/wiki/Secure_Remote_Password_protocol) (SRP)

## 3. Implementations

### 3.1 Bash

#### 3.1.1 Preparations (public and private key)

##### 3.1.1.1 Private key "private.pem" (System B)

```
user$ openssl genpkey -algorithm RSA -out private.pem -pkeyopt rsa_keygen_bits:2048
user$ cat private.pem
```

```
-----BEGIN PRIVATE KEY-----
MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQChBx8ujTTGJw/m
gnzIhyWC1U1kGRramkp9TszJEls2lBgiVskGaIVhra02K1gYXRNowDeTZnmiacFq
3YwQTlTb6iNYEahySuFlr7SHrUKsUa5P22oN6EXsfE/YkbJ+JDeTUzyjEE1w4QBM
7uWqEdUIR9he3ADvCenBlGsbUlhxHIE8uRVM1Zy1fRIncOlnOs9MnBYQ7m+zb7yD
FKhr1zjTMtYGc3BwInRUMxNXZadNVQXB5RemuDlve821yuJ1DX+xLRkLHZSJzGkd
23kxq1Y3fQhow1poThisUJsbAyOmNnzapwSoUSHrtsW1//c8Nu3qQt8Y6nVqNKhi
C9mhIFExAgMBAAECggEAH7DpIB5GPqE9bd5MdKK0bTVRj9uo/1DSTCsP/pqQPQOU
ZF20HoC/j2PA7SJGqjTXNwxtY6MNWTt7B28mu6bO6KEB57lB74xxI7Qa0YD12DgT
GEBUdPw7lrk4daTm/hBep64ABw+UThzaFEoIBRqRVJnfKXwe6uyGhsSQ98WTBl+H
w2LOHCSdSDT47x1ErtRwWFCg0cvZQJK0w+aDNkjyeoalIj5beC+QJbze6Tyvwo1c
K5CdI79PHqxfBaLi+/nFEYTK4/LkjMCj3xErZmu3FMfUNIfJRNW5PI4Pf2bIJOrQ
4HxXspPmYw/kgzaKWZExkJqDAseDI+muVKrVAX8oaQKBgQDVbRq6AA9p+QqNIsVX
FvLO2U8sj6aecQBNKM6/fYzkpbTYH/gdGuv2THLdzeJ0Bfc00PW5I/DTv0MY5wy7
tcOne9bgBLeK/Fj5HVt9PrsvmuCyNHg1QwGxMZ3FKABKsIpGlyAwU7MEhLz6JBo9
c1BdfIHlaBakQpakNomlEqjs4wKBgQDBJjlhPEk05zHpVBkY13a9jCup+5xPPxoF
q20bhwmmFMdlh3Wdb0XO8duqessR8v11ny9stwKRHcDKXMbzmf+2FXavn0XBJ2iM
Y/UoYIROdO+tzm7+oNAdSCPFIPlABEMFfbyTAyEsEhmZpmY7CHaPH26S7oE2CK1+
MFQVvu6Z2wKBgHvZz4umY0t84LmcNuZeA9MzWfWi+u6w5prgFnIbGnrJClPs4V+K
cum/3VyHkGUB3T3CEQY6LBPExtwZoFMBnKOBguUG97foznzpo2Df2WI7vy7KsgM+
einogAScPOca4XMrWduRhq4VlVCXSL7mPvmxOfP1XkY9+gsbNu8bD/o/AoGAXFsT
qsvx0UsPUZt12KwGSgJBSqlWB4qLvdRHepcqZPCgm4qXEa2IOrjpKW5HtZBz4483
VQt5Pbx1WA3ez9J+NCm1M6q75u0aD68oJaNpAD7n8Dq6ViS8/pNlDziCFjszdOe3
iLBBZ1pMRW0MiwOz9SG5dKZ4wEaL9r/TJQbD/msCgYBqe5o6RYb/g5bS1q/pmKfc
0+arpAOxaOq5b4wxzXpDyZDUuUGdzPSDUlLGR9KX5JTkeWqLkOepat9uMI1f58T3
fYrhQ6beGp3GWtmtTk4kiclHlu/rUPqRQQZ4iLvjc4pTxDdz8U5jv6/j5WKd6xwy
SyuRojfsMfUIFOQJ6NCW2w==
-----END PRIVATE KEY-----
```

#### 3.1.1.2 Public key "public.pem" (System A)

```
user$ openssl rsa -pubout -in private.pem -out public.pem
user$ cat public.pem
```

```
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAoQcfLo00xicP5oJ8yIcl
gtVNZBka2ppKfU7MyRJbNpQYIlbJBmiFYa2tNitYGF0TaMA3k2Z5omnBat2MEE5U
2+ojWBGockrhZa+0h61CrFGuT9tqDehF7HxP2JGyfiQ3k1M8oxBNcOEATO7lqhHV
CEfYXtwA7wnpwZRrG1JYcRyBPLkVTNWctX0SJ3DpZzrPTJwWEO5vs2+8gxSoa9c4
0zLWBnNwcCJ0VDMTV2WnTVUFweUXprg5b3vNtcridQ1/sS0ZCx2UicxpHdt5MatW
N30IaMNaaE4YrFCbGwMjpjZ82qcEqFEh67bFtf/3PDbt6kLfGOp1ajSoYgvZoSBR
MQIDAQAB
-----END PUBLIC KEY-----
```

#### 3.1.2 Encryption (System A)

##### 3.1.2.1 Generate the iv and key from given passphrase

The passphrase is "MySecretPassphrase". In some cases you will need the passphrase. In some cases the equivalent iv and key:

```
user$ openssl enc -nosalt -aes-256-cbc -nosalt -pass pass:MySecretPassphrase -P | \
sed 's/key=\([0-9a-z]\+\)/\1:/gi' | \
sed 's/iv =\([0-9a-z]\+\)/\1/gi' | \
tr --delete '\n'
```

The result is:

```
71EB7C9E4F6E4B4A1341E4AD519FB22D0BD4A0AF0B8CB77FEA0C6E1F82870B0C:10A8C339AEC170CCBA8D3816785F67F6
```

Which means:

```
passphrase=MySecretPassphrase
key=71EB7C9E4F6E4B4A1341E4AD519FB22D0BD4A0AF0B8CB77FEA0C6E1F82870B0C
iv=10A8C339AEC170CCBA8D3816785F67F6
```

Encrypt the key and iv or your secret passphrase, depending on what your decryption library supports. Below is the example with a key and iv. The combination will encrypted with the public key "public.pem":

```
user$ $ rsaCiphertext=$(\
    openssl enc -nosalt -aes-256-cbc -nosalt -pass pass:MySecretPassphrase -P | \
    sed 's/key=\([0-9a-z]\+\)/\1:/gi' | \
    sed 's/iv =\([0-9a-z]\+\)/\1/gi' | \
    tr --delete '\n' | \
    openssl rsautl -encrypt -pubin -inkey public.pem | \
    base64 \
) && echo -e "$rsaCiphertext"
```

As an example, the output below which differs from yours:

```
NdqZLQkmyq3BVgz5M1F/wWX/KNIBxkYWGau3JS6r7t88o08KbsT7N7paS7SsUnclWtLj2Dt4YLu5
7sybKc1m8S/vXj4pJ4wQicgSv2+KvV0baebQ/jw559W8y52HPKj/KNEL/uf1NULijyn0fVuMzaWn
bz0UTwN7NVfZcG5ohyXOLEiS6eEkGIHeqAV7VcJf51wxNMHg0aH1ENB/3Zs7zUY6lQJtUIIDZYiF
/c9QMg49g8RytB8Bkg7Fqd5DmptbjXXbGAK3TAKOfdKv3H8TOtkItQGg9DILCRrBzX0PgdpmnRCE
EftyO2lwVc88+ql2+GVFRkxxOlSdQ46FTeryag==
```

##### 3.1.2.2 Encrypt the message

For example with AES encryption and the passphrase:

```
user$ aesCiphertext=$(\
    echo -en "Hello world! :)\n\nThis is my secret text." | \
    openssl enc -base64 -e -aes-256-cbc -nosalt -pass pass:MySecretPassphrase \
) && echo -e "$aesCiphertext"
```

The result:

```
4FFWdfqQzuMd/JP3fvpriRC5oajS8ENpCD3ZOxDVBZmWAFPhIkb4iVbWYnWPDNCw
```

##### 3.1.2.3 Combine the RSA ciphertext and AES ciphertext

```
user$ echo -e "$rsaCiphertext\n\n$aesCiphertext"
```

With the result:

```
NdqZLQkmyq3BVgz5M1F/wWX/KNIBxkYWGau3JS6r7t88o08KbsT7N7paS7SsUnclWtLj2Dt4YLu5
7sybKc1m8S/vXj4pJ4wQicgSv2+KvV0baebQ/jw559W8y52HPKj/KNEL/uf1NULijyn0fVuMzaWn
bz0UTwN7NVfZcG5ohyXOLEiS6eEkGIHeqAV7VcJf51wxNMHg0aH1ENB/3Zs7zUY6lQJtUIIDZYiF
/c9QMg49g8RytB8Bkg7Fqd5DmptbjXXbGAK3TAKOfdKv3H8TOtkItQGg9DILCRrBzX0PgdpmnRCE
EftyO2lwVc88+ql2+GVFRkxxOlSdQ46FTeryag==

4FFWdfqQzuMd/JP3fvpriRC5oajS8ENpCD3ZOxDVBZmWAFPhIkb4iVbWYnWPDNCw
```

Encode the result with base64:

```
user$ echo -en "$rsaCiphertext\n\n$aesCiphertext" | base64
```

The following combined ciphertext is only decryptable with the private key (private.pem) and can be safely sent over any data network:

```
TmRxWkxRa215cTNCVmd6NU0xRi93V1gvS05JQnhrWVdHYXUzSlM2cjd0ODhvMDhLYnNUN043cGFT
N1NzVW5jbFd0TGoyRHQ0WUx1NQo3c3liS2MxbThTL3ZYajRwSjR3UWljZ1N2MitLdlYwYmFlYlEv
anc1NTlXOHk1MkhQS2ovS05FTC91ZjFOVUxpanluMGZWdU16YVduCmJ6MFVUd043TlZmWmNHNW9o
eVhPTEVpUzZlRWtHSUhlcUFWN1ZjSmY1MXd4Tk1IZzBhSDFFTkIvM1pzN3pVWTZsUUp0VUlJRFpZ
aUYKL2M5UU1nNDlnOFJ5dEI4QmtnN0ZxZDVEbXB0YmpYWGJHQUszVEFLT2ZkS3YzSDhUT3RrSXRR
R2c5RElMQ1JyQnpYMFBnZHBtblJDRQpFZnR5TzJsd1ZjODgrcWwyK0dWRlJreHhPbFNkUTQ2RlRl
cnlhZz09Cgo0RkZXZGZxUXp1TWQvSlAzZnZwcmlSQzVvYWpTOEVOcENEM1pPeERWQlptV0FGUGhJ
a2I0aVZiV1luV1BETkN3
```

Write the complete ciphertext to file "cipher.txt":

```
user$ echo -en "$rsaCiphertext\n\n$aesCiphertext" | base64 > cipher.txt
```

#### 3.1.3 Decryption (System B)

##### 3.1.3.1 Extract the asymmetrical and the symmetrical part

```
user$ cat cipher.txt | base64 --decode
```

The expected result is:

```
NdqZLQkmyq3BVgz5M1F/wWX/KNIBxkYWGau3JS6r7t88o08KbsT7N7paS7SsUnclWtLj2Dt4YLu5
7sybKc1m8S/vXj4pJ4wQicgSv2+KvV0baebQ/jw559W8y52HPKj/KNEL/uf1NULijyn0fVuMzaWn
bz0UTwN7NVfZcG5ohyXOLEiS6eEkGIHeqAV7VcJf51wxNMHg0aH1ENB/3Zs7zUY6lQJtUIIDZYiF
/c9QMg49g8RytB8Bkg7Fqd5DmptbjXXbGAK3TAKOfdKv3H8TOtkItQGg9DILCRrBzX0PgdpmnRCE
EftyO2lwVc88+ql2+GVFRkxxOlSdQ46FTeryag==

4FFWdfqQzuMd/JP3fvpriRC5oajS8ENpCD3ZOxDVBZmWAFPhIkb4iVbWYnWPDNCw
```


Now. Split the result. The asymmetrical part:

```
user$ cat cipher.txt | base64 --decode | sed '/^$/q'
```

```
NdqZLQkmyq3BVgz5M1F/wWX/KNIBxkYWGau3JS6r7t88o08KbsT7N7paS7SsUnclWtLj2Dt4YLu5
7sybKc1m8S/vXj4pJ4wQicgSv2+KvV0baebQ/jw559W8y52HPKj/KNEL/uf1NULijyn0fVuMzaWn
bz0UTwN7NVfZcG5ohyXOLEiS6eEkGIHeqAV7VcJf51wxNMHg0aH1ENB/3Zs7zUY6lQJtUIIDZYiF
/c9QMg49g8RytB8Bkg7Fqd5DmptbjXXbGAK3TAKOfdKv3H8TOtkItQGg9DILCRrBzX0PgdpmnRCE
EftyO2lwVc88+ql2+GVFRkxxOlSdQ46FTeryag==
```

The symmetrical part:

```
user$ cat cipher.txt | base64 --decode | sed '1,/^$/d'
```

```
4FFWdfqQzuMd/JP3fvpriRC5oajS8ENpCD3ZOxDVBZmWAFPhIkb4iVbWYnWPDNCw
```

##### 3.1.3.2 Decrypt the key and iv (from asymmetrical part)

```
user$ cat cipher.txt | base64 --decode | sed '/^$/q' | base64 --decode | openssl rsautl -decrypt -ssl -inkey private.pem
```

```
71EB7C9E4F6E4B4A1341E4AD519FB22D0BD4A0AF0B8CB77FEA0C6E1F82870B0C:10A8C339AEC170CCBA8D3816785F67F6
```

##### 3.1.3.3 Decrypt the ciphertext (from symmetrical part)

With the iv and the related key:

```
$ echo $(cat cipher.txt | base64 --decode | sed '1,/^$/d') | openssl enc -d -base64 -aes-256-cbc -nosalt -K 71EB7C9E4F6E4B4A1341E4AD519FB22D0BD4A0AF0B8CB77FEA0C6E1F82870B0C -iv 10A8C339AEC170CCBA8D3816785F67F6
```

```
Hello world! :)

This is my secret text.
```

Or with the passphrase above (depending on what is currently available):

```
user$ echo $(cat cipher.txt | base64 --decode | sed '1,/^$/d') | openssl enc -d -base64 -aes-256-cbc -nosalt -pass pass:MySecretPassphrase
```

```
Hello world! :)

This is my secret text.
```

### 3.2 Javascript

#### 3.2.1 Preparations (public and private key)

TODO...

#### 3.2.2 Encryption (System A)

TODO...

#### 3.2.3 Decryption (System B)

TODO...

### 3.3 PHP

#### 3.3.1 Preparations (public and private key)

```
<?php
  
/* Configuration settings for the key */
$config = array(
    "digest_alg" => "sha512",
    "private_key_bits" => 4096,
    "private_key_type" => OPENSSL_KEYTYPE_RSA,
);

/* Create the private and public key */
$res = openssl_pkey_new($config);

/* Extract the private key into $private_key */
openssl_pkey_export($res, $private_key);

/* Extract the public key into $public_key */
$public_key = openssl_pkey_get_details($res);
$public_key = $public_key["key"];

/* echo the public key */
echo $public_key."\n";

/* echo the private key */
echo $private_key."\n";
```

```
-----BEGIN PUBLIC KEY-----
MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAsiltxODGMWWn6jJbsu64
/nmkZMYSFzEqdr61FVZN+u3C2oxioTAQvHYiCXvH0Kzek69hjDUE8UOcNoQWJ2C1
N7gmUdj+j4CaaGlU5Wo3CFuinfuj5BpH7OazZfkp5T0yql5Afv6HH9/y11bJ4kHZ
LOuN2osce0OsknGj9wFt7VQ+NoPMdDh5xR5qVA45KXaAGvOEeKnQ3v+IaxRxiLEr
wzXVjbbQ9ufdxp/gYwaQje9++jeC47Ksc7iiA0FFl67TRkJquaD0XXl35XgwKbG0
KP576/43vD0ojeaJFfDa+rZfjOEAhF/B+KDcqq2Bgm1VFcLq2WUY2DZcUji3BiPT
taWwifBcJgmmvWbI46dcTh1AfPnAHEvq8AEQUnEL+ZuBVeYMCUnoeBhPYT4kzsS0
34mcB/+MxtVwmENM5f71PtzWWiNV6o6r2jLIepE3zCcIim2+vv3uIkvlVtreBc7f
2lL4nIkg79fZVsFG2Mz/Jq4Stnw0dSpIz0CArAm73aTpLqGEarbf/Oko96sNp9OZ
gon0WBaJaEbwiTrjy5L8BRwJMapsB5YcWnJbXyfL8IT551nR+TYT67RG5rc59Inh
jkAjHB3dAgF0xns0s9wsVBk9NsHim+GmTI9QCQM5MFtV9aVJRdmOIDZWY0Xb3C/Y
lNoau1fErFFcPhFZ1jpJj5kCAwEAAQ==
-----END PUBLIC KEY-----
```

```
-----BEGIN PRIVATE KEY-----
MIIJQgIBADANBgkqhkiG9w0BAQEFAASCCSwwggkoAgEAAoICAQCyKW3E4MYxZafq
Mluy7rj+eaRkxhIXMSp2vrUVVk367cLajGKhMBC8diIJe8fQrN6Tr2GMNQTxQ5w2
hBYnYLU3uCZR2P6PgJpoaVTlajcIW6Kd+6PkGkfs5rNl+SnlPTKqXkB+/ocf3/LX
VsniQdks643aixx7Q6yScaP3AW3tVD42g8x0OHnFHmpUDjkpdoAa84R4qdDe/4hr
FHGIsSvDNdWNttD2593Gn+BjBpCN7376N4LjsqxzuKIDQUWXrtNGQmq5oPRdeXfl
eDApsbQo/nvr/je8PSiN5okV8Nr6tl+M4QCEX8H4oNyqrYGCbVUVwurZZRjYNlxS
OLcGI9O1pbCJ8FwmCaa9Zsjjp1xOHUB8+cAcS+rwARBScQv5m4FV5gwJSeh4GE9h
PiTOxLTfiZwH/4zG1XCYQ0zl/vU+3NZaI1XqjqvaMsh6kTfMJwiKbb6+/e4iS+VW
2t4Fzt/aUviciSDv19lWwUbYzP8mrhK2fDR1KkjPQICsCbvdpOkuoYRqtt/86Sj3
qw2n05mCifRYFoloRvCJOuPLkvwFHAkxqmwHlhxacltfJ8vwhPnnWdH5NhPrtEbm
tzn0ieGOQCMcHd0CAXTGezSz3CxUGT02weKb4aZMj1AJAzkwW1X1pUlF2Y4gNlZj
RdvcL9iU2hq7V8SsUVw+EVnWOkmPmQIDAQABAoICAFYugDDaYkUG3aEGVyFJJSfE
A+fTgHDDkbz7J3F43CPj23wIqLU8IPxpULGxtMiWttxN3CwMgaWLhQdCAc1ulHqt
k6vIAeu80/Rp721CYfijCxjM30y6AczxFBrh2ohPgDC1gxFrYkXi+P99tg7Ct6Fp
GKd833wpElOMsToM8PX66FVKkB4wK4dU3S5n6vLJpdJjtdMAok8c4QqbSwhKW9cE
NZdltdOZ+cfZEpwUUty124CCVch7Z7xatdRJQLbNFNpJyoKc/1gwJ/VSnEmu8m1a
HOvdf2yJURLDT9DTP7pDehkVxkBCafwxJE1TvPAwnxX1wdEDfG8qbKJBWReZQREw
VVJolV11cxEoSLiUZxR2EROKZI1OQStS+wGTYtJyi9oBSguO2dT6XJQKgxlb6U8P
KASoG+4Q0vaLd9JI3DoxeRGH0fGmcE6/YEi8ir/55j9TS0XC/m+lTjU/ZaAwY2NB
BOVigsjXk0JXwH9g3H/sEkmlzUt85dJBMusaBHvrui0HytAw2T1fkaJCFyBsJpMZ
rCnRIjiBeBFdWc1Wfs1F/teODNmiJqAOlDKVFFZuPnc9NsfMUA1epyE24v+5JQoa
ios74DOVsC1e5qL8B4dj8PeTAC+D4b+Qt49T5f08IeA13CTRrux/cLxoWOAa0m+u
FMRnyNk27iunomLVxuABAoIBAQDj7ahwiXpg2Wmkx5MAVRigcyvfor6bZIPEHYo5
EAi5DIvb1OAenDEdHvPQ68JtXXa5p1qQyEYn4aBS63dNYh+praSD+66//XvS5qEM
nKt3LPa+DYuBhtLe44UqdF11EQ0P+0DH/lsLxTp0uwuzg5Hh4II4DBT6uoRdB6sC
2qlIa5f0+4+9eB4iOF0OJx9iN7RCkNudcVfh+xH2XJciEduZSQC1Jc4Vh3LEd8IC
SQsml9z+fmTSeqTKc2KXNMCoIo0CYqgrPO1IZzRcDZw2K0emwxoTSE6Vqeezk4L1
yStwe3T7AIUxYDE1rAK+f0JnPurBBD7GqlY5yclRv8tY46GZAoIBAQDIGq9BlMQG
FSCAb3xxeebwWIEOjN7rJa9wTdFCfq4G6+C41Ux3d9o5DH1TdCjjDZxDhPNUoaox
zkh+Y1s19JS+sDQGRF7JOP59/pBuRiwh4LPtG3p2/dfNR+Qm9zxBjadrAlh7Dp/j
vPKO5rwllJNjUE+PSCIV/s2V5JAxT2YzIO13asyzNF1jxK0fnFV6YswILpDDe4FF
o3rPL6G+nPcRDQ38O1ui2cjnLCsQ4TwCyWxgSNTaRelEhdmTo6pcKPUhveMG3cej
TONRM+aLvUlGG+T+54uOWpZrkBPPFh3u8l7AYAUSSiWaqnFhixPymmMc4SuRbpGX
iWQVMtJN5h4BAoIBAQCryCVH08VhEtrVLvjyqi/qVYL+hJilYwcQGrdfNF9uoC8U
WocjatJ1QSu/DMC3Tla5q5DNR7PgQONlO0PqFYcJie5Q7rIQzsmw9NLyP23XXxMD
wA+hamypQc7OZW8+WMCAh/uV/3S9FUNuUL6L6CBdnahm92wkX8h8mNfhSc2F4Flh
cOsvgEUtw08W6JN1ocgA1049hfwXO/OYusXJDq50A5o97KU6gqATxLJ6qHR3/MK5
J6dzHq3uSzJGBaMh1RBzeMmH9N5c0DOdIUDXbp0M6URQvhFEKQ6QwB9WgOx1VQag
Wg8IXJgZ/G8BBcaVK80f9cQeVKix2wwYybVHZCAZAoIBADR8e1eyU7Bcvkex9mw1
U1Pbgw5z+Myo99l3L9pHLBJ4sFsK56G2eDDai8zl/QuBOGmlZ8XdGa0ytGUiXnxK
iPFzelHigRI6ttYJfYzPLyg7rjYVLQwlDQO1RazK0K1JII668MZmUZ4Eo4LEFrms
vPQhzpyAiSBH01jruL6WWvIyQtc91i9zHsPahKZz9R/C5k2HGUWNEZ1Ygg/yKHS8
6zk3uWFdmG2gvkeUmD83NOxuNNUUhXAzQjpM+YL2POsrexC8o93bMlAtDLrx6Bjj
L2MKUghiZ4KRVD8mbWu2G2fffubqyKnBdReaeV7igfryb+jVTv44iEu9J9k/mVYB
dAECggEAXP5BOVdJcDX63U9+OHaFSbvwx5xQtQFOcDQF4p6pxFwLGTNPyrMr4Uoc
w1CtBCyhodq07gd0T3hKfPjl9hayG5bIob2P11AJX6vAdCaDswpF8rghp9KpxSYW
RAGbpAuA0hFRzQhYLtMvle/2y0y7gvM6eGAPNmfRLYuEuGOv0QjxC0gv19uKyyiS
gcG3cymUO2gEvu5IUOG9A2WE3ADs/e/rmemggwgs0PAq0gbYdexC10eoePh0089/
mLxrr7Rm8iG2GPcg7VYsdg+gNrNufvp5UElj+kehtPc79IUUZDleZRlPJ6ktE2Hz
goHztrHKEfdakTIGpcrDUOXzgqiVDw==
-----END PRIVATE KEY-----
```

#### 3.3.2 Encryption (System A)

TODO...

#### 3.3.3 Decryption (System B)

TODO...

## A. Authors

* Björn Hempel <bjoern@hempel.li> - _Initial work_ - [https://github.com/bjoern-hempel](https://github.com/bjoern-hempel)

## B. License

This project is licensed under the MIT License - see the [LICENSE](/LICENSE) file for details


