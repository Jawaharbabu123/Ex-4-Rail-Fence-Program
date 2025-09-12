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
~~~
def encrypt_rail_fence(message, rails):
    length = len(message)
    rail = [['\n' for _ in range(length)] for _ in range(rails)]
    row = 0
    direction = 1
    for i in range(length):
        rail[row][i] = message[i]
        row += direction
        if row == rails - 1 or row == 0:
            direction *= -1
    encrypted = ''
    for i in range(rails):
        for j in range(length):
            if rail[i][j] != '\n':
                encrypted += rail[i][j]
    print("Encrypted text:", encrypted)
def main():
    message = input("Enter a Secret Message: ").replace(" ", "")
    rails = int(input("Enter number of rails: "))
    encrypt_rail_fence(message, rails)
if __name__ == "__main__":
    main()
~~~
# OUTPUT
<img width="1920" height="987" alt="Screenshot 2025-09-12 131550" src="https://github.com/user-attachments/assets/a242f749-ff8a-422e-9dfa-5d466e27d72b" />

# RESULT
the program is executed successfully
