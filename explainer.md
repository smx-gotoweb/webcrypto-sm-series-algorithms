# SM series Algorithms in WebCrypto

## Problem Statement
The Web Crypto API is an interface allowing a script to use cryptographic primitives in order to build systems using cryptography, it now supports regular internal algorithms like RSA, SHA, AES, etc. Now the SM series algorithms are accepted by ISO/IEC. also the SM series algorithm is applied in the financial field. For example, the website of “Bank of China”(https://ebssec.boc.cn/boc15/login.html), provides HTTPS access that supporting SM series algorithm. so we may use those algorithms on the web applications. 



## Support SM series algorithms in the Web Cryptography API

We propose to solve the above problem by adding support for SM series algorithms in the
Web Cryptography API, containing at least SM2 , SM3 and SM4.

### SM2

The following operations are supported with the recognized algorithm name
"SM2":

1. generateKey
2. sign
3. verify

### SM3

The following operations are supported with the recognized algorithm name
"SM3":

1. digest


### SM4-CBC

The following operations are supported with the recognized algorithm name
"SM4-CBC":

1. generateKey
2. encrypt
3. decrypt

## Algorithm dictionary object
Similar to `AesKeyGenParams` in WebCrypto API,we need to add  `Sm2KeyGenParams` and `Sm4KeyGenParams`
dictionary.The `Sm2KeyGenParams` dictionary  represents the object that should be passed as the `algorithm` parameter into `SubtleCrypto.generateKey()`, when generating any SM2-256 curve-based key pair. The `Sm4KeyGenParams` dictionary represents the object that should be passed as the algorithm parameter into `SubtleCrypto.generateKey()`, when generating an SM4-CBC key.
Also，similar to `AesCbcParams` in WebCrypto API , we need to add an object named `Sm4CbcParams` dictionary. It represents the object that should be passed as the algorithm parameter into `crypto.subtle.encrypt(), crypto.subtle.decrypt()`, when using the SM4-CBC algorithm.

### Sm2KeyGenParams
```
Properties
name
  A [DOMString]. This should be set to `SM2`, depending on the algorithm you want to use.
```

### Sm4KeyGenParams
```
Properties
name
  A DOMString. This should be set to `SM4-CBC`, depending on the algorithm you want to use.
length
  A Number — the length in bits of the key to generate. This must be one of: 128, 192, or 256.
```
### Sm4CbcParams
```
Properties
name
  A DOMString. This should be set to `SM4-CBC`, depending on the algorithm you want to use.
iv
  A BufferSource.The initialization vector. Must be 16 bytes, unpredictable, and preferably     cryptographically random. However, it need not be secret (for example, it may be transmitted   unencrypted along with the ciphertext).
```

## Code Examples

### SM Key generation


```js
//1. SM2 Key generation
//Use a string of the recognized algorithm name.
const sm2_key = await window.crypto.subtle.generateKey(
 'SM2',true /* extractable */,['sign', 'verify']);
// Or use Sm2KeyGenParams dictionary with its Properties.
const sm2_key = await window.crypto.subtle.generateKey(
  {name: 'SM2'}, true /* extractable */, ['sign', 'verify']);

//2. SM4 Key generation
//Use Sm4KeyGenParams dictionary with its Properties.
const sm4_key = crypto.subtle.generateKey(
{name: "SM4-CBC",length: 256},true/* extractable */,["encrypt", "decrypt"]);
```

### Digital signature with SM2

```js
// |data| is to be signed.
// The digital signature parameter has only the name property:
//   name, a string that should be set to 'SM2'.
const alg = {name: 'SM2'};
window.crypto.subtle.sign(alg, sm2_key.privateKey, data).then(signature =>
  window.crypto.subtle.verify(alg, sm2_key.publicKey, signature, data))
```

### Digest with SM3
```js
// |data| is to be digested.
const hashBuffer = await crypto.subtle.digest('SM3', data);
```

### Encrypt and Decrypt with SM4

```js
//Use sm4_key with Sm4CbcParams dictionary to encrypt and decrypt.
ciphertext = crypto.subtle.encrypt(
 {name: "SM4-CBC",iv: iv},sm4_key,plaintext);

decrypted = crypto.subtle.decrypt(
 {name: "SM4-CBC",iv: iv},sm4_key,ciphertext);
```

## Reference
1. [ISO-SM3] International Organization for Standardization, "IT Security techniques -- Hash-functions -- Part 3: Dedicated hash-functions", ISO ISO/IEC 10118-3:2018, October 2018.
2. [ISO-SM2/SM9] International Organization for Standardization, "IT Security techniques -- Digital signatures with appendix -- Part 3: Discrete logarithm based mechanisms", ISO ISO/IEC 14888-3:2018, November 2018.
3. [ISO-SM4] International Organization for Standardization, "IT Security techniques -- Encryption algorithms -- Part 3: Block ciphers", ISO ISO/IEC 18038-3:2010, December 2010.
[ISO-SM3]:  https://www.iso.org/standard/67116.html
[ISO-SM2/SM9]:  https://www.iso.org/standard/76382.html
[ISO-SM4]:  https://www.iso.org/standard/54531.html
[WebCrypto API]:  https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto
                            https://www.w3.org/TR/WebCryptoAPI

