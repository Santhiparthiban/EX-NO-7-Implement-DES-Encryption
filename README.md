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
#include <stdint.h>

uint32_t feistel(uint32_t right, uint32_t key)
{
    return right ^ key;
}

/* Encryption */
uint64_t encrypt(uint64_t plaintext, uint64_t key)
{
    uint32_t left, right;
    uint32_t roundKey;

    left = (uint32_t)(plaintext >> 32);
    right = (uint32_t)plaintext;

    for (int i = 0; i < 16; i++)
    {
        roundKey = (uint32_t)(key >> (i % 32));

        uint32_t newRight =
            left ^ feistel(right, roundKey);

        left = right;
        right = newRight;
    }

    /* Final swap */
    return ((uint64_t)right << 32) | left;
}

/* Decryption */
uint64_t decrypt(uint64_t ciphertext, uint64_t key)
{
    uint32_t left, right;
    uint32_t roundKey;

    /*
       Encryption performs a final swap.
       Therefore, undo the swap here.
    */
    left = (uint32_t)ciphertext;
    right = (uint32_t)(ciphertext >> 32);

    for (int i = 15; i >= 0; i--)
    {
        roundKey = (uint32_t)(key >> (i % 32));

        uint32_t newLeft =
            right ^ feistel(left, roundKey);

        right = left;
        left = newLeft;
    }

    return ((uint64_t)left << 32) | right;
}

int main()
{
    char text[9];
    char keyText[9];

    uint64_t plaintext = 0;
    uint64_t key = 0;
    uint64_t ciphertext;
    uint64_t decrypted;

    printf("Enter 8-character plaintext: ");
    scanf("%8s", text);

    printf("Enter 8-character key: ");
    scanf("%8s", keyText);

    /* Convert plaintext to 64-bit value */
    for (int i = 0; i < 8; i++)
    {
        plaintext = (plaintext << 8) |
                    (uint64_t)(unsigned char)text[i];
    }

    /* Convert key to 64-bit value */
    for (int i = 0; i < 8; i++)
    {
        key = (key << 8) |
              (uint64_t)(unsigned char)keyText[i];
    }

    /* Encryption */
    ciphertext = encrypt(plaintext, key);

    printf("\nPlaintext  : %s", text);
    printf("\nKey        : %s", keyText);

    printf("\nCiphertext : %016llX",
           (unsigned long long)ciphertext);

    /* Decryption */
    decrypted = decrypt(ciphertext, key);

    printf("\nDecrypted  : ");

    for (int i = 7; i >= 0; i--)
    {
        printf("%c",
               (char)(decrypted >> (i * 8)));
    }

    printf("\n");

    return 0;
}
```

## Output:

<img width="1357" height="732" alt="Screenshot 2026-09-02 101107" src="https://github.com/user-attachments/assets/b38eeec7-774c-4b60-b217-d58444600a29" />

## Result:
  The program is executed successfully

