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
      "salt": "yuOVXZ9Fh5Mo6xNbIYWVJQ==",
      "iterations": 101042,
      "derivedKeyLengthInBytes": 32,
      "keyIdentifier": "ZG9lcyBub3QgbWF0dGVy",
      "checksum": "69A42C91B916D1929AE3A8F9E6AF9F923EE73280454BDD92C6F81DAC0E4C4EDF"
    }
  ],
  "loginInformations": [
    {
      "title": "dXdjZzNpYTIuanZv",
      "url": "aHR0cHM6Ly9lYnZkeWliYS5jcno=",
      "email": "YnRveTFoMDUuNXlpQHRjejRjZHowLjVnbA==",
      "username": "NDRsbjAydDIuYWlu",
      "password": "d3I0eHJza20ubXht",
      "notes": "",
      "creationTime": 1572896083,
      "modificationTime": 1572896083,
      "icon": "",
      "category": "",
      "tags": "",
      "checksum": "72B00CDD716B05727AF2D2EB1CF0F3FDC6FD510B2F7E2F0266056B749DB05B4E"
    }
  ],
  "loginInformationSecrets": [
    {
      "keyIdentifier": "ZG9lcyBub3QgbWF0dGVy",
      "audalfData": "Ak1VfSPEJUhFEH5F4h6oGhIRXUqkuJ4xSpt5fxt4TOMpL1nYxWMclvzi0NZZ9XL8E3n67x7Cfb9a7B93m0YqtlSvi81hXYazCPXANSu6Vwwxxh8HhrE+46nVJq41N2NlnoYmElAyquVgkscQC2RK3LEhuXSmMyOdDi6CTtPEi5o9F2HkxrEcV7LXxSKQ17etNsuL2yqzhLUm88JsxELCUJpcGGgvPqiMdhNziviWyEC7TfP6Orp+wV3WJ5SHW6wuvDPiiLot2ds2pH/10Azndpmg0UbOUtculOmhk+A7YgR+pLCua5X8n2cX9BAVMiEq60QL+I8V8a3n+SctSOU4CXrL1i27MR01lJD05WluFZDWh3w5OaaMwu+lR1Up3QV4ZdB68Y1Kt95pK3OjpkH2prYPAdt9miPljKTw+ccjTEOrAN6IOQ0fTiR06ze/kyiqHgME+ln3wtR8vkpjby/zqtT63iOzdda4DP2WasxlaTWxn2OyAmiRj0xVYL04LxiIh5TSn3MVjl2JtX9UzKqftHEsZysrtXSD1W3kGkjNB32v1gap4gm6tWhaBvyBCysFKC25x5LgzBDjxUjBqtOD/YGmyjCVha/95y6zgjoDCVq6uVevaLBnqf6dRIDkIuIltgXklBBWAzZ8OEzWVH8Ms/AWj4PFZiqVApDaAoDuOVYVqE4BJQ8yrAMt592Caart903uOUVEVP/wSpAn9bS6TvP5uE6V0mTv0d6n5o9+8Hx2zOD2r1ip1Poc1gLV3HELDcr3fwhQN+kssc/nCNW5Nw==",
      "algorithm": {
        "algorithm": "AES_CTR",
        "keySizeInBits": 256,
        "settingsAES_CTR": {
          "initialCounter": "8PHy8/T19vf4+fr7/P3+/w=="
        },
        "settingsChaCha20": null
      },
      "checksum": "F922FCE68AAC90D6163839580A66648125DC865EAEF0308BEA45D9205333654C"
    }
  ],
  "notes": [
    {
      "noteTitle": "PXhwe3oyRDs=",
      "noteText": "PDpnJHAhc3hyIExyeiplS0kpcHBpW3lQTmNSUz0qdi8nVm4zNEZoeGY8O3J1QC8zMkRRcUFTUV9AN1QtTUBbaCg8akM7UTcjQHYpTD8mWS5TP0B4WCVtUyUucntwW0pGYFJpWVVqd2AsTVBJSSRAOlxGWC5+YjAjTTc+LV46MmNLYmtrOyBXZ0ZfaypTQykhbFc+SSI8R3xCZis+TGohcDtrfGU3U35cbXBnPnYmTiotPT8memdhLzttSVNzOTpbXnltZkVDaDlYYVowUykmPDghMC9LeXRTKm1KSClKZ1RVK157N2ZjaVMlTTksUFoyZyw7cigrL2MlOlxXdz8vLXgmWkdJKiRRPUZaRkxbRlgyOGB8L3RLSnt6dnwpK3AzdD9AJnUyZ1woaFRhT2g3SHIkRV9dMn0jWi9LTjMnRzJUR1AsOkBifk8kdEU/aHkyYk0qJWQxVGFBPEplZjlJIEBCLCg4Ky5SQEYvWT1XYnA1OWtle0JMQ3FtaX10ezg2WnMlfFxxeVY/V2M+IXpEaVhZUExNYyN9dGc1SUAvXEQteH5JUmU0Qj80RkRdLkF2SSBEO0pqZ3VvJidzW081L3k+MCh6ejdxRC0tOTxeQGZGPiBAakB4QjAo",
      "creationTime": 1572896083,
      "modificationTime": 1572896083,
      "checksum": "B00D9A4C2237139765A36720581639A81E2F24A326D228B20B8A5EFAC0A9C790"
    }
  ],
  "noteSecrets": [
    {
      "keyIdentifier": "ZG9lcyBub3QgbWF0dGVy",
      "audalfData": "IlIHl7Mtq4yTEe4IILK9RJTRqqIVRV4rWXkbgmZoUbqM/B2docG8e9uF3Fb64FVuNkHJUrhHiRGGlGshfefvl5CdsbA3CFw8H5OBPTLzbbFmx/pByLT/p2vb5Z7RffX9k2/iX1A4uIg43E3iqVqQArLWX8C4ig2MqF+s0rA379JFaURhV5G9v71u31qii4AFEssPYHryfbRePolrOFXT/jV8l5mx26YMUyAtRdBE/M64oUjzhC30CeGkN0R8jyf6u/XbvivtWecTwicv31oqxbVCsAdNlB7NPYOam5/+eqwpenVNWOHOwuNtA/ISGS8UKY+q3mT+DE0af0j+hW3qZkKHInrDaJy2doLDMMNfj7MFlngOaroOLc9HrqaJnYIM5PC0apmEvq77oGP+K3NQ0GIp6l0QfvYyYBTlnVFb5/AcAj8W+uNaqIR49+/Uq9s9tWlJHP5Zey3KRfy3oNsM6bXR/fWnO/IFzesEQQy+SAFlDmnXH6xMvL+0QR63r+Yk906N/9bEJs8UEVvJxJoFUzkuMAvpfFthuBefxcg5A3UhvFw6c9r2UJL3du+idkd2nL9MLpkBI00YYY+Zm+BhPnqC94HRiclnT0UFos1iXvgJf1bMwIdK03Cp/q1aAidrB9F0sOey7Owuxt0GFvwirTTKzQaMNGdtb9O1qL1EPnaB5xKPhNdEuclt5/UJ0yYFwGKFMdCx/moFf2mSzAANVXAcmMysbfI373LbqOPn24Ct9E33fcBptz+vaveUc5DdrZWEBqzA4m6L2SaxxO6bnFTwCU2PPn5mc/4blUdvkKEBxiFCEll+KIXD56K6f0gn/jav48dFq8urHJlmbNgyng6zLxN/TcsV4m+16zI8X4URNnjZxg25sE95YDlCF4lWBeezJU6lM8H5P82t/l2b81JHg7muCPJicPqlGcf+KxtZ+On8T03j7LjfarNEDWJqZKjsWM5qOwHvH4v79gI5hUfJqpBYyKlKjASd/YC34n3BWVwqZ6ZkhEsJ2C2BAqBdyXx/VfoYS6LKlki7McC1PZixrXyEs5Vv0q2R6R6cib7MAGbij9x8tIJdKDjn1cwN/FGUZIVFkHlYDLW1zuesZfXxVUA5pZlUwM1AGysZLSR7k4sortSl30xkCPS4ZJhkNymJBikTvvY2Y1/hjuMnKhJOmnRSl4vSboRIexXP8qz/xaENoVK2a8UDgbFHPFS7kCtgKcYibEr1tqKdGzwh43UZwWWZckUwAJVaq5Lvn09ZKrQFBLV8gTDhj+ctI6xhQHnBd+3MLX9BgZiCQIHk1FuAZdwqNXJnAVK8bTuZbasHBI4FCU5QFB1Dj33YKIJg2YUZWK+yJm7HliHQMWHyNcEhksZdAab9g0ZvSyhq39GGgE7Y7Yv1HX3eiu2EHXFMSf9CPfY1FspucFX96C7OVDEuBoH7ptatrYlxlg/+MC9nDQSzYWGbaqJByu/Sfjk38WO5gS1+uSjLe3GOPmAFzDoWAN8YmUuyTJkJNzgnYR9JPb/GmbWG/VjnbpE9UoPbCL8Sr4wdXI2918562dbrS2C9XC7LMCTvbeVARtfQqsUYdQugpELQwAbsqlRTqCZO2BU5je5zwiDb+fI/idvvlxMjw9yx4Tr/HXRxepIZjyRI76KSPu9/2j42woooZxubgql+hB/ROSn1sNtNc9BMOT7ATbfYnu005RwukJ+6hFAH0ZMzQZtjV8LsHxf5ndLyWYW/i0rGxCFtK2DxoArkCo+i+kpCPMk1bPPvGFuH+xArGZtCIRIvT2evIztiCEz4cwrQXvuVS6OcY1/h6zNDGy8CuHL8V0VB8mvoYFeNpwsPD02jpr8rgU6zc0KlxVZwGWjdjoG0DLLLe+9lveV3d43NtZSgKvYX2pnWNwv9ZWiG6oqJwqfwfG9eIMfjemJJ3qZO6cOkKOBq6+FTNZD1LjuMyYu20PWpo/VKhNEk/Kx/E2hXgDcu19Q7k4wR205ny640456lp9dROfoXwFMqk3iuRYguSypufJT7dZaS4flxs0oHfRMFPcYCdj6F7VwgGPmtobnbKwPmu6isxSn1X641CPtz/CFM0cx+ZYiHXHjjyUvJiZpf9qePHK4ZhuWMjYq7JBinbekF5jLttgCxOyR12IB5ax1+vZeKZyuUwNW779od4BYdZFd3kEhkj5fB8aHoUcIQsjLzCKnf+66yVnucYRzorCbnuqPp91qw6dXa1eqqcYL8MaRpeMNJ88sSnZ2CJbvSrtM7dd1JEehEHJTsd2YUErF5+SyUFtbtaUKEzrtGA66Ra/RbX+hS2B55nn9assOf6ZHzs6GNdBU7z5tB/1mtDn5qdC58EPGnZxejyOGMX9p7cI6Sy6bjvxSBdozzi1Bcyt3QN7CVCB/N7OFbFJDBO0ya7SItGo9mF0EZAj0Zz9iPV9xIoxayWu7CqrJch0BiUcK4K8PtJKs3sY1NQ5K+4eqTtkTRvs86VLvhqCvu2Df7H+tbcsPy7Fx2K36mzPW9TY3Bz1paxTdW+iIATeWRJ4wTmxYeWJ93/ytYE4fZx60/4RJi3fRJoNkGU+cDLjlem4X+stRbvSlYK1KQ62C+dghOeEXZ8ChFPtDxlgKfx69/R93JnIisTO3CQKJNQbNq6SXJGgJ8N4hj5GcFp3eyacVd1kchYSxpmD4LuhzHle+bndXcbnnI+Nbp5esRdUN4RpLQ5NEhi+vbl3ut1VbuZNTgmskEpeJheXvDZRVxZdzjWlbPnb6gY43xgmoAwZxh4qPzz52wOqfRoz0QR6IhUHX6",
      "algorithm": {
        "algorithm": "ChaCha20",
        "keySizeInBits": 256,
        "settingsAES_CTR": null,
        "settingsChaCha20": {
          "nonce": "dyYagCCq3FYAAAAA",
          "counter": 870378
        }
      },
      "checksum": "882EBD4FB5D2312B9CC3A21CC36D05AF7C68DD458FAF94B74F6609F9847D7F35"
    }
  ],
  "files": [
    {
      "filename": "NHdycTI1YjEud24x",
      "fileContent": "xsv6MOGl/DDN8cXo6Y8C7y88KL1DM7MXAxmB2irgmwP1EP0D2pHL4AzKUrq3lYdcSs4Scb1YX5IX4izHJCIF7VbB89iR/hSecEixeOH5YG6SJJBczSlGnLFr7PhkBLzpxGVj9aGvy0u5dAF1p+axHoG9Nf+SqCAte1YnJhIcOWyMx7N7lWvN4llEo1go0fXKuc13p8+8VxtENnlLiKQ5nTqU6N8zNYgV8FKmTQXHBKpgXGxEpZKd0HCXNl/yglq0CwUek+gWl4RFYbZ8FQoWfTHP6is39Pin9xhvm/4pI2738UIAqHHBSsXo/0PcILplgbktI5cvfRYNd5zQp/yFGz1IhSTHFdXADZ9lTvS0y9ZeCRlF/ADWx3Mr8jHU8aPJY+QGlJqVnmzkbBX4yi4iWKzFcp7iQB89cb6wnCKj6xv8m+sQrjY8yGutYY/q3v1FCZqFD38F5iLEySLc5QFJQID6+y5DEap1iakyNd+PUpPAa5OIHtyb9rTITOUUX+NpZCAO8OLOAffvEIbW0rFDNHaPG3luwCKkXgV5esXFYCnGydG+gWKw8mmbmQ5WxSQDhRduhERp+qP+apHdVYcyKa9cDwjghLMU3ykP0ycTTpjgdfWtVtvlXc8twBfQ05ziaG9f+bYbIgBkWqUaWSd86hz4/N+ShdPTd7I5ssSbQwyNLWq3tFTixFP0Sfw2ygOosdX719a8UOOci4IE4nA8yBaZjSy8xDbHFjiMnTvWnayukQHuoGs10NyHGyjR3uLit4DlnD3X6+yfM8GdL7Knxe7WVVFuTierY7xPNKgN9jdWqeW78QBv1qUUTm2pmKAp31Y6+4iRdGlZOjiAiLdEkj2JR4bN7NTtZn6rWf+6AcscJVVS0/uvxDV7YrbI707u0LwwIFAaXPOBTJQJ5RpqnjhsY2Ni8b9C2oJQUYodJHcwvYlDiuF7Achi0YZmpd8aEcN+XIvrjN/97UXNyQtoYycd2SiRJhRW8WKaACA42zWjNj/Hn8jrRTGpRpycrTi9+W1eSQ==",
      "creationTime": 1572896083,
      "modificationTime": 1572896083,
      "checksum": "CE24D1C8AF86D9320E563E7B433BBDBEE734BDC64AE4349974792EB6FF59EDAB"
    }
  ],
  "fileSecrets": [
    {
      "keyIdentifier": "ZG9lcyBub3QgbWF0dGVy",
      "audalfData": "Ak1VfSPEJUg1Fn5F4h6oGh0RXUqkuJ4xSpt5fxt4TOMRL1nYxWMcliTi0NZZ9XL8I3r67x7Cfb+C7h93m0Yqtgyui81hXYaz7p2sUEXbOmmTxx8ChrE+423UJq41N2NlG7VNfThDmYNe8qh2C2RK3IojuXSmMyOdbUfuK5Cr5e4sEGGIo7EcV7HXxCeQ17etD8iL2yqzhLXiEk6rm1uTZD/XtUo/FDtH1Ncsu2xgL6C5hdzQ57zMGM6/yzzTQ9tzasdHYjunUlj6IVMtXC7/mQrOg06D3ZbFtnNPVN7eFY02pd4xOmmicizFEJLXOPtT2G8Ht28fxG5+2fm6QQB9tjR14qtq2QT9EbWi5lCGsf7y4X9IiqRW6UIOWWQ3G+ExFxULLiOReEegMIlHA+3SOv3ShtwNqMWoprPDB74eyae2ngddQss9Fz3Z1C4yglBXdybsumYWGpPS/ICHsJGesDRA7/NT4DTpiq5c/xATqSEfyZGDI1lCYn6TwH8GlJPuOUNfTZO3k5GlTL3dqOn13BCIkF0ffl0ewMBdIIgiFbNkst+sCuSOSBP4ciJ72yizRyhbOFb4/f9MNfX0QjCIrlE8Lt/84NCIh9fp5oBpBgaWNsyVUaEOZ7gefBaASpp1c7vfNYTvbOPCX6VB6bI58BR3fosm3tmftoc1E41ofDjwjdD6C2f1K3IEgZjNVliISl7591VJBfNYGy1iqzQPUSRCXty463GXSLcxXN7TS+Lw1ioMwS73A1rugY9KezyKbjWH6VAKAJLSLvtBfkMDKpD7JDqzL9qrcwEAW7IdGYcygRT9PIuebw+eStZUUNhbOsVkM43O0fbkUz4CK7fkHDkQXHO9iigDosnYFzFMASvlnK4X9VGaR+P9eOgpks6N2+FR336+3aJoLu2qrOP0EhsW4bJOOozfU0U6ELklB2IihPpqmEsWJB/HhiLkDQuZF/7jYBtslv4uKKBxBKws8Wnws2bblCxmh/Kcx2BGBRySU57YSXLQ/b+plVUvHbbVHXmsdB5N3Tq1zjYJTKL5bKcztoyzwogDHYv52vIFiFMMM7vTvDghOLeKxtA3X3cqic0vrBHvwoIFBJF0ODLzwWIRuBxLFDES3soX7OWvvv7k7xQpq1FCxJCjqsv6kLwKWbHIATYB39kG2dKP9k1bZZMEbW0Q3mXv2alBWUulxcmpUG9FqHkCNSuXDK5gb9PCkL9HRdBQbgKiRnV3ezBav9uB9USe+CdmC5fTFH6pcL47x3yL3cz+93WZZp5A8Z5Pkd6H0VI7bFjGEHdk+DOuQjQzVaHhXdhl/iVFYEZYkM+1HonlDxzeOMl3KSMeTwTWbuLsIryFiz0ppAbQvjjM7UCC/aqwrHvGxa07Avq0Jlgg9LVuBp0iL+K/ZGFYbZnW",
      "algorithm": {
        "algorithm": "AES_CTR",
        "keySizeInBits": 256,
        "settingsAES_CTR": {
          "initialCounter": "8PHy8/T19vf4+fr7/P3+/w=="
        },
        "settingsChaCha20": null
      },
      "checksum": "D116E43D2AC13E4FBCBD538D2668E2369F986AE5C8FAF70A88FB85925FB367C5"
    }
  ]
}
```

## Version history

0.2 Added first public JSON sample  
0.1 First working draft