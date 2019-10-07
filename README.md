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

# CommonSecrets

CommonSecrets is specification for storing encrypted and plaintext login information (username, password, URL etc.), notes and files.

## Why?

Because I needed something like this for my personal project.

## Key features

* Can use any data-interchange format (JSON, XML, YAML etc.)
* Limited selection of supported encryption, key generation and checksum algorithms 
* Easy to parse without any special libraries

## Algorithms

* For [key derivation functions](https://en.wikipedia.org/wiki/Key_derivation_function) only [PBKDF2](https://en.wikipedia.org/wiki/PBKDF2)
* For [symmetric-key algorithms](https://en.wikipedia.org/wiki/Symmetric-key_algorithm) options are [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) (CTR) and [ChaCha20](https://en.wikipedia.org/wiki/Salsa20#ChaCha_variant)
* For [checksums](https://en.wikipedia.org/wiki/Checksum) only [SHA256](https://en.wikipedia.org/wiki/SHA-2)

## Why were certain algorithms chosen?

I tried to make this easy to implement in many programming languages and environments. Main target was [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API/Supported_algorithms).

## Implementations

C# implementation will come later

## What are the negative traits?

Since most of info/data is text-based, CommonSecrets isn't ideal storage space wise. And because [AUDALF](https://github.com/mcraiha/AUDALF) is used to store encrypted info, some other limitations apply.

## License

Specifications are licensed under [Unlicense](LICENSE), so you might use these specs as you want.

## Sample JSON

```json
{
  "version": 1,
  "keyDerivationFunctionEntries": [
    {
      "algorithm": "PBKDF2",
      "pseudorandomFunction": "HMACSHA256",
      "salt": "gb6BdxgjL8cQlj5O4FojdQ==",
      "iterations": 101295,
      "derivedKeyLengthInBytes": 32,
      "keyIdentifier": "ZG9lcyBub3QgbWF0dGVy",
      "checksum": "EC4D3489D350C85C9A25B7FF66EAE6C8B72B95ECD92671C2B474976CA95AB102"
    }
  ],
  "loginInformations": [
    {
      "title": "dDVkYXBzYzAua3Yy",
      "url": "aHR0cHM6Ly9uNTF1djJ3eS4ybTA=",
      "username": "NW5xY2did2cubWpq",
      "password": "c2Izem1penQuaWNt",
      "notes": "",
      "creationTime": 1570475222,
      "modificationTime": 1570475222,
      "icon": "",
      "category": "",
      "tags": "",
      "checksum": "69F5BAA3209801E2BE59372A8874889838500775B7F8BC0D7AB9075A69F22C35"
    }
  ],
  "loginInformationSecrets": [
    {
      "keyIdentifier": "ZG9lcyBub3QgbWF0dGVy",
      "audalfData": "mUVWkbudtc1GFZvmqSlKazm9ZjWp694WdUAroALTj5co+uyhXbBlGgDfi1LGULjxhOfUnUGVVzz1D+uwfaxkjcOa+zREFXRYnJqM8J8a4JX7UFSc6LkQnkJJ4MIrDwpEP5Yk5Njbx24l0jhN8ETFqNgWK14+rmHy3KIKRf+ofMRoSyV9ZwLdJyD/a0LohcwRwTzKxK/58khDPx1RnRCXTeJwtae7BDxorLyNnkFvIjEvmYtI4fuCCzsUPJZbpTKX8r9eoYebIxNi3MX5LR60/a/+hOOEgINI807uU6L18p/xFXVfPwDT9NbUZgLlNaAFQidQz6Hs4ic4wVu1iQzAQlydTgWdtYzVZV8X/tkGhEv7LGfSxQjM7yzBZEk9jkFK48VvMX3Mgo3u6FTPJtwsULeuy221AP/P+UwU2+F9BfuOpgOrsu+xkPCNWmULgjk/QYFNQn9XWfAG93n3uasj0yQURdQgm/r0gOF+Trc6v1jJwfGY1M+2QFvNvZvdxB0jQA5y1Tsn+Fy75FmcRHDlk4jTiRvYYiXnYoBdZeDHJdsJEszPh/o+2JfleWknGxJddR8Cr0SLkIckvD5t2Xd0QV5MztWbQYV8JAD/fioqNEOscsOo+nZqx+z3k2XPUG2bzOFA40c1hP7yQWwlg8/2x91mFp5pkmnrl2RdhlYUG6vY/T47b5RKrw==",
      "algorithm": {
        "algorithm": "AES_CTR",
        "keySizeInBits": 256,
        "settingsAES_CTR": {
          "initialCounter": "8PHy8/T19vf4+fr7/P3+/w=="
        },
        "settingsChaCha20": null
      },
      "checksum": "920B1BAFA13F1CC45190D26A51D9EB3F30797C76982C886EA616C463584AE051"
    }
  ],
  "notes": [
    {
      "noteTitle": "ICAgICAg",
      "noteText": "ICAg",
      "creationTime": 1570475222,
      "modificationTime": 1570475222,
      "checksum": "87E68D0EAF3D23EDB258E9903155A05115BECE3231460345660B805A3067735C"
    }
  ],
  "noteSecrets": [
    {
      "keyIdentifier": "ZG9lcyBub3QgbWF0dGVy",
      "audalfData": "1zEke8FUkLqadx/i538qxUxMvPyg6ntCijVMd7egCz+HgSo0vxcGNEC5/13kfssa1JWmJLN8eSf8AVWwCYRSJk6MS8g7PDYEsRpDUNKSfoDK/EnbbUYCxeWMQs16ckEDjrkhpp9RSP1DMksnCKBnFaXloNG2FhpkopWaJOjqjJlfzz/FblksNSvO6jay1weDRpCKBIrOJtVFeCZSfTe97hzuqvfaojQxMTceiCkAMhw80KfrngrMBTplqJpU/eLuZ9+HiLvACCi7MWMlMd3l5elLGTbAXKMAtsmruQOIDDkLQHauiG4Rdw==",
      "algorithm": {
        "algorithm": "ChaCha20",
        "keySizeInBits": 256,
        "settingsAES_CTR": null,
        "settingsChaCha20": {
          "nonce": "Ovx+n/f8Be0AAAAA",
          "counter": 33654
        }
      },
      "checksum": "1BA6EF21BFBD96BD43A6B362438FB4CECB01AEB3F5885746880B4B8D5DF3CFC6"
    }
  ],
  "files": [
    {
      "filename": "bXpxc2p0YjUub3li",
      "fileContent": "AAAAAAAAAAAAAAAAAAAAAAAAAAA=",
      "creationTime": 1570475222,
      "modificationTime": 1570475222,
      "checksum": "88FF65BE1D0FE38E57250ECF0F11FAA31F293A1D7FD19728FB73073049539EF8"
    }
  ],
  "fileSecrets": [
    {
      "keyIdentifier": "ZG9lcyBub3QgbWF0dGVy",
      "audalfData": "mUVWkbudtc1OFpvmqSlKaze9ZjWp694WdUAroALTj5cY+uyhXbBlGtDfi1LGULjx7OfUnUGVVzwlDuuwfaxkjfOb+zREFXRYovLglfF7jfB5UVSZ6LkQnuZI4MIrDwpEw6dN0Ly2vw3jv18h8ETFqNYWK14+rmHyzqISTNnHErAPJVF4ZwLdJy3/akLohcwRr1KosZ+awiRtVmg9nRCXTeFwtae7BDxo2c7hnkFvIjEhmYtN4fuCC0xmWfcvzF35zqJHtPShDDwHuKmGHHaAklcWd42EgINI607uU6L18p/pCXRENwjd8KC9CWmxXM1gTydQyKHs4ieLIqba7mq1cA==",
      "algorithm": {
        "algorithm": "AES_CTR",
        "keySizeInBits": 256,
        "settingsAES_CTR": {
          "initialCounter": "8PHy8/T19vf4+fr7/P3+/w=="
        },
        "settingsChaCha20": null
      },
      "checksum": "5F63C18DD51DC72303E229E79808C939F70DAF0A4FC0382E3A453173F0852139"
    }
  ]
}
```

## Version history

0.2 Added first public JSON sample  
0.1 First working draft