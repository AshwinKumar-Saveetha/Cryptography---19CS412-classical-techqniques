# Cryptography - 19CS415
# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:
To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:
### Step 1:
Design of Vigenere Cipher algorithnm 
### Step 2:
Implementation using C or pyhton code
### Step 3:
Testing algorithm with different key values. 

ALGORITHM DESCRIPTION:
The Vigenere cipher is a method of encrypting alphabetic text by using a series of different Caesar ciphers based on the letters of a keyword. It is a simple form of polyalphabetic substitution.To encrypt, a table of alphabets can be used, termed a Vigenere square, or Vigenere table. It consists of the alphabet written out 26 times in different rows, each alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses a different alphabet from one of the rows used. The alphabet at each point depends on a repeating keyword.

## PROGRAM:
```
#include <stdio.h>
#include <ctype.h>
#include <string.h>
#include<stdlib.h>
void encipher();
void decipher();
void main()
{
int choice;
while(1)
{
printf("\n1. Encrypt Text");
printf("\t2. Decrypt Text");
printf("\t3. Exit");
printf("\n\nEnter Your Choice : ");
scanf("%d",&choice);
if(choice == 3)
break;
else if(choice == 1)
encipher();
else if(choice == 2)
decipher();
else
printf("Please Enter Valid Option.");
 }
}
void encipher()
{
unsigned int i,j;
char input[50],key[10];
printf("\n\nEnter Plain Text: ");
scanf("%s",input);
printf("\nEnter Key Value: ");
scanf("%s",key);
printf("\nResultant Cipher Text: ");
for(i=0,j=0;i<strlen(input);i++,j++)
{
if(j>=strlen(key))
{ j=0;
}
printf("%c",65+(((toupper(input[i])-65)+(toupper(key[j])-
65))%26));
}}
void decipher()
{
unsigned int i,j;
char input[50],key[10];
int value;
printf("\n\nEnter Cipher Text: ");
scanf("%s",input);
 printf("\n\nEnter the key value: ");
scanf("%s",key);
for(i=0,j=0;i<strlen(input);i++,j++)
{
if(j>=strlen(key))
{ j=0; }
value = (toupper(input[i])-64)-(toupper(key[j])-64);
if( value < 0)
{ value = value * -1;
}
printf("%c",65 + (value % 26));
}
}
```
## OUTPUT:

![image](https://github.com/user-attachments/assets/6006ef22-b1a3-4a57-9b0d-648ff018347b)

## RESULT:
The program is executed successfully
