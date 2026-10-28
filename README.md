NAME: SANTHOSH SIVAKUMAR

REG NO:212225040382
# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
```
#include <stdio.h>
#include <string.h>

#define SIZE 1000

/* Which rail does character position j land on? */
int railOf(int j, int rails)
{
    int cycle, pos;

    if (rails == 1) return 0;
    cycle = 2 * (rails - 1);
    pos = j % cycle;
    return (pos < rails) ? pos : cycle - pos;
}

/* Read rails top to bottom, left to right */
void railEncrypt(const char *text, char *out, int rails)
{
    int r, j, k = 0, len = strlen(text);

    for (r = 0; r < rails; r++) {
        for (j = 0; j < len; j++) {
            if (railOf(j, rails) == r) {
                out[k++] = text[j];
            }
        }
    }
    out[k] = '\0';
}

/* Put the cipher characters back into the zigzag positions */
void railDecrypt(const char *cipher, char *out, int rails)
{
    int r, j, k = 0, len = strlen(cipher);

    for (r = 0; r < rails; r++) {
        for (j = 0; j < len; j++) {
            if (railOf(j, rails) == r) {
                out[j] = cipher[k++];
            }
        }
    }
    out[len] = '\0';
}

int main(void)
{
    char str[SIZE], enc[SIZE], dec[SIZE];
    int rails;

    printf("Enter a Secret Message\n");
    if (fgets(str, sizeof(str), stdin) == NULL) {
        printf("Failed to read message.\n");
        return 1;
    }
    str[strcspn(str, "\n")] = '\0';

    if (strlen(str) == 0) {
        printf("Message cannot be empty.\n");
        return 1;
    }

    printf("Enter number of rails\n");
    if (scanf("%d", &rails) != 1 || rails < 1) {
        printf("Rails must be a positive integer.\n");
        return 1;
    }

    railEncrypt(str, enc, rails);
    printf("Encrypted Message: %s\n", enc);

    railDecrypt(enc, dec, rails);
    printf("Decrypted Message: %s\n", dec);

    return 0;
}
```

# OUTPUT

<img width="1623" height="806" alt="image" src="https://github.com/user-attachments/assets/22bcb03b-c298-4895-8604-a2083667c6d8" />


# RESULT

The program is executed successfully


