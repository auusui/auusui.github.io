/*****************************************************************************
 // NAME: Aubrie Usui
 //
 // HOMEWORK: 3
 //
 // CLASS: ICS 212 - Program Structure
 //
 // INSTRUCTOR: Ravi Narayan
 //
 // DATE: September 23, 2020
 //
 // FILE: database.c
 //
 // DESCRIPTION: defines what the functions do that are listed in database.h
 //
 //
******************************************************************************/

#include "database.h"
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

extern int debugmode;

/*****************************************************************************
// FUNCTION NAME: addRecord
// //
// // DESCRIPTION: will add a record to the database
// //
// // PARAMETERS: a (struct record**) -- accnum (int) -- address (char) -- name (char)
// //
// // RETURN VALUES: -1 -- record was not added
//                   0 -- record was added
// //
// //
******************************************************************************/

int addRecord (struct record ** a, int accnum, char uname[], char uaddress[])
{

    struct record *prev, *current, *new;
    int inputnum, currentnum, prevnum, answer;
    answer = -1;

    current = *a;
    new = NULL;
    prev = NULL;

    if (debugmode)
    {
        printf("\n\nFUNCTION: addRecord\nStruct Record: %p\nAccount number: %d \nName: %s \nAddress: %s \n\n",(void *) a, accnum, uname, uaddress);
    }
    
    if (*a == NULL)
    {
        printf("\nAdding record into empty list\n");
        current = (struct record*) malloc (sizeof(struct record));
        current->accountno = accnum;
        strcpy(current->name, uname);
        strcpy(current->address, uaddress);
        current->next = NULL;
        *a = current;
        answer = 0;
    }    
    else if (*a != NULL)
    {
        inputnum = accnum;
        currentnum = current->accountno;
        prevnum = 0;

        /* If the inputnum == the start record accountno*/
        if (inputnum > currentnum && inputnum != currentnum)
        {
            printf("\nAltering start record\n");
            new = (struct record*) malloc(sizeof(struct record));
            new->accountno = accnum;
            strcpy(new->name, uname);
            strcpy(new->address, uaddress);
            new->next = current;
            *a = new;
            answer = 0;
        } 
        else if (inputnum == currentnum)
        {
            printf("\nAdding after start record\n");
            new = (struct record*) malloc(sizeof(struct record));
            new->accountno = accnum;
            strcpy(new->name, uname);
            strcpy(new->address, uaddress);
            prev = current->next;
            new->next = prev;
            current->next = new;
            *a = current;
            answer = 0; 
         }

        while ((answer == -1))
        {
            printf("\nComparing record with accountno: %d\n", currentnum);
            if ((inputnum < prevnum && inputnum > currentnum) || (inputnum == currentnum))
            {
                printf("Altering middle records to maintain descending order");
                new = (struct record*) malloc(sizeof(struct record));
                new->accountno = accnum;
                strcpy(new->name, uname);
                strcpy(new->address, uaddress);
                new->next = current;
                prev->next = new;
                answer = 0;
            }
             
            else
            { 
                prev = current;
                current = current->next;

                if (current == NULL)
                {
                    printf("\nAdding to end of list.\n");
                    new = (struct record*) malloc(sizeof(struct record));
                    new->accountno = accnum;
                    strcpy(new->name, uname);
                    strcpy(new->address, uaddress);
                    new->next = NULL;
                    prev->next = new;
                    answer = 0;
                }
                else 
                {
                    prevnum = currentnum;
                    currentnum = current->accountno; 
                }
            }
        }  
    }
    return answer;
}

/*****************************************************************************
// FUNCTION NAME: printAllRecords
medicaid_norm_ndc.agg([min, max])
// //
// // DESCRIPTION: prints all the records in the database
// //
// // PARAMETERS: next (struct record *)
// //
// // RETURN VALUES: doesnʻt return anything
// //
// //
******************************************************************************/

void printAllRecords (struct record * a) 
{

    struct record *temp;
    int count = 0;
    temp = a;

    if (debugmode)
    {
        printf("\n\nFUNCTION: printAllRecords \nStruct Record: %p\n", (void *) a);
    }

    if (temp == NULL)
    {
        printf("\nThere are no records to print.\n");
    }

    while (temp != NULL)
    {
        printf("\n\n%d\n", temp->accountno);
        printf("%s\n", temp->name);
        printf("%s\n", temp->address);
        temp = temp->next;
        ++count;
    }
    
    if (count > 0)
    {
        printf("\nAll records are shown");
    }
}

/*****************************************************************************
// FUNCTION NAME: findRecord
// //
// // DESCRIPTION: finds and returns a record that is in the database that matches the account number entered
// //
// // PARAMETERS: next (struct record *) -- accnum (int)
// //
// // RETURN VALUES: -1 -- record not found
//                   0 -- record was found
// //
// //
******************************************************************************/

int findRecord (struct record * a, int accnum)
{

    struct record *current;
    int answer, input, currentnum;

    answer = -1;

    if (debugmode)
    {
        printf("\n\nFUNCTION: findRecord \nStruct Record: %p\nAccount number: %d\n", (void *) a, accnum);
    }

    current = a;

    if (a == NULL)
    {
        printf("\n\nThere are no records to find.\n\n");
    }
    else if (a != NULL)
    {
        input = accnum;

        while (current != NULL)
        {
            currentnum = current->accountno;
            if (input == currentnum)
            {
                printf("\n\n%d\n%s\n%s", current->accountno, current->name, current->address);
                answer = 0;
                current = current->next; 
            }

            if (input != currentnum) 
            {
                current = current->next;
                if (current == NULL && answer == -1)
                {
                    printf("There were no records found with accountno: %d", input); 
                }
            }
        }
    }
 
    return answer;
}


/*****************************************************************************
// FUNCTION NAME: deleteRecord
// //
// // DESCRIPTION: deletes a record in database with account number entered
// //
// // PARAMETERS: next (struct record **) -- accnum (int)
// //
// // RETURN VALUES: -1 -- record wasnʻt deleted
//                   0 -- record was deleted
// //
// //
******************************************************************************/

int deleteRecord (struct record ** a, int accnum) 
{

    struct record *prev, *deleted, *temp;
    int answer, current, input;

    answer = -1;
    deleted = *a;

    if (debugmode)
    {
        printf("\n\nFUNCTION: deleteRecord \nStruct Record: %p\nAccount number: %d\n", (void *) a, accnum);
    } 
    
 
    if (*a == NULL)
    {
        answer = -1;
    }
    else if (*a != NULL)
    {
        current = deleted->accountno;
        input = accnum;

        while (input == current)
        {
            printf("Deleting start record and updating");
            temp = deleted->next;
            free(deleted);
            *a = temp;
            deleted = *a;
            current = deleted->accountno;
            answer = 0;
        }
  
        prev = *a;
        
        deleted = prev->next;
        while (deleted != NULL)
        {
            current = deleted->accountno;
              if (input == current)
            {
                printf("\nDeleting record\n");
                temp = deleted->next;
                free(deleted);
                prev->next = temp;
                answer = 0;
                deleted = prev->next;
            } 
            else 
            {
                prev = deleted;
                deleted = prev->next;
            }
        }
      
    }
    if (answer == -1)
    {
        printf("No record was found with account number '%d'", accnum);
    }   

    return answer;
}

/*****************************************************************************
// FUNCTION NAME: readfile
//
// DESCRIPTION: reads each record from a text file and stores it into an array
//
// PARAMETERS: array (struct record **) -- num (int *) -- filename (char)
//
// RETURN VALUES: 0 -- records were read
//                -1 -- records werenʻt read
//
//
******************************************************************************/

int readfile (struct record ** array, char filename[])
{
    char name[25], address[80], emptyline[2];
    int len, size, answer, accountno;
    FILE * file;
    size = 0;
    len = 0;

    if (debugmode)
    {
        printf("\n\nFUNCTION: readfile\nStruct Record: %p\nFilename: %s\n\n", (void *) array, filename);
    }

    file = fopen(filename, "r");
    if (file == NULL)
    {
        printf("\n\nFile is empty. There are no records to be added\n\n");
        answer = -1;
    }
    else if (file != NULL)
    {
        printf("\nNow reading file...\n\n");
        while (fscanf(file, "%d\n", &accountno) != EOF)
        {
            printf("Scanning record\n\n");
            fgets(name, 25, file);
            len = strlen(name);
                
            if (name[len-2] == '\n')
            {
                printf("Changing last char to empty\n\n");
                name[len-2] = '\0';
            }

            fgets(emptyline, 2, file);
            len = strlen(emptyline);
            if (emptyline[len-1] == '\n')
            {
                printf("skipping empty line");
                emptyline[len-1] = '\0';
            }

            fgets(address, 80, file);
            len = strlen(address);
            if (address[len-1] == '$')
            {
                printf("Changing $ to '/0'");
                address[len-1] = '\0';
            }

            size++;
            if (addRecord(array, accountno, name, address) == 0)
            {
                printf("\n\nAdding Record...\n%d\n%s\n%s", accountno, name, address);
            }   
            else 
            {
                printf("\n\nAdd Record Failed\n");
            }
      
        }
        answer = 0;
        fclose(file);
    }
    else 
    {
        answer = -1;
    }
    
    printf("Number of records added: %d\n\n", size);
    return answer;
}


/*****************************************************************************
// FUNCTION NAME: writefile
//
// DESCRIPTION: reads each record from the heap and stores it into a test file
//
// PARAMETERS: array (struct record **) -- num (int) -- filename (char)
//
// RETURN VALUES: 0 -- records were read
//                -1 -- records werenʻt read
//
//
******************************************************************************/

int writefile (struct record * array, char filename[])
{
    struct record *pstart;
    int answer;
    FILE * out;
    answer = 0;
    pstart = array;

    if (debugmode)
    {
        printf("\n\nFUNCTION: writefile\nStruct Record: %p\nFilename: %s\n\n", (void *) array, filename);
    }

    out = fopen(filename, "w");

    if (out == NULL)
    {
        printf("\nFile is empty. There are no files to write into text file.\n\n");
        answer = -1;
    }

    if (out != NULL)
    {
        while (pstart != NULL)
        {
            fprintf(out, "%d\n%s\n%s\n\n", pstart->accountno, pstart->name, pstart->address);
            pstart = pstart->next;
        }

        fclose(out); 
        printf("All files are written into %s", filename);
    }
    return answer;
}


/*****************************************************************************
// FUNCTION NAME: cleanup
//
// DESCRIPTION: frees all space on heap before exiting
//
// PARAMETERS: next (struct record **) 
//
// RETURN VALUES: no return values
//
//
******************************************************************************/

void cleanup (struct record ** ustart)
{
    struct record *a, *temp;
    a = *ustart;
    temp = *ustart;
    ustart = NULL;
  
    if (debugmode)
    {
        printf("\n\nFUNCTION: Cleanup\nStruct Record: %p\n\n", (void *) ustart);
    }

    if (a == NULL)
    {
        printf("Your list is already empty");
    }

    while (a != NULL)
    {
        temp = a->next;
        free(a);
        a = NULL;
        a = temp;
    }

    printf("\n\nAll your records have been wiped clean.\n");
}

