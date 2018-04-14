# A tutorial to securely transfer messages

This is a tutorial to securely transfer messages from a to b with various coding languages.

## 0. Contents

* [1. Preliminary considerations](#user-content-1-preliminary-considerations)
  * [1.1 Unciphered message transfer](#user-content-11-unciphered-message-transfer)
    * [1.1.1 Unciphered transfer](#user-content-111-unciphered-transfer)
  * [1.2 Ciphered message transfer](#user-content-12-ciphered-message-transfer)
    * [1.2.1 Symmetric cryptography](#user-content-121-symmetric-cryptography)
    * [1.2.2 Asymmetric cryptography](#user-content-122-asymmetric-cryptography)
    * [1.2.3 Hybrid cryptography](#user-content-123-hybrid-cryptography)
* [2. Implementations](#user-content-2-implementations)
  * [2.1 Bash](#user-content-21-bash)
  * [2.2 Javascript](#user-content-22-javascript)
  * [2.3 PHP](#user-content-23-php)

## 1. Preliminary considerations

### 1.1 Unciphered message transfer

#### 1.1.1 Unciphered transfer

##### 1.1.1.1 Advantages

##### 1.1.1.2 Disadvantage

### 1.2 Ciphered message transfer

#### 1.2.1 Symmetric cryptography

##### 1.2.1.1 Advantages

##### 1.2.1.2 Disadvantage

#### 1.2.2 Asymmetrical cryptography

##### 1.2.2.1 Advantages

##### 1.2.2.2 Disadvantage

#### 1.2.3 Hybrid cryptography

##### 1.2.3.1 Advantages

##### 1.2.3.2 Disadvantage

## 2. Implementations

### 2.0 Building public and private key

#### Bash example

Private key: private.pem

Public key: public.pem

```
user$ openssl genpkey -algorithm RSA -out private.pem -pkeyopt rsa_keygen_bits:2048
user$ openssl rsa -pubout -in private.pem -out public.pem
```

##### Example public.pem

```
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

##### Example private.pem

```
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

### 2.1 Bash

#### 2.1.1 Encryption

#### 2.1.2 Decryption

### 2.2 Javascript

#### 2.2.1 Encryption

#### 2.2.2 Decryption

### 2.3 PHP

#### 2.3.1 Encryption

#### 2.3.2 Decryption
