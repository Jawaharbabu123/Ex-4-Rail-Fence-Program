# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:
~~~
STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.
~~~
# PROGRAM
~~~

#include <stdio.h>
#include <string.h>
#include <stdbool.h>

void encryptRailFence(char *text, int key, char *result) {
    int len = strlen(text);
    char rail[key][len];

    
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            rail[i][j] = '\n';

    bool dir_down = false;
    int row = 0, col = 0;

    for (int i = 0; i < len; i++) {
        
        if (row == 0 || row == key - 1)
            dir_down = !dir_down;

        rail[row][col++] = text[i];

        row += dir_down ? 1 : -1;
    }

    
    int index = 0;
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] != '\n')
                result[index++] = rail[i][j];
    result[index] = '\0';
}

void decryptRailFence(char *cipher, int key, char *result) {
    int len = strlen(cipher);
    char rail[key][len];

    
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            rail[i][j] = '\n';

    // Mark the places with '*'
    bool dir_down;
    int row = 0, col = 0;
    for (int i = 0; i < len; i++) {
        if (row == 0)
            dir_down = true;
        if (row == key - 1)
            dir_down = false;

        rail[row][col++] = '*';
        row += dir_down ? 1 : -1;
    }

    
    int index = 0;
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] == '*' && index < len)
                rail[i][j] = cipher[index++];

  
    row = 0, col = 0;
    dir_down = false;

    index = 0;
    for (int i = 0; i < len; i++) {
        if (row == 0)
            dir_down = true;
        if (row == key - 1)
            dir_down = false;

        if (rail[row][col] != '\n')
            result[index++] = rail[row][col++];
        row += dir_down ? 1 : -1;
    }
    result[index] = '\0';
}

int main() {
    char text[100], cipher[100], decrypted[100];
    int key;

    printf("Enter text: ");
    scanf("%s", text);

    printf("Enter key (number of rails): ");
    scanf("%d", &key);

    encryptRailFence(text, key, cipher);
    printf("Encrypted Text: %s\n", cipher);

    decryptRailFence(cipher, key, decrypted);
    printf("Decrypted Text: %s\n", decrypted);

    return 0;
}

~~~
# OUTPUT
<img width="1899" height="1150" alt="Screenshot 2025-09-13 082249" src="https://github.com/user-attachments/assets/898f04cb-78e9-4a08-bef2-2f77de023ccc" />


# RESULT
The output is verified successfully
