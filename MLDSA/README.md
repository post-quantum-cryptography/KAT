## KAT for FIPS-204 (draft)

Compliant with FIPS-204 draft, published on August 24, 2023.
Those vectors include [comments](https://csrc.nist.gov/Projects/post-quantum-cryptography/post-quantum-cryptography-standardization/example-files) published by NIST on October 31, 2023.

## File format:

| Field     | Meaning                                                              |
|-----------|----------------------------------------------------------------------|
| ``seed``  | AES-CTR-drbg seed                                                    |
| ``count`` | Test number                                                          |
| ``mlen``  | Length of the ``msg``                                                |
| ``msg``   | Message to sign                                                      |
| ``pk``    | Resulting public key                                                 |
| ``sk``    | Resulting secret key                                                 |
| ``sm``    | Resulting signature concatenated with the message (``sm`` | ``msg``) |
| ``smlen`` | Length of the ``sm`` buffer                                          |

## How it was generated

We use DRBG based on based on AES-CTR (see [SP800-90A](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-90Ar1.pdf)) for generating random bytes. For each KAT vector, the DRBG is seeded with the ``seed`` value (personalisation string is not used). The test first generates a secret and public key. Then it encapsulates and decapsulates the shared secret.

## Differences with the FIPS-204 and caveats
* Byte oriented implementation
* We don't provide negative tests
