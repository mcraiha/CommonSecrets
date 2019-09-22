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

**Table of Contents**

| Section        | Description | Link |
| ------------- |:-------------:| -----:|
| Common things    | Common definitions | [Common things](#Common-things) |
| File extensions  | How file extensions should work | [File extensions](#File-extensions) |
| Mandatory parts | What entries every file must have | [Mandatory parts](#Mandatory-parts) |
| Key derivation functions (KDF) | Definition of available KDF options | [Key derivation functions (KDF)](#Key-derivation-functions-(KDF)) |
| Key and value pairs | Definition of key and value pairs of AUDALT | [Key and value pairs](#Key-and-value-pairs)


## Common things

There are three different variable types that are supported. Integers (signed), [UTF-8](https://en.wikipedia.org/wiki/UTF-8) strings for text and [base64](https://en.wikipedia.org/wiki/Base64) encoded byte arrays for binary data.

## File extensions

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

Base64 encoded UTF-8 string as identifier of KDF, used to pair KDF and Symmetric-key algorithm. SHOULD be unique, so every KDF in a file should have unique identifer.

&nbsp;

### Login informations

Login information (plaintext ones). Every variable MUST be included even if they are empty.

#### Title

Base64 encoded UTF-8 string, used to identify entries (doesn't need to unique)

#### Address / URL

Base64 encoded UTF-8 string, might contain e.g. HTTPS URL

#### Username

Base64 encoded UTF-8 string

#### Password

Base64 encoded UTF-8 string

#### Notes

Base64 encoded UTF-8 string, additional notes for this entry

#### Creation time

Integer, [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds

#### Modification time

Integer, [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds

#### Icon

Base64 encoded byte array that contains either [SVG](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics) or [JPEG](https://en.wikipedia.org/wiki/JPEG) image file as logo

#### Category

Base64 encoded UTF-8 string

#### Tags

Base64 encoded UTF-8 string that contains tab (**\t**) separated tag entries

#### Checksum

UTF-8 string (can only contain hex chars, so numbers 0-9 and letters A-F) that contain SHA-256 checksum of all other login information variables concatenated together

&nbsp;

### Login informations (secret)

Encrypted entries, each entry MUST contain following:

#### Key identifier

Base64 encoded UTF-8 string Key identifier is used to pair one KDF entry to this login information

#### Algorithm

See [Symmetric-key algorithms](Symmetric-key-algorithms)

#### Data

Base64 encoded byte array that contains encrypted [AUDALF](https://github.com/mcraiha/AUDALF) bytes. AUDALF contains following entries:

##### Title

UTF-8 string, used to identify entries (doesn't need to unique)

##### Address / URL

UTF-8 string, might contain e.g. HTTPS URL

##### Username

UTF-8 string

##### Password

UTF-8 string

##### Notes

UTF-8 string, additional notes for this entry

##### Creation time

64 bit unsigned integer, Unix time in seconds (see type ID **117440513** in AUDALF specifications)

##### Modification time

64 bit unsigned integer, Unix time in seconds (see type ID **117440513** in AUDALF specifications)

##### Icon

Byte array that contains either [SVG](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics) or [JPEG](https://en.wikipedia.org/wiki/JPEG) image file as logo

##### Category

UTF-8 string

##### Tags

UTF-8 string that contains tab (**\t**) separated tag entries

#### Checksum

UTF-8 string (can only contain hex chars, so numbers 0-9 and letters A-F) that contain SHA-256 checksum of all other login information secret variables concatenated together

&nbsp;

### Symmetric-key algorithms

Two encryption algorithms are supported, they are [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) (CTR) and [ChaCha20](https://en.wikipedia.org/wiki/Salsa20#ChaCha_variant).

#### AES (CTR)

Name is **AES-CTR**

Following values must be included

##### Key size

Integer, valid values are 128, 192 or 256 (bits)

##### Initial counter

Base64 encoded byte array that contains 128 bits of nonce used to init AES-CTR

#### ChaCha20

Name is **ChaCha20**

Following values must be included

##### Key size

Valid integer value is 256 (bits)

##### Nonce

Base64 encoded byte array that contains 96 bits of nonce used to init ChaCha20

##### Counter

Integer value that contains counter that is used to init ChaCha20

&nbsp;


### Notes

Can contain multiple note entries which are in following format:

#### Note text

Base64 encoded UTF-8 string that contains the content of note

#### Creation time

Integer, [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds

#### Modification time

Integer, [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds

#### Checksum

UTF-8 string (can only contain hex chars, so numbers 0-9 and letters A-F) that contain SHA-256 checksum of note

&nbsp;

&nbsp;


### Notes (secret)

Can contain multiple note entries which are in following format:

&nbsp;

#### Key identifier

Base64 encoded UTF-8 string, is used to pair one KDF entry to this note

#### Algorithm

See [Symmetric-key algorithms](Symmetric-key-algorithms)

#### Data

Base64 encoded byte array that contains encrypted [AUDALF](https://github.com/mcraiha/AUDALF) bytes. AUDALF contains following entries:

##### Note text

UTF-8 string

##### Creation time

64 bit unsigned integer, Unix time in seconds (see type ID **117440513** in AUDALF specifications)

##### Modification time

64 bit unsigned integer, Unix time in seconds (see type ID **117440513** in AUDALF specifications)

&nbsp;

#### Checksum

Base64 encoded UTF-8 string that contain SHA-256 checksum of note data