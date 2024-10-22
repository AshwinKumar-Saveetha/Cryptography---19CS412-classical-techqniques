
## PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.

 
## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

### ALGORITHM DESCRIPTION:
The Playfair cipher uses a 5 by 5 table containing a key word or phrase. To generate the key table, first fill the spaces in the table with the letters of the keyword, then fill the remaining spaces with the rest of the letters of the alphabet in order (usually omitting "Q" to reduce the alphabet to fit; other versions put both "I" and "J" in the same space). The key can be written in the top rows of the table, from left to right, or in some other pattern, such as a spiral beginning in the upper-left-hand corner and ending in the centre.
The keyword together with the conventions for filling in the 5 by 5 table constitutes the cipher key. To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. Then apply the following 4 rules, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter. Encrypt the new pair and continue. Some   
   variants of Playfair use "Q" instead of "X", but any letter, itself uncommon as a repeated pair, will do.
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively (wrapping 
   around to the left side of the row if a letter in the original pair was on the right side of the row).
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively (wrapping around 
   to the top side of the column if a letter in the original pair was on the bottom side of the column).
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of 
   corners of the rectangle defined by the original pair. The order is important – the first letter of the encrypted pair is the one that 
    lies on the same row as the first letter of the plaintext pair.
To decrypt, use the INVERSE (opposite) of the last 3 rules, and the 1st as-is (dropping any extra "X"s, or "Q"s that do not make sense in the final message when finished).


## PROGRAM:
## PlayFair Cipher
~~~
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define SIZE 5

void prepareKeyMatrix(char key[], char keyMatrix[SIZE][SIZE]) {
   int used[26] = {0};
   int i, j, k = 0;

   used['J' - 'A'] = 1;

   for (i = 0; key[i] != '\0'; i++) {
       char currentChar = toupper(key[i]);
       if (!used[currentChar - 'A']) {
           keyMatrix[k / SIZE][k % SIZE] = currentChar;
           used[currentChar - 'A'] = 1;
           k++;
       }
   }

   for (i = 0; i < 26; i++) {
       if (!used[i]) {
           keyMatrix[k / SIZE][k % SIZE] = 'A' + i;
           k++;
       }
   }
}

void printKeyMatrix(char keyMatrix[SIZE][SIZE]) {
   printf("Key Matrix:\n");
   for (int i = 0; i < SIZE; i++) {
       for (int j = 0; j < SIZE; j++) {
           printf("%c ", keyMatrix[i][j]);
       }
       printf("\n");
   }
}

void findPosition(char keyMatrix[SIZE][SIZE], char letter, int *row, int *col) {
   if (letter == 'J') letter = 'I';
   for (int i = 0; i < SIZE; i++) {
       for (int j = 0; j < SIZE; j++) {
           if (keyMatrix[i][j] == letter) {
               *row = i;
               *col = j;
               return;
           }
       }
   }
}

void encrypt(char text[], char keyMatrix[SIZE][SIZE], char encryptedText[]) {
   int i, row1, col1, row2, col2;
   char first, second;
   int length = strlen(text);

   for (i = 0; i < length; i += 2) {
       first = toupper(text[i]);
       second = (i + 1 < length) ? toupper(text[i + 1]) : 'X';

       findPosition(keyMatrix, first, &row1, &col1);
       findPosition(keyMatrix, second, &row2, &col2);

       if (row1 == row2) {
           encryptedText[i] = keyMatrix[row1][(col1 + 1) % SIZE];
           encryptedText[i + 1] = keyMatrix[row2][(col2 + 1) % SIZE];
       } else if (col1 == col2) {
           encryptedText[i] = keyMatrix[(row1 + 1) % SIZE][col1];
           encryptedText[i + 1] = keyMatrix[(row2 + 1) % SIZE][col2];
       } else {
           encryptedText[i] = keyMatrix[row1][col2];
           encryptedText[i + 1] = keyMatrix[row2][col1];
       }
   }
   encryptedText[length] = '\0';
}

void decrypt(char text[], char keyMatrix[SIZE][SIZE], char decryptedText[]) {
   int i, row1, col1, row2, col2;
   char first, second;
   int length = strlen(text);

   for (i = 0; i < length; i += 2) {
       first = toupper(text[i]);
       second = (i + 1 < length) ? toupper(text[i + 1]) : 'X';

       findPosition(keyMatrix, first, &row1, &col1);
       findPosition(keyMatrix, second, &row2, &col2);

       if (row1 == row2) {
           decryptedText[i] = keyMatrix[row1][(col1 - 1 + SIZE) % SIZE];
           decryptedText[i + 1] = keyMatrix[row2][(col2 - 1 + SIZE) % SIZE];
       } else if (col1 == col2) {
           decryptedText[i] = keyMatrix[(row1 - 1 + SIZE) % SIZE][col1];
           decryptedText[i + 1] = keyMatrix[(row2 - 1 + SIZE) % SIZE][col2];
       } else {
           decryptedText[i] = keyMatrix[row1][col2];
           decryptedText[i + 1] = keyMatrix[row2][col1];
       }
   }
   decryptedText[length] = '\0';
}

int main() {
   char key[100], text[100], keyMatrix[SIZE][SIZE], encryptedText[100], decryptedText[100];

   printf("Enter the keyword: ");
   fgets(key, sizeof(key), stdin);
   key[strcspn(key, "\n")] = '\0';

   printf("Enter the plaintext: ");
   fgets(text, sizeof(text), stdin);
   text[strcspn(text, "\n")] = '\0';

   if (strlen(text) % 2 != 0) {
       strcat(text, "X");
   }

   prepareKeyMatrix(key, keyMatrix);
   printKeyMatrix(keyMatrix);

   printf("Plaintext: %s\n", text);

   encrypt(text, keyMatrix, encryptedText);
   printf("Encrypted Text: %s\n", encryptedText);

   decrypt(encryptedText, keyMatrix, decryptedText);
   printf("Decrypted Text: %s\n", decryptedText);

   return 0;
}

~~~

## OUTPUT:
![image](https://github.com/user-attachments/assets/61848221-c1cd-4006-bdcb-b4066c6ec044)



## RESULT:
The program is executed successfully

