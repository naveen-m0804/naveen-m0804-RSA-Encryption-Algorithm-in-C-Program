# RSA-Encryption-Algorithm-in-C-Program

### AIM
To implement the RSA Encryption Algorithm in C, where a message is encrypted using a public key and decrypted using a private key.

### PROCEDURE
Understanding RSA:

RSA (Rivest–Shamir–Adleman) is a public-key encryption algorithm.
It uses two keys: Public Key (for encryption) and Private Key (for decryption).
Steps Involved:

Key Generation:

Choose two distinct prime numbers p and q.
Compute n = p * q.
Compute phi(n) = (p - 1) * (q - 1).
Choose an integer e such that 1 < e < phi(n) and gcd(e, phi(n)) = 1.
Compute the private key d such that d ≡ e^(-1) (mod phi(n)).
Encryption:

The ciphertext C is calculated using the formula:
C = (M^e) % n
where M is the message.
Decryption:

The plaintext M is recovered using the formula:
M = (C^d) % n.

### PROGRAM:
```c
#include <stdio.h>
#include <math.h>

// Function to calculate GCD
int gcd(int a, int b) {
    int temp;
    while (b != 0) {
        temp = a % b;
        a = b;
        b = temp;
    }
    return a;
}

// Function to find modular inverse
int modInverse(int e, int phi) {
    int d = 1;
    while ((e * d) % phi != 1) {
        d++;
    }
    return d;
}

// Function to perform modular exponentiation
long long int powerMod(long long int base, long long int exp, long long int mod) {
    long long int result = 1;
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

int main() {
    // Step 1: Choose two prime numbers
    int p = 61;
    int q = 53;
    int n = p * q;
    int phi = (p - 1) * (q - 1);

    // Step 2: Choose e such that 1 < e < phi(n) and gcd(e, phi(n)) = 1
    int e = 17;
    while (gcd(e, phi) != 1) {
        e++;
    }

    // Step 3: Calculate d such that (e * d) % phi(n) = 1
    int d = modInverse(e, phi);

    // Display the public and private keys
    printf("Public Key: (e = %d, n = %d)\n", e, n);
    printf("Private Key: (d = %d, n = %d)\n", d, n);

    // Step 4: Encrypt the message
    int message = 65; // Example message
    printf("Original Message: %d\n", message);
    long long int encryptedMessage = powerMod(message, e, n);
    printf("Encrypted Message: %lld\n", encryptedMessage);

    // Step 5: Decrypt the message
    long long int decryptedMessage = powerMod(encryptedMessage, d, n);
    printf("Decrypted Message: %lld\n", decryptedMessage);

    return 0;
}
```

### OUTPUT:

Public Key: (e = 17, n = 3233)
Private Key: (d = 2753, n = 3233)
Original Message: 65
Encrypted Message: 2790
Decrypted Message: 65


### RESULT:
The RSA encryption algorithm was successfully implemented in C. The program generates public and private keys, encrypts a message, and then decrypts it to retrieve the original message.
