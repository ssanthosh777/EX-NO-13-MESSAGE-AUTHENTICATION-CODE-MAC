# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC
```
NAME: SANTHOSH S
REG.NO: 212224100052
```

## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

## ALGORITHM:

1. Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

2. Initialization:
   - Choose a cryptographic hash function \( H \) (e.g., SHA-256) and a secret key \( K \).
   - The message \( M \) to be authenticated is input along with the secret key \( K \).

3. MAC Generation:
   - Compute the MAC by applying the hash function to the combination of the message \( M \) and the secret key \( K \): 
     \[
     \text{MAC}(M, K) = H(K || M)
     \]
     where \( || \) denotes concatenation of \( K \) and \( M \).

4. Verification:
   - The recipient, who knows the secret key \( K \), computes the MAC using the received message \( M \) and the same hash function.
   - The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.

5. Security: The security of the MAC relies on the secret key \( K \) and the strength of the hash function \( H \), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

## Program:

```c
#include <stdio.h>
#include <string.h>

#define MAC_SIZE 32

void computeMAC(const char *key,
                const char *message,
                char *mac)
{
    int key_len = strlen(key);
    int msg_len = strlen(message);

    for(int i = 0; i < MAC_SIZE; i++)
    {
        mac[i] =
        key[i % key_len] ^
        message[i % msg_len];
    }

    mac[MAC_SIZE] = '\0';
}

int main()
{
    char key[100];
    char message[100];

    char mac[MAC_SIZE + 1];
    char receivedMAC[MAC_SIZE + 1];

    printf("MESSAGE AUTHENTICATION CODE\n");

    printf("\nEnter the secret key: ");
    scanf("%s", key);

    printf("Enter the message: ");
    scanf("%s", message);

    computeMAC(key, message, mac);

    printf("\nComputed MAC (in hex):\n");

    for(int i = 0; i < MAC_SIZE; i++)
    {
        printf("%02x",
               (unsigned char)mac[i]);
    }

    printf("\n");

    printf("\nEnter the received MAC (as hex):\n");

    for(int i = 0; i < MAC_SIZE; i++)
    {
        scanf("%02hhx",
              &receivedMAC[i]);
    }

    if(memcmp(mac,
              receivedMAC,
              MAC_SIZE) == 0)
    {
        printf("\nMAC verification successful.");
        printf("\nMessage is authentic.\n");
    }
    else
    {
        printf("\nMAC verification failed.");
        printf("\nMessage is not authentic.\n");
    }

    return 0;
}


```



## Output:
<img width="726" height="185" alt="image" src="https://github.com/user-attachments/assets/1996bf30-1c72-48a8-9940-6b13d5e3699a" />


## Result:
The program is executed successfully.
