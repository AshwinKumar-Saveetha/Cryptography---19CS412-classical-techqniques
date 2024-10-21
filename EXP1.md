# Cryptography---19CS412-classical-techqniques
# Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To encrypt and decrypt the given message by using Ceaser Cipher encryption algorithm.


## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

1.	In Ceaser Cipher each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet.
2.	For example, with a left shift of 3, D would be replaced by A, E would become B, and so on.
3.	The encryption can also be represented using modular arithmetic by first transforming the letters into numbers, according to the   
    scheme, A = 0, B = 1, Z = 25.
4.	Encryption of a letter x by a shift n can be described mathematically as,
                       En(x) = (x + n) mod26
5.	Decryption is performed similarly,
                       Dn (x)=(x - n) mod26


## PROGRAM:
## CaearCipher.
~~~
#include <stdio.h>
#include <ctype.h>

void caesar_cipher(char *text, int shift, int encrypt) {
    int i;

    for (i = 0; text[i] != '\0'; i++) {
        if (isalpha(text[i])) {
            char base = isupper(text[i]) ? 'A' : 'a';
            text[i] = (char)((text[i] - base + (encrypt ? shift : -shift)) % 26 + base);
        }
    }
}

int main() {
    char text[100];
    int shift;

    printf("Enter the text: ");
    fgets(text, 100, stdin);

    printf("Enter the shift value: ");
    scanf("%d", &shift);

    caesar_cipher(text, shift, 1); // Encrypt

    printf("Encrypted text: %s\n", text);

    caesar_cipher(text, shift, 0); // Decrypt

    printf("Decrypted text: %s\n", text);

    return 0;
}

~~~
## OUTPUT:
![image](https://github.com/user-attachments/assets/58f9d649-8343-4021-a9f9-5bf933d25fc2)

## RESULT:
The program is executed successfully
