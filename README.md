# Lab-Exercise---8---Implement-the-AES-Encryption-and-decryption
## Aim
To use Advanced Encryption Standard (AES) Algorithm for a practical application like URL Encryption.
## Procedure
1. AES is based on a design principle known as a substitution-permutation.
2. AES does not use a Feistel network like DES, it uses variant of Rijndael.
3. It has a fixed block size of 128 bits, and a key size of 128, 192, or 256 bits.
4. AES operates on a \(4 \times 4\) column-major order array of bytes, termed the state.
## Program
```
import os
import base64
from cryptography.hazmat.primitives.ciphers.aead import AESGCM

def aes_encrypt(plaintext: str, key: bytes) -> str:
    nonce = os.urandom(12) # 96-bit nonce recommended for GCM
    aesgcm = AESGCM(key)
    ciphertext = aesgcm.encrypt(nonce, plaintext.encode(), None)
    return base64.b64encode(nonce + ciphertext).decode()

def aes_decrypt(token: str, key: bytes) -> str:
    raw = base64.b64decode(token)
    nonce, ciphertext = raw[:12], raw[12:]
    aesgcm = AESGCM(key)
    return aesgcm.decrypt(nonce, ciphertext, None).decode()

# --- Example usage ---
key = AESGCM.generate_key(bit_length=256) # AES-256 key
message = "Hello AES Encryption!"
print("Plain Text:", message)

encrypted = aes_encrypt(message, key)
print("Encrypted:", encrypted)

decrypted = aes_decrypt(encrypted, key)
print("Decrypted:", decrypted)

```
## Output
<img width="1690" height="882" alt="Screenshot 2026-11-21 144055" src="https://github.com/user-attachments/assets/259dcee3-fe32-457b-bd47-3c2143d887b4" />
## Result

The program run successfully.
