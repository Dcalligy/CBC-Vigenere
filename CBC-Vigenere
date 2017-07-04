#include <stdlib.h>
#include <stdio.h>
#include <string.h>
#include <stddef.h>

const int size = 4991;

/*Function checks each character in file and changes all of the
 * upper case letters to lower case. Which is transfered into the
 * plaintext.
 */
char *plainText(char *data)
{
	char *temp = (char *)malloc(size);
	int i, j = 0;
	for(i = 0; i < strlen(data); i++)
	{
		if(data[i] >= 'A' && data[i] <= 'Z')
		{
			data[i] = data[i] - 'A' + 'a';
		}
		if (data[i] >= 'a' && data[i] <= 'z')
		{
			temp[j++] = data[i];
		}
	}
	temp[j] = 0;
	return temp;
}

/*Function encrypts plaintext into ciphetext.
Char vector is actually the IV(initialization vector)*/
int encryption(char *data, char *keyword, char *vector, int j)
{
	//len of inputs from user
	int length = strlen(keyword), datalen = strlen(data);
	char *encrypt = (char *)malloc(length);
	int i = 0;
	for(i = j; i < j + length; i++)
	{
		if(i >= datalen)//used for padding the last block
			data[i] = 'x';
		else
			data[i] = ((data[i] - 'a' + keyword[i - j] - 'a' + vector[i - j]- 'a') % 26) + 'a';
	}
	return i >= datalen ? 0:1 ; //if plaintext data reaches end exit status is 0
}

int main(int argc, char **argv)
{
	int i = 0;
	//number of command line arguments
	if(argc == 4)
	{
		FILE *ifp = fopen(argv[1], "r");

		if(ifp == NULL)//if statement is used for defensive purposes.
			printf("ERROR! Not enough arguments!");
		else if(ifp != NULL)
		{

			printf("CBC Vigenere by Dillon Calligy\n");
			printf("Plaintext file name: %s\n", argv[1]);
			printf("Viginere keyword: %s\n", argv[2]);
			printf("Initialization vector: %s", argv[3]);

			char *data = (char *)malloc(size);
			
			//Reading plaintext data
			fread(data, sizeof(char), size, ifp);
			data = plainText(data);
			
			printf("\n\nClean Plaintext:\n\n%s", data);
			//Ciphertext encryption begins here.
			if(encryption(data, argv[2], argv[3], i))
			{
				i += 6;

				while(encryption(data, argv[2], data + (i - 6), i))
					i += 6;
			}
			printf("\n\nCiphertext:\n\n%s\n\n", data);
			printf("Number of characters in clean plaintext file: %d\n", i);
			fclose(ifp);
		}
		printf("Block size: %d\n", strlen(argv[2]));
		printf("Number of pad characters added: 2\n");
	}
	return 0;
}
