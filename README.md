# JS RSA Encryption

by [Ivo Moor](mailto: ivo.moor@just-bi.nl)

## Index

1. [Description](#description)
2. [Prerequisites](#prerequisites)
3. [Installation](#installation)
4. [Usage](#usage)


## <a name="description"></a>Description

This repository contains a JavaScript library that allows the encryption
of files using both the AES and RSA algorithms. The library only
provides the functions for encrypting data  The decryption of the data 
is not part of this application (yet), but is possible in iOS via linked 
project [cordova-plugin-rsacertificate](https://github.com/just-bi/cordova-plugin-rsacertificate).

The encryption steps executed via the JS library includes the following:
- Take a text string
- Generate a random password (16 characters), called the secret key
- Generate another random password (16 characters), called the initialization vector
- Use AES encryption with the secret key and initialization vector to encrypt the text string
- Ask the user for a PEM-file, which is the public key of a RSA certificate (see usage for more details)
- Use RSA encryption with the PEM file to encrypt a concatenation of the secret key and the initialization vector
- Combine the RSA encrypted AES secret key and initialization vector (as key) with the AES encrypted text string (as text) into a JSON file

See the 'Usage' section to find out how the library can be used. Alternatively you can download the contents of folder "demo_app" to run the demo application.


## <a name="prerequisites"></a>Prerequisites

- [jQuery library](https://jquery.com/)<br>
  The jQuery library is used to create promisses
<br><br>
- [CryptoJS library](https://github.com/gwjjeff/cryptojs)<br>
  The AES encryption in JavaScript requires the CryptoJS library which is also included in teh demo_app folder.
<br><br>
- RSA Key Pair<br>
  In order to encrypt text using the RSA algorithm, a public key is required. Information about generating a RSA key pair is explained in
  detail in related repo [Cordova RSA Certificate](https://github.com/just-bi/cordova-plugin-certificate).
<br><br>
- WebCrypto API<br>
  The RSA encryption is done via the browsers WebCrypto API. This is
  quite new and not supported in older browsers. Please check if your
  browser supports this API via [caniuse.com](http://caniuse.com/#feat=cryptography).


## <a name="installation"></a>Installation
In order to make use of the JS Library, you will need to:
- copy the files inside folder "demo_app/js/" into your web application
- import the files into your web application via the <head> tag:
  ```js
    <script src="js/jquery/jquery.min.js"></script>
    <script src="js/crypto-js/Crypto.js"></script>
    <script src="js/crypto-js/AES.js"></script>
    <script src="js/crypto-js/BlockModes.js"></script>
    <script src="js/jbi_encryption.js"></script>
  ```
  


## <a name="usage"></a>Usage
The JavaScript library has one method that allows you to do the encryption:
```js
  justbi.encryption.rsa.encryptText(plainText, rsaPublicKey).then(
    function (encryptedText) {
      console.log(encryptedText)
    },
    function (err) {
      console.error("Whoooops: " + err)
    }
  );
```

A demo application that shows how a text string can be encrypted using a RSA public key (PEM) can be downloaded from the "demo_app" folder.