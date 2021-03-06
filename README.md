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
* [4. Tools](#user-content-4-tools)
  * [4.1 Check the private key](#user-content-41-check-the-private-key)
  * [4.2 Check private and public key](#user-content-42-check-private-and-public-key)
  * [4.3 Sign and verify a message](#user-content-43-sign-and-verify-a-message)
  
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

##### 2.2.1.1 Explanation

The message is sent unencrypted from system A to system B. This message can be read by anyone (confidentiality). The data can be changed unnoticed (integrity). The authenticity of the received message can not be confirmed (authenticity).

[![No cryptography](/images/no_cryptography.png)](/images/no_cryptography.png)

##### 2.1.1.2 Advantages

* The transfer is easy to implement (just send the "readable message")

##### 2.1.1.3 Disadvantage

* The message is catchable and modifiable. This transfer breaks some rules of information security:
  * confidentiality
  * integrity
  * authenticity

### 2.2 Ciphered message transfer

#### 2.2.1 Symmetric cryptography

##### 2.2.1.1 Explanation

Before the readable message is sent, it is encrypted with the symmetric key. Only recipients with the knowledge of this symmetric key can decrypt the message. It is important to ensure that the key exchange is transmitted via a secure way to keep the rules of confidentiality, integrity and authenticity. The key exchange is the sore spot here.

[![No cryptography](/images/symmetric_cryptography.png)](/images/symmetric_cryptography.png)

##### 2.2.1.2 Advantages

* simple key management, it only needs one secret key for ciphering and deciphering
* a symmetrical cryptosystem is faster than an asymmetrical one
* suitable for encrypting large amounts of data
* only a system which possesses the secret key are able to decrypt a message
* the encryption itself is fully compatible with the confidentiality provisions of information security

##### 2.2.1.3 Disadvantage

* symmetrical cryptosystems have a problem with key transportation
* the key must be transmitted via a secure route
* if someone gains access to the secret key, he or she can decrypt the sent message

##### 2.2.1.4 Implementations

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

##### 2.2.2.1 Explanation

[![No cryptography](/images/asymmetric_cryptography.png)](/images/asymmetric_cryptography.png)

##### 2.2.2.2 Advantages

* high security
* it solves the key exchange problem entirely (different keys when encrypting and decrypting)
* the knowledge of the public key of the recipient is enough to encrypt
* less complexity in keeping the keys secret
* [digital signatures](https://en.wikipedia.org/wiki/Digital_signature) - possibility of authentication (authenticity)

##### 2.2.2.3 Disadvantage

* asymmetrical cryptography works slow (up to 10.000 times slower than symmetrical methods)
* not suitable for encrypting large amounts of data (the maximum message length is determined by the size of key length)

##### 2.2.2.4 Implementations

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

##### 2.2.3.1 Explanation

###### 2.2.3.1.1 Version 1 - The receiving system generates the symmetric key

[![No cryptography](/images/hybrid_cryptography.png)](/images/hybrid_cryptography.png)

**Please note:** This variant is more secure than the following variant 2 because the message recipient expects his own generated key and initial vector pair to decrypt the message from the system 1.

###### 2.2.3.1.2 Version 2 - The transmitting system generates the symmetric key

[![No cryptography](/images/hybrid_cryptography_2.png)](/images/hybrid_cryptography_2.png)

**Please note:** Although this variant is easier to implement than version 1, it should be considered that this type of transmission does not regard to the rules of authenticity. It is possible that this message could be intercepted and filled with own content by attackers. In order to keep the authenticity, I recommend to additionally sign the sent message.

##### 2.2.3.2 Advantages

* it combines the advantages of symmetric and asymmetric encryption:
  * this procedure is fast, because it uses the symmetric encryption to encrypt the message
  * no key exchange problem
  * suitable for encrypting large amounts of data

##### 2.2.3.3 Disadvantage

* more complex implementation on both the encryption system (system A) and the decryption system (system B)
* both systems need to comprehend the used encryption methods

##### 2.2.3.4 Implementations

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

The following implementations are fully compatible with each other. This allows you, for example, immediate encryption in the browser (Javascript) and the later decryption on the server (PHP or Bash). Assumed that you use the same public/private key pair.

### 3.1 Bash

#### 3.1.1 Preparations (public and private key)

##### 3.1.1.1 Private key "private.pem" (System B)

```console
user@sh$ openssl genpkey -algorithm RSA -out private.pem -pkeyopt rsa_keygen_bits:2048
user@sh$ cat private.pem
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

```console
user@sh$ openssl rsa -pubout -in private.pem -out public.pem
user@sh$ cat public.pem
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

```console
user@sh$ openssl enc -nosalt -aes-256-cbc -nosalt -pass pass:MySecretPassphrase -P | \
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

I recommend to generate the key and the iv automatically. To better understand the examples below, we use a fixed key and iv as previously used.

Encrypt the key and iv or your secret passphrase, depending on what your decryption library supports. Below is the example with a key and iv. The combination will encrypted with the public key "public.pem":

```console
user@sh$ rsaCiphertext=$(\
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

```console
user@sh$ aesCiphertext=$(\
    echo -en "Hello world! :)\n\nThis is my secret text." | \
    openssl enc -base64 -e -aes-256-cbc -nosalt -pass pass:MySecretPassphrase \
) && echo -e "$aesCiphertext"
```

The result:

```
4FFWdfqQzuMd/JP3fvpriRC5oajS8ENpCD3ZOxDVBZmWAFPhIkb4iVbWYnWPDNCw
```

##### 3.1.2.3 Combine the RSA ciphertext and AES ciphertext

```console
user@sh$ echo -e "$rsaCiphertext\n\n$aesCiphertext"
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

```console
user@sh$ echo -en "$rsaCiphertext\n\n$aesCiphertext" | base64
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

```console
user@sh$ echo -en "$rsaCiphertext\n\n$aesCiphertext" | base64 > cipher.txt
```

#### 3.1.3 Decryption (System B)

##### 3.1.3.1 Extract the asymmetrical and the symmetrical part

```console
user@sh$ cat cipher.txt | base64 --decode
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

```console
user@sh$ cat cipher.txt | base64 --decode | sed '/^$/q'
```

```
NdqZLQkmyq3BVgz5M1F/wWX/KNIBxkYWGau3JS6r7t88o08KbsT7N7paS7SsUnclWtLj2Dt4YLu5
7sybKc1m8S/vXj4pJ4wQicgSv2+KvV0baebQ/jw559W8y52HPKj/KNEL/uf1NULijyn0fVuMzaWn
bz0UTwN7NVfZcG5ohyXOLEiS6eEkGIHeqAV7VcJf51wxNMHg0aH1ENB/3Zs7zUY6lQJtUIIDZYiF
/c9QMg49g8RytB8Bkg7Fqd5DmptbjXXbGAK3TAKOfdKv3H8TOtkItQGg9DILCRrBzX0PgdpmnRCE
EftyO2lwVc88+ql2+GVFRkxxOlSdQ46FTeryag==
```

The symmetrical part:

```console
user@sh$ cat cipher.txt | base64 --decode | sed '1,/^$/d'
```

```
4FFWdfqQzuMd/JP3fvpriRC5oajS8ENpCD3ZOxDVBZmWAFPhIkb4iVbWYnWPDNCw
```

##### 3.1.3.2 Decrypt the key and iv (from asymmetrical part)

```console
user@sh$ cat cipher.txt | base64 --decode | sed '/^$/q' | base64 --decode | openssl rsautl -decrypt -ssl -inkey private.pem
```

```
71EB7C9E4F6E4B4A1341E4AD519FB22D0BD4A0AF0B8CB77FEA0C6E1F82870B0C:10A8C339AEC170CCBA8D3816785F67F6
```

##### 3.1.3.3 Decrypt the ciphertext (from symmetrical part)

With the iv and the related key:

```console
user@sh$ echo $(cat cipher.txt | base64 --decode | sed '1,/^$/d') | openssl enc -d -base64 -aes-256-cbc -nosalt -K 71EB7C9E4F6E4B4A1341E4AD519FB22D0BD4A0AF0B8CB77FEA0C6E1F82870B0C -iv 10A8C339AEC170CCBA8D3816785F67F6
```

```
Hello world! :)

This is my secret text.
```

Or with the passphrase above (depending on what is currently available):

```console
user@sh$ echo $(cat cipher.txt | base64 --decode | sed '1,/^$/d') | openssl enc -d -base64 -aes-256-cbc -nosalt -pass pass:MySecretPassphrase
```

```
Hello world! :)

This is my secret text.
```

### 3.2 Javascript

The symmetric and asymmetric encryptions are not natively supported by Javascript. In the following examples I will use this library for asymmetric encription: https://github.com/travist/jsencrypt. For the symmetric part I will use this library: https://code.google.com/archive/p/crypto-js/. Fell free to use different ones.

#### 3.2.1 Preparations

```javascript
var keySize = 2048;
var crypt = new JSEncrypt({default_key_size: keySize});
var privateKey = crypt.getPrivateKey();
var publicKey  = crypt.getPublicKey();
```

##### 3.2.1.1 Private key

```javascript
console.log(privateKey);
```

```
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQBty7csQsS1w83IftrnRBk2YNmgcAaMWV6tZY4LD0N2Dv7JAl+L
FivBbI7l+ct9lIZtiIXDnbwXsEyZ7Pd6VgbmHIC7XD289Aj9sbAecTw5qvidiH00
GKw1RBpl/TF3Pbwtrq2BI07YlkhZkfcdg86jHQbrwVApQ+7jZQx0QbH7lv+C/92y
1qdE5BeTf7V70ewf8AWaspETcRO4h2qzXvLFIvdPBxn002hay7tGZKUmU6+Sq98M
TbkjQNhDR1t9oISnp5DOSc9VVX4vfU1xUmC2I54I6a9JFgn6ejzkXX9Z8eaDqnSA
8XKr0v1taGYHrPAxOybSqpJRdNShJP8qY9GbAgMBAAECggEASlln2Z4BDMDh6cIV
RAP2Or+Mvzr9BC9EkJCzhkO4wApZeA6WWl4SFTII9iyYIprgCO4o/pUimLv2s0kn
MH1uwIZOmhFVcU2jhP+9LnApgzeGkU6q0gtfGdbbNXMl+wQgGKMvtMIPE1V4+saA
G0l1NTljxWOrf7YT34I+077k4mOvgYjzBD2lmxvvoJtf5TAtrNDxM4KQncbm++BU
ppXFsfchJKr0CGzSPK6/dVu3KmqDRvtPZlz1uvyIiQuKXbNeMlni5RDjfY+Y4Onj
sNvEXF61Xq8J6/Id7qkp8vFaH7djUGx6PApBFG4PTVOWAdYhL3V4Wtr3Rq7X8WN1
zy2SqQKBgQDMBW8naqJX8IvbsH6VThHEQCTPD8rcylUHOJ5jffn+YRzjimhPC5kx
fHF92DIVlB5yM65Ia6rtq2mwFUzJAoNIkQoO/mK4Ky1Xu7t9LjvKOos3jy5IXU5A
TX5p9E2Uv8gW1Fpc8vqbA+B4YlHutk8C04uz5Flye2OEO0tbqFnTHwKBgQCJxMHl
lSV90y9ZLol79rf/+TqzXUuCjydFGfTCG7dig0XOkgNCKTNqTCxVXn0n7YZr6I3i
k84BjE44r4nqudejcDSMQ9DpxovFAgDztIRrLwYf05XkTKCgTiwS69f6nAAiO6lZ
km0c92DykUZt31QpOOPeStGQnL7TpaW6FQkOBQKBgDRnyO91ApJYJXSe10T+sq2Y
VFwjkFY6WrDqKDUiLM7cnxELglObhRQjBPvwRp0oWNG42LGdhmBaQWGLdxfC33oK
V20WhsELxi/c9wHmmFEPzKbOznKkFO+LeEc7C5qD0J+cmEF74EdlLYl+p9ELXyw4
ro/cveUcMKnMmUTH75q9AoGAVaO0sGVVR/EWVsbB+gg0+u7PmZ3eCYu5apAnAN6/
0YIuy6kiU2dPKb2uNWcmP8K8M6n9QSKGBZpVKZGdFwdtT5C5aZPict/UFKQZOWU2
h3ZUxUX+wEsN8niFl0F6IbQFtUIHFMIcB8yTPFYoRLZ2F6XgqFc0DEQTr3ciHRlk
Zo0CgYEAueWy60JdrvfbuQnVfumu4ATdis9yQik8SNGuy4NZwedKPm0vl06kuCxe
7k3Xc4mrjB2cPjcq3H0uzpqWJJeGeIzj865LK4o/PmCgr2zHhxH3Y1qvk8DbvCqM
HQGNjvQKa0q5Q9MfnA23R3yiTi6q4K+tYZDQkczDW8rzfv96k7M=
-----END RSA PRIVATE KEY-----
```

##### 3.2.1.2 Public key

```javascript
console.log(publicKey);
```

```
-----BEGIN PUBLIC KEY-----
MIIBITANBgkqhkiG9w0BAQEFAAOCAQ4AMIIBCQKCAQBty7csQsS1w83IftrnRBk2
YNmgcAaMWV6tZY4LD0N2Dv7JAl+LFivBbI7l+ct9lIZtiIXDnbwXsEyZ7Pd6Vgbm
HIC7XD289Aj9sbAecTw5qvidiH00GKw1RBpl/TF3Pbwtrq2BI07YlkhZkfcdg86j
HQbrwVApQ+7jZQx0QbH7lv+C/92y1qdE5BeTf7V70ewf8AWaspETcRO4h2qzXvLF
IvdPBxn002hay7tGZKUmU6+Sq98MTbkjQNhDR1t9oISnp5DOSc9VVX4vfU1xUmC2
I54I6a9JFgn6ejzkXX9Z8eaDqnSA8XKr0v1taGYHrPAxOybSqpJRdNShJP8qY9Gb
AgMBAAE=
-----END PUBLIC KEY-----
```

#### 3.2.2 Encryption (System A)

##### 3.2.2.1 Encrypt the iv and key

```javascript
var key = '71EB7C9E4F6E4B4A1341E4AD519FB22D0BD4A0AF0B8CB77FEA0C6E1F82870B0C';
var iv  = '10A8C339AEC170CCBA8D3816785F67F6';
var rsaCiphertext = crypt.encrypt(key + ':' + iv);
console.log(rsaCiphertext);
```

As an example, the output below which differs from yours:

```
XIOG1gExmNaYLEMy4X+r2hpobNz0rZRJfQpGgksjlbtgFEH2QYA7sAWAnTgGi5cZDY8GUmGkRYIP4Mhe7RetLXUIbDBNgg8k+ZjDuBAyA1VZBvcvxjR7ZRkbBg45qmWHtkgP9zLGq95soJZJ7mWrKniWz0V8jIz4vsdzy5vNdvNx6JmHnxI3kGLyhwKmBRS2C4ks/LcZP1rjhiyqEGeWQxN7mrg9ywjuuj5QHcqFflerkqnMCPLDXM9lplAuB2rx2+8+TYR9GM4+VNKhbW6fTZxCCcEFPjbfwq2uNpAWZfIvvRHFdhSCBzHXO3dmbA6ZOybIpTzgiTN9keRcCEB6eg==
```

##### 3.2.2.2 Encrypt the message

```javascript
var key = '71EB7C9E4F6E4B4A1341E4AD519FB22D0BD4A0AF0B8CB77FEA0C6E1F82870B0C';
var iv  = '10A8C339AEC170CCBA8D3816785F67F6';
var message = "Hello world! :)\n\nThis is my secret text.";
var encrypted = CryptoJS.AES.encrypt(message, CryptoJS.enc.Hex.parse(key), {iv: CryptoJS.enc.Hex.parse(iv)});
var aesCiphertext = encrypted.ciphertext.toString(CryptoJS.enc.Base64);
console.log(aesCiphertext);
```

The result:

```
4FFWdfqQzuMd/JP3fvpriRC5oajS8ENpCD3ZOxDVBZmWAFPhIkb4iVbWYnWPDNCw
```

##### 3.2.2.3 Combine the RSA ciphertext and AES ciphertext

```javascript
var ciphertext = btoa(rsaCiphertext + '\n\n' + aesCiphertext);
```

The following combined ciphertext is only decryptable with the private key (private.pem) and can be safely sent over any data network:

```
WElPRzFnRXhtTmFZTEVNeTRYK3IyaHBvYk56MHJaUkpmUXBHZ2tzamxidGdGRUgyUVlBN3NBV0FuVGdHaTVjWkRZOEdVbUdrUllJUDRNaGU3UmV0TFhVSWJEQk5nZzhrK1pqRHVCQXlBMVZaQnZjdnhqUjdaUmtiQmc0NXFtV0h0a2dQOXpMR3E5NXNvSlpKN21XcktuaVd6MFY4akl6NHZzZHp5NXZOZHZOeDZKbUhueEkza0dMeWh3S21CUlMyQzRrcy9MY1pQMXJqaGl5cUVHZVdReE43bXJnOXl3anV1ajVRSGNxRmZsZXJrcW5NQ1BMRFhNOWxwbEF1QjJyeDIrOCtUWVI5R000K1ZOS2hiVzZmVFp4Q0NjRUZQamJmd3EydU5wQVdaZkl2dlJIRmRoU0NCekhYTzNkbWJBNlpPeWJJcFR6Z2lUTjlrZVJjQ0VCNmVnPT0KCjRGRldkZnFRenVNZC9KUDNmdnByaVJDNW9halM4RU5wQ0QzWk94RFZCWm1XQUZQaElrYjRpVmJXWW5XUEROQ3c=
```

#### 3.2.3 Decryption (System B)

##### 3.2.3.1 Extract the asymmetrical and the symmetrical part

```javascript
var decryptedSections = atob(ciphertext).split('\n\n');
console.log(decryptedSections[0]);
console.log(decryptedSections[1]);
```

The expected result is:

```
XIOG1gExmNaYLEMy4X+r2hpobNz0rZRJfQpGgksjlbtgFEH2QYA7sAWAnTgGi5cZDY8GUmGkRYIP4Mhe7RetLXUIbDBNgg8k+ZjDuBAyA1VZBvcvxjR7ZRkbBg45qmWHtkgP9zLGq95soJZJ7mWrKniWz0V8jIz4vsdzy5vNdvNx6JmHnxI3kGLyhwKmBRS2C4ks/LcZP1rjhiyqEGeWQxN7mrg9ywjuuj5QHcqFflerkqnMCPLDXM9lplAuB2rx2+8+TYR9GM4+VNKhbW6fTZxCCcEFPjbfwq2uNpAWZfIvvRHFdhSCBzHXO3dmbA6ZOybIpTzgiTN9keRcCEB6eg==
```

```
4FFWdfqQzuMd/JP3fvpriRC5oajS8ENpCD3ZOxDVBZmWAFPhIkb4iVbWYnWPDNCw
```


##### 3.2.3.2 Decrypt the key and iv (from asymmetrical part)

```javascript
crypt.setPrivateKey(privateKey);
var keyIv = crypt.decrypt(decryptedSections[0]);
console.log(keyIv);
```

```
71EB7C9E4F6E4B4A1341E4AD519FB22D0BD4A0AF0B8CB77FEA0C6E1F82870B0C:10A8C339AEC170CCBA8D3816785F67F6
```

##### 3.2.3.3 Decrypt the ciphertext (from symmetrical part)

```javascript
var splittedKeyIv = crypt.decrypt(decryptedSections[0]).split(':');
var decrypted = CryptoJS.AES.decrypt(decryptedSections[1], CryptoJS.enc.Hex.parse(splittedKeyIv[0]), {iv: CryptoJS.enc.Hex.parse(splittedKeyIv[1])});
console.log(decrypted.toString(CryptoJS.enc.Utf8));
```

Now we get the unciphered and expected message:

```
Hello world! :)

This is my secret text.
```

### 3.3 PHP

#### 3.3.1 Preparations (public and private key)

##### 3.3.1.1 Private and public key (System A and B)

```php
/* Configuration settings for the key */
$config = array(
    "digest_alg" => "sha512",
    "private_key_bits" => 2048,
    "private_key_type" => OPENSSL_KEYTYPE_RSA,
);

/* Create the private and public key */
$res = openssl_pkey_new($config);

/* Extract the private key into $privateKey */
openssl_pkey_export($res, $privateKey);

/* Extract the public key into $publicKey */
$publicKey = openssl_pkey_get_details($res);
$publicKey = $publicKey["key"];

/* echo the public key */
echo $publicKey."\n";

/* echo the private key */
echo $privateKey."\n";
```

```
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA66PIvbJwwfpvgfmAk84+
ogJQvc2w3BhnKx2NOioqK8OPE4Z4BrVefBxrb8hX1UjAZTUe2yaCARKEk3BPdz9y
nOdKmewvPs7laMAw72sjPJ4LEqxkdsqoummt+/n8pJt/HXA4Ecf6bcfXN0DQ3Xd9
E2Rr17nn7dsHeKfHdhs2lIgHlkh7zr+eJxDySiOAfScyg+3elO8Ny51LqVjIdhiD
1sGWs/56et/13Mwwpb9IlnowKLQQV5Katj/n7RZFV7edkKWISx+Ax4y1B+ghYNQn
RWfk7+fM0plUVL0KrB/cYDjqowLIlEE2aPKf2yYJhlVSm9Qk0l4YXK/slwM6Fbs+
WwIDAQAB
-----END PUBLIC KEY-----
```

```
-----BEGIN PRIVATE KEY-----
MIIEvwIBADANBgkqhkiG9w0BAQEFAASCBKkwggSlAgEAAoIBAQDro8i9snDB+m+B
+YCTzj6iAlC9zbDcGGcrHY06Kiorw48ThngGtV58HGtvyFfVSMBlNR7bJoIBEoST
cE93P3Kc50qZ7C8+zuVowDDvayM8ngsSrGR2yqi6aa37+fykm38dcDgRx/ptx9c3
QNDdd30TZGvXueft2wd4p8d2GzaUiAeWSHvOv54nEPJKI4B9JzKD7d6U7w3LnUup
WMh2GIPWwZaz/np63/XczDClv0iWejAotBBXkpq2P+ftFkVXt52QpYhLH4DHjLUH
6CFg1CdFZ+Tv58zSmVRUvQqsH9xgOOqjAsiUQTZo8p/bJgmGVVKb1CTSXhhcr+yX
AzoVuz5bAgMBAAECggEBALnaQngsB3dXeR+AlIL/hrLtNJWfaEEQFj8RXdRkcUJ3
SZ/SzVQtNMqa97oAwBX+/ZBVp3KeGqeR3XMUf/jD2DgczOA+Qr09Hf/SpkYPsIkc
9grSYaK4EQCGXa2B7FxAMLAdVHvhyIlRt1NjEdm7ZrEm4VAS1vTpbikh29YxfIkE
hdamp5+1oI+mjcWe49ls+1iFbG7/6tSYxLVlU8mBdmtXu/4TBbrI1uFHYaj1NXxu
ZgiVBI/+kXO7Bg+KCwv0OjXVhYglFHeJhHSdwkgplMLVYQxpOT1bF5TGDB0LgjZB
SJJuWRA1CkCnDbAufd7uPeTSkI9lLN5d4L40stITuuECgYEA9q0fYavc7Oe8Sk/H
ZKtsxlG2aoinyYTvLFHiUYLmuQQ7qOASFJTTf53gy5imqZ9bAg2eXT1tzQKhOPHT
dvJI5Dk9L+HwsE+alYJf4g5EuGcwp0Z99N243qhQmqhdfAwzpEjgNrdUTa9LBPuQ
goik67AIGEg246DXFa86XzyOypMCgYEA9Ive80vRSZ9qYZInXbeN9toG2oj2no86
VYMsmwfPmjQg1vzEeJxKrZr6KKM8JhL3RQ0iDj6rJoo5QVkQDxjW063XfCF0zS1M
3V++KCynXAa6NUNg67RkbAvcsFf0lFyFkqS07nvamhvwBS4ITHQ+cEa29DZyEXav
aRDxh8ycchkCgYEAgvkm2Wg0NEFSky5K02PFrIMEVQpb9D618xVDEj5rnL7nomHe
l7jxlyfPjKpvi06GNs/eTuln3FtSGPclbVl1ZGAT4dGYRzTtAgcoO9GRoUuA5MAj
7pivKOG7cnKEuHGOFeNv0P2EMH8rWOjtMLG2x0E++w2Uv0XODcBtQNXZhysCgYBI
eqw5r9730yfUg1znid+pqjUd0DpIBGtlrNsrl8UQDyMslP4mQSxhB+3c3YSWREjF
Tn8peamAYrdVhvAbiWEinAOh5siXhzWg5x+VCKcRv2yxHKc9NNoOq/VczrTOxB1S
uT5m8I553o3k+x+6iTl4TX0sJHbqdiLHIR51AU/dAQKBgQDVAza0G1pMwDsGShf5
IA6FVqawHv6Z4fO4T8RpBzDmvJxd3oXz9g2fqp/iHJDv1DaXHxPOk9Nm45nBtJmd
JnxOzdrCZbilLX27iPhNuH1EJ2y+UOiHjeZaVHNGNFys5ZO9OhrbxbfDetZU1c/y
aF/4UXNChWkvF87X9jZt7zC9zw==
-----END PRIVATE KEY-----
```

#### 3.3.2 Encryption (System A)

##### 3.3.2.1 Encrypt the iv and key

```php
$key       = '71EB7C9E4F6E4B4A1341E4AD519FB22D0BD4A0AF0B8CB77FEA0C6E1F82870B0C';
$iv        = '10A8C339AEC170CCBA8D3816785F67F6';
$publicKey = file_get_contents('id_rsa.pub');

/* encrypt the key and iv */
$keyIv = sprintf('%s:%s', $key, $iv);

/* encrypt using the public key */
openssl_public_encrypt($keyIv, $encryptedKeyIvBin, $publicKey);
$encryptedKeyIv = base64_encode($encryptedKeyIvBin);
echo $encryptedKeyIv;                                                                             
```

As an example, the output below which differs from yours:

```
irwsNkv5/WjslmOki4uZXLJFCL/bNa8tPAvBih+joXhtf1KNlFZ1xguJECGRgtwuV2+vNRHCa7mYtsbfgkqFpjfjdIZSYRX5h4081CPr24GqmnA8MTOeJGGvgi39y9NOWYAt+iGiMOsRFKwKCq2uWfL2n1xdqaG7Z5oSYWnMVKE66C3GeBmrpWTXH/dau2bxbae3zZLSimrp4LXHvRZ8pqwX/lv1Lz+kIemicQPUJtG3jI5ttb6k8gzWiKwZ9MPjBpqAfA0JhjK+eQSVzCyWrqpFGz23/1KAhN1hQhGe81hDBjLY7W3QgvBST7iuKU+nkDr60+yhcjD6f59SH5KkSQ==
```

##### 3.3.2.2 Encrypt the message

```php
/* the message */
$message = <<<MESSAGE
Hello world! :)

This is my secret text.
MESSAGE;
$cipher  = 'aes-256-cbc';
$options = OPENSSL_RAW_DATA;

/* encrypt the message */
$encryptedMessage = base64_encode(openssl_encrypt($message, $cipher, hex2bin($key), $options, hex2bin($iv)));
echo $encryptedMessage;
```

The result:

```
4FFWdfqQzuMd/JP3fvpriRC5oajS8ENpCD3ZOxDVBZmWAFPhIkb4iVbWYnWPDNCw
```

##### 3.3.2.3 Combine the RSA ciphertext and AES ciphertext

```php
/* combine the asymmetric and the symmetric part */
$encrypted = base64_encode($encryptedKeyIv."\n\n".$encryptedMessage);
echo $encrypted;
```

With the result:

```
aXJ3c05rdjUvV2pzbG1Pa2k0dVpYTEpGQ0wvYk5hOHRQQXZCaWgram9YaHRmMUtObEZaMXhndUpFQ0dSZ3R3dVYyK3ZOUkhDYTdtWXRzYmZna3FGcGpmamRJWlNZUlg1aDQwODFDUHIyNEdxbW5BOE1UT2VKR0d2Z2kzOXk5Tk9XWUF0K2lHaU1Pc1JGS3dLQ3EydVdmTDJuMXhkcWFHN1o1b1NZV25NVktFNjZDM0dlQm1ycFdUWEgvZGF1MmJ4YmFlM3paTFNpbXJwNExYSHZSWjhwcXdYL2x2MUx6K2tJZW1pY1FQVUp0RzNqSTV0dGI2azhneldpS3daOU1QakJwcUFmQTBKaGpLK2VRU1Z6Q3lXcnFwRkd6MjMvMUtBaE4xaFFoR2U4MWhEQmpMWTdXM1FndkJTVDdpdUtVK25rRHI2MCt5aGNqRDZmNTlTSDVLa1NRPT0KCjRGRldkZnFRenVNZC9KUDNmdnByaVJDNW9halM4RU5wQ0QzWk94RFZCWm1XQUZQaElrYjRpVmJXWW5XUEROQ3c=
```

This combined ciphertext is only decryptable with the private key (private.pem) and can be safely sent over any data network.

#### 3.3.3 Decryption (System B)

##### 3.3.3.1 Extract the asymmetrical and the symmetrical part

```php
/* decrypted the hybrid message: 0 - asymmetric section, 1 - symmetric section */
$decryptedSections = explode("\n\n", base64_decode($encrypted));
print_r($decryptedSections);
```

The expected result is:

```php
Array
(
    [0] => irwsNkv5/WjslmOki4uZXLJFCL/bNa8tPAvBih+joXhtf1KNlFZ1xguJECGRgtwuV2+vNRHCa7mYtsbfgkqFpjfjdIZSYRX5h4081CPr24GqmnA8MTOeJGGvgi39y9NOWYAt+iGiMOsRFKwKCq2uWfL2n1xdqaG7Z5oSYWnMVKE66C3GeBmrpWTXH/dau2bxbae3zZLSimrp4LXHvRZ8pqwX/lv1Lz+kIemicQPUJtG3jI5ttb6k8gzWiKwZ9MPjBpqAfA0JhjK+eQSVzCyWrqpFGz23/1KAhN1hQhGe81hDBjLY7W3QgvBST7iuKU+nkDr60+yhcjD6f59SH5KkSQ==
    [1] => 4FFWdfqQzuMd/JP3fvpriRC5oajS8ENpCD3ZOxDVBZmWAFPhIkb4iVbWYnWPDNCw
)
```

##### 3.3.3.2 Decrypt the key and iv (from asymmetrical part)

```php
/* decrypt the data using the private key */
$privateKey = file_get_contents('id_rsa');
openssl_private_decrypt(base64_decode($decryptedSections[0]), $decrypted, $privateKey);
echo $decrypted;
```

```
71EB7C9E4F6E4B4A1341E4AD519FB22D0BD4A0AF0B8CB77FEA0C6E1F82870B0C:10A8C339AEC170CCBA8D3816785F67F6
```

##### 3.3.3.3 Decrypt the ciphertext (from symmetrical part)

With the iv and the related key:

```php
/* decrypt the message */
$keyIvSections = explode(':', $decrypted);
$message = openssl_decrypt(base64_decode($decryptedSections[1]), $cipher, hex2bin($keyIvSections[0]), $options, hex2bin($keyIvSections[1]));
echo $message;
```

Now we get the unciphered and expected message:

```
Hello world! :)

This is my secret text.
```

## 4. Tools

### 4.1 Check the private key

```console
user@sh$ openssl rsa -in private.pem -check
```

```
RSA key ok
writing RSA key
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAoQcfLo00xicP5oJ8yIclgtVNZBka2ppKfU7MyRJbNpQYIlbJ
BmiFYa2tNitYGF0TaMA3k2Z5omnBat2MEE5U2+ojWBGockrhZa+0h61CrFGuT9tq
DehF7HxP2JGyfiQ3k1M8oxBNcOEATO7lqhHVCEfYXtwA7wnpwZRrG1JYcRyBPLkV
TNWctX0SJ3DpZzrPTJwWEO5vs2+8gxSoa9c40zLWBnNwcCJ0VDMTV2WnTVUFweUX
prg5b3vNtcridQ1/sS0ZCx2UicxpHdt5MatWN30IaMNaaE4YrFCbGwMjpjZ82qcE
qFEh67bFtf/3PDbt6kLfGOp1ajSoYgvZoSBRMQIDAQABAoIBAB+w6SAeRj6hPW3e
THSitG01UY/bqP9Q0kwrD/6akD0DlGRdtB6Av49jwO0iRqo01zcMbWOjDVk7ewdv
JrumzuihAee5Qe+McSO0GtGA9dg4ExhAVHT8O5a5OHWk5v4QXqeuAAcPlE4c2hRK
CAUakVSZ3yl8HurshobEkPfFkwZfh8NizhwknUg0+O8dRK7UcFhQoNHL2UCStMPm
gzZI8nqGpSI+W3gvkCW83uk8r8KNXCuQnSO/Tx6sXwWi4vv5xRGEyuPy5IzAo98R
K2ZrtxTH1DSHyUTVuTyOD39myCTq0OB8V7KT5mMP5IM2ilmRMZCagwLHgyPprlSq
1QF/KGkCgYEA1W0augAPafkKjSLFVxbyztlPLI+mnnEATSjOv32M5KW02B/4HRrr
9kxy3c3idAX3NND1uSPw079DGOcMu7XDp3vW4AS3ivxY+R1bfT67L5rgsjR4NUMB
sTGdxSgASrCKRpcgMFOzBIS8+iQaPXNQXXyB5WgWpEKWpDaJpRKo7OMCgYEAwSY5
YTxJNOcx6VQZGNd2vYwrqfucTz8aBattG4cJphTHZYd1nW9FzvHbqnrLEfL9dZ8v
bLcCkR3AylzG85n/thV2r59FwSdojGP1KGCETnTvrc5u/qDQHUgjxSD5QARDBX28
kwMhLBIZmaZmOwh2jx9uku6BNgitfjBUFb7umdsCgYB72c+LpmNLfOC5nDbmXgPT
M1n1ovrusOaa4BZyGxp6yQpT7OFfinLpv91ch5BlAd09whEGOiwTxMbcGaBTAZyj
gYLlBve36M586aNg39liO78uyrIDPnop6IAEnDznGuFzK1nbkYauFZVQl0i+5j75
sTnz9V5GPfoLGzbvGw/6PwKBgFxbE6rL8dFLD1GbddisBkoCQUqpVgeKi73UR3qX
KmTwoJuKlxGtiDq46SluR7WQc+OPN1ULeT28dVgN3s/SfjQptTOqu+btGg+vKCWj
aQA+5/A6ulYkvP6TZQ84ghY7M3Tnt4iwQWdaTEVtDIsDs/UhuXSmeMBGi/a/0yUG
w/5rAoGAanuaOkWG/4OW0tav6Zin3NPmq6QDsWjquW+MMc16Q8mQ1LlBncz0g1JS
xkfSl+SU5Hlqi5DnqWrfbjCNX+fE932K4UOm3hqdxlrZrU5OJInJR5bv61D6kUEG
eIi743OKU8Q3c/FOY7+v4+VinescMksrkaI37DH1CBTkCejQlts=
-----END RSA PRIVATE KEY-----
```

### 4.2 Check private and public key

```console
user@sh$ diff <(cat id_rsa.pub | grep -v "PUBLIC KEY" | tr -d '\n') <(openssl rsa -pubout -in id_rsa 2>/dev/null | grep -v "PUBLIC KEY" | tr -d '\n') 1>/dev/null && echo 'ok' || echo 'failed'
```

Returns "ok" if the private and public keys match. Returns "failed" if not.

### 4.3 Sign and verify a message

#### 4.3.1 Sign the message (System A)

Create the signature from the given message and the private key "private.pem". The private key in that case is from the message sender:

```console
user@sh$ echo -en "Hello world! :)\n\nThis is my secret text." | openssl dgst -sha256 -sign private.pem | openssl base64
```

It returns

```
EDkjt+1Hwui8eCZeP24K3yO0IuTxVZlNUDaAF4WTWkjSx8jPAoASSANQBtLG25Ss
l2RBgDryW9+HVeD80sevyiUP91VxRs1YmfMWEwoJp+cLR46Gbkrw1q5CfDYssH01
XqnRdIF/053eFN2p0V7jshM+W59B5C4tG3oOh1rQRIFb0ekWEYpj3Y4oeRiDsT5Y
AvGxcozLkkFHKEbwL02nCqksIDSO6EAWMt6uzygOxeEWwF5P7wm0aIAjF7xtoHKk
VaVcacgwqrDSGGmFJuWDKY47ZRNdidh5eNEmwgzZVZWjJWLAFx42Jz94BSafNZwr
dbofMCup1rPoFlz9m4N90Q==
```

You can now save this signature to signature.txt for example.

#### 4.3.1 Verify the signature (System B)

Check if the message authenticates with the public key "public.pem" from the message sender:

```console
user@sh$ echo -en "Hello world! :)\n\nThis is my secret text." | openssl dgst -sha256 -verify public.pem -signature <(openssl base64 -d -in signature.txt)
```

If the verification succeeds you will see:

```
Verified OK
```

Otherwise:

```
Verification Failure
```

## A. Authors

* Björn Hempel <bjoern@hempel.li> - _Initial work_ - [https://github.com/bjoern-hempel](https://github.com/bjoern-hempel)

## B. License

This tutorial is licensed under the MIT License - see the [LICENSE](/LICENSE) file for details


