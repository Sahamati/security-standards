# Annexure A – Business Layer Security – End-to-End Encryption

| Cryptographic primitives | Minimum Implementation Standards |
| :--- | :--- |
| Key Exchange Algorithm | Elliptic Curve Diffie-Hellman \(ECDH\) \[1\] |
| Elliptic Curve Group | Curve25519 \[2\] |
| Message Hash function | SHA-256, HMAC-SHA256 \[FIPS PUB 180-4\] \[3\] |
| Generating the shared session key for encryption | SHA-256 \[4\], HKDF \[5\] |
| Encryption Algorithm | AES-128-GCM \[6\] |
| Generation of Random Number | Randomness Requirements for Security \[RFC 4086\] \[7\] |

\[1\] [https://tools.ietf.org/html/rfc8418](https://tools.ietf.org/html/rfc8418)  
\[2\] [https://ianix.com/pub/curve25519-deployment.html](https://ianix.com/pub/curve25519-deployment.html)  
\[3\] [https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)  
\[4\] [https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)  
\[5\] [https://tools.ietf.org/html/rfc5869](https://tools.ietf.org/html/rfc5869)  
\[6\] [https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-38d.pdf](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-38d.pdf)  
\[7\] [https://tools.ietf.org/html/rfc4086](https://tools.ietf.org/html/rfc4086)

