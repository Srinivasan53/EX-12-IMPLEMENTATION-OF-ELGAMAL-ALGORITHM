
## AIM:

To implement the ElGamal encryption and decryption algorithm using C for secure communication.
## NAME: SRINIVASAN S
## REGISTER NO: 212224220105

## ALGORITHM:
1.	Choose a large prime number p and a primitive root g of p.
2.	Select a private key x such that 1 < x < p.
3.	Compute the public key y = g^x mod p.
4.	To encrypt a message M:
a.	Choose a random integer k such that 1 < k < p.
b.	Compute C1 = g^k mod p.
c.	Compute C2 = (M * y^k) mod p.
d.	The ciphertext is the pair (C1, C2).
5.	To decrypt the ciphertext (C1, C2):
a.	Compute s = C1^(p-1-x) mod p.
b.	Compute the original message M = (C2 * s) mod p.
6.	Display the decrypted message.


## PROGRAM:
```
#include <stdio.h>
#include <stdlib.h>

// Function to calculate (base^exp) % mod using modular exponentiation
int modular_exponentiation(int base, int exp, int mod) {
    int result = 1;
    base = base % mod;

    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        exp = exp >> 1; // divide exp by 2
        base = (base * base) % mod;
    }

    return result;
}

int main() {
    int p, g, x, k, M; // p = prime, g = primitive root, x = private key, k = random integer
    int y, C1, C2, decrypted_message;

    // Input the parameters
    printf("Enter a prime number p: ");
    scanf("%d", &p);

    printf("Enter a primitive root g of p: ");
    scanf("%d", &g);

    printf("Enter the private key x: ");
    scanf("%d", &x);

    // Generate public key y = g^x mod p
    y = modular_exponentiation(g, x, p);
    printf("Public key y: %d\n", y);

    // Encryption
    printf("Enter the message (integer) to encrypt: ");
    scanf("%d", &M);

    printf("Enter a random integer k: ");
    scanf("%d", &k);

    // Calculate ciphertext (C1, C2)
    C1 = modular_exponentiation(g, k, p);
    C2 = (M * modular_exponentiation(y, k, p)) % p;

    printf("Encrypted message: (C1, C2) = (%d, %d)\n", C1, C2);

    // Decryption
    // M = (C2 * (C1^(p-1-x))) mod p  — using Fermat’s Little Theorem for modular inverse
    decrypted_message = (C2 * modular_exponentiation(C1, p - 1 - x, p)) % p;

    printf("Decrypted message: %d\n", decrypted_message);

    return 0;
}

```

## OUTPUT:
<img width="764" height="368" alt="image" src="https://github.com/user-attachments/assets/bfd4eb20-0f28-4c1d-90c4-b587cc47921f" />

## RESULT:
The ElGamal encryption algorithm has been successfully implemented and tested. The original message is correctly encrypted and decrypted, demonstrating asymmetric cryptography.
