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
| Login informations | Definition of login informations | [Login informations](#Login-informations)
| Login informations (secret / encrypted) |  Definition of login informations (secret / encrypted) | [Login informations (secret / encrypted)](#Login-informations-(secret-/-encrypted))
| Note entries | Definition of Note entries | [Note entries](#Note-entries)
| Note entries (secret / encrypted) | Definition of Note entries (secret / encrypted) | [Note entries (secret / encrypted)](#Note-entries-(secret-/-encrypted))
| File entries | Definition of File entries | [File entries](#File-entries)
| File entries (secret / encrypted) | Definition of File entries (secret / encrypted) | [File entries (secret / encrypted)](#File-entries-(secret-/-encrypted))
| Contact informations | Definition of contact informations | [Contact informations](#Contact-informations)
| Contact informations (secret / encrypted) | Definition of contact informations (secret / encrypted) | [Contact informations (secret / encrypted)](#Contact-informations-(secret-/-encrypted))
| Payment cards | Definition of payment cards | [Payment cards](#Payment-cards)
| Payment cards (secret / encrypted) |  Definition of payment cards (secret / encrypted) | [Payment cards (secret / encrypted)](#Payment-cards-(secret-/-encrypted))

## Common things

There are three different variable types that are supported. Integers (signed), [UTF-8](https://en.wikipedia.org/wiki/UTF-8) strings for text and [base64](https://en.wikipedia.org/wiki/Base64) encoded byte arrays for binary data or text.

Basically all hardcoded strings (e.g. enum likes) are stored as UTF-8. Anything that user can input (e.g. URL) is stored as base64 encoded byte array (so UTF-8 string is converted to bytes and then base64 encoded). This decision is made in name of interoperability (so one can e.g. copy values from JSON to XML and everything should just work).

## File extensions

CommonSecrets file should have file extension chain that explains how it should be opened. e.g. *foods.commonsecrets.xml* would mean that CommonSecrets is stored to XML format, and *fruits.commonsecrets.json.png* would mean that CommonSecrets is stored to JSON which is then stored to PNG image file.

## Mandatory parts

### Version number

This **MUST** be first element (and this is only element where order matters). It is first element because it is easier to check file formats when needed information is as early as possible. 

Version number is an integer that tells what CommonSecrets version this file uses. Currently there is only version **1**.

## Data parts

### Key derivation functions (KDF)

List of text objects that define key derivation functions. There can be multiple Key derivation functions defined in one CommonSecrets file.

When derived key is used for encrypting/decrypting data, only needed bytes MUST be used. e.g. HMAC-SHA512 will provide 64 bytes, but ChaCha20 will only use first 32 bytes.

| Type    | Bytes as hex |
| -------- | ------- |
| HMAC-SHA512 example output | `9d55fd1b69cd6a28cb4500c0873c5d9f2efb937e4be8016befb30b927bec0091dc040107379fd7f34f0270c6d2aca4091d2b64f3b0879c056baeb10159d49c15` |
| ChaCha20 cipher key | `9d55fd1b69cd6a28cb4500c0873c5d9f2efb937e4be8016befb30b927bec0091` |
| CTR-AES256 cipher key | `9d55fd1b69cd6a28cb4500c0873c5d9f2efb937e4be8016befb30b927bec0091` |
| CTR-AES192 cipher key | `9d55fd1b69cd6a28cb4500c0873c5d9f2efb937e4be8016b` |
| CTR-AES128 cipher key | `9d55fd1b69cd6a28cb4500c0873c5d9f` |


#### KDF Algorithms

Only [PBKDF2](https://en.wikipedia.org/wiki/PBKDF2) is supported, with **HMAC-SHA256** and **HMAC-SHA512** as pseudo-random functions.

##### PBKDF2 options

###### Salt

Base64 encoded salt, decoded content should be 16 bytes (128 bits)

###### Iterations

Integer that tells how many iterations have to be done. Minimum value is 1, recommended is something over 100 000 and the maximum is 2 147 483 647.

#### Identifier

Base64 encoded UTF-8 string as identifier of KDF, used to pair KDF and Symmetric-key algorithm. SHOULD be unique, so every KDF in a file should have unique identifer.

---  


### Login informations

Login information (plaintext ones). Every variable MUST be included even if they are empty.

#### Title

Base64 encoded UTF-8 string, used to identify entries (doesn't need to be unique)

#### Address / URL

Base64 encoded UTF-8 string, might contain e.g. HTTPS URL

#### Email

Base64 encoded UTF-8 string

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

UTF-8 string (can only contain hex chars, so numbers 0-9 and letters A-F) that contain SHA-256 checksum of all other login information variables concatenated together. Integer variables are first turn into little-endian byte arrays.

---


### Login informations (secret / encrypted)

Encrypted entries, each entry MUST contain following:

#### Key identifier

Base64 encoded UTF-8 string Key identifier is used to pair one KDF entry to this login information

#### Algorithm

See [Symmetric-key algorithms](Symmetric-key-algorithms)

#### Data

Base64 encoded byte array that contains encrypted [AUDALF](https://github.com/mcraiha/AUDALF) bytes. AUDALF contains following entries:

##### Title

UTF-8 string, used to identify entries (doesn't need to be unique)

##### Address / URL

UTF-8 string, might contain e.g. HTTPS URL

##### Email

UTF-8 string

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

---


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

---


### Note entries

Can contain multiple note entries which are in following format:

#### Note title

Base64 encoded UTF-8 string that contains the title of note

#### Note text

Base64 encoded UTF-8 string that contains the content of note

#### Creation time

Integer, [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds

#### Modification time

Integer, [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds

#### Checksum

UTF-8 string (can only contain hex chars, so numbers 0-9 and letters A-F) that contain SHA-256 checksum of note. Integer variables are first turn into little-endian byte arrays.

---


### Note entries (secret / encrypted)

Can contain multiple note secret entries which are in following format:


#### Key identifier

Base64 encoded UTF-8 string, is used to pair one KDF entry to this note secret

#### Algorithm

See [Symmetric-key algorithms](Symmetric-key-algorithms)

#### Data

Base64 encoded byte array that contains encrypted [AUDALF](https://github.com/mcraiha/AUDALF) bytes. AUDALF contains following entries:

##### Note title

UTF-8 string that contains the title of note

##### Note text

UTF-8 string that contains the content of note

##### Creation time

64 bit unsigned integer, Unix time in seconds (see type ID **117440513** in AUDALF specifications)

##### Modification time

64 bit unsigned integer, Unix time in seconds (see type ID **117440513** in AUDALF specifications)


#### Checksum

UTF-8 string (can only contain hex chars, so numbers 0-9 and letters A-F) that contain SHA-256 checksum of all other note secret variables concatenated together

---


### File entries

Can contain multiple file entries which are in following format:

#### File name

Base64 encoded UTF-8 string that contains the name of the file

#### File content

Base64 encoded byte array that contains the content of file

#### Creation time

Integer, [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds

#### Modification time

Integer, [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds

#### Checksum

UTF-8 string (can only contain hex chars, so numbers 0-9 and letters A-F) that contain SHA-256 checksum of file entry variables concatenated together. Integer variables are first turn into little-endian byte arrays.

---


### File entries (secret / encrypted)

Can contain multiple file entries which are in following format:


#### Key identifier

Base64 encoded UTF-8 string, is used to pair one KDF entry to this file entry

#### Algorithm

See [Symmetric-key algorithms](Symmetric-key-algorithms)

#### Data

Base64 encoded byte array that contains encrypted [AUDALF](https://github.com/mcraiha/AUDALF) bytes. AUDALF contains following entries:

##### File name

UTF-8 string that contains the file name

##### File content

Byte array that contains the file content

##### Creation time

64 bit unsigned integer, Unix time in seconds (see type ID **117440513** in AUDALF specifications)

##### Modification time

64 bit unsigned integer, Unix time in seconds (see type ID **117440513** in AUDALF specifications)


#### Checksum

UTF-8 string (can only contain hex chars, so numbers 0-9 and letters A-F) that contain SHA-256 checksum of all other file entry secret variables concatenated together

---


### Contact informations

Can contain multiple contact informations which are in following format:

#### First name

Base64 encoded UTF-8 string that contains first name of the contact

#### Last name

Base64 encoded UTF-8 string that contains last name of the contact

#### Middle name

Base64 encoded UTF-8 string that contains middle name of the contact

#### Name prefix

Base64 encoded UTF-8 string that contains name prefix of the contact

#### Name suffix

Base64 encoded UTF-8 string that contains name suffix of the contact

#### Nickname

Base64 encoded UTF-8 string that contains nickname of the contact

#### Company

Base64 encoded UTF-8 string that contains company of the contact

#### Job title

Base64 encoded UTF-8 string that contains job title of the contact

#### Department

Base64 encoded UTF-8 string that contains department of the contact

#### Emails

Base64 encoded UTF-8 string that contains tab (**\t**) separated email entries. Amount MUST match Email descriptions entries

#### Email descriptions

Base64 encoded UTF-8 string that contains tab (**\t**) separated email description entries. Amount MUST match Email entries

#### Phone numbers

Base64 encoded UTF-8 string that contains tab (**\t**) separated phone number entries. Amount MUST match Phone number descriptions entries

#### Phone number descriptions

Base64 encoded UTF-8 string that contains tab (**\t**) separated phone number description entries. Amount MUST match phone number entries

#### Country

Base64 encoded UTF-8 string that contains country

#### Street address

Base64 encoded UTF-8 string that contains street address

#### Street address additional

Base64 encoded UTF-8 string that contains additional street address info

#### Postal code

Base64 encoded UTF-8 string that contains postal code

#### City

Base64 encoded UTF-8 string that contains city

#### PO Box

Base64 encoded UTF-8 string that contains PO Box

#### Birthday

Base64 encoded UTF-8 string that contains birthday

#### Websites

Base64 encoded UTF-8 string that contains tab (**\t**) separated website address entries

#### Relationship

Base64 encoded UTF-8 string that contains relationship

#### Notes

Base64 encoded UTF-8 string, additional notes for this contact

#### Creation time

Integer, [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds

#### Modification time

Integer, [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds

#### Checksum

UTF-8 string (can only contain hex chars, so numbers 0-9 and letters A-F) that contain SHA-256 checksum of contact information variables concatenated together. Integer variables are first turn into little-endian byte arrays

---

### Contact informations (secret / encrypted)

Can contain multiple encrypted Contact informations which are in following format:


#### Key identifier

Base64 encoded UTF-8 string, is used to pair one KDF entry to this Contact information secret

#### Algorithm

See [Symmetric-key algorithms](Symmetric-key-algorithms)

#### Data

Base64 encoded byte array that contains encrypted [AUDALF](https://github.com/mcraiha/AUDALF) bytes. AUDALF contains following entries:

##### First name

UTF-8 string that contains first name of the contact

##### Last name

UTF-8 string that contains last name of the contact

##### Middle name

UTF-8 string that contains middle name of the contact

##### Name prefix

UTF-8 string that contains name prefix of the contact

##### Name suffix

UTF-8 string that contains name suffix of the contact

##### Nickname

UTF-8 string that contains nickname of the contact

##### Company

UTF-8 string that contains company of the contact

##### Job title

UTF-8 string that contains job title of the contact

##### Department

UTF-8 string that contains department of the contact

##### Emails

UTF-8 string that contains tab (**\t**) separated email entries. Amount MUST match Email descriptions entries

##### Email descriptions

UTF-8 string that contains tab (**\t**) separated email description entries. Amount MUST match Email entries

##### Phone numbers

UTF-8 string that contains tab (**\t**) separated phone number entries. Amount MUST match Phone number descriptions entries

##### Phone number descriptions

UTF-8 string that contains tab (**\t**) separated phone number description entries. Amount MUST match phone number entries

##### Country

UTF-8 string that contains country

##### Street address

UTF-8 string that contains street address

##### Street address additional

UTF-8 string that contains additional street address info

##### Postal code

UTF-8 string that contains postal code

##### City

UTF-8 string that contains city

##### PO Box

UTF-8 string that contains PO Box

##### Birthday

UTF-8 string that contains birthday

##### Websites

UTF-8 string that contains tab (**\t**) separated website address entries

##### Relationship

UTF-8 string that contains relationship

##### Notes

UTF-8 string, additional notes for this contact

##### Creation time

64 bit unsigned integer, Unix time in seconds (see type ID **117440513** in AUDALF specifications)

##### Modification time

64 bit unsigned integer, Unix time in seconds (see type ID **117440513** in AUDALF specifications)

#### Checksum

UTF-8 string (can only contain hex chars, so numbers 0-9 and letters A-F) that contain SHA-256 checksum of contact information variables concatenated together. Integer variables are first turn into little-endian byte arrays

---


### Payment cards

Can contain multiple file payment cards which are in following format:

#### Title

Base64 encoded UTF-8 string, used to identify entries (doesn't need to be unique)

#### Name on card

Base64 encoded UTF-8 string, name displayed on payment card

#### Card type

Base64 encoded UTF-8 string, card type (usually either Credit or Debit)

#### Number

Base64 encoded UTF-8 string, number on the card

#### Security code

Base64 encoded UTF-8 string, security code on the card

#### Start date

Base64 encoded UTF-8 string, first valid date of the card (usually month / year)

#### Expiration date

Base64 encoded UTF-8 string, expiration date of the card (usually month / year)

#### Notes

Base64 encoded UTF-8 string, additional notes for this payment card

#### Creation time

Integer, [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds

#### Modification time

Integer, [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds

#### Checksum

UTF-8 string (can only contain hex chars, so numbers 0-9 and letters A-F) that contain SHA-256 checksum of contact information variables concatenated together. Integer variables are first turn into little-endian byte arrays

---

### Payment cards (secret / encrypted)

Can contain multiple encrypted payment cards which are in following format:


#### Key identifier

Base64 encoded UTF-8 string, is used to pair one KDF entry to this payment card secret

#### Algorithm

See [Symmetric-key algorithms](Symmetric-key-algorithms)

#### Data

Base64 encoded byte array that contains encrypted [AUDALF](https://github.com/mcraiha/AUDALF) bytes. AUDALF contains following entries:

##### Title

UTF-8 string, used to identify entries (doesn't need to be unique)

##### Name on card

UTF-8 string, name displayed on payment card

##### Card type

UTF-8 string, card type (usually either Credit or Debit)

##### Number

UTF-8 string, number on the card

##### Security code

UTF-8 string, security code on the card

##### Start date

UTF-8 string, first valid date of the card (usually month / year)

##### Expiration date

UTF-8 string, expiration date of the card (usually month / year)

##### Notes

UTF-8 string, additional notes for this payment card

##### Creation time

64 bit unsigned integer, Unix time in seconds (see type ID **117440513** in AUDALF specifications)

##### Modification time

64 bit unsigned integer, Unix time in seconds (see type ID **117440513** in AUDALF specifications)


#### Checksum

UTF-8 string (can only contain hex chars, so numbers 0-9 and letters A-F) that contain SHA-256 checksum of all other payment card secret variables concatenated together