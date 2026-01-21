# JWT Xray

Analyze JSON Web Tokens (JWTs), detect common vulnerabilities, misconfigurations, and brute force weak secrets.



## Contents
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Available options](#available-options)
- [Usage](#usage)
- [Issues](#issues)
- [Contributing](#contributing)
- [License](#license)



## Features
- **JWT Analysis**
  - Decodes header & payload without signature verification
  - Highlights insecure algorithms (e.g., `alg=none`)
  - Detects missing claims (`exp`, `iss`, `aud`, etc.)
  - Flags suspicious headers (`jwk`, `jku`, `x5u`, `kid`, `x5c`)
  - Identifies expired or not yet valid tokens
  - Warns about oversized tokens

- **Signature Verification**
  - Supports HMAC (HS256/384/512) with secret string
  - Supports RSA/PS/ECDSA algorithms with PEM formatted public key

- **Brute Force Mode**
  - Crack weak HMAC secrets using wordlist
  - Supports HS256, HS384, HS512 algorithms
 


## Prerequisites
- [Python3](https://www.python.org/downloads/)
- [pyjwt](https://pypi.org/project/PyJWT/): Install using `pip install pyjwt`
- pyjwt[crypto]: Install using `pip install pyjwt[crypto]` (Optional, required to verify JWTs signed with RSA/PS/ECDSA algorithms)



## Installation
1. Clone this repo:
    ```
    git clone https://github.com/StellarSand/jwt-xray.git
    ```

2. Move into the project directory:
    ```
    cd jwt-xray
    ```

3. Give executable permissions to the script (Not required for Windows):
    ```
    chmod +x jwtxray
    ```


## Available options
```
-h, --help              Show this help message and exit
-t, --token             Token to analyze
-s, --secret            Secret key for HMAC verification
-pk, --pubkey           Public key file in PEM format for RSA/PS/ECDSA verification
-w, --wordlist          Wordlist for brute force (HMAC algorithms only)
```



## Usage
- Analyze a token:
    ```
    python3 jwtxray -t <token>
    ```
    **Example**:
    ```
    python3 jwtxray -t eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWUsImlhdCI6MTUxNjIzOTAyMn0.KMUFsIDTnFmyG3nMiGM6H9FNFUROf3wh7SmqJp-QV30
    ```

- Verify a token signed with HMAC (HS256/384/512) algorithm:
    ```
    python3 jwtxray -s <secret string> -t <token>
    ```
    **Example**:
    ```
    python3 jwtxray -s a-string-secret-at-least-256-bits-long -t eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWUsImlhdCI6MTUxNjIzOTAyMn0.KMUFsIDTnFmyG3nMiGM6H9FNFUROf3wh7SmqJp-QV30
    ```

- Verify a token signed with RSA/PS/ECDSA algorithms:
    ```
    python3 jwtxray -pk /path/to/public_key_file -t <token>
    ```
    **Example**:
    ```
    python3 jwtxray -pk /home/JohnDoe/Documents/jwt_pub.pem -t eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWUsImlhdCI6MTUxNjIzOTAyMn0.KMUFsIDTnFmyG3nMiGM6H9FNFUROf3wh7SmqJp-QV30
    ```

- Brute force a token using a wordlist (HMAC algorithms only):
    ```
    python3 jwtxray -w /path/to/wordlist -t <token>
    ```
    **Example**:
    ```
    python3 jwtxray -w /usr/share/wordlists/rockyou.txt -t eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWUsImlhdCI6MTUxNjIzOTAyMn0.KMUFsIDTnFmyG3nMiGM6H9FNFUROf3wh7SmqJp-QV30
    ```



## Issues
If you find bugs or have suggestions, please report it to the [issue tracker](https://github.com/StellarSand/jwt-xray/issues). 
- Please search for existing issues before opening a new one. Any duplicates will be closed.



## Contributing
Pull requests can be submitted [here](https://github.com/StellarSand/jwt-xray/pulls).



## License
This project is licensed under the terms of [GPL v3.0 license](https://github.com/StellarSand/jwt-xray/blob/main/LICENSE).
