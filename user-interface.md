/*****************************************************************************
 *
 *    NAME: Aubrie Usui 
 *
 *    HOMEWORK: 3
 *
 *    CLASS: ICS 212 -- Program Structure
 *
 *    INSTRUCTOR: Ravi Narayan
 *
 *    DATE: September 23, 2020
 *
 *    FILE: user_interface.c
 *
 *    DESCRIPTION: get user input and apply functions defined in database.c
 *
 *
******************************************************************************/

#include "database.h"
#include <string.h>
#include <stdio.h>
#include "record.h"

int debugmode;

void getaddress(char [], int );

/*****************************************************************************
 // FUNCTION NAME: getaddress
 //
 // DESCRIPTION: retrieves the address from the user interface
 //
 // PARAMETERS: address (char) -- size (int)
 //
 // RETURN VALUES: returns nothing
 //
 //
******************************************************************************/

void getaddress (char address[], int size)
{

    int i, num;
    i = 0;

    printf("Once you are finished, enter the character '$' at the end then press 'ENTER': \n");    

    while ((num = getchar()) != '$')
    {
        address[i] = num;
        ++i;
    }
    size = i-1;
 
    address[i] = '$';
    address[i+1] = '\0';

    if (debugmode)
    {
        printf("\n\nFUNCTION: getaddress\nAddress: %s\nSize: %d\n\n", address, size);
    }  
}


/*****************************************************************************
// FUNCTION NAME: main
// //
// // DESCRIPTION: main user interface where functions are executed
// //
// // PARAMETERS: argc (int) -- argv (char *)
// //
// // RETURN VALUES: 0
// //
// //
******************************************************************************/

int main (int argc, char * argv [] ) 
{

    struct record * start = NULL;
    int option, accountnum, transaction;
    char name[25], address[80], empty[20], input[1][10], answer[10];
    option = 0;
    debugmode = 0;
    transaction = 1;

/* introductory message */

    /* If two parameters were entered */
    if (argc == 2)
    {
        if (strcmp(argv[1], "debug") == 0)
        {
            debugmode = 1;
            printf("\n\n******************You are now entering debug mode**********************\n\n");
        }
        else 
        {
            printf("ERROR: Executable did not match.  Try ./project debug instead");
            transaction = 0;
        }
    }
    /* if more than 2 parameters are entered */
    else if (argc > 2)
    {
        transaction = 0;
        printf("\nERROR: Too many parameters in executable.");
    }
    else
    {
        debugmode = 0;
        printf("\n\nEntering transaction\n\n");
    }


    if (transaction != 0)
    {
        printf("\n\nWelcome.  Below you will see a table of options you can perform.  Please enter the value that is next to the option you want to perform.\n");
        printf("----------------------------------------------------------------------\n\n");
    
        if (readfile(&start, "savedfiles.txt") == 0)
        {
            printf("Your previous records have been added\n\n");
        }
    }
    
    /* all in a while loop */
    /*options menu displayed for user */
    while ((transaction == 1)) 
    {

        printf("\n----------------------------\n");
        printf("Type 'add' : Add new record\n");
        printf("Type 'printall' : Print all records\n");
        printf("Type 'find' : Find a record\n");
        printf("Type 'delete' : Delete record\n");
        printf("Type 'quit' : Quit the program\n");
        printf("----------------------------\n\n");

    /*scan user input for option number */

        scanf("%s", answer);
        strcpy(input[0], answer);

        if (strncmp (input[0], "axx", 1) == 0)
        {
            option = 1;
        }
        else if (strncmp (input[0], "pxxxxxxx", 1) == 0)
        {
            option = 2;
        }
        if (strncmp (input[0], "fxxx", 1) == 0)
        {
            option = 3;
        }
        if (strncmp (input[0], "dxxxxx", 1) == 0)
        {
            option = 4;
        }
        if (strncmp (input[0], "qxxx", 1) == 0)
        {
            option = 5;
        }
        else if (option == 0)
        {
            printf("ERROR: Please enter a valid input from the menu\n\n");
        }

    /*collect appropriate information for each option */

        if (option == 1) 
        {
            printf("\n\nYou chose Add Record.  Follow the prompts below.\n\n");

            printf("Enter your account number:\n");
            scanf("%d", &accountnum);
            getchar();

            printf("Enter the name for the account.  Once you are finished press 'ENTER' twice: \n");
            fgets(name, 25, stdin);
            fgets(empty, 20, stdin);

            printf("Enter your address: \n");
            getaddress(address, 80);
            getchar();
        
            if (addRecord(&start, accountnum, name, address) == 0)
            {
                printf("\n\nRecord has successfully been added\n\n");
            }
            else  
            {
                printf("\n\nSomething went wrong, Record was not added.\n\n");
            }

        }
        else if (option == 2)
        {
            printf("\n\nYou chose Print All Records. Here are your records:\n\n");
            printAllRecords(start);
        }
    
        else if (option == 3)
        {
            printf("\n\nYou chose Find Record.  Follow the prompt below.\n\n");
            printf("Enter your account number:\n");
            scanf("%d", &accountnum);
            getchar();

            findRecord(start, accountnum);
        }    
        else if (option == 4)
        {
            printf("\n\nYou chose Delete Record\n\n");
            printf("Enter your account number:\n");
            scanf("%d", &accountnum);
            getchar();

            if (deleteRecord(&start, accountnum) == 0)
            {
                printf("\n\nThe record(s) were deleted!\n\n");
            }
        }
    
        else if (option == 5)
        {
            if (writefile(start, "savedfiles.txt") == 0)
            {
                cleanup(&start);
            }
            else 
            {
                printf("Writefile didnʻt work");
            }
            transaction = 0;
            printf("You have successfully exited the program\n");
        }
    
    /* display the results */
    }
    printf("Program terminated\n");

    return 0;
}
