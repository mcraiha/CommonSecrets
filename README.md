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

For [key derivation functions](https://en.wikipedia.org/wiki/Key_derivation_function) only 

## Why were certain algorithms chosen?

I tried to make this easy to implement in many programming languages and environments. Main target was [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API/Supported_algorithms).

## Implementations

C# implementation will come later

## What are the negative traits?

Since most of info/data is text-based, CommonSecrets isn't ideal storage space wise. And because [AUDALF](https://github.com/mcraiha/AUDALF) is used to store encrypted info, some other limitations apply.

## License

Specifications are licensed under [Unlicense](LICENSE), so you might use these specs as you want.

## Version history

0.1 First working draft