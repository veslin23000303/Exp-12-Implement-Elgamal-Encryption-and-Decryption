# Exp-12 : Implement Elgamal Encryption and Decryption

## AIM:
To encrypt and decrypt a message using the ElGamal encryption algorithm.

## DESIGN STEPS:
### Step 1:
Select a prime number p, a generator g of the multiplicative group Zp, and a private key x.

### Step 2:
Calculate the public key y = g^x mod p.

### Step 3:
For encryption, choose a random integer k and compute:
C1 = g^k mod p
C2 = (M * y^k) mod p where M is the message.

### Step 4:
For decryption, use the private key x to calculate:
M = (C2 * (C1^x)^-1) mod p.

### Step 5:
Output the encrypted ciphertext (C1, C2) and the decrypted message.

# PROGRAM:
```
NAME:VESLIN ANISH
REGISTER NO:212223240175
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

// Function to calculate (base^exp) % mod using modular exponentiation
long long mod_exp(long long base, long long exp, long long mod) {
    long long result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

// Function to calculate the modular inverse using Extended Euclidean Algorithm
long long mod_inverse(long long a, long long m) {
    a = a % m;
    for (long long x = 1; x < m; x++) {
        if ((a * x) % m == 1)
            return x;
    }
    return -1;
}

int main() {
    long long p, g, x, M;  // prime, generator, private key, message

    // Input prime number p
    printf("Enter a prime number (p): ");
    scanf("%lld", &p);

    // Input generator g
    printf("Enter a generator (g): ");
    scanf("%lld", &g);

    // Input private key x
    printf("Enter a private key (x): ");
    scanf("%lld", &x);

    // Calculate public key y = g^x mod p
    long long y = mod_exp(g, x, p);
    printf("Public key (y) is: %lld\n", y);

    // Input the message to be encrypted
    printf("Enter the message to encrypt (as a number): ");
    scanf("%lld", &M);

    // Choose a random integer k (for simplicity, we input k)
    long long k;
    printf("Enter a random integer (k) for encryption: ");
    scanf("%lld", &k);

    // Calculate C1 = g^k mod p
    long long C1 = mod_exp(g, k, p);

    // Calculate C2 = (M * y^k) mod p
    long long C2 = (M * mod_exp(y, k, p)) % p;

    printf("Encrypted Ciphertext: (C1 = %lld, C2 = %lld)\n", C1, C2);

    // Decryption: Calculate M = (C2 * (C1^x)^-1) mod p
    long long temp = mod_exp(C1, x, p);  // C1^x mod p
    long long inverse_temp = mod_inverse(temp, p);  // (C1^x)^-1 mod p
    long long decrypted_message = (C2 * inverse_temp) % p;

    printf("Decrypted Message: %lld\n", decrypted_message);

    return 0;
}

```
# OUTPUT:

![image](https://github.com/user-attachments/assets/18aab40b-1c16-4b45-8018-873ebea001e2)


# RESULT:
Thus, the ElGamal encryption and decryption algorithm has been successfully implemented in C.
