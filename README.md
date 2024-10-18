# Ex-9-RSA-Encryption-Algorithm

## Aim:
To implement the RSA encryption algorithm in C++.

## Algorithm:
1. Key Generation: Choose two prime numbers p and q. Compute n = p * q. Compute Euler's Totient Function φ(n) = (p-1)(q-1). Choose an integer e such that 1 < e < φ(n) and gcd(e, φ(n)) = 1. Compute d such that d * e ≡ 1 (mod φ(n)).
2. Encryption: ciphertext = (plaintext^e) mod n.
3. Decryption: plaintext = (ciphertext^d) mod n.

## Program:

```
#include <iostream>
#include <cmath>

using namespace std;

// Function to calculate GCD (Greatest Common Divisor)
int gcd(int a, int h) {
    while (1) {
        int temp = a % h;
        if (temp == 0)
            return h;
        a = h;
        h = temp;
    }
}

// Function to perform modular exponentiation
long long modExpo(long long base, long long exponent, long long mod) {
    long long result = 1;
    base = base % mod;
    while (exponent > 0) {
        if (exponent % 2 == 1)
            result = (result * base) % mod;
        exponent = exponent >> 1;
        base = (base * base) % mod;
    }
    return result;
}

int main() {
    // 1. Select two prime numbers
    int p = 61;  // Example prime number 1
    int q = 53;  // Example prime number 2
    
    // 2. Compute n = p * q
    int n = p * q;
    
    // 3. Compute φ(n) = (p-1)*(q-1)
    int phi = (p - 1) * (q - 1);
    
    // 4. Choose e such that 1 < e < φ(n) and gcd(e, φ(n)) = 1
    int e = 3;  // Example public key exponent (must be co-prime with φ(n))
    while (gcd(e, phi) != 1) {
        e++;
    }
    
    // 5. Compute d such that d * e ≡ 1 (mod φ(n))
    int d = 1;
    while ((d * e) % phi != 1) {
        d++;
    }
    
    // Display the public and private keys
    cout << "Public Key: (" << e << ", " << n << ")" << endl;
    cout << "Private Key: (" << d << ", " << n << ")" << endl;
    
    // 6. Encrypt the message
    long long plaintext;
    cout << "Enter a number to encrypt: ";
    cin >> plaintext;
    
    long long ciphertext = modExpo(plaintext, e, n);
    cout << "Encrypted message: " << ciphertext << endl;
    
    // 7. Decrypt the message
    long long decryptedMessage = modExpo(ciphertext, d, n);
    cout << "Decrypted message: " << decryptedMessage << endl;
    
    return 0;
}
```

## Output:

![Screenshot 2024-10-14 114259](https://github.com/user-attachments/assets/f88b5e59-43e6-41da-9fc7-04abb9e34608)

## Result:

The RSA encryption and decryption algorithm has been successfully implemented.
