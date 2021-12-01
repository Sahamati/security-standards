# Annexure C – Protocol Layer security – Payload Encryption using TLSv1.2

A summary of the steps that enable the TLS client service and the server service to communicate with each other as follows:

![](<../.gitbook/assets/annexure-c (1).png>)

In TLS Handshake, a client and server agree on a mutually supported cipher suite Cipher Suites , and then use the chosen cipher suite to negotiate a secure connection. For instance, an example of a cipher suite:

**TLS**\_**ECDHE**\_**ECDSA**\_WITH\_**AES\_128\_GCM**\_**SHA256**

Represented bolded to represent the ciphers.

TLS: protocol.

ECDHE: during the handshake the keys will be exchanged via ephemeral Elliptic Curve Diffie Hellman (ECDHE).

RSA: authentication algorithm.

AES\_128\_GCM: bulk encryption algorithm: AES running Galois Counter Mode with 128-bit key size.

SHA-256: hashing algorithm.

Cipher suites are named combinations of:

• Key Exchange Algorithms (RSA, DH, ECDH, DHE, ECDHE, PSK)

• Authentication/Digital Signature Algorithm (RSA, ECDSA, DSA)

• Bulk Encryption Algorithms (AES)

• Message Authentication Code Algorithms (SHA-256)
