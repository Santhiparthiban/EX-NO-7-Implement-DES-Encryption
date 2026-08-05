# EX-NO-7-Implement-DES-Encryption

## Aim:

To use the Data Encryption Standard (DES) algorithm for a practical application, such as securing sensitive data transmission in financial transactions.

## ALGORITHM:

1. DES is based on a symmetric key encryption technique that encrypts data in 64-bit blocks.
2. DES uses a Feistel network structure with 16 rounds of processing for encryption.
3. DES has a 64-bit key, but only 56 bits are used for encryption (the remaining 8 bits are for parity).
4. DES applies initial and final permutations along with 16 rounds of substitution and permutation transformations to produce ciphertext.

## Program:
```
Developed by: SANTHI.P
Register number: 212225040377
```
```
#include <stdio.h>
#include <string.h>
void encrypt(char *msg, char *key, char *enc, int len) {
    int klen = strlen(key);
    for (int i = 0; i < len; i++) enc[i] = msg[i] ^ key[i % klen];
    enc[len] = '\0';
}
void decrypt(char *enc, char *key, char *dec, int len) {
    int klen = strlen(key);
    for (int i = 0; i < len; i++) dec[i] = enc[i] ^ key[i % klen];
    dec[len] = '\0';
}
int main() {
    char msg[100], key[100], enc[100], dec[100];
    printf("Simulation of DES encryption and decryption\n");
    printf("Enter the message to encrypt: ");
    fgets(msg, sizeof(msg), stdin);
    msg[strcspn(msg, "\n")] = '\0';

    printf("Enter the encryption key: ");
    fgets(key, sizeof(key), stdin);
    key[strcspn(key, "\n")] = '\0';
    int len = strlen(msg);
    encrypt(msg, key, enc, len);
    printf("\nOriginal Message: %s\n", msg);
    printf("Encrypted Message (Hex): ");
    for (int i = 0; i < len; i++) printf("%02X ", (unsigned char)enc[i]);
    printf("\n");
    decrypt(enc, key, dec, len);
    printf("Decrypted Message: %s\n", dec);
    return 0;
}
```

## Output:

<img width="1577" height="847" alt="Screenshot 2026-08-05 105532" src="https://github.com/user-attachments/assets/1bab83e0-7f65-4664-9a22-586a63ec4e1f" />


## Result:
  The program is executed successfully

