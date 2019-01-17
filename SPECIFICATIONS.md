```
 __          __        _       _                                                  
 \ \        / /       | |     (_)                                                 
  \ \  /\  / /__  _ __| | __   _ _ __     _ __  _ __ ___   __ _ _ __ ___  ___ ___ 
   \ \/  \/ / _ \| '__| |/ /  | | '_ \   | '_ \| '__/ _ \ / _` | '__/ _ \/ __/ __|
    \  /\  / (_) | |  |   <   | | | | |  | |_) | | | (_) | (_| | | |  __/\__ \__ \
     \/  \/ \___/|_|  |_|\_\  |_|_| |_|  | .__/|_|  \___/ \__, |_|  \___||___/___/
                                         | |               __/ |                  
                                         |_|              |___/                   
```

# Specification for CommonSecrets

## Common things

There are three different types that are supported. Integers (signed), [UTF-8](https://en.wikipedia.org/wiki/UTF-8) strings for text and [base64](https://en.wikipedia.org/wiki/Base64) encoded byte arrays for binary data.

## File extension

CommonSecret file should have file extension chain that explains how it should be opened. e.g. *foods.commonsecret.xml* would mean that CommonSecret is stored to XML format, and *fruits.commonsecret.json.png* would mean that CommonSecret is stored to JSON which is then stored to PNG image file.

## Mandatory parts

### Version number

This **MUST** be first element (and this is only element where order matters). Contains an integer that tells what CommonSecret version this file uses. Currently there is only version 1.

## Data parts

### Key derivation functions (KDF)

List of text objects that define key derivation functions. There can be multiple Key derivation functions defined in one CommonSecret file.

#### KDF Algorithms

Only [PBKDF2](https://en.wikipedia.org/wiki/PBKDF2) is supported, with **HMAC-SHA256** and **HMAC-SHA512** 

##### PBKDF2 options

###### Salt

Base64 encoded salt, decoded content should be 16 bytes (128 bits)

###### Iterations

Integer that tells how many iterations have to be done. Minimum value is 1, recommended is

#### Identifier

Identifier of KDF, used to pair KDF and Symmetric-key algorithm. Base64 encoded UTF-8 string. SHOULD be unique, so every KDF in a file should have unique identifer.

### Login information

Login information. Every varianble MUST be included even if they are empty

#### Title

Base64 encoded UTF-8 string

#### Address / URL

Base64 encoded UTF-8 string

#### Username

Base64 encoded UTF-8 string

#### Password

Base64 encoded UTF-8 string

#### Notes

Base64 encoded UTF-8 string

#### Creation time

Integer, [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds

#### Modification time

Integer, [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds

#### Icon

Base64 encoded byte array that contains either [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics) or [JPEG](https://en.wikipedia.org/wiki/JPEG) image file as logo

#### Category

Base64 encoded UTF-8 string

#### Tags

Base64 encoded UTF-8 string that contains tab separated tag entries

#### Symmetric-key algorithms

Two encryption algorithms are supported, they are [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) (CTR) and [ChaCha20](https://en.wikipedia.org/wiki/Salsa20#ChaCha_variant).


