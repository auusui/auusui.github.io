/*****************************************************************
//  NAME:        Aubrie Usui
//
////  HOMEWORK:    project2
////
////  CLASS:       ICS 212
////
////  INSTRUCTOR:  Ravi Narayan
////
////  DATE:        December 2, 2020
////
////  FILE:        llist.cpp
////
////  DESCRIPTION:  defines what the function do that are listed in llist.h
////
****************************************************************/

#include "record.h"
#include "llist.h"
#include <fstream>
#include <iostream>
#include <sstream>
#include <cstring>

/*Constructor -- intitializes start and also calls readfile */
llist :: llist()
{
    #ifdef PROJECT_DEBUG
        cout << "llist constructor was called\n";
        cout << "No parameters\n";
    #endif

    strcpy(filename, "savedfiles.txt");
    start = NULL;
    readfile();

}

/*Constructor-- calling readfile and initializing start*/
llist :: llist (char input[])
{
    #ifdef PROJECT_DEBUG
        cout << "llist constructor was called\n";
        cout << "Parameters: (char[])\n";
    #endif

    strcpy(filename, input);
    start = NULL;
    readfile();
}

/*Destructor-- calling writefile and cleanup*/
llist :: ~llist()
{
    #ifdef PROJECT_DEBUG
        cout << "llist destructor was called\n";
        cout << "No parameters\n";
    #endif

    writefile();
    cleanup();
}



/*****************************************************************************
// FUNCTION NAME: addRecord
//
// // DESCRIPTION: will add a record to the database
// //
// // PARAMETERS: a (struct record**) -- accnum (int) -- address (char) -- name (char)
// //
// // RETURN VALUES: -1 -- record was not added
//                   0 -- record was added
// //
// //
******************************************************************************/

int llist :: addRecord (int accnum, char uname[], char uaddress[] )
{
    struct record *prev, *newlist, *current;
    int inputnum, currentnum, prevnum, answer;
    answer = -1;
    current = start;

    if (start == NULL)
    {
        cout << "\nAdding record into empty list\n";
        newlist = new record;
        newlist->accountno = accnum;
        strcpy(newlist->name, uname);
        strcpy(newlist->address, uaddress);
        newlist->next = NULL;
        start = newlist;
        answer = 0;
    }
    else if (start != NULL)
    {
        inputnum = accnum;
        currentnum = current->accountno;
        prevnum = 0;
  
        if (inputnum > currentnum && inputnum != currentnum)
        {
            cout << "\nAltering start record\n";
            newlist = new record;
            newlist->accountno = accnum;
            strcpy(newlist->name, uname);
            strcpy(newlist->address, uaddress);

            newlist->next = current;
            start = newlist;
            answer = 0;
        }
        else if (inputnum == currentnum)
        {
            cout << "\nAdding after start record\n";
            newlist = new record;
            newlist->accountno = accnum;
            strcpy(newlist->name, uname);
            strcpy(newlist->address, uaddress);

            prev = current->next;
            newlist->next = prev;
            current->next = newlist;
            start = current;
            answer = 0;
        }
    }

    while (answer == -1)
    {
        cout << "\nComparing record with accountno " << currentnum << "\n";
        if ((inputnum < prevnum && inputnum > currentnum) || (inputnum == currentnum))
        {
            cout << "\nAltering mddle records to maintain descending order\n";
            newlist = new record;
            newlist->accountno = accnum;
            strcpy(newlist->name, uname);
            strcpy(newlist->address, uaddress);
            newlist->next = current;
            prev->next = newlist;
            answer = 0;

        }
        else 
        {
            prev = current;
            current = current->next;

            if (current == NULL)
            {
                cout << "\nAdding to end of list\n";
                newlist = new record;
                newlist->accountno = accnum;
                strcpy(newlist->name, uname);
                strcpy(newlist->address, uaddress);
                newlist->next = NULL;
                prev->next = newlist;
                answer = 0;

            }
            else 
            {
                prevnum = currentnum;
                currentnum = current->accountno;
            }
        }
 
    }
    return answer;   
}


/*****************************************************************************
// FUNCTION NAME: findRecord
//
// // DESCRIPTION: finds and returns a record that is in the database that matches the account number entered
// //
// // PARAMETERS: next (struct record *) -- accnum (int)
// //
// // RETURN VALUES: -1 -- record not found
//                   0 -- record was found
// //
// //
******************************************************************************/

int llist :: findRecord (int accnum) 
{
    struct record *current;
    int answer, input, currentnum;

    answer = -1;
    
    current = start;
    if (start == NULL)
    {
        cout << "\n\nThere are no records to find.\n\n";
    }
    else if (start != NULL)
    {
        input = accnum;
        while (current != NULL)
        {
            currentnum = current->accountno;
            if (input == currentnum)
            {
                cout << "\n\n" << current->accountno << "\n" << current->name << "\n" << current->address;
                answer = 0;
                current = current->next;
            }
            if (input != currentnum)
            {
                current = current->next;
                if (current == NULL && answer == -1)
                {
                    cout << "There were no records foun with accountnumber: " << input;
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
// //                   0 -- record was deleted
// //
// //
******************************************************************************/

int llist :: deleteRecord (int accnum)
{
    struct record *prev, *deleted, *temp, *check;
    int answer, current, input;

    answer = -1;
    deleted = start;

    if (start == NULL)
    {
        answer = -1;
        cout << "There are no records in the system";

    }
    else if (start != NULL)
    {
        check = start->next;
        if (check == NULL)
        {
            delete deleted;
            start = NULL;
            cout << "\n\nYou have deleted the last record.  Start is now null.\n";
            answer = 0;
        }
        else 
        {
            current = deleted->accountno;
            input = accnum;

            while (input == current)
            {
                 cout << "Deleting start record and updating";
                 temp = deleted->next;
                 delete deleted;
                 start = temp;
                 deleted = start;
                 current = deleted->accountno;
                 answer = 0;
            }

            prev = start;
            deleted = prev->next;

            while (deleted != NULL)
            {
                current = deleted->accountno;
                if (input == current)
                {
                    cout << "\nDeleting record\n";
                    temp = deleted->next;
                    delete deleted;
                    prev->next = temp;
                    answer = 0;
                    deleted = prev->next;
                } 
            } 
        }
    }
    
    if (answer == -1)
    {
        cout << "\nNo record was found with accountno: " << accnum;
    }

    return answer;
}


/*****************************************************************************
// FUNCTION NAME: readfile
//
//// DESCRIPTION: reads each record from a text file and stores it into an array
////
//// PARAMETERS: array (struct record **) -- num (int *) -- filename (char)
////
//// RETURN VALUES: 0 -- records were read
////                -1 -- records werenʻt read
////
////
******************************************************************************/

int llist :: readfile()
{
    char name[25], address[80], c, accnum[20];
    int i, line, size, answer, accountno;
    ifstream myfile;
    size = 0;
    i = 0;
    line = 0;

    cout << "\nYou are now entering Readfile Function\n\n";

    
    myfile.open(filename);

    if (myfile == NULL)
    {
        cout << "\n\nFile is empty";
        answer = -1;
        start = NULL;
    }
    else if (myfile != NULL)
    {

        cout << "\nNow reading file\n";
        while (!myfile.eof())
        {
            myfile.get(c);
            if (line == 0)
            {
                if (c == '\n')
                {
                    accnum[i] = '\0';
                    stringstream str(accnum);
                    str >> accountno;
                    line = 1;
                    i = 0;
                }    
                else 
                {
                    accnum[i] = c;
                    i++;
                }
            }
            else if (line == 1)
            {
                if (c == '\n' || i > 23)
                {
                    name[i] = '\0';
                    line = 2;
                    i = 0;
                }
                else 
                {
                    name[i] = c;
                    i++;
                }
            }
            else if (line == 2)
            {
                if (c == '$')
                {
                    addRecord(accountno, name, address);
                    address[i] = '\0';
                    line = 0;
                    i = 0;
                    size++;
                    accnum[0] = '\0';
                }
                else 
                {
                    address[i] = c;
                    i++;
                }
            }

        #ifdef DEBUG
        cout << "DEBUG (inside readfile) START\n\n";
        cout << "Function Called:\taddRecord\n\n";
        cout << "Parameters:\n";
        cout << "Account Number:\t" << accnum;
        cout << "\nName:\t" << name;
        cout << "\nAddress:\t" << address;
        cout << "\nDEBUG (inside readfile) END\n";
        #endif

        }
        
        cout << "Size is " << size;
        myfile.close();
    }
    return answer;
}

/*****************************************************************************
// FUNCTION NAME: writefile
//
//// DESCRIPTION: reads each record from the heap and stores it into a test file
////
//// PARAMETERS: array (struct record **) -- num (int) -- filename (char)
////
//// RETURN VALUES: 0 -- records were read
////                -1 -- records werenʻt read
////
******************************************************************************/

int llist :: writefile()
{
    struct record *pstart;
    int answer;
    ofstream myfile;
    pstart = start;
    answer = -1;

    cout << "\nYou are now entering Writefile Function\n\n";

    myfile.open(filename);
    if (myfile == NULL)
    {
        cout << "File is empty.  There are no files to write into text file.\n";
        answer = -1;
    }
    else if (myfile != NULL) 
    {
        while (pstart != NULL)
        {
            myfile << "\n" << pstart->accountno << "\n" << pstart->name << "\n" << pstart->address <<  "$" << endl;
            pstart = pstart->next;
        }
        answer = 0;
        myfile.close();
        cout << "\nAll files are written into " << filename;
    }
    return answer;
}


/*****************************************************************************
// FUNCTION NAME: cleanup
//
//// DESCRIPTION: frees all space on heap before exiting
////
//// PARAMETERS: next (struct record **)
////
//// RETURN VALUES: no return values
////
////
******************************************************************************/

void llist :: cleanup()
{
    struct record *pstart, *next;
    printf("\nHold one while we clean the memory\n\n");
    pstart = start;

    if (pstart == NULL)
    {
        cout << "Your list is already empty\n";
    }
    else 
    {
        while (pstart != NULL)
        {
            next = pstart;
            pstart = pstart->next;
            delete(next);
        }
        cout << "All records have been deleted\n";
    }
    
} 


ostream & operator << (ostream &os, const llist &mylist)
{
    struct record *temp;

    temp = mylist.start;

    while (temp != NULL)
    {
        cout << "\n\n" << temp->accountno << endl;
        cout << "\n" << temp->name << endl;
        cout << "\n" << temp->address << endl;

        temp = temp->next;
    }

    return os;
}


   
